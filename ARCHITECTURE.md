# BOWLERA — ARCHITECTURE.md
> Bu belge Bowlera'nın teknik kontrat dosyasıdır.
> Her bileşenin/modülün interface'i, veri modeli ve sınırları burada tanımlanır.
> Kod yazılmadan önce Claude bu dosyayı okumak zorundadır.
> Kaynak: MASTER_PLAN.md §3, §5 + CORE.md §2, §4

---

## 1. SİSTEM MİMARİSİ — GENEL AKIŞ

```
lib/menu-data.json (MVP) ─┐
                           ├──► app/api/menu/route.ts ──► Server/Client Components
CMS: Sanity/Contentful ────┘        (ISR ile, büyüme fazı)         │
                                                                     ▼
                                                          components/menu/MenuCard.tsx
                                                          (kalori ZORUNLU render edilir)
                                                                     │
                                                                     ▼
                                              "Özelleştir" tıklanınca ──► app/menu/customize/[id]/page.tsx
                                                                     │
                                                                     ▼
                                              store/useCustomizerStore.ts (Zustand — adım state'i)
                                                                     │
                                              ┌──────────────────────┼──────────────────────┐
                                              ▼                      ▼                      ▼
                                   components/customizer/  components/customizer/  components/customizer/
                                   StepBase/Protein/...     VisualPreview.tsx        SummaryPanel.tsx
                                   (seçim UI)                (katmanlı CSS/SVG)      (fiyat/kalori canlı toplam)
                                                                     │
                                                          "Sepete Ekle" tıklanınca
                                                                     ▼
                                                          store/useCartStore.ts (Zustand + persist)
                                                                     │
                                              ┌──────────────────────┼──────────────────────┐
                                              ▼                                              ▼
                                   components/cart/CartBadge.tsx              components/cart/CartDrawer.tsx
                                   (logo-degrade pulse animasyonu)             (sepet içeriği, checkout'a yönlendirme)
                                                                                              │
                                                                                              ▼
                                                                          app/siparis/page.tsx (checkout — kanal ZORUNLU)
                                                                                              │
                                                                                              ▼
                                                                          lib/integrations/whatsapp.ts | marketplace.ts
                                                                          (wa.me linki | Adisyo/SepetTakip API — server-side)
                                                                          ⚠️ WhatsApp köprüsü şube numarası bekleniyor (§2.9)

app/giris/page.tsx ──► app/api/auth/otp/{send,verify}/route.ts ──► auth.ts (Auth.js JWT session)
                                                                                │
                                                                                ▼
                                                                lib/db/client.ts (Neon Postgres, Drizzle ORM)
                                                                                │
                                              ┌─────────────────────────────────┴─────────────────────────────────┐
                                              ▼                                                                     ▼
                                   users tablosu (phone, address,                                    app/hesap/page.tsx ──► app/api/user/profile/route.ts
                                   displayName, loyaltyPoints, verifiedAt)                            (GET/PATCH — sadece session.user.phone kullanır)
```

### Katman Sınırı Kuralları

