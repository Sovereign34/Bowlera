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
                                                                          lib/integrations/whatsapp.ts | marketplace.ts
                                                                          (wa.me linki | Adisyo/SepetTakip API — server-side)

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
// Amaç:    Sepet öğelerini yönetir, tarayıcı kapansa da korur
// Bağlı:   CartBadge, CartDrawer, Customizer "Sepete Ekle" butonu
// Risk:    Hatalı state güncelleme → yanlış fiyat/miktar sepette görünür
// Dokunma: BSC-6 (race condition) kontrolü — çift tıklama koruması component tarafında

import { create } from 'zustand'
import { persist } from 'zustand/middleware'
import { CartItem } from '@/types'

interface CartState {
  cart: CartItem[]
  addToCart: (item: CartItem) => void
  removeFromCart: (cartId: string) => void
  clearCart: () => void
}

export const useCartStore = create<CartState>()(
  persist(
    (set) => ({
      cart: [],
      addToCart: (item) => set((state) => ({ cart: [...state.cart, item] })),
      removeFromCart: (cartId) =>
        set((state) => ({ cart: state.cart.filter((i) => i.cartId !== cartId) })),
      clearCart: () => set({ cart: [] }),
    }),
    { name: 'bowlera-cart-storage' }
  )
)
```

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
// Bağlı:   CartDrawer "WhatsApp ile Sipariş Ver" butonu
// Risk:    Encode hatası → şubeye eksik/bozuk sipariş mesajı gider
// Dokunma: INTEGRATIONS.md §WhatsApp Köprüsü — mesaj şablonu orada tanımlı

export function buildWhatsAppOrderLink(branchPhone: string, cart: CartItem[]): string {
  const message = formatOrderMessage(cart)   // INTEGRATIONS.md şablonuna göre
  return `https://wa.me/${branchPhone}?text=${encodeURIComponent(message)}`
}
```

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
> Auth katmanı sepetin üzerine kurulmaz, yanına eklenir.

> **DB durumu (Karar #20 ile güncellendi):** Bu belgenin önceki sürümü "DB henüz yok, session
> sadece JWT'de kalıcı" diyordu — bu artık DOĞRU DEĞİL. Neon Postgres (Vercel Marketplace)
> kuruldu, Drizzle ORM ile `users` tablosu (`phone`, `address`, `displayName`, `loyaltyPoints`,
> `verifiedAt`, `createdAt`) oluşturuldu. JWT session artık DB'deki kalıcı kayıtla birlikte
> çalışıyor — kullanıcı farklı cihaz/tarayıcıdan tekrar giriş yaptığında telefon numarasıyla
> eşleşen profil verisi DB'den okunur, sadece o oturuma özgü kalmaz.

### 2.8 `app/api/user/profile/route.ts` + `app/hesap/page.tsx` — Kullanıcı Profili/Adres

```ts
// app/api/user/profile/route.ts
// Amaç:    GET — oturum sahibinin profilini (address, displayName) döner.
//          PATCH — oturum sahibinin profilini günceller.
// Bağlı:   app/hesap/page.tsx, components/account/{useProfileForm,ProfileForm}.tsx,
//          lib/db/queries/user-profile.ts, lib/user/profile-validation.ts
// Risk:    Kimlik SADECE session.user.phone'dan alınır — request body'den phone kabul
//          edilirse başka bir kullanıcının profili üzerine yazılabilir (BSC-3, kritik sınır,
//          bkz. Katman Sınırı Kuralı §1 madde 8)
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

