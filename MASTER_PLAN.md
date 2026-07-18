# BOWLERA — Master Teknik Referans Belgesi (NİHAİ)
**Sürüm:** 2.1 · **Tarih:** 18 Temmuz 2026 (v2.1 — customizer 5 adıma çıkarıldı, bkz. §3.3)
**Kaynaklar:** (1) Claude'un ilk masaüstü araştırması · (2) Deep Research Raporu A · (3) Deep Research Raporu B — üç kaynak sentezlenmiştir, çelişkiler giderilmiştir.
**Durum:** Onaylandı — geliştirmeye hazır

---

## 1. Yönetici Özeti

Bowlera, "Healthy Bowls" sloganıyla konumlanan fast-casual sağlıklı bowl
markası. Üç ayrı araştırma kaynağı da aynı temel stratejide birleşiyor:
**site genelinde toprak tonu (olive/bronze/espresso/cream) paleti hakim
olacak; logodaki mor-pembe-turuncu degrade yalnızca dönüşüm noktalarında
(CTA, sepet, özelleştirici adımları, hover) sınırlı bir vurgu olarak
kullanılacak.** Bu, hem marka tutarlılığını korur hem de logo enerjisini
dijital deneyime taşır.

Teknik karar netleşmiştir: **Next.js (App Router) + Tailwind CSS +
Zustand**. Sitenin merkezinde "Kâseni Yarat" özelleştirme akışı ve
Türkiye pazarına özel sipariş entegrasyonları (Yemeksepeti/Getir/Trendyol,
WhatsApp sipariş köprüsü, masaya QR menü) yer alıyor.

---

## 2. Rakip ve İlham Analizi

| Marka | Renk Paleti | Fotoğraf Stili | Sipariş UX | Marka Sesi |
|---|---|---|---|---|
| **Sweetgreen** | Kale yeşili, mat siyah, doğal ahşap | Doğal ışık, kusursuz olmayan taze malzeme | Çok adımlı, sadakat programı entegreli | Samimi, topluluk odaklı |
| **CAVA** | Safran turuncusu, kozmik bej | Canlı, yüksek kontrast, Akdeniz güneşi | Tamamen görselleştirilmiş adım adım sihirbaz | Enerjik, yaratıcı |
| **DIG** | Soluk yeşil, toprak kahvesi, kirli beyaz | Üstten (flat-lay), tarladan tabağa | Minimalist arayüz, şubeye özel stok | Şef odaklı, samimi, dürüst |
| **Freshii** | Canlı çim yeşili, temiz beyaz | Parlak, yüksek anahtarlı aydınlatma | Kategori filtreleme + kalori hesaplama | Fonksiyonel, bilimsel |
| **Just Salad** | Sature lacivert, gri, taupe | Doygun renkli, iştah kabartıcı yakın plan | Ekspres öğle sipariş akışı | Bilimsel, çevre aktivisti |
| **Pokeworks** | Doğal ahşap, okyanus mavisi | Parlak stüdyo, çiğ balık makro çekim | Protein/sos bazlı doğrusal özelleştirme | Canlı, tazeleyici |
| **Poke House** | Pastel pembe, California sarısı | Plaj/sörf kültürü, yaşam tarzı | Hızlı sepet, popüler kombinasyon önerisi | Rahat, genç, enerjik |

**Ana çıkarım:** Toprak tonu / "earthy" tasarım dilinde en başarılı
örnekler **DIG** ve **Sweetgreen** — Bowlera'nın paleti bu iki markanın
organik güvenilirlik stratejisiyle doğrudan örtüşüyor. CAVA'nın adım
adım görselleştirilmiş özelleştirme sihirbazı, Bowlera'nın "Kâseni
Yarat" akışı için doğrudan referans alınmalı.

---

## 3. Site Mimarisi (Sitemap)

```
Ana Sayfa
├── Menü
│   ├── İmza Kaseler
│   ├── Kâseni Yarat (Bowl Customizer)
│   └── İçecekler & Atıştırmalıklar
├── Sipariş Ver
│   ├── Paket Servis
│   └── Gel Al
├── Hakkımızda
├── Şubeler / Konum Bulucu
└── İletişim
```

Bilgi mimarisi, kullanıcının **en fazla 3 tıklamayla siparişini
tamamlaması** hedefiyle kurgulanmıştır.