```
1. Menü verisi her zaman lib/menu-data.json veya CMS'ten okunur — bileşen içine hardcode edilemez
2. Kalori/protein alanı BowlItem tipinde zorunlu — komponent bu alanı gizleyemez/opsiyonel gösteremez
3. Sepet state'i sadece useCartStore üzerinden değişir — bileşenler doğrudan localStorage'a yazamaz
4. Üçüncü parti API çağrıları (Adisyo/SepetTakip/Twilio) sadece app/api/ Route Handler'larından yapılır — client component'ten asla
5. Customizer adım sırası useCustomizerStore'daki currentStep ile kontrol edilir — URL manipülasyonuyla atlanamaz
6. Tasarım sistemi token'ları (renk/tipografi) sadece tailwind.config.ts üzerinden kullanılır — inline hex kod yasak (DESIGN_SYSTEM.md)
7. Auth (telefon+OTP) katmanı sepet akışından bağımsızdır — guest checkout her zaman geçerli kalır, useCartStore auth durumuna göre dallanmaz (INTEGRATIONS.md §5)
8. Kullanıcı profili/adres verisi SADECE app/api/user/profile/route.ts üzerinden okunur/yazılır — bu route request body'den phone KABUL ETMEZ, kimlik her zaman session'dan (session.user.phone) alınır (BSC-3 kritik sınır, Karar #23)
9. Adres alanı sipariş akışını (checkout) BLOKLAMAZ — FulfillmentChannel ("pickup" | "dine-in") delivery içermediği için adres sadece profil/sadakat verisidir, opsiyonel olarak /hesap sayfasında toplanır (Karar #23)
10. Teslimat kanalı (fulfillmentChannel) app/siparis/page.tsx'te ZORUNLU seçim haline getirilir — kanal seçilmeden WhatsApp sipariş CTA'sı aktif olamaz (Açık Sorun #26, bu güncelleme)
11. Üçüncü parti entegrasyon için gerekli kimlik bilgisi (ör. şube telefon numarası) eksikken ilgili CTA gerçek işlevle bağlanamaz — sahte/placeholder değer YASAK (BSC-5, CORE §9); bunun yerine CTA bilinçli olarak devre dışı + açıklamalı bırakılır
```

---

## 2. MODÜL KONTRATLARI

### 2.1 `app/layout.tsx` — Root Layout

```tsx
// app/layout.tsx
// Amaç:    Tüm sayfalar için ortak iskelet — font, tema, Header/Footer, global provider'lar
// Bağlı:   Her sayfa buradan render edilir
// Risk:    Hatalı font/tema yüklemesi → tüm site etkilenir
// Dokunma: DESIGN_SYSTEM.md §Tipografi kontrol et

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="tr">
      <body className={`${cormorantGaramond.variable} ${nunito.variable}`}>
        <Header />
        {children}
        <Footer />
        <CartDrawer />
      </body>
    </html>
  )
}
```

### 2.2 `app/api/menu/route.ts` — Menü Veri Endpoint'i (MVP)

```ts
// app/api/menu/route.ts
// Amaç:    menu-data.json'ı servis eder — tek veri kaynağı
// Bağlı:   Menü sayfası, MenuCard, Customizer başlangıç verisi
// Risk:    Hatalı response → menü boş görünür, sipariş alınamaz
// Dokunma: CMS geçişinde bu route'un response şekli DEĞİŞMEMELİ (backward compat)

export async function GET() {
  const data = await readMenuData()   // MVP: fs.readFile, Büyüme: CMS SDK
  return Response.json(data)
}
```

> ⚠️ MVP → CMS geçişinde bu endpoint'in **response contract'ı sabit kalmalı** —
> aksi halde MenuCard/Customizer'ın hepsi güncellenmek zorunda kalır (DEPENDENCIES.md).

### 2.3 `store/useCartStore.ts` — Sepet State

```ts
// store/useCartStore.ts
// Amaç:    Sepet öğelerini ve teslimat kanalını yönetir, tarayıcı kapansa da korur
// Bağlı:   CartBadge, CartDrawer, Customizer "Sepete Ekle" butonu, app/siparis/page.tsx
// Risk:    Hatalı state güncelleme → yanlış fiyat/miktar sepette görünür.
//          fulfillmentChannel boş kalırsa teslimat şekli belirsizleşir (Açık Sorun #26)
// Dokunma: BSC-6 (race condition) kontrolü — çift tıklama koruması component tarafında

import { create } from 'zustand'
import { persist } from 'zustand/middleware'
import type { CartItem, FulfillmentChannel } from '@/types'

interface CartState {
  cart: CartItem[]
  fulfillmentChannel: FulfillmentChannel | null   // sepet/oturum seviyesinde TEK alan — Karar #13
  addToCart: (item: CartItem) => void
  removeFromCart: (cartId: string) => void
  setFulfillmentChannel: (channel: FulfillmentChannel) => void
  clearCart: () => void
}

export const useCartStore = create<CartState>()(
  persist(
    (set) => ({
      cart: [],
      fulfillmentChannel: null,
      addToCart: (item) => set((state) => ({ cart: [...state.cart, item] })),
      removeFromCart: (cartId) =>
        set((state) => ({ cart: state.cart.filter((i) => i.cartId !== cartId) })),
      setFulfillmentChannel: (channel) => set({ fulfillmentChannel: channel }),
      clearCart: () => set({ cart: [] }),   // fulfillmentChannel BİLİNÇLİ olarak sıfırlanmıyor
    }),
    { name: 'bowlera-cart' }
  )
)
```

