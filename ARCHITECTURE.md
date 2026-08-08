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
                                              store/useCustomizerStore.ts (Zustand — 5 adımlı state makinesi)
                                                                     │
                                              ┌──────────────────────┼──────────────────────┐
                                              ▼                      ▼                      ▼
                                   components/customizer/  components/customizer/  components/customizer/
                                   StepBase/Main/Garden/    VisualPreview.tsx        SummaryPanel.tsx
                                   SignatureFlavor/Finish    (katmanlı CSS/SVG)      (fiyat/kalori canlı toplam)
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

app/kayit-ol/page.tsx ──► app/api/auth/register/route.ts ──► auth.ts (Auth.js JWT session)
(rıza esaslı kayıt — Session 8 ile BİRİNCİL akış oldu)                        │
                                                                                ▼
                                                                lib/db/client.ts (Neon Postgres, Drizzle ORM)
                                                                                │
                              ┌─────────────────────────────────┬─────────────┴─────────────────────────────────┐
                              ▼                                 ▼                                                ▼
                   consentRegistrations tablosu        users tablosu (phone, address,               app/hesap/page.tsx ──► app/api/user/profile/route.ts
                   (KVKK rıza kaydı, Session 8)         displayName, loyaltyPoints,                  (GET/PATCH — sadece session.user.phone kullanır)
                                                          verifiedAt, ⚠️ + doğrulama-durumu
                                                          alanı — KARARLAŞTIRILDI, HENÜZ
                                                          KODLANMADI, bkz. §2.7a)