### 3.1 Ana Sayfa Bileşenleri
1. **Hero:** Büyük tipografik başlık + yüksek kaliteli kase görseli + "Kâseni Tasarla" / "Menüyü Keşfet" CTA'ları
2. **Değer Önerisi (3 kolon):** Taze içerik garantisi, yerel üretici desteği, sürdürülebilir paketleme
3. **Öne Çıkan Ürünler:** En çok tercih edilen 3 imza kase (fotoğraf, fiyat, kalori, sepete ekle)
4. **Kâseni Yarat Teaser:** Özelleştiriciye yönlendiren interaktif önizleme
5. **Sosyal Kanıt:** Google puanı, kullanıcı yorumları, #BowleraSağlığı Instagram galerisi

### 3.2 Menü Sayfası
- Sticky kategori navigasyonu (İmza Kaseler, Sıcak Tahıl Kaseleri, Vegan, İçecekler)
- Filtre paneli: alerjen (glüten, kuruyemiş, laktoz, soya, kabuklu deniz ürünü) + diyet/kalori (Keto, Vegan, Yüksek Protein, Düşük Kalori)
- Kart grid: fotoğraf, gramaj, **kalori (zorunlu, her kartta görünür)**, makro değerler, fiyat, "Özelleştir" butonu

### 3.3 Kâse Özelleştirme Akışı (en kritik ekran)

> ⚠️ **v2.1 güncellemesi (Oturum 2, 2026-07-18):** Akış 4 adımdan 5 adıma
> çıkarıldı, isimlendirme İngilizce'ye geçirildi. Gerekçe ve geçiş detayı:
> `docs/schema-changes/20260718001123_customizer_5_adim_gecisi.md`.
> Tam kontrat: `CUSTOMIZER_SPEC.md`.

Doğrusal, bilişsel yükü azaltan **5 adım** — bir şefin mutfaktaki düşünme
sırasına (temel → ana ürün → tazelik → lezzet karakteri → son dokunuş)
referansla kurgulanmıştır. İsimlendirme bilinçli olarak İngilizce'dir
(premium/global algı kararı) — bu istisna yalnızca customizer adım ve
malzeme isimlerini kapsar, sitenin geri kalanındaki Türkçe marka sesi
(CONTENT_GUIDE.md §1) değişmez.

| Adım | İçerik | Seçim Tipi |
|---|---|---|
| 1. Base | Jasmine Rice, Brown Rice, Quinoa, Mixed Greens, Spinach, Half Rice + Half Greens | Tekli |
| 2. Main | Grilled Chicken, Crispy Chicken, Beef, Falafel, Shrimp, Salmon, Tofu | Tekli/çift porsiyon |
| 3. Garden | Cherry Tomato, Cucumber, Corn, Pickled Onion, Red Cabbage, Carrot, Avocado | Max 4 ücretsiz, ekstra ücretli — Avokado miktarı ne olursa olsun her zaman ücretli (premium malzeme) |
| 4. Signature Flavor | Mediterranean Herb, Smoky BBQ, Lemon Garlic, Spicy Harissa, Teriyaki Sesame, Sweet Chili | Tekli — sos+baharat birleşik lezzet profili |
| 5. Finish | Feta, Parmesan, Roasted Seeds, Crispy Onion, Fresh Herbs, Lime, Chili Flakes | Max 1 ücretsiz, ekstra ücretli |

**"Make it Yours" ek seçenekleri** (ayrı adım değil, Finish adımına
entegre alt-bölüm): Extra Avocado, Extra Sauce, Extra Crunch. "Double
Main" için ayrı bir mekanizma açılmadı — 2. adımdaki mevcut çift porsiyon
seçeneği (`mainPortion: 'double'`) yeniden kullanılır.

Sağ tarafta **sabit özet panel**: canlı kase görseli, **anlık kalori/makro
toplamı (zorunlu, her zaman görünür)**, güncel fiyat, "Sepete Ekle" butonu.

---

## 4. Tasarım Sistemi

### 4.1 Renk Kullanım Tablosu (WCAG doğrulamalı)