> ⚠️ **Bu güncelleme, önceki v1.3'te yapılan bir HATAYI düzeltir:** `fulfillmentChannel`
> önceki sürümde yanlışlıkla `CartItem` tipine (§3) eklenmişti — ama gerçek kod
> (`store/useCartStore.ts`) bunun `CartState` seviyesinde **tek bir alan** olduğunu
> gösteriyor, her `CartItem`'da tekrarlanmıyor. Kaynak: kullanıcının paylaştığı gerçek
> dosya içeriği, bu turda görüldü.

### 2.4 `store/useCustomizerStore.ts` — Kâseni Yarat State

```ts
// store/useCustomizerStore.ts
// Amaç:    4 adımlı özelleştirme akışının state makinesi (adım + seçimler + canlı toplam)
// Bağlı:   StepBase/Protein/Toppings/Sauce, SummaryPanel, VisualPreview
// Risk:    Hatalı adım geçişi → kullanıcı eksik seçimle sepete ekleyebilir
// Dokunma: CUSTOMIZER_SPEC.md — adım sırası ve validasyon kuralları burada tanımlı

interface CustomizerState {
  currentStep: 1 | 2 | 3 | 4
  base: string | null
  protein: string | null
  toppings: string[]        // max 4 ücretsiz
  sauce: string | null
  goToStep: (step: 1 | 2 | 3 | 4) => void   // yalnızca önceki adımlar doluysa izin verir
  getTotals: () => { price: number; calories: number; protein: number; carbs: number; fat: number }
}
```