⚠️ app/giris/page.tsx (Twilio OTP) — PARKLI (Açık Sorun #32/#56). Eski Twilio OTP UI'ı
   Session 8'de KALDIRILDI. Twilio kararı acil değil, bkz. §2.7 not.

⚠️ GENEL GİRİŞ/KAYIT AKIŞI (Session 11 — KARARLAŞTIRILDI, HENÜZ KODLANMADI, bkz. §2.7a):
   Guest kullanıcı menüde serbestçe gezinebilir → bir ürün SEÇTİĞİ an giriş sayfasına
   yönlendirilir (istisna: Masaya Sipariş guest girişi, §2.7a) → giriş sayfası her zaman
   [giriş] veya [kayıt] seçeneği sunar → kayıt seçilirse kullanıcı bilgisi + KVKK →
   kanal seçimi (Masaya Servis / Gel Al / Online Platform) ZORUNLU tamamlanmadan kayıt
   bitmez.

app/api/orders/history/route.ts ──► order_history tablosu (Neon Postgres, Session 10'da
   migrate edildi ve doğrulandı) — Personel Sipariş Paneli (#62) için temel veri katmanı.
   ⚠️ Bu route ve panelin kendisi HENÜZ KODLANMADI — sadece DB şeması hazır.
```

### Katman Sınırı Kuralları

```
1. Menü verisi her zaman lib/menu-data.json veya CMS'ten okunur — bileşen içine hardcode edilemez
2. Kalori/protein alanı BowlItem tipinde zorunlu — komponent bu alanı gizleyemez/opsiyonel gösteremez
3. Sepet state'i sadece useCartStore üzerinden değişir — bileşenler doğrudan localStorage'a yazamaz
4. Üçüncü parti API çağrıları (Adisyo/SepetTakip/Twilio) sadece app/api/ Route Handler'larından yapılır — client component'ten asla
5. Customizer adım sırası useCustomizerStore'daki currentStep ile kontrol edilir — URL manipülasyonuyla atlanamaz
6. Tasarım sistemi token'ları (renk/tipografi) sadece tailwind.config.ts üzerinden kullanılır — inline hex kod yasak (DESIGN_SYSTEM.md)
7. ⚠️ **[Session 12 ile GÜNCELLENDİ, henüz kodlanmadı]** Auth katmanı sepet akışından
   tamamen bağımsız DEĞİL artık — ama kapsam Session 11'e göre DARALTILDI. Masaya Sipariş
   (§2.7b) artık bu sitenin auth/kanal-seçimi mimarisinin TAMAMEN DIŞINDA, ayrı bir
   yüzeyde (`/masaya-siparis/*`) yaşıyor — `middleware.ts`'in matcher'ı (`/menu/customize/:path*`)
   bu yüzeyi hiç kapsamaz, YENİ BİR İSTİSNA YAZILMASINA GEREK YOK. Gel Al ve Online
   Platform kanallarında ürün seçimi hâlâ giriş/kayıt akışını TETİKLER (§2.7a).
   `useCartStore` hem `/menu/customize/*` (Gel Al) hem `/masaya-siparis/*` (Masaya) tarafından
   PAYLAŞILIR — store'un kendisi auth durumuna göre dallanmaz (state mutasyonu değişmedi),
   sadece iki farklı giriş noktası (route) vardır, ikisi de aynı store'u kullanır.
8. Kullanıcı profili/adres verisi SADECE app/api/user/profile/route.ts üzerinden okunur/yazılır — bu route request body'den phone KABUL ETMEZ, kimlik her zaman session'dan (session.user.phone) alınır (BSC-3 kritik sınır, Karar #23)
9. Adres alanı sipariş akışını (checkout) BLOKLAMAZ — FulfillmentChannel ("pickup" | "dine-in") delivery içermediği için adres sadece profil/sadakat verisidir, opsiyonel olarak /hesap sayfasında toplanır (Karar #23)
10. Teslimat kanalı (fulfillmentChannel) app/siparis/page.tsx'te ZORUNLU seçim haline getirilir — kanal seçilmeden WhatsApp sipariş CTA'sı aktif olamaz (Açık Sorun #26, KAPANDI)
11. Üçüncü parti entegrasyon için gerekli kimlik bilgisi (ör. şube telefon numarası) eksikken ilgili CTA gerçek işlevle bağlanamaz — sahte/placeholder değer YASAK (BSC-5, CORE §9); bunun yerine CTA bilinçli olarak devre dışı + açıklamalı bırakılır
12. [YENİ, Session 11 — KARARLAŞTIRILDI, HENÜZ KODLANMADI] Gel Al kanalında ilk sipariş,
    Personel Sipariş Paneli üzerinden personel tarafından telefon/WhatsApp ile erişim teyidi
    yapılıp MANUEL ONAY verilmeden tamamlanamaz. Onay sonrası kullanıcının doğrulama durumu
    `confirmed` olarak işaretlenir, sonraki siparişler bu adımı tekrarlamaz (§2.7a, Açık
    Sorun #64 — KAPANDI).
```

> ⚠️ **ÖNEMLİ NOT (bu güncelleme, Session 11 senkronu):** Yukarıdaki madde 7 ve 12 ile
> §2.7a'da tarif edilen genel giriş/kayıt akışı SESSION_INDEX.md'deki Session 11 kararlarına
> dayanır — bu kararlar netleşti ama **kod olarak henüz üretilmedi**. Bu dosyanın amacı
> kararı doğru yerde belgelemek; kod yazılana kadar madde 7 (eski hâli) fiilen hâlâ
> yürürlüktedir. Kod üretildiğinde bu not kaldırılır.

---

## 2. MODÜL KONTRATLARI

### 2.1 `app/layout.tsx` — Root Layout

```tsx
// app/layout.tsx
// Amaç:    Tüm sayfalar için ortak iskelet — font, tema, Header/Footer, oturum context'i
// Bağlı:   Her sayfa buradan render edilir
// Risk:    Hatalı font/tema yüklemesi → tüm site etkilenir.
//          SessionProvider olmadan Header/diğer client component'ler useSession() çağıramaz.
// Dokunma: DESIGN_SYSTEM.md §Tipografi kontrol et

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="tr">
      <body className={`${cormorantGaramond.variable} ${nunito.variable}`}>
        <SessionProvider>
          <Header />
          {children}
          <Footer />
        </SessionProvider>
      </body>
    </html>
  )
}
```

> Açık Sorun #33 (Header hesap ikonu oturum-farkında değildi) bu yapıyla KAPANDI —
> `SessionProvider` (next-auth/react) eklendi, `Header.tsx` `useSession()` ile okuyor.

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
//          fulfillmentChannel boş kalırsa teslimat şekli belirsizleşir (Açık Sorun #26, KAPANDI)
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

### 2.4 `store/useCustomizerStore.ts` — Kâseni Yarat State

```ts
// store/useCustomizerStore.ts
// Amaç:    5 adımlı özelleştirme akışının state makinesi (adım + seçimler + canlı toplam)
// Bağlı:   StepBase/Main/Garden/SignatureFlavor/Finish, SummaryPanel, VisualPreview
// Risk:    Hatalı adım geçişi → kullanıcı eksik seçimle sepete ekleyebilir
// Dokunma: CUSTOMIZER_SPEC.md §3 — adım sırası, guard mantığı ve validasyon kuralları
//          birebir buradan alınmıştır; bu iki dosya SENKRON tutulmalı

interface CustomizerSelection {
  base: string | null
  main: string | null
  mainPortion: 'single' | 'double'
  garden: string[]              // max 4 ücretsiz (avokado hariç), sonrası ücretli
  signatureFlavor: string | null
  finish: string[]              // max 1 ücretsiz, sonrası ücretli
  extras: {
    extraAvocado: boolean
    extraSauce: boolean
    extraCrunch: boolean
  }
}

interface CustomizerState {
  currentStep: 1 | 2 | 3 | 4 | 5
  selections: CustomizerSelection
  maxReachedStep: 1 | 2 | 3 | 4 | 5   // guard için — ileri atlama kontrolü

  selectBase: (id: string) => void
  selectMain: (id: string, portion: 'single' | 'double') => void
  toggleGardenItem: (id: string) => void
  selectSignatureFlavor: (id: string) => void
  toggleFinishItem: (id: string) => void
  toggleExtra: (key: keyof CustomizerSelection['extras']) => void
  goToStep: (step: 1 | 2 | 3 | 4 | 5) => void   // step <= maxReachedStep+1 değilse no-op
  nextStep: () => void                           // mevcut adım validasyonunu geçmeden ilerlemez
  previousStep: () => void
  reset: () => void

  getTotals: () => { price: number; calories: number; protein: number; carbs: number; fat: number }
  isStepValid: (step: 1 | 2 | 3 | 4 | 5) => boolean
}
```

> Adım sırası: 1. Base → 2. Main → 3. Garden → 4. Signature Flavor → 5. Finish
> (Karar #1, Oturum 2). `goToStep` guard'ı `step <= maxReachedStep + 1` kuralına uyar,
> URL manipülasyonuyla atlanamaz (§1 Katman Sınırı Kuralı madde 5, CUSTOMIZER_SPEC.md §3.2).
> "Sepete Ekle" YALNIZCA `isStepValid(5)` true olduğunda aktiftir — yani base + main +
> signatureFlavor doldurulmuş olmalı; Garden ve Finish opsiyonel olduğu için o adımların
> kendisi her zaman "valid" sayılır (CUSTOMIZER_SPEC.md §7).
>
> ✅ Açık Sorun #10 KAPANDI (Session 4) — bu blok CUSTOMIZER_SPEC.md §3.1 (v1.1) ile senkron.

### 2.5 `components/menu/MenuCard.tsx`

```tsx
// components/menu/MenuCard.tsx
// Amaç:    Menü kartını render eder — fotoğraf, kalori (ZORUNLU), fiyat, "Özelleştir" butonu
// Bağlı:   Menü sayfası grid'i, Ana Sayfa "Öne Çıkan Ürünler"
// Risk:    Kalori alanı render edilmezse yasal/UX ihlali (MASTER_PLAN §5.5)
// Dokunma: DESIGN_SYSTEM.md §Renk — CTA rengi Primary Olive, badge'ler logo-degrade
```

> ⚠️ [Session 11 ile İLGİLİ, henüz kodlanmadı] "Özelleştir" tıklaması, kanalın Masaya
> Sipariş olmadığı durumlarda artık giriş/kayıt akışını (§2.7a) tetikleyecek şekilde
> genişleyecek — bu bileşenin kendisi değişmeyecek, yönlendirme mantığı üst seviyede
> (route/middleware) ele alınacak. Bu dosyanın "Dokunma" alanına henüz eklenmedi çünkü
> kesin uygulama noktası (component mi, middleware mi) kodlama aşamasında netleşecek.

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
> [Session 11] Bu akış artık Gel Al kanalının ilk-sipariş manuel onay kuyruğuyla da
> kesişiyor (§2.7a, §2.9) — Personel Sipariş Paneli (#62) tasarımı netleşince bu bölüm
> güncellenecek.

### 2.7 `app/api/auth/register/route.ts` — Rıza Esaslı Kayıt (`/kayit-ol`)

```ts
// app/api/auth/register/route.ts
// Amaç:    Kullanıcı bilgisi + KVKK rızası alarak hesap oluşturur, Auth.js JWT session açar
// Bağlı:   app/kayit-ol/page.tsx, lib/registration/validation.ts, lib/auth/rate-limit.ts,
//          lib/db/queries (consentRegistrations + users tabloları)
// Risk:    KVKK rızası kaydedilmeden hesap açılırsa yasal risk; rate-limit'siz bırakılırsa
//          kayıt endpoint'i kötüye kullanılabilir (BSC-7)
// Dokunma: KVKK metni değişirse app/kvkk/page.tsx ve bu route'un rıza-versiyon alanı
//          birlikte güncellenmeli

// [Session 8] Eski app/giris/page.tsx (Twilio OTP) UI'ı KALDIRILDI.
// Bu route artık BİRİNCİL kayıt/giriş akışıdır. Backend + Frontend tamam, /kayit-ol'a
// BAĞLANDI, consentRegistrations migration'ı canlıda koşuldu, uçtan uca test BAŞARILI.
```

> ⚠️ **Bilinen açık:** Kayıt sonrası oturum/kullanıcı adı gösterimi netleşmedi (Açık Sorun #59).
>
> ⚠️ **Twilio/Netgsm — PARKLI (#32/#56):** `app/giris/page.tsx` (Twilio Verify OTP akışı)
> Session 8'de arayüzden kaldırıldı. Backend route'ları (`app/api/auth/otp/*`) kod
> seviyesinde repoda duruyor olabilir ama **aktif kullanılmıyor** — canlı akışa bağlı
> değil. Twilio'nun Türkiye'yi "restricted country" işaretlemesi (Açık Sorun #32) hâlâ
> çözülmedi, ama bu artık acil değil çünkü birincil akış `/kayit-ol`'a taşındı.
> Twilio/Netgsm nihai kararı (kullanılacak mı, hangi sağlayıcı) hâlâ AÇIK.

### 2.7a Genel Giriş/Kayıt Akışı — [Session 11, KARARLAŞTIRILDI, HENÜZ KODLANMADI]

> ⚠️ Bu alt bölüm henüz karşılık gelen kodu olmayan bir MİMARİ KARAR belgesidir.
> SIRADAKİ GÖREVLER listesindeki 1b maddesi bu kontratı kodlayacaktır. Kod üretildiğinde
> bu blok normal bir modül kontratına (dosya + amaç/bağlı/risk/dokunma) dönüştürülmeli.
>
> ⚠️ **[Session 12 ile KAPSAM DARALTILDI]** Bu bölüm artık SADECE Gel Al ve Online
> Platform kanallarını kapsar. Masaya Sipariş bu akıştan tamamen ÇIKARILDI — kendi ayrı
> mimarisi için bkz. §2.7b. Aşağıdaki akış/tablo bu değişikliğe göre güncellenmiştir.

**Akış:**
1. Girişsiz (guest) kullanıcı menüde serbestçe gezinebilir.
2. Bir ürün **seçtiği an** (customizer'a girmek üzere tıklamak, `/menu/customize/*`)
   giriş sayfasına yönlendirilir. **Masaya Sipariş bu akışın dışındadır** (§2.7b) —
   `/masaya-siparis/*` bu kurala tabi değildir, ayrı bir route prefix'idir.
3. Giriş sayfası her zaman iki seçenek sunar: **giriş** veya **kayıt**.
4. Kayıt seçilirse: kullanıcı bilgileri + KVKK metni okutulur → giriş sağlanmadan ÖNCE
   kanal seçimi (Gel Al / Online Platform) ZORUNLU.

**Kanal bazlı davranış:**

| Kanal | Bilgi/Giriş gereksinimi | Sipariş tamamlama koşulu |
|---|---|---|
| Gel Al | Hesapla giriş (kayıt veya mevcut hesap), sepeti serbestçe doldurur | **İlk siparişte** Personel Sipariş Paneli'nden (§2.9a) personel, telefon/WhatsApp üzerinden erişim teyidi yaptıktan sonra MANUEL ONAY vermeden sipariş tamamlanmaz |
| Online Platform | — | `/online-siparis` (henüz yok, Açık Sorun #57) üzerinden Yemeksepeti/Getir/Trendyol'a yönlendirme |

> ⚠️ Masaya Sipariş satırı bu tablodan Session 12'de ÇIKARILDI — sebep silme değil,
> TAŞIMA: bkz. §2.7b. Not: `RegistrationChannel` tipinden (`types/index.ts`)
> `"masaya-siparis"` değerinin çıkarılıp çıkarılmayacağı HENÜZ KARARLAŞTIRILMADI — bu
> dosya `types/index.ts`'i içermiyor, kod üretilirken netleştirilmeli (Açık Sorun, yeni).

**Doğrulama durumu alanı (Açık Sorun #64 — KAPANDI, Session 11):** Gel Al kanalında ilk
siparişteki manuel onay sırasında kullanıcı zaten DB'ye yazıldığı için, onay adımı SADECE
ilk siparişte gereklidir. Mimari yansıması: `AuthenticatedUser` tipine bir doğrulama durumu
alanı eklenir (bkz. §3, `verificationStatus: "pending" | "confirmed"`), ilk onaydan sonra
sonraki siparişler otomatik "confirmed"/aktif sayılır.

**Personel Sipariş Paneli ile kesişim (Açık Sorun #62 — hâlâ AÇIK, kapsam genişledi):**
"Kasa paneli" ile Açık Sorun #62'de tanımlı Personel Sipariş Paneli AYNI panel olduğu
teyit edildi. Panel artık hem Masaya Sipariş'in gerçek-zamanlı akışını (§2.7b'den gelen
siparişler) hem Gel Al'ın ilk-sipariş manuel onay kuyruğunu yönetecek. Personel auth
yöntemi, real-time teknoloji (WebSocket/SSE/polling) ve onay kuyruğu UI/veri modeli
**HÂLÂ TASARLANMADI** — bkz. §2.9a.

### 2.7b Masaya Sipariş — Ayrı QR Menü Sayfası — [Session 12, KARARLAŞTIRILDI, HENÜZ KODLANMADI]

> ⚠️ **KARAR GEREKÇESİ:** Session 11'de Masaya Sipariş'in genel giriş/kayıt akışı içinde
> "bilgi vermeden guest istisnası" olarak yaşaması kararlaştırılmıştı (§2.7a eski hâli).
> Session 12'de kod incelemesi sırasında ortaya çıktı: mevcut `RegistrationForm.tsx` TÜM
> kanallar için (Masaya dahil) aynı ad/telefon/KVKK formunu zorunlu tutuyordu — bu, Session
> 11 kararıyla DOĞRUDAN ÇELİŞİYORDU (Açık Sorun #65). Kullanıcıyla değerlendirildi: bu
> çelişkiyi kod-içi istisnalarla ("iki farklı UX modelini tek akışta zorlamak") çözmek
> yerine, Masaya Sipariş'i TAMAMEN AYRI bir yüzeye taşımak kararlaştırıldı. Gerekçe: masada
> oturan müşterinin QR okutup saniyeler içinde sipariş verebilmesi gerekiyor — ad/telefon/
> KVKK formu bu deneyime uymuyor. Bu karar #65'i çözmüyor, ORTADAN KALDIRIYOR.

```
// app/masaya-siparis/page.tsx (+ app/masaya-siparis/customize/[id]/page.tsx)
// Amaç:    Genel QR'dan gelen misafirin, HİÇBİR kimlik/rıza bilgisi vermeden menüyü
//          gezip özelleştirip doğrudan sipariş verebildiği bağımsız yüzey
// Bağlı:   lib/menu-data.json (AYNI veri kaynağı, kopya YOK), store/useCartStore.ts
//          (PAYLAŞILIR — §1 madde 7), order_history tablosu (channel="dine-in")
// Risk:    Bu route'un `/menu/customize/*` matcher'ına YANLIŞLIKLA dahil edilmesi guard'ı
//          bozar (tüm masaya misafirlerini girişe zorlar); tersi de mümkün — matcher
//          genişletilirken bu prefix'in dışarıda kaldığından emin olunmalı
// Dokunma: middleware.ts matcher'ı DEĞİŞMİYOR — bu route zaten kapsamı dışında, bu
//          yüzden guest-gate kodunda HİÇBİR değişiklik gerekmiyor (bkz. §1 madde 7)
```

**Netleşen kararlar:**
- Route prefix: `/masaya-siparis/*` — mevcut kod tabanındaki `"masaya-siparis"` terimiyle
  tutarlı (bkz. `channel-options.ts`), yeni bir isim uydurulmadı.
- Sepet: `useCartStore` PAYLAŞILIR, ayrı/basitleştirilmiş bir state kurulmuyor — sebep:
  customizer fiyat/kalori hesaplama mantığı zaten yazılı+test edilmiş
  (`customizer-summary-format.test.ts`), tekrar yazmak Sahte Veri Yasağı ruhuna aykırı
  bir bakım yükü yaratırdı.
- Guest gate etkisi: `middleware.ts` matcher'ı `/menu/customize/:path*` olarak KALIYOR —
  `/masaya-siparis/*` bu prefix'in dışında olduğu için middleware'e YENİ BİR İSTİSNA
  YAZILMASINA GEREK YOK. Açık Sorun #65 bu kararla KAPANIYOR (kod üretildiğinde).
- **[YENİ, #67 KAPANDI]** Checkout: `/masaya-siparis`'in **kendi bağımsız mini-checkout'u**
  olacak — `app/siparis/page.tsx`'in (§2.9, artık Gel Al'a özel) bir varyantı DEĞİL, ayrı
  bir bileşen/route (`app/masaya-siparis/checkout/page.tsx` gibi, kesin dosya adı bu
  yüzey kodlanırken netleşecek). Gerekçe: bu bölümün başındaki KARAR GEREKÇESİ'yle
  tutarlılık — Masaya'yı auth/kanal-seçimi mimarisinden TAMAMEN izole etmenin asıl amacı,
  `/siparis`'e bağlanmanın Gel Al'a özel mantığı (hesap girişi zorunluluğu, ilk-sipariş
  manuel onay) yanlışlıkla Masaya'ya sızdırma riskini taşımasıydı. Fiyat/sepet özet
  gösterimi (`SummaryPanel.tsx` gibi paylaşılan bir bileşen üzerinden) paylaşılabilir —
  paylaşılan, checkout AKIŞININ KENDİSİ değil, sadece gösterim katmanı olmalı.

**[#68 KAPANDI, bu güncelleme]** `RegistrationChannel` tipinden (`types/index.ts`)
`"masaya-siparis"` değeri ÇIKARILDI, `FulfillmentChannel`'a taşınmadı (zaten oradaki
`"dine-in"` karşılığı yeterli). `lib/db/schema.ts` incelendi: `consentRegistrations.channel`
sütunu Postgres enum DEĞİL, düz `text` — migration gerekmedi. Şema notu:
`docs/schema-changes/20260808000000_registration_channel_masaya_siparis_cikarildi.md`.

**HÂLÂ AÇIK olan soru (kod üretilmeden netleşmeli):**
1. Sipariş `order_history`'ye düştüğünde Personel Paneli'nin (§2.9a) bunu nasıl ayırt
   edeceği — `channel: "dine-in"` alanı zaten yeterli mi, yoksa ek bir kaynak/route
   alanı mı gerekiyor? (Açık Sorun #69)



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
// Amaç:    Server component — oturum yoksa /kayit-ol'a redirect eder, varsa ProfileForm'u render eder
// Bağlı:   auth.ts (session kontrolü), components/account/ProfileForm.tsx
// Risk:    Adres toplama checkout'u BLOKLAMAZ (Karar #23, Katman Sınırı Kuralı §1 madde 9) —
//          bu sayfa tamamen opsiyonel, sepet/sipariş akışından bağımsızdır
```

> ⚠️ **[Bu güncelleme]** Redirect hedefi `/giris` → `/kayit-ol` olarak düzeltildi (Session 8
> ile birincil akış değişti, bu dosya güncellenmemişti — geriye dönük senkron).
>
> ⚠️ Bilinen açıklar: `ProfileForm.tsx`'teki Tailwind renk sınıfları DESIGN_SYSTEM.md
> görülmeden tahmin edildi, teyit edilmeli (Açık Sorun #38).

### 2.9 `app/siparis/page.tsx` — Checkout (Gel Al)

```tsx
// app/siparis/page.tsx
// Amaç:    Sepet özeti + ZORUNLU teslimat kanalı seçimi + sipariş CTA'sı
// Bağlı:   store/useCartStore.ts, components/order/{OrderSummary,FulfillmentGate,WhatsAppOrderButton}.tsx
// Risk:    Kanal seçimi zorunlu kılınmazsa teslimat şekli belirsiz sipariş oluşur (Açık Sorun #26 — KAPANDI)
// Dokunma: ⚠️ [Session 12 ile GÜNCELLENDİ] Bu sayfa artık SADECE Gel Al kanalı içindir —
//          guest checkout istisnası TAMAMEN KALKTI (Masaya Sipariş §2.7b'ye taşındı, kendi
//          ayrı akışı olacak). Gel Al kanalında artık hesap girişi ön koşuldur (§2.7a).
//          §2.7b Açık Soru #1: Masaya'nın kendi checkout'u bu sayfanın varyantı mı olacak,
//          netleşmedi — netleşene kadar bu sayfa Gel Al'a özel kalır.
```

> **Karar:** WhatsApp CTA'sı bilinçli olarak devre dışı bırakıldı —
> `INTEGRATIONS.md §0`'daki şube telefon numarası blokajı çözülene kadar
> `lib/integrations/whatsapp.ts`'e bağlanmayacak (Katman Sınırı Kuralı madde 11, CORE §9).
> Sayfa boş sepette mesaj gösterir, kanal seçilene kadar CTA'nın nedenini açıkça belirtir.

### 2.9a Personel Sipariş Paneli — [Açık Sorun #62, TASARIM AŞAMASINDA]

```
// Amaç:    (1) Masaya Sipariş'in gerçek-zamanlı akışını (artık §2.7b'deki
//          `/masaya-siparis/*` yüzeyinden gelir) VE (2) Gel Al'ın ilk-sipariş manuel
//          telefon/WhatsApp onay kuyruğunu TEK panelde yönetmek
// Bağlı:   order_history tablosu (Neon Postgres, Session 10'da migrate edildi ve
//          doğrulandı — bu panelin temel veri katmanı hazır)
// Risk:    Personel auth zayıfsa sipariş verisi/onay yetkisi yetkisiz erişime açılır (BSC ihlali riski)
// Dokunma: Bu bölüm henüz bir dosya kontratı DEĞİL — aşağıdaki 3 karar netleşmeden
//          kod üretilemez (AGENT.md Self-Check: "Tüm gerekli dosyalar sağlandı mı?")
//          [Session 12] §2.7b Açık Soru #3 (order_history'de kanal ayrımı) burayı da etkiler.
```

**Hâlâ AÇIK olan 3 mimari soru:**
1. Personel auth yöntemi (ayrı personel hesabı mı, rol bazlı mı, PIN mi?)
2. Real-time teknoloji seçimi (WebSocket / SSE / polling?)
3. Onay kuyruğu UI/veri modeli — `pending`/`confirmed` durumların panelde nasıl gösterileceği

> Bu üç soru netleşmeden bu modül için `confidence: HIGH` verilemez (AGENT.md Self-Check,
> Bağlam Katmanı). SIRADAKİ GÖREVLER listesinde öncelik 1 olarak duruyor — 1b tamamlandıktan
> sonra ele alınacak (bkz. sohbetteki önceki KARAR BİLDİRİMİ gerekçesi).

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

type FulfillmentChannel = "pickup" | "dine-in"
// ⚠️ [Session 12 ile GÜNCELLENDİ] "dine-in" değeri artık Gel Al kanalının giriş/kayıt
// akışından DEĞİL, §2.7b'deki ayrı `/masaya-siparis/*` yüzeyinden geliyor. Online Platform
// kanalı hâlâ checkout'u değil, ayrı bir yönlendirme sayfasını (/online-siparis, Açık
// Sorun #57) kullanıyor. [#68 KAPANDI] Bu tipe üçüncü bir değer eklenmedi —
// RegistrationChannel'daki "masaya-siparis" FulfillmentChannel'a taşınmadan, doğrudan
// union'dan çıkarıldı (bkz. RegistrationChannel tanımı, types/index.ts).

type CartItem = {
  cartId: string                 // uuid — sepet içi benzersiz kimlik
  bowlItem: BowlItem | null      // imza kase ise dolu, custom ise null
  customization?: CustomizerSelection   // §2.4'teki 5 adımlı seçim şeması — özel kase ise dolu
  quantity: number
  unitPrice: number
  unitCalories: number
  // ⚠️ fulfillmentChannel BURADA DEĞİL — kanal, CartState seviyesinde tek bir alan,
  // her CartItem'da tekrarlanmıyor (Karar #13, bkz. §2.3).
}

type AuthenticatedUser = {
  phone: string                  // kimlik anahtarı — Karar #17, "1 numara = 1 hesap"
  verifiedAt: string             // ISO timestamp — son doğrulama/kayıt zamanı
  // Karar #20 ile bu alanlar KALICI OLARAK SAKLANIYOR — Neon Postgres, users tablosu.
  address?: string                // Karar #23 — SADECE profil/sadakat verisi, checkout'u bloklamaz
  displayName?: string
  loyaltyPoints?: number          // sadakat programı — mekanik henüz netleşmedi (Açık Sorun #30)
  verificationStatus?: "pending" | "confirmed"
  // ⚠️ [YENİ, Session 11, Açık Sorun #64 — KARAR KAPANDI, HENÜZ KODLANMADI]
  // Gel Al kanalında ilk sipariş onayı bekleniyorsa "pending", personel manuel onay
  // verdikten sonra "confirmed" — sonraki siparişler tekrar onay istemez (§2.7a).
  // Online Platform kanalında bu alan kullanılmaz (marketplace yönlendirmesi).
  // [Session 12] Masaya Sipariş artık AuthenticatedUser kapsamının dışında — §2.7b,
  // hiç kimlik/hesap oluşturmuyor.
}

type OrderHistoryEntry = {
  // ⚠️ [YENİ, Session 10 — DB TABLOSU CANLIDA VAR, TypeScript tipi HENÜZ TANIMLANMADI]
  // order_history tablosu migrate edildi ve doğrulandı ama bu tipin alan listesi bu
  // güncellemenin kapsamı dışında — Personel Sipariş Paneli (§2.9a) tasarlanırken
  // netleştirilmeli. Burada YER TUTUCU olarak bırakılıyor, hardcode/varsayım YAPILMADI
  // (AGENT.md Kural #4, Sahte Veri Yasağı).
}
```

> Kaynak: MASTER_PLAN §5.5 — kalori/protein alanı zorunlu, opsiyonel değil.
> `CustomizerSelection` tipinin tam tanımı için: §2.4 (bu dosya) ve CUSTOMIZER_SPEC.md §3.1
> — iki dosya senkron tutulmalı, tip burada tekrar edilmiyor (AGENT.md Kural #5).
>
> ⚠️ `BowlItem.category` enum'ı MASTER_PLAN §3.2'deki kategori isimleriyle senkron değil —
> Açık Sorun #35, bu güncellemenin kapsamı dışında.

---

## 4. DEPLOY & PERFORMANS

### 4.1 Deploy
| Alan | Değer |
|---|---|
| Platform | ✅ Vercel — proje `bowlera-site` olarak bağlı, deploy yeşil |
| Ortam Değişkenleri | CONFIG_SCHEMA.md'de tanımlı, platform dashboard'undan girilir — ⚠️ CONFIG_SCHEMA.md v1.2 de bu Session 8-11 kararlarına göre AYRI olarak güncellenmeli (bu görevin 2. adımı) |
| Veritabanı | ✅ Neon Postgres (Vercel Marketplace, Frankfurt region) — Karar #20. Session 8: `consentRegistrations` tablosu eklendi. Session 10: `order_history` tablosu eklendi. |
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
4. Rollback sonrası SESSION_INDEX.md güncellenir, ilgili maddeye 🔴 ile işaretlenir
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
| Kullanıcı kimliği/oturum (rıza esaslı) | `auth.ts`, `app/api/auth/register/*` (`/kayit-ol`) | Sepet/checkout akışı (Masaya Sipariş kanalında bağımsız kalır; diğer kanallarda giriş ön koşul — §2.7a, henüz kodlanmadı) |
| Kullanıcı profili/adres | `app/api/user/profile/route.ts`, `lib/db/queries/user-profile.ts` | Checkout/sipariş akışı (bloklamaz) |
| Üçüncü parti iletişim | `lib/integrations/*` (server-side) | UI (WhatsApp CTA henüz bağlı değil) |
| Genel giriş/kayıt akışı (guest gate, kanal seçimi zorunluluğu) | ⚠️ HENÜZ BİR DOSYA YOK — §2.7a'daki karar, 1b görevinde kodlanacak | — |
| Personel Sipariş Paneli (#62) | ⚠️ HENÜZ BİR DOSYA YOK — §2.7b'deki açık soru (#69) netleşmeden kodlanamaz (#68 KAPANDI) | `order_history` DB şeması (zaten canlıda, ayrı katman) |

---

*BOWLERA ARCHITECTURE.md — v1.9 — Session 12 devamı — 2026-08-08*
*Kaynak: MASTER_PLAN.md §3, §5 · CORE.md §2, §4 · AGENT.md (BSC referansları) · SESSION_INDEX.md (Session 8-12 senkronu)*
*v1.9 (bu güncelleme): §2.7b Açık Soru #1 (RegistrationChannel/FulfillmentChannel tip etkisi)
KAPANDI — Açık Sorun #68. `lib/db/schema.ts` ve `types/index.ts` bu turda görüldü (ilk kez).
Karar: `RegistrationChannel`'dan `"masaya-siparis"` ÇIKARILDI, `FulfillmentChannel`'a
taşınmadı. Gerekçe: `consentRegistrations.channel` sütunu Postgres enum değil düz `text` —
migration gerekmedi, geçmiş Session 9 canlı satırları etkilenmedi. Şema notu:
`docs/schema-changes/20260808000000_registration_channel_masaya_siparis_cikarildi.md`.
§2.7b'deki açık soru listesi 2'den 1'e indi (sadece #69 kaldı). Değişiklikler: (1) §2.7b
Açık Soru #1 KAPANDI notu; (2) §3 `FulfillmentChannel` yorumu senkronize edildi; (3) §5
Personel Sipariş Paneli satırı güncellendi. ⚠️ Bu güncelleme dokümantasyon + tip değişikliği
(`types/index.ts` düzenlendi) — Personel Paneli'nin kendisi hâlâ KODLANMADI (#69 açık).*
*v1.8 (önceki güncelleme): §2.7b Açık Soru #1 (checkout varyantı) KAPANDI — kullanıcı onayıyla
Seçenek A benimsendi: `/masaya-siparis` KENDİ BAĞIMSIZ mini-checkout'unu kullanacak,
`app/siparis/page.tsx`'in (§2.9, Gel Al'a özel) varyantı OLMAYACAK. Gerekçe: Session 12'nin
Masaya'yı auth/kanal-seçimi mimarisinden tamamen izole etme kararıyla tutarlılık — `/siparis`'e
bağlanmak, Gel Al'a özel mantığın (hesap girişi zorunluluğu, ilk-sipariş manuel onay)
yanlışlıkla Masaya'ya sızma riskini taşıyordu. Fiyat/sepet özet GÖSTERİMİ paylaşılabilir
(`SummaryPanel.tsx` gibi), ama checkout AKIŞININ KENDİSİ paylaşılmayacak. §2.7b'deki açık
soru listesi 3'ten 2'ye indi (#68, #69 hâlâ açık). Bu güncelleme SADECE dokümantasyon —
mini-checkout'un kendisi HENÜZ KODLANMADI (kesin dosya adı/route kodlama turunda netleşecek).
SESSION_INDEX.md v27 ile eşleştirildi.*
*v1.7 (önceki güncelleme): Masaya Sipariş, genel giriş/kayıt akışından (§2.7a) TAMAMEN AYRILDI —
yeni §2.7b eklendi (`/masaya-siparis/*`, auth gerektirmeyen bağımsız yüzey). Gerekçe: Session
11 kararı ("Masaya Sipariş = bilgi vermeden guest girişi") ile mevcut kodun (`RegistrationForm.tsx`
TÜM kanallar için aynı formu zorunlu tutuyordu) ÇELİŞTİĞİ Session 12'de kod incelemesiyle
tespit edildi (Açık Sorun #65). Çözüm: istisna eklemek yerine Masaya Sipariş'i mimariden
çıkarmak. Değişiklikler: (1) §1 madde 7 — Masaya Sipariş artık middleware matcher kapsamı
dışında, YENİ İSTİSNA GEREKMİYOR; (2) §2.7a — tablo Gel Al/Online'a daraltıldı; (3) §2.7b
YENİ — route (`/masaya-siparis`), sepet kararı (`useCartStore` PAYLAŞILIR, ayrı state YOK)
ve 3 açık soru (checkout varyantı, RegistrationChannel/FulfillmentChannel tip etkisi,
order_history kanal ayrımı); (4) §2.9 — checkout artık Gel Al'a özel; (5) §2.9a — Masaya
akışının kaynağı güncellendi; (6) §3 — FulfillmentChannel ve AuthenticatedUser yorumları
senkronize edildi. ⚠️ Bu güncelleme SADECE dokümantasyon — kod HENÜZ YAZILMADI (1b/§2.7b
SIRADAKİ GÖREVLER'de duruyor).*
*v1.6: Session 11 — 2026-08-07*
*v1.6 (bu güncelleme): Dosya, kodun önceden ilerlediği ama dokümana hiç yansımadığı
Session 8-11 aralığına SENKRONİZE edildi — bu, CORE.md'nin "kod yazılmadan önce Claude
bu dosyayı okumak zorundadır" kuralının bozulmasını önlemek için yapıldı (dosya, SESSION_INDEX
ile çelişen eski bir akışı "güncel" gibi gösteriyordu). Değişiklikler:
(1) §1 genel akış diyagramı — `/giris` (Twilio OTP) birincil akış görselinden kaldırıldı,
yerine `/kayit-ol` (rıza esaslı kayıt, Session 8) birincil akış olarak işlendi; Twilio
PARKLI (#32/#56) notuyla küçültüldü.
(2) §1 Katman Sınırı Kuralı madde 7 — "guest checkout her zaman geçerli" ifadesi, Session 11
kararına göre "SADECE Masaya Sipariş kanalında geçerli" olarak güncellendi; yeni madde 12
Gel Al ilk-sipariş manuel onay kuralını ekledi.
(3) §2.7 — `/giris` yerine `app/api/auth/register/route.ts` (`/kayit-ol`) birincil kontrat
olarak yazıldı, Twilio parklı durumu ayrı notla belirtildi.
(4) YENİ §2.7a — Session 11'in genel giriş/kayıt akışı kararı (guest gezinme → giriş
tetikleyici, giriş/kayıt seçimi, kanal bazlı tablo, doğrulama durumu alanı, Personel Panel
kesişimi) KOD OLARAK HENÜZ ÜRETİLMEDİ notuyla belgelendi.
(5) §2.8 — `/hesap` redirect hedefi `/giris` → `/kayit-ol` düzeltildi (geriye dönük senkron,
Session 8'de koda yansımış ama dokümana hiç işlenmemiş bir değişiklik).
(6) YENİ §2.9a — Personel Sipariş Paneli (#62) için 3 açık mimari soru + `order_history`
tablosunun (Session 10, canlıda) bu panelin temel katmanı olduğu not edildi.
(7) §3 Veri Modeli — `AuthenticatedUser.verificationStatus` alanı (KARAR kapandı #64, henüz
kodlanmadı) ve yer tutucu `OrderHistoryEntry` tipi (alanları HENÜZ TANIMLANMADI — sahte veri
yasağı gereği varsayım yapılmadı) eklendi. `FulfillmentChannel`'ın üçüncü kanal (Online
Platform) ihtiyacı olup olmadığı AÇIK NOT olarak işaretlendi.
(8) §4.1 — Neon tablo geçmişine `consentRegistrations` (Session 8) ve `order_history`
(Session 10) eklendi; CONFIG_SCHEMA.md'nin AYRICA (bu görevin 2. adımında) güncellenmesi
gerektiği not edildi.
(9) §5 Sorumluluk Sınırları — kullanıcı kimliği satırı `/kayit-ol`'a güncellendi; genel
giriş/kayıt akışı ve Personel Paneli için "henüz dosya yok" satırları eklendi.
⚠️ Bu güncelleme SESSION_INDEX.md'nin ANLATI ÖZETİNE dayanıyor — Session 8-11'in ürettiği
gerçek kod (route dosyaları, DB migration dosyaları) doğrudan görülmedi (confidence: MEDIUM,
bkz. bu sohbetteki KARAR BİLDİRİMİ). Kod dosyaları paylaşılırsa bu senkron doğrulanmalı.
Açık Sorun #35 (category enum) ve #10 (KAPANDI) önceki versiyondan değişmeden korundu.*
*v1.5: Açık Sorun #10 kapatıldı — §2.4, CUSTOMIZER_SPEC.md §3.1'deki gerçek 5 adımlı state
şemasıyla birebir senkronize edildi.*
*v1.4: (1) SELF-CORRECTION — fulfillmentChannel'ın CartState seviyesinde tek alan olduğu
düzeltildi (§2.3, §3). (2) Açık Sorun #26 kapatıldı — yeni §2.9 app/siparis/page.tsx kontratı.*
*v1.3: Karar #20/#23 senkronu — §2.7/§2.8 DB durumu, §3 AuthenticatedUser.address.*