| Renk | Hex | Rol | Kontrast (Cream üzerinde) | WCAG |
|---|---|---|---|---|
| Warm Cream | `#F4F0E7` | Sayfa arka planı | — | — |
| Charcoal Black | `#1F1A18` | Ana metin/başlık | 15.14:1 | AAA |
| Espresso Brown | `#38221D` | İkincil metin, fiyatlar | 13.05:1 | AAA |
| Primary Olive | `#53502A` | Birincil CTA/buton | 7.24:1 | AAA |
| Deep Olive | `#6A6541` | İkincil buton/ikon | 5.20:1 | AA |
| Bronze | `#816E44` | Dekoratif, büyük başlık (18px+) | 4.35:1 | AA Large only |

> Bronze küçük gövde metninde **kullanılmamalı** — sadece 18px+ kalın
> başlıklarda veya dekoratif sınır/illüstrasyonlarda.

### 4.2 Logo Degradesinin Sınırlı Kullanımı

```css
background: linear-gradient(135deg, #8A2387 0%, #E94057 50%, #F27121 100%);
```
Yalnızca: özelleştirici aktif adım göstergesi · sepet rozet (badge) ·
CTA hover kenarlığı (2px) · "Süper Gıda" etiket arka planı.
**Site arka planlarında asla kullanılmaz.**

### 4.3 Tipografi
- **Başlık:** Cormorant Garamond (serif, logoyla uyumlu) — `font-weight: 700`
- **Gövde/UI:** Nunito veya Raleway (sans-serif, mobilde okunabilir) — `font-weight: 400/600`

### 4.4 Fotoğraf Direktifi
- Ana kase çekimleri: 90° tam üstten (flat-lay)
- Destekleyici görseller: 45° stüdyo açısı
- Işık: yumuşak gölgeli, sıcak-doğal (5000–5500K), sert flaş yok
- Zemin: mat traverten, açık meşe veya Warm Cream tonlu beton — parlak/yansıtıcı yüzey yok

### 4.5 İkonografi
**Kütüphane:** Genel arayüz ikonları için **Lucide React** (hafif, tutarlı çizgi stili, React ile native entegrasyon). Logodaki yaprak/zeytin motifi ise Lucide'da yok — bu, özel SVG olarak vektörel çizilip imza desen olarak kullanılmalı: yükleme ekranlarında, bölüm ayraçlarında, "Sağlıklı Tercih" rozetlerinde. İnce çizgisel (outline), Primary Olive renginde, Lucide ikonlarıyla aynı stroke kalınlığında (2px) tutulmalı.

### 4.7 Animasyon ve Mikro-Etkileşim Sistemi

**Felsefe:** Animasyon dekorasyon değil, yönlendirmedir. Her hareket bir
şeyi açıklamalı (seçim yapıldı, sayfa değişti, öğe eklendi) — amaçsız
"gösteriş" animasyonundan kaçınılmalı. Toprak tonu paletin sakinliğiyle
tezat oluşturmayacak şekilde **yumuşak, organik easing** kullanılmalı
(sert/mekanik değil).

**Kütüphane:** **Framer Motion** (Next.js/React ile native uyumlu,
`AnimatePresence` ile giriş-çıkış animasyonları, `whileHover`/
`whileTap` ile mikro-etkileşimler). Basit hover geçişleri için
kütüphane yükü gereksiz — onlar sade CSS `transition` ile yapılmalı;
Framer Motion yalnızca sayfa geçişi, scroll-reveal ve özelleştirici
adım geçişleri gibi **orkestrasyon gerektiren** yerlerde kullanılmalı.

| Bileşen/Alan | Animasyon | Süre & Easing | Tetikleyici |
|---|---|---|---|
| Hero başlık | Alttan yukarı fade+slide (staggered, kelime/satır bazlı) | 600ms, `ease-out`, 80ms stagger | Sayfa yüklenince |
| Hero arka plan görseli | Hafif Ken Burns efekti (yavaş zoom) | 8-12s, `linear`, sonsuz döngü | Sayfa yüklenince |
| Bölüm başlıkları/kartlar (scroll reveal) | Alttan fade+slide, %10 viewport'a girince | 500ms, `ease-out` | Scroll (Intersection Observer) |
| MenuCard hover | Hafif yükselme (`translateY(-4px)`) + gölge derinleşmesi | 200ms, `ease-in-out` | Hover |
| Sepete Ekle butonu | Tıklamada kısa "scale bounce" (0.95→1.05→1) | 300ms, `spring` | Click |
| Sepet rozeti (badge) | Sayı değiştiğinde logo-degrade renkli "pulse" | 400ms, `spring` | Sepete ürün eklenince |
| Özelleştirici adım geçişi | Yatay slide (mevcut adım sola çıkar, yeni adım sağdan girer) | 350ms, `ease-in-out` | "Sonraki Adım" tıklanınca |
| VisualPreview katmanı | Yeni malzeme seçilince ilgili katman fade-in + hafif scale (0.9→1) | 250ms, `ease-out` | Malzeme seçimi |
| Özet panel (sticky) fiyat/kalori güncelleme | Sayı değişiminde kısa vurgu rengi flaşı (logo-degrade) | 300ms | Değer değişince |
| Sayfa geçişleri | Hafif fade (crossfade) | 250ms, `ease-in-out` | Route değişimi (Next.js) |
| Instagram galeri / sosyal kanıt | Yatay kayan (marquee) şerit, hover'da durur | 30-40s tam döngü, `linear` | Sayfa görünür olunca |