> ⚠️ Bu blok hâlâ 4 adımlı eski şemayı yansıtıyor — 5 adımlı geçiş (Karar #1, Oturum 2) bu
> dosyaya işlenmedi. Açık Sorun #10/#36 kapsamında, bu güncellemenin dışında bırakıldı.
> Gerçek kontrat için: `CUSTOMIZER_SPEC.md §3.1` (5 adımlı, güncel).

### 2.5 `components/menu/MenuCard.tsx`

```tsx
// components/menu/MenuCard.tsx
// Amaç:    Menü kartını render eder — fotoğraf, kalori (ZORUNLU), fiyat, "Özelleştir" butonu
// Bağlı:   Menü sayfası grid'i, Ana Sayfa "Öne Çıkan Ürünler"
// Risk:    Kalori alanı render edilmezse yasal/UX ihlali (MASTER_PLAN §5.5)
// Dokunma: DESIGN_SYSTEM.md §Renk — CTA rengi Primary Olive, badge'ler logo-degrade
```

### 2.6 `lib/integrations/whatsapp.ts`

```ts
// lib/integrations/whatsapp.ts
// Amaç:    Özelleştirilen kaseyi wa.me linkine dönüştürür
// Bağlı:   components/order/WhatsAppOrderButton.tsx (§2.9) — HENÜZ BAĞLANMADI
// Risk:    Encode hatası → şubeye eksik/bozuk sipariş mesajı gider
// Dokunma: INTEGRATIONS.md §2 — mesaj şablonu orada tanımlı

export function buildWhatsAppOrderLink(branchPhone: string, cart: CartItem[]): string {
  const message = formatOrderMessage(cart)   // INTEGRATIONS.md şablonuna göre
  return `https://wa.me/${branchPhone}?text=${encodeURIComponent(message)}`
}
```

> ⚠️ Bu fonksiyon var ama **hiçbir UI bileşeninden çağrılmıyor** — `INTEGRATIONS.md §0`
> "Şube telefon numaraları bekleniyor" diyor. `WhatsAppOrderButton.tsx` (§2.9) bilinçli
> olarak bu fonksiyona bağlanmadı (Katman Sınırı Kuralı madde 11).

### 2.7 `app/api/auth/otp/*` — Telefon + OTP Girişi

```ts
// app/api/auth/otp/send/route.ts + verify/route.ts
// Amaç:    Twilio Verify ile telefon+OTP girişi, başarılı doğrulamada Auth.js JWT session açar
// Bağlı:   /giris sayfası, Header'daki hesap ikonu (canlı doğrulandı — Oturum 4)
// Risk:    Twilio trial hesabı Türkiye'yi SMS için "restricted country" işaretliyor — bu route'lar
//          kod seviyesinde tamam ama canlıda uçtan uca fonksiyonel test edilemedi (Açık Sorun #32)
// Dokunma: INTEGRATIONS.md §5 — tam kontrat, edge case'ler ve rate limit orada
```

> ⚠️ Guest checkout bu akıştan bağımsızdır — `useCartStore` hiç dokunulmaz (§2.3).
> Auth katmanı sepetin üzerine kurulmaz, yanına eklenir. `app/siparis/page.tsx` (§2.9)
> oturum kontrolü YAPMAZ — bu bilinçli bir tasarım kararıdır.

> **DB durumu (Karar #20 ile güncellendi):** Neon Postgres (Vercel Marketplace) kuruldu,
> Drizzle ORM ile `users` tablosu oluşturuldu. JWT session artık DB'deki kalıcı kayıtla
> birlikte çalışıyor.

### 2.8 `app/api/user/profile/route.ts` + `app/hesap/page.tsx` — Kullanıcı Profili/Adres

```ts
// app/api/user/profile/route.ts
// Amaç:    GET — oturum sahibinin profilini (address, displayName) döner.
//          PATCH — oturum sahibinin profilini günceller.
// Bağlı:   app/hesap/page.tsx, components/account/{useProfileForm,ProfileForm}.tsx,
//          lib/db/queries/user-profile.ts, lib/user/profile-validation.ts, lib/auth/rate-limit.ts
// Risk:    Kimlik SADECE session.user.phone'dan alınır — request body'den phone kabul
//          edilirse başka bir kullanıcının profili üzerine yazılabilir (BSC-3, kritik sınır,
//          bkz. Katman Sınırı Kuralı §1 madde 8). PATCH `checkProfileRateLimit` ile korunur (BSC-7).
// Dokunma: lib/db/schema.ts'teki users tablosu şeması değişirse lib/user/profile-validation.ts
//          ve lib/db/queries/user-profile.ts da güncellenmeli
```

```tsx
// app/hesap/page.tsx
// Amaç:    Server component — oturum yoksa /giris'e redirect eder, varsa ProfileForm'u render eder
// Bağlı:   auth.ts (session kontrolü), components/account/ProfileForm.tsx
// Risk:    Adres toplama checkout'u BLOKLAMAZ (Karar #23, Katman Sınırı Kuralı §1 madde 9) —
//          bu sayfa tamamen opsiyonel, sepet/sipariş akışından bağımsızdır
```

> ⚠️ Bilinen açıklar: `ProfileForm.tsx`'teki Tailwind renk sınıfları DESIGN_SYSTEM.md
> görülmeden tahmin edildi, teyit edilmeli (Açık Sorun #38). Bu iki dosya + rate-limit
> kod seviyesinde tamam ama Twilio kısıtı (#32) yüzünden canlıda hiç fonksiyonel test
> edilemedi (Açık Sorun #39). Ayrıca bu dosya grubunun (7 dosya, Karar #23) gerçekten
> repoda mevcut olup olmadığı tek tek doğrulanmalı — bir tutarsızlık bu turda keşfedildi.

### 2.9 `app/siparis/page.tsx` — Checkout (Paket Servis / Gel Al)

```tsx
// app/siparis/page.tsx
// Amaç:    Sepet özeti + ZORUNLU teslimat kanalı seçimi + sipariş CTA'sı
// Bağlı:   store/useCartStore.ts, components/order/{OrderSummary,FulfillmentGate,WhatsAppOrderButton}.tsx
// Risk:    Kanal seçimi zorunlu kılınmazsa teslimat şekli belirsiz sipariş oluşur (Açık Sorun #26 — KAPANDI)
// Dokunma: Katman Sınırı Kuralı madde 7 — guest checkout burada da korunmalı, auth ZORUNLU KILINAMAZ
```

> **Karar (bu güncelleme):** WhatsApp CTA'sı bilinçli olarak devre dışı bırakıldı —
> `INTEGRATIONS.md §0`'daki şube telefon numarası blokajı çözülene kadar
> `lib/integrations/whatsapp.ts`'e bağlanmayacak (Katman Sınırı Kuralı madde 11, CORE §9).
> Sayfa boş sepette mesaj gösterir, kanal seçilene kadar CTA'nın nedenini açıkça belirtir.

---

## 3. VERİ MODELİ

```ts
// types/index.ts

type BowlItem = {
  id: string
  name: string
  category: "signature" | "build-your-own" | "içecek"
  price: number
  image: string                // DESIGN_SYSTEM.md §Fotoğraf Adlandırma Standardı
  tags: string[]                // "vegan", "glutensiz", "yüksek protein"
  allergens?: ("gluten" | "dairy" | "nuts" | "soy" | "shellfish")[]
  calories: number              // ZORUNLU alan — opsiyonel değil
  protein: number               // ZORUNLU alan
  carbs?: number
  fat?: number
}

type CustomizerSelection = {
  base: string
  protein: string
  toppings: string[]            // max 4 ücretsiz, ekstra ücretli
  sauce: string
}

type FulfillmentChannel = "pickup" | "dine-in"

type CartItem = {
  cartId: string                 // uuid — sepet içi benzersiz kimlik
  bowlItem: BowlItem | null      // imza kase ise dolu, custom ise null
  customization?: CustomizerSelection
  quantity: number
  unitPrice: number
  unitCalories: number
  // ⚠️ fulfillmentChannel BURADA DEĞİL — düzeltme: bkz. §2.3 notu. Kanal, CartState
  // seviyesinde tek bir alan, her CartItem'da tekrarlanmıyor (Karar #13).
}

type AuthenticatedUser = {
  phone: string                  // kimlik anahtarı — Karar #17, "1 numara = 1 hesap"
  verifiedAt: string             // ISO timestamp — son OTP doğrulama zamanı
  // Karar #20 ile bu alanlar artık KALICI OLARAK SAKLANIYOR — Neon Postgres, users tablosu.
  address?: string                // Karar #23 — SADECE profil/sadakat verisi, checkout'u bloklamaz
  displayName?: string
  loyaltyPoints?: number          // sadakat programı — mekanik henüz netleşmedi (Açık Sorun #30)
}
```

> Kaynak: MASTER_PLAN §5.5 — kalori/protein alanı zorunlu, opsiyonel değil.
>
> ⚠️ `BowlItem.category` enum'ı MASTER_PLAN §3.2'deki kategori isimleriyle senkron değil —
> Açık Sorun #35, bu güncellemenin kapsamı dışında.

---

## 4. DEPLOY & PERFORMANS

### 4.1 Deploy
| Alan | Değer |
|---|---|
| Platform | ✅ Vercel — proje `bowlera-site` olarak bağlı, deploy yeşil |
| Ortam Değişkenleri | CONFIG_SCHEMA.md'de tanımlı (v1.2 — `DATABASE_URL` dahil), platform dashboard'undan girilir |
| Veritabanı | ✅ Neon Postgres (Vercel Marketplace, Frankfurt region) — Karar #20 |
| Build Komutu | `next build` |
| Önizleme | Her PR için otomatik preview deploy önerilir |

### 4.2 Performans Hedefleri (Core Web Vitals)
> Kaynak: MASTER_PLAN §5.3

| Metrik | Hedef |
|---|---|
| LCP | < 2.5s |
| FID / INP | < 100ms |
| CLS | < 0.1 |
| Lighthouse Performans Puanı | 90+ |

**Uygulama kuralları:**
- Hero görseli `next/image` ile, `priority` flag'i ile yüklenir (LCP)
- Tüm animasyonlar yalnızca `transform`/`opacity` kullanır (CLS riski — AGENT.md §Self-Check)
- Font `next/font` ile self-host edilir, layout shift önlenir

### 4.3 Rollback / Geri Alma

```
1. Vercel/hosting panelinden önceki başarılı deploy'a "Instant Rollback"
2. Git: son commit'i revert et → otomatik yeniden deploy tetiklenir
3. Kritik veri değişikliği (menu-data.json şeması VEYA lib/db/schema.ts) varsa CORE.md §7.4 protokolü izlenir
4. Rollback sonrası SESSION_INDEX.md güncellenir, session_log'a 🔴 ile kaydedilir
```

---

## 5. SORUMLULUK SINIRLARI ÖZETİ

| Katman | Sorumlu Dosya | Sorumlu Değil |
|---|---|---|
| Veri kaynağı | `lib/menu-data.json` / CMS | Fiyat/kalori hesaplama mantığı |
| Fiyat/kalori hesaplama | `useCustomizerStore.getTotals()` | Render |
| Render | Bileşenler (`MenuCard`, `SummaryPanel`) | State mutasyonu |
| Sepet kalıcılığı + teslimat kanalı | `useCartStore` (persist) | Checkout UI, ödeme |
| Checkout / kanal zorunluluğu | `app/siparis/page.tsx`, `components/order/*` | Ödeme işlemi (henüz yok), WhatsApp gönderimi (blokajlı) |
| Kullanıcı kimliği/oturum | `auth.ts`, `app/api/auth/otp/*` | Sepet/checkout akışı (bağımsız kalır) |
| Kullanıcı profili/adres | `app/api/user/profile/route.ts`, `lib/db/queries/user-profile.ts` | Checkout/sipariş akışı (bloklamaz) |
| Üçüncü parti iletişim | `lib/integrations/*` (server-side) | UI (WhatsApp CTA henüz bağlı değil) |

---

*BOWLERA ARCHITECTURE.md — v1.4 — Session 4 — 2026-07-19*
*Kaynak: MASTER_PLAN.md §3, §5 · CORE.md §2, §4 · AGENT.md (BSC referansları)*
*v1.3: Karar #20/#23 senkronu (Açık Sorun #36 kapatıldı) — §2.7/§2.8 DB durumu, §3 AuthenticatedUser.address.*
*v1.4 (bu güncelleme — İKİ DEĞİŞİKLİK): (1) SELF-CORRECTION — v1.3'te `fulfillmentChannel`
yanlışlıkla `CartItem` tipine eklenmişti, gerçek `useCartStore.ts` kodu görülünce bunun
`CartState` seviyesinde tek alan olduğu doğrulandı ve düzeltildi (§2.3, §3). (2) Açık Sorun
#26 kapatıldı — yeni §2.9 `app/siparis/page.tsx` kontratı: sepet özeti + ZORUNLU kanal seçimi.
WhatsApp CTA'sı, şube telefon numarası blokajı (INTEGRATIONS.md §0) çözülene kadar BİLİNÇLİ
olarak devre dışı bırakıldı — sahte veri kullanılmadı (Katman Sınırı Kuralı yeni madde 10/11).
⚠️ #10 (5 adımlı customizer/§2.4 senkronu) ve #35 (category enum) hâlâ AÇIK, bu turun
kapsamı dışında bırakıldı.*