> ⚠️ Bilinen açıklar (kod içi yorumla işaretlendi, tahmin edilmedi — AGENT.md Kural #2):
> `route.ts` şu an rate-limit'siz — `lib/auth/rate-limit.ts`'in gerçek export imzası görülmeden
> entegre edilmedi (Açık Sorun #37). `ProfileForm.tsx`'teki Tailwind renk sınıfları
> DESIGN_SYSTEM.md görülmeden tahmin edildi, teyit edilmeli (Açık Sorun #38).
>
> ⚠️ Bu iki dosya kod seviyesinde tamam ama Twilio kısıtı (#32) yüzünden canlıda hiç
> fonksiyonel test edilemedi — giriş yapıp adres kaydetme akışı doğrulanmadı (Açık Sorun #39).

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

type CartItem = {
  cartId: string                 // uuid — sepet içi benzersiz kimlik
  bowlItem: BowlItem | null      // imza kase ise dolu, custom ise null
  customization?: CustomizerSelection
  quantity: number
  unitPrice: number
  unitCalories: number
  fulfillmentChannel: "pickup" | "dine-in"   // sepet/oturum seviyesinde tek alan — Karar #13
}

type AuthenticatedUser = {
  phone: string                  // kimlik anahtarı — Karar #17, "1 numara = 1 hesap"
  verifiedAt: string             // ISO timestamp — son OTP doğrulama zamanı
  // Karar #20 ile bu alanlar artık KALICI OLARAK SAKLANIYOR — Neon Postgres, users tablosu.
  // Auth.js JWT session, DB'deki bu kayıtla senkronize çalışır (bkz. §2.7 not).
  address?: string                // Karar #23 — SADECE profil/sadakat verisi, checkout'u bloklamaz
  displayName?: string
  loyaltyPoints?: number          // sadakat programı — mekanik henüz netleşmedi (Açık Sorun #30)
}
```

> Kaynak: MASTER_PLAN §5.5 — kalori/protein alanı zorunlu, opsiyonel değil.
> `AuthenticatedUser` — INTEGRATIONS.md §5 kaynaklı, Karar #20 (DB) ve Karar #23 (adres modeli)
> ile birlikte okunmalı.
>
> ⚠️ `BowlItem.category` enum'ı MASTER_PLAN §3.2'deki kategori isimleriyle (İmza Kaseler, Sıcak
> Tahıl Kaseleri, Vegan, İçecekler) senkron değil — Açık Sorun #35, bu güncellemenin kapsamı dışında.

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
> NEXUS'taki ayrı ROLLBACK.md dosyasının yerine — Bowlera'nın deploy ölçeğinde tek bölüm yeterli.

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
| Sepet kalıcılığı | `useCartStore` (persist) | Checkout/ödeme |
| Kullanıcı kimliği/oturum | `auth.ts`, `app/api/auth/otp/*` | Sepet/checkout akışı (bağımsız kalır) |
| Kullanıcı profili/adres | `app/api/user/profile/route.ts`, `lib/db/queries/user-profile.ts` | Checkout/sipariş akışı (bloklamaz) |
| Üçüncü parti iletişim | `lib/integrations/*` (server-side) | UI |

---

*BOWLERA ARCHITECTURE.md — v1.3 — Session 4 — 2026-07-19*
*Kaynak: MASTER_PLAN.md §3, §5 · CORE.md §2, §4 · AGENT.md (BSC referansları)*
*v1.1: §2.4 ve §5 — `calculateTotals` → `getTotals` olarak düzeltildi (CUSTOMIZER_SPEC.md ile tutarlılık, Açık Sorun #5 kapatıldı).*
*v1.2: §1 Katman Sınırı Kuralları'na madde 7 (auth/sepet bağımsızlığı) eklendi. Yeni §2.7 —
`app/api/auth/otp/*` kontratı. §3 Veri Modeli'ne `AuthenticatedUser` tipi + DB-agnostic uyarı
notu eklendi (Karar #17/#19, INTEGRATIONS.md §5). ⚠️ Bu dosya hâlâ 5 adımlı customizer'a ve
FulfillmentChannel'a göre senkron değil — Açık Sorun #10, bu güncellemenin kapsamı dışında.*
*v1.3 (bu güncelleme, Açık Sorun #36 kapatıldı): Karar #20 (Neon Postgres kuruldu, DB artık
KALICI) ve Karar #23 (adres/profil akışı) ile senkronize edildi. §1'e madde 8/9 eklendi. §2.7
"DB henüz yok" ifadesi düzeltildi. Yeni §2.8 — `app/api/user/profile/route.ts` +
`app/hesap/page.tsx` kontratı. §3'e `CartItem.fulfillmentChannel` ve `AuthenticatedUser.address`
eklendi, DB-agnostic uyarı notu "artık kalıcı saklanıyor" şeklinde güncellendi. §4.1'e Vercel/Neon
deploy durumu eklendi. §5'e iki yeni satır (kullanıcı kimliği, kullanıcı profili) eklendi.
⚠️ Bu güncelleme #36'yı kapatır ama #10 (5 adımlı customizer/FulfillmentChannel enum senkronu,
§2.4/§3 category) ve #35 (BowlItem.category enum uyuşmazlığı) hâlâ AÇIK — bu turun kapsamı dışında
bırakıldı, bilinçli olarak dokunulmadı.*