**Performans ve erişilebilirlik kuralları:**
- Tüm animasyonlar `prefers-reduced-motion: reduce` medya sorgusunu
  kontrol etmeli — bu tercih aktifse animasyonlar devre dışı bırakılıp
  anında geçiş yapılmalı.
- Yalnızca `transform` ve `opacity` animasyonlu; `width`/`height`/`top`
  gibi layout tetikleyen özellikler animasyonlu bırakılmamalı (CLS
  riski).
- Scroll-reveal animasyonları tek seferlik olmalı (her scroll'da tekrar
  tetiklenmemeli) — performans ve "rahatsız edici" his riskini önler.

### 4.8 Fotoğraf Adlandırma Standardı
Tutarlı dosya yönetimi ve SEO alt-text üretimi için:
```
[kategori]-[ürün-adı-kebab-case].webp
Örn: signature-teriyaki-tavuk.webp
     build-your-own-kinoa-taban.webp
     subeler-kadikoy-dis-mekan.webp
```

---

## 5. Teknik Mimari

### 5.1 Framework Kararı: Next.js (App Router)
Next.js, sade React (Vite) yerine tercih edilmiştir çünkü:
- **SEO:** Şube sayfaları ve menü içeriğinin SSR/SSG ile anında dizine eklenmesi gerekir
- **Görsel optimizasyonu:** `next/image` ile otomatik WebP/AVIF dönüşümü, ~%70 sıkıştırma
- **Performans:** Sunucu tarafı render ile düşük JS yükü → iyi Core Web Vitals

### 5.2 Bileşen Yapısı
```
/components/layout    → Header, Footer
/components/menu      → MenuGrid, MenuCard, NutritionalFacts
/components/customizer → BowlCustomizer, IngredientSelector, VisualPreview
/components/location   → LocationFinder (Google Maps API)
/components/motion     → ScrollReveal, PageTransition (Framer Motion sarmalayıcıları — bkz. 4.7)
```

**VisualPreview teknik kararı:** Three.js/Canvas gibi 3D çözümler bu
aşama için gereksiz karmaşıklık ve performans yükü getirir. MVP için
**katmanlı CSS/SVG illüstrasyon** yaklaşımı tercih edilmeli — her
malzeme (**Base, Main, Garden, Signature Flavor, Finish** — bkz. §3.3
v2.1) önceden hazırlanmış şeffaf PNG/SVG katmanı olarak `z-index`
sırasıyla üst üste bindirilir. Kullanıcı seçim yaptıkça ilgili katman
`opacity`/`display` ile açılır. Hafif, hızlı, ek kütüphane gerektirmez;
ileride marka bütçesi büyürse gerçek ürün fotoğrafı kompozisyonuna
(server-side image composition) geçilebilir.

**Mobil özelleştirici UX:** Masaüstünde yan yana duran adım+özet paneli,
mobilde dikey akışa döner: adımlar tam ekran kart olarak sırayla
gösterilir, özet panel ekranın altında **sabit (sticky) bir çekmece**
olarak durur ve yukarı kaydırılarak açılır — kullanıcı her an toplam
fiyat/kaloriyi görür ama ana odak seçim adımında kalır.

### 5.3 Performans Hedefleri (Core Web Vitals)
| Metrik | Hedef |
|---|---|
| LCP (Largest Contentful Paint) | < 2.5s |
| FID / INP | < 100ms |
| CLS (Cumulative Layout Shift) | < 0.1 |
| Lighthouse Performans Puanı | 90+ |


### 5.4 State Yönetimi: Zustand
Özelleştirici ve sepet gibi yoğun güncellenen state'ler için
`useState/useContext` gereksiz re-render'lara yol açar → **Zustand** tercih edilir:

```ts
// store/useCartStore.ts
import { create } from 'zustand';
import { persist } from 'zustand/middleware';
import { CartItem } from '@/types';

interface CartState {
  cart: CartItem[];
  addToCart: (item: CartItem) => void;
  removeFromCart: (cartId: string) => void;
  clearCart: () => void;
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
    { name: 'bowlera-cart-storage' } // tarayıcı kapansa da sepet korunur
  )
);
```

### 5.5 Menü Veri Modeli
**MVP aşaması:** statik `menu-data.json`, Next.js API Route (`/api/menu`) üzerinden servis edilir — sıfır veritabanı maliyeti.
**Büyüme aşaması:** headless CMS'e geçiş (Sanity.io veya Contentful), Next.js ISR ile otomatik yeniden derleme.

> **Kalori bilgisi zorunludur, opsiyonel değildir.** Türkiye'de zincir
> restoranlar için kalori etiketlemesi yasal bir gereklilik haline
> gelmektedir; ayrıca kullanıcı deneyimi açısından da menü kartında,
> özelleştirici özet panelinde ve sepette kalori her zaman görünür
> olmalıdır. "Düşük kalori" / "Yüksek protein" filtreleri bu alana
> dayanır.

```ts
type BowlItem = {
  id: string;
  name: string;
  category: "signature" | "build-your-own" | "içecek";
  price: number;
  image: string;              // bkz. 4.6 Fotoğraf Adlandırma Standardı
  tags: string[];              // "vegan", "glutensiz", "yüksek protein"
  allergens?: ("gluten" | "dairy" | "nuts" | "soy" | "shellfish")[];
  calories: number;            // ZORUNLU alan — opsiyonel değil
  protein: number;             // ZORUNLU alan
  carbs?: number;
  fat?: number;
};
```

> ⚠️ Not: "Build Your Bowl" (customizer) için `Garden`/`Signature Flavor`/
> `Finish` malzeme kategorilerinin `menu-data.json`'a nasıl ekleneceği
> Oturum 3 kapsamındadır — bu veri modeli değişikliği henüz yapılmadı,
> yalnızca akış kontratı (`CUSTOMIZER_SPEC.md`) hazırlandı.

### 5.6 Üçüncü Parti Entegrasyonlar (Türkiye Pazarı)
- **Pazar yeri toplama:** Adisyo veya SepetTakip API'leri ile Yemeksepeti/Getir Yemek/Trendyol Yemek siparişlerini tek ekranda toplayıp POS/adisyo yazıcısına aktarma
- **WhatsApp sipariş köprüsü:** Özelleştirilen kase, şablon mesaj olarak şubenin WhatsApp hattına yönlendirilir (`wa.me` linki)
- **Masaya QR menü:** QR kod → `/menu?table=14` parametresiyle sipariş doğrudan ilgili masaya düşer
- **Sipariş sonrası bildirim:** Hazırlık süresi ve durum takibi için SMS/e-posta bildirimi (ör. Twilio veya yerel bir SMS API sağlayıcısı) — bu, ilk lansmandan sonraki bir faz olarak planlanmalı, POS entegrasyonuyla birlikte devreye alınmalı

---

## 6. Marka Sesi ve Örnek Metinler

**Ton:** Enerjik, şeffaf, bilinçli, sofistike. Kentli hızlı yaşam
temposuna saygılı ama sağlık/lezzetten ödün vermeyen; süslü jargon yok,
malzeme odaklı dürüst dil.

- ✅ "Doğrudan yerel çiftçimizden aldığımız taze avokadolarla hazırladık."
- ❌ "Eşsiz lezzet patlaması yaratan mucizevi süper kase."

**Hero başlık alternatifleri:**
1. *Dönüşüm odaklı:* "Şehrin Ritmini Yakalayan Taze ve Sağlıklı Kaseler" — CTA: "Kâseni Yarat"
2. *Zanaatkar odaklı:* "Toprağın Doğallığı, Şeflerin Dokunuşuyla Kâsende" — CTA: "Hemen Sipariş Ver"
3. *Kişiselleştirme odaklı:* "Senin Kaselerin, Senin Kuralların" — CTA: "Kendi Kâseni Tasarla"

**CTA örnekleri:** "Sağlığı Keşfet" · "Ekspres Sipariş" · "Sepete Ekle" · "Kâseni Onayla"

> Not (v2.1): Customizer adım isimleri (Base/Main/Garden/Signature
> Flavor/Finish) bu Türkçe marka sesi kuralının **bilinçli bir istisnası**
> olarak İngilizce bırakılmıştır — bkz. §3.3. CTA'lar ve genel sayfa
> metinleri bu istisnanın dışındadır, Türkçe kalmaya devam eder.

---

## 7. SEO ve Yerel Görünürlük

**Anahtar kelimeler:**
- Birincil: "sağlıklı kase yemek", "poke bowl istanbul", "kendi kaseni yarat"
- İkincil: "kinoa salatası sipariş", "vegan kase alternatifleri", "avokadolu somon kase"

**Yerel SEO:** Her şube için ayrı Google Business Profile; NAP (isim/adres/telefon) bilgileri "Şubeler" sayfasıyla birebir eşleşmeli.

**Schema (JSON-LD) — her şube sayfasına gömülmeli:**
```json
{
  "@context": "http://schema.org",
  "@type": "Restaurant",
  "name": "Bowlera - Kadıköy Şubesi",
  "servesCuisine": ["Healthy Bowls", "Poke Bowls", "Salads"],
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Caferağa Mahallesi, Moda Caddesi No:45",
    "addressLocality": "Kadıköy",
    "addressRegion": "İstanbul",
    "addressCountry": "TR"
  },
  "hasMenu": {
    "@type": "Menu",
    "hasMenuSection": [{
      "@type": "MenuSection",
      "name": "İmza Kaseler",
      "hasMenuItem": {
        "@type": "MenuItem",
        "name": "Teriyaki Tavuk Kase",
        "offers": { "@type": "Offer", "price": "240.00", "priceCurrency": "TRY" },
        "nutrition": { "@type": "NutritionInformation", "calories": "520 kcal", "proteinContent": "35g" }
      }
    }]
  }
}
```

---

## 8. Sonraki Adımlar (Oturum Planı — Güncellenmiş)

Özelleştirici akışı (state yönetimi + katmanlı görsel önizleme + mobil
UX) tek oturumda bitecek kadar hafif değil; ayrı oturuma bölündü.

| Oturum | İçerik |
|---|---|
| **1** | Next.js + Tailwind kurulumu, font/renk sistemi, Header/Footer, Ana Sayfa hero |
| **2** | Menü sayfası, filtreleme, MenuCard (kalori/alerjen dahil), statik menü verisi |
| **3** | Zustand store kurulumu + BowlCustomizer akışı (**5 adım** — bkz. §3.3 v2.1, masaüstü) |
| **4** | VisualPreview (katmanlı CSS/SVG), mobil özelleştirici uyarlaması, sepet |
| **5** | Hakkımızda, Şubeler, İletişim + JSON-LD/SEO etiketleri + performans/responsive son kontrol |

**Kullanıcı testi:** Özelleştirici akışı canlıya alınmadan önce en az
5–10 kişilik bir grupla test edilmeli (adım netliği, mobilde özet
panelin fark edilirliği, "Sepete Ekle" adımına kadarki süre ölçülmeli).
Bu, Oturum 4 sonrası, Oturum 5'ten önce ayrı bir kontrol noktası olarak
planlanmalı. 5 adıma çıkan akışın 10 saniyelik "ilk kez gören müşteri"
hedefini karşılayıp karşılamadığı bu testte özellikle ölçülmeli.

Gerçek görsel/menü içeriği (fotoğraflar, fiyatlar, şube adresleri) hazır
olduğunda süreç hızlanır. Üçüncü parti sipariş entegrasyonları (Adisyo/
SepetTakip, WhatsApp, QR menü) ayrı bir sonraki faz olarak planlanmalı —
bunlar gerçek API anahtarları ve iş ortaklığı gerektirir.

---

*Bu belge üç kaynağın (ilk araştırma + 2 deep research raporu) sentezidir; aralarında çelişki tespit edilmemiştir, bulgular birbirini teyit etmektedir.*
*v2.1 (18 Temmuz 2026): §3.3, §5.2, §6, §8 — customizer 5 adıma çıkarıldı, İngilizce isimlendirme kararı eklendi. Kaynak: `20260718001123_customizer_5_adim_gecisi.md`.*
