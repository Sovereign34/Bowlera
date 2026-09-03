# BOWLERA — PREMIUM MOTION SYSTEM

**Claude Teknik Uygulama ve Animasyon Mimarisi Raporu v1.1**
*(v1.1 — Mobil/dokunmatik strateji eklendi; bkz. §1a ve dosya sonu Değişiklik Notu)*

**Amaç:** Bowlera web sitesindeki mevcut animasyon sistemini, "daha fazla efekt" mantığıyla değil, premium bir motion-design sistemi olarak yeniden yapılandırmak.

**Teknoloji tabanı:**
- Next.js App Router
- TypeScript
- Tailwind CSS
- Framer Motion / güncel Motion API yaklaşımı
- Zustand
- Mevcut Bowlera Design System

Bowlera'nın mevcut mimarisinde Framer Motion zaten sayfa geçişleri, scroll-reveal ve customizer orkestrasyonu için tanımlanmış; basit hover'lar için CSS transition kullanılıyor.

---

## 1. Stratejik Karar

Mevcut problem:

> Animasyonların sayısı az değil; motion hierarchy yeterince gelişmiş değil.

Mevcut sistemde bazı temel hareketler zaten bulunuyor:

- Hero stagger
- MenuCard hover
- Add-to-cart scale bounce
- Scroll reveal
- Customizer transition
- Page crossfade

Fakat sistemin eksik tarafı, bu animasyonların birbirleriyle aynı tasarım dili içinde konuşmaması.

Bowlera'nın hedefi:

> Calm luxury + organic motion + tactile interaction + spatial continuity

olmalıdır.

Yani Apple/Framer seviyesinde "temiz", modern premium ürün sitelerinde görülen hareket mantığı alınmalı; ancak Bowlera'nın doğal/sağlıklı/earthy marka karakteri korunmalıdır.

Framer'ın güncel yaklaşımı da animasyonu yalnızca dekorasyon değil; kullanıcıya ilişki, tıklanabilirlik, durum ve mekânsal bağlam anlatan bir araç olarak ele alıyor.

---

## 1a. Dokunmatik Öncelik — Zorunlu Ön Koşul

> **Bowlera trafiği neredeyse tamamen dokunmatik.** Bu rapordaki hiçbir etkileşim katmanı
> (özellikle Level 2 — Tactile Interaction) SADECE `hover` üzerinden tanımlanamaz.

Bu bölüm sonradan (P0-2/MenuCard uygulaması sırasında canlıda tespit edilen bir bulgu üzerine)
eklendi: raporun ilk sürümü (v1.0) `whileHover`'ı tek tetikleyici olarak ele almıştı ve gerçek
kullanıcı deneyiminde (dokunmatik cihaz) bu etkileşimlerin **hiç görünmediği** canlıda doğrulandı.

**Kural — rapordaki her yeni etkileşim katmanı için geçerli:**

1. Fare/imleç davranışı (`whileHover`) ve dokunma davranışı (`whileTap`) **aynı hedef state'e**
   gitmeli — iki ayrı görsel dil icat edilmemeli.
2. **Giriş** (rest → aktif) ease/duration tabanlı kalabilir (mevcut Design System kararları
   korunur). **Çıkış** (aktif → rest) — hem `mouse-leave` hem `tap-release` için — fiziksel bir
   "geri sekme" hissi vermeli; bunun için `duration`/`bounce` tabanlı bir spring önerilir (elle
   `stiffness`/`damping` tahmini yerine, çünkü süre/sertlik hissini doğrudan ayarlamayı sağlar).
2a. Referans değer (canlıda kullanıcı onayıyla kalibre edildi — MenuCard P0-2): `{ type: "spring",
   duration: 0.45, bounce: 0.15 }`. Bu, `lib/motion/tokens.ts`'e `springs.cardRelease` olarak
   eklenmesi ve dokunma hedefli TÜM kart/CTA tipi bileşenlerde (MenuCard, ileride benzer kartlar)
   tekrar kullanılması önerilen bir başlangıç değeridir — sertse `bounce` düşürülür, yavaşsa
   `duration` düşürülür.
3. `layoutId` tabanlı geçişler (Level 3 — CategoryNav gibi) zaten bir `state` değişikliğine
   (tıklama/dokunma ile seçim) bağlı olduğu için bu kuraldan ETKİLENMEZ — risk SADECE
   `whileHover`'a bağımlı, dokunmada hiç tetiklenmeyen etkileşimlerde var.
4. Yeni bir tactile bileşen tasarlanırken önce şu soru sorulmalı: **"Bu davranışı dokunmatik bir
   kullanıcı hiç görecek mi?"** Cevap hayırsa, bileşen "premium" değil eksik sayılır.

---

## 2. Bowlera Motion Hiyerarşisi

Claude uygulamayı aşağıdaki beş katmanda ele almalı:

### Level 1 — Presence

Sayfa açıldığında Hero, Section, Product, Image, CTA kullanıcıya kontrollü şekilde görünür.

```
opacity: 0 → 1
y: 16 → 0
```

Ancak her element ayrı ayrı animasyonlanmayacak. Hierarchical stagger kullanılacak.

### Level 2 — Tactile Interaction

Kullanıcı bir nesneyle etkileştiğinde nesne fiziksel tepki verecek. **Fare ve dokunma AYNI
hedefe gitmeli** (bkz. §1a) — aşağıdaki üçü birbirinin alternatifi değil, aynı davranışın farklı
giriş yollarıdır:

```
hover (mouse)      → whileHover  → y: -2 / -4 (veya scale, bileşene göre)
tap (touch)         → whileTap="hover" (AYNI hedef variant)
release (her ikisi) → spring back — springs.cardRelease (duration/bounce, bkz. §1a)
```

Buradaki amaç: **"Bu UI elemanı canlı ve fiziksel."** hissidir — ve bu his masaüstü kadar
dokunmatik kullanıcıya da ulaşmalı, çünkü Bowlera trafiğinin büyük çoğunluğu dokunmatik.

### Level 3 — Spatial Continuity

Bir şey bir yerden başka yere gidiyorsa hareketi takip edilecek. Burada `layoutId` kritik.

Örneğin CategoryNav'da aktif pill'in kaybolup yeniden oluşması yerine fiziksel olarak bir kategoriden diğerine hareket etmesi. Motion'ın `layoutId` sistemi tam olarak bu shared-element davranışı için tasarlanmış durumda.

### Level 4 — Spatial Transition

Drawer, modal, dropdown ve sayfa değişimlerinde kullanıcı nereden nereye geçtiğini hissetmeli.

Örneğin CartDrawer sağdan gelir, kapanırken tekrar sağa gider. Backdrop eş zamanlı olarak fade olur.

### Level 5 — Ambient Motion

Bu en üst seviye.

- Hero image: `scale 1.00 → 1.04`, 8–12 saniyelik çok yavaş hareket
- Instagram/social proof marquee — görsel atmosfer

Fakat sürekli hareket eden her şey sınırlı kullanılmalı. Premium tasarımın sırrı:

> Her şey hareket etmiyor. Hareket eden şey doğru zamanda hareket ediyor.

---

## 3. Global Motion Token Sistemi

Claude'un komponentlere rastgele duration/easing yazması engellenmeli.

```ts
export const motionTokens = {
  duration: {
    micro: 0.18,
    fast: 0.25,
    normal: 0.35,
    reveal: 0.5,
    cinematic: 0.8,
  },

  ease: {
    organic: [0.22, 1, 0.36, 1],
    calm: [0.16, 1, 0.3, 1],
    smooth: [0.4, 0, 0.2, 1],
  },

  spring: {
    soft: {
      type: "spring",
      stiffness: 300,
      damping: 28,
    },

    tactile: {
      type: "spring",
      stiffness: 400,
      damping: 30,
    },

    // EKLENDİ (v1.1) — dokunmatik "release" (hover→rest / tap-release) hissi için.
    // duration/bounce tabanlı: stiffness/damping'i elle tahmin etmek yerine süre ve
    // sekme miktarını doğrudan ayarlar. Referans değer canlı kullanıcı testiyle kalibre
    // edildi (bkz. §1a) — MenuCard P0-2'de kullanılıyor, benzer kart/CTA bileşenlerinde
    // tekrar kullanılabilir.
    cardRelease: {
      type: "spring",
      duration: 0.45,
      bounce: 0.15,
    },
  },
};
```

Böylece MenuCard, CartDrawer, Header, CategoryNav, AccountMenu, Hero, Customizer aynı motion language'ı kullanır.

---

## 4. Cart Drawer — En Önemli Premium Upgrade

Mevcut CartDrawer mimarisinde önemli bir problem var:

```
if (!isOpen || !isMounted) return null
```

Bu nedenle drawer React tree'den doğrudan çıkıyor ve exit animation gerçekleşemiyor. Bu alan ilk uygulanacak değişiklik olmalı.

Motion `AnimatePresence`, React tree'den çıkarılan component'in DOM'da exit animasyonu tamamlanana kadar tutulmasını sağlıyor.

**Yeni davranış — Açılış:**

```
backdrop: opacity 0 → .4
drawer:   x: 100% → 0
```

**Kapanış:**

```
drawer:   x: 0 → 100%
backdrop: opacity .4 → 0
```

**Drawer transition:**

```
type: spring
stiffness: 320
damping: 32
```

Amaç: "sliding panel" değil, fiziksel olarak sayfadan ayrılan bir yüzey hissi.

---

## 5. Cart Content Stagger

Drawer'ın kendisi geldikten sonra içerik aynı anda patlamamalı.

```
Drawer
 ↓
Header
 ↓ 40ms
Cart item 1
 ↓ 40ms
Cart item 2
 ↓ 40ms
Cart item 3
 ↓
Total
 ↓
CTA
```

```
opacity: 0 → 1
y: 10 → 0
```

Fakat stagger çok kısa tutulmalı — 40–60ms aralığı. Amaç gösteri değil: **Drawer'ın içeriğinin "yerleştiğini" hissettirmek.**

---

## 6. MenuCard — Premium Ürün Etkileşimi

Mevcut Design System: `translateY(-4px)`, shadow increase, 200ms diyor. Bu korunmalı fakat tek başına bırakılmamalı.

**Yeni davranış:**

```
CARD
 ├── whileHover VE whileTap="hover" (AYNI hedef, bkz. §1a)
 ├── y: 0 → -4
 ├── shadow: subtle → deep
 │
 └── IMAGE
       scale: 1 → 1.045 (variant propagation ile, ayrı whileHover/whileTap tanımlamaz)
```

**Giriş/çıkış ayrımı (v1.1 — canlıda zorunlu hale geldi):**
- Giriş (rest→hover, hem mouse-enter hem tap-down): mevcut `200ms ease-in-out` korunur.
- Çıkış (hover→rest, hem mouse-leave hem tap-release): `springs.cardRelease` (bkz. §3) — sabit
  ease yerine fiziksel geri sekme.

Kritik nokta: Image zoom card'ın dışına taşmayacak — `overflow-hidden` kullanılmalı.

Bu küçük değişiklik bile ürün kartını statik ecommerce kartından daha "premium product interface" seviyesine taşır — **ama sadece dokunma da tetiklenirse** (§1a); aksi halde mobil kullanıcının büyük çoğunluğu bu yükseltmeyi hiç görmez.

---

## 7. MenuCard CTA Micro-interaction

Kart hover (VEYA dokunma — bkz. §1a, aynı hedef) olduğunda CTA'nın da çok hafif tepki vermesi öneriliyor.

```
card hover / tap
    ↓
image zoom
    ↓
CTA y: -1px
    ↓
icon x: +2px
```

CTA kendi `whileHover`/`whileTap`'ini tanımlamaz — kart'ın variant state'ini miras alır (variant
propagation), böylece CTA da dokunmada otomatik tetiklenir, ayrı kod gerekmez.

Fakat her şeyi hareket ettirmek yasak. Logo, fiyat, kalori, badge vs. aynı anda hareket ettirilmemeli.

---

## 8. CategoryNav — layoutId

Bu Bowlera'daki en görünür premium yükseltmelerden biri olabilir.

Mevcut yapı aktif kategoriyi `bg-olive-primary` / `text-cream` ile değiştiriyor.

**Yeni yaklaşım:**

```tsx
{isActive && (
  <motion.span
    layoutId="category-active-pill"
    ...
  />
)}
```

Sonuç: pill yeni kategoriye fiziksel olarak akar. Bu, kullanıcının "aktif state değişti" demesinden daha iyi bir algı yaratır:

> "Seçimim hareket ederek yeni konuma geçti."

Motion'ın `layoutId` sistemi bu shared-element geçişlerini destekliyor.

---

## 9. Account Menu

Mevcut dropdown `{isOpen && (...)}` şeklinde aniden ortaya çıkıyor.

**Premium davranış — Açılış:**

```
opacity: 0 → 1
scale: .96 → 1
y: -4 → 0
```

**Kapanış:**

```
opacity: 1 → 0
scale: 1 → .98
y: 0 → -3
```

Burada spring çok hafif kullanılabilir. Bounce olmamalı — çünkü account menu bir oyuncak değil, utility UI.

---

## 10. Header — Scroll Intelligence

Burada büyük bir hata yapılmamalı: **Header yüksekliği sürekli değişmemeli.**

Design System'ın layout animation kuralı gereği width/height/top gibi layout tetikleyen değerler animasyon konusu yapılmamalı.

Bunun yerine:

- **Initial:** cream / subtle
- **Scroll sonrası:** slightly stronger surface + shadow layer opacity increase + logo scale ≈ .97

Header'ın kendisinin yüksekliği değiştirilmez. Bu çok daha rafine görünür.

---

## 11. Hero — "Cinematic" Ama Sakin

Hero şu anda zaten kelime bazlı stagger kullanıyor (opacity 0→1, y 16→0, 600ms, 80ms stagger). Bu korunmalı.

Fakat premium versiyonda hero dört ayrı katmanda çalışmalı: Headline, Supporting copy, CTA, Hero visual.

**Önerilen zaman çizgisi:**

```
0ms    Headline
120ms  headline continuation
260ms  paragraph
400ms  CTA
500ms  visual begins
...    slow ambient image motion
```

Bu sayede sayfa "elementler yükleniyor" hissinden çıkıp **"art-directed entrance"** hissine geçer.

---

## 12. Hero Image — Ken Burns

Design System zaten 8–12 saniyelik Ken Burns yaklaşımını destekleyen bir animasyon dili tanımlıyor.

```
scale 1 → 1.025 / 1.04
```

Çok düşük amplitüd kullanılmalı. Yavaş, kesintisiz, ama kullanıcı interaction'ını engellememeli. Reduced motion aktifse kapatılmalı.

---

## 13. Scroll Reveal Sistemi

Mevcut Design System: 500ms, ease-out, viewport'a yaklaşık %10 giriş, tek seferlik olarak tanımlıyor. Bu korunmalı.

Ancak tüm sayfaya `EVERYTHING → fade + slide` uygulanmamalı. Premium sistem hiyerarşik reveal yapmalı:

```
Section enters
      ↓
Heading
      ↓ 60ms
Description
      ↓ 80ms
Cards
```

Kartların kendi içinde tekrar uzun stagger kullanılması gereksizdir.

---

## 14. Page Transitions

Mevcut sistem 250ms crossfade tanımlıyor. Bunu opacity + micro-scale haline getirmek daha premium olacaktır.

**Enter:**

```
opacity: 0 → 1
scale: .985 → 1
```

**Exit:**

```
opacity: 1 → 0
scale: 1 → .995
```

Buradaki scale farkı çok küçük olmalı — 0.95 gibi agresif değerler kullanılmamalı.

---

## 15. Customizer

Burada Bowlera'nın en güçlü premium fırsatlarından biri var.

Mevcut sistem zaten step transition, 350ms, horizontal slide tanımlıyor. Bunu tamamen değiştirmek yerine geliştirmek gerekir.

**Önerilen:**

```
Previous step: x: 0 → -20,  opacity: 1 → 0
Next step:     x: +20 → 0,  opacity: 0 → 1
```

Ancak seçilen ingredient'in VisualPreview'daki görünümü ayrıca `opacity 0→1, scale .9→1` şeklinde çalışmalı. Bu zaten Design System tarafından tanımlanan pattern ile uyumludur.

---

## 16. Add to Cart

Mevcut AddToCartButton zaten `0.95 → 1.05 → 1` bounce kullanıyor. Burada amaç bunu kaldırmak değil.

Ancak 1.05 bazı durumlarda fazla olabilir. Premium tactile interaction için:

```
tap:          scale .97
confirmation: scale 1.02
return:       1
```

daha kontrollü olabilir. Özellikle hızlı ardışık click durumlarında mevcut duplicate-add guard korunmalı.

---

## 17. Cart Badge

Design System'da badge için zaten 400ms spring pulse tanımlı. Bunu premium hale getirmek için:

```
number change
     ↓
badge scale .85
     ↓
1.08
     ↓
1
```

çok hafif opacity/highlight değişimi kullanılabilir. Ama her ürün eklemede tüm header hareket etmemeli — sadece badge tepki vermeli.

---

## 18. Motion Accessibility — Zorunlu

Bu rapordaki en önemli teknik kurallardan biri.

Bowlera Design System zaten `prefers-reduced-motion`, yalnızca transform/opacity, scroll reveal'in tek seferlik olması kurallarını açıkça zorunlu kılıyor.

Motion'ın güncel React API'sinde de `MotionConfig reducedMotion="user"` ile site genelinde kullanıcı tercihini uygulamak mümkün.

**Önerilen global yapı:**

```tsx
<MotionConfig reducedMotion="user">
    {children}
</MotionConfig>
```

Böylece kullanıcı OS seviyesinde Reduced Motion seçtiğinde transform/layout animasyonları otomatik olarak azaltılabilir; opacity gibi daha güvenli geçişler korunabilir.

Bunun üzerine özel componentlerde `const shouldReduceMotion = useReducedMotion()` kullanılmalı. Özellikle: Hero, Drawer, Parallax, Ken Burns, Page transition için.

Motion'ın resmi dokümantasyonu da reduced-motion durumunda büyük transform hareketlerini opacity ile değiştirmeyi ve parallax'ı kapatmayı öneriyor. Apple'ın erişilebilirlik yaklaşımı da scaling, spinning, peripheral motion ve depth-simulating hareketlerin reduced-motion durumunda azaltılmasını/değiştirilmesini öneriyor.

---

## 19. Performans Mimarisi

Premium animation, yüksek efekt sayısı değildir. Premium animation, **yüksek frame stability'dir.**

Web performansında transform ve opacity, layout tetikleyen width, height, left, margin gibi özelliklerden daha uygun animasyon özellikleridir.

| İzin verilen | Kısıtlı | Animasyonlanmayacak |
|---|---|---|
| transform | filter | width |
| opacity | background-color | height |
| | box-shadow | top / left |
| | | margin / padding |
| | | font-size |

Design System'ın mevcut kuralı da tam olarak bu yönde.

---

## 20. Parallax Konusunda Karar

Global premium sitelerde parallax sık kullanılıyor. Ancak Bowlera'da ağır parallax → **HAYIR**. Özellikle mouse tracking, 3D tilt, cursor-follow, multi-axis movement ana sistem yapılmamalı.

Bunun nedeni sadece performans değil — Bowlera'nın marka karakteri: doğal, sakin, premium, sağlıklı, organik.

- **Subtle depth → EVET:** image scale, very small y movement, slow ambient motion
- **Artificial 3D → HAYIR**

Bu ayrım önemli.

---

## 21. Global Motion Map

Claude uygulamayı aşağıdaki sırayla gerçekleştirmeli:

| Alan | Motion | Öncelik |
|---|---|---|
| CartDrawer | Slide + backdrop + stagger | P0 |
| MenuCard | Lift + image zoom | P0 |
| CategoryNav | layoutId active pill | P0 |
| AccountMenu | Spring dropdown | P1 |
| Header | Scroll intelligence | P1 |
| Hero | Cinematic orchestration | P1 |
| Page transition | Fade + micro-scale | P1 |
| AddToCart | Tactile feedback | P1 |
| Cart badge | Spring pulse | P2 |
| Customizer | Spatial step transition | P2 |
| VisualPreview | Layer entrance | P2 |
| Instagram | Controlled marquee | P3 |

---

## 22. Claude'a Verilecek Uygulama Kuralı

Claude'a özellikle şu talimat verilmelidir:

> "Mevcut animasyonları topluca silip yeniden yazma."

Bunun yerine:

```
Existing behavior
       ↓
Motion audit
       ↓
Reusable tokens
       ↓
Component upgrade
       ↓
Accessibility
       ↓
Performance validation
       ↓
Visual QA
```

uygulanmalı. Çünkü mevcut Design System zaten animasyon kararlarını tanımlıyor.

---

## 23. Önerilen Dosya Mimarisi

Claude mümkünse şu yapıyı oluşturmalı:

```
lib/
  motion/
    tokens.ts
    variants.ts
    transitions.ts
    reduced-motion.ts
```

```
motion/
 ├── tokens
 │    ├── durations
 │    ├── easings
 │    └── springs
 │
 ├── variants
 │    ├── reveal
 │    ├── drawer
 │    ├── dropdown
 │    ├── page
 │    └── stagger
 │
 └── utilities
      └── reducedMotion
```

Bu sayede componentlerin içine yüzlerce farklı `transition={{ ... }}` serpiştirilmez.

---

## 24. Motion Component'leri

Her şeyi tek bir `PremiumAnimation` component'ine sokmak da yanlış — çünkü CartDrawer, MenuCard, Hero, CategoryNav, PageTransition aynı davranışı göstermiyor.

Bunun yerine motion primitives yaklaşımı kullanılmalı: Reveal, Stagger, PageTransition, DrawerMotion, DropdownMotion, Pressable.

Ama bunlar mevcut UI mimarisini bozmadan küçük abstraction'lar olmalı.

---

## 25. Global MotionConfig

Uygulamanın üst seviyesinde `<MotionConfig reducedMotion="user">` kullanılması önerilir.

Bunun avantajı: Claude'un her componentte reduced-motion mantığını yeniden icat etmesini engeller. Motion resmi dokümantasyonunda bu yaklaşım doğrudan destekleniyor.

---

## 26. Premium Seviyeyi Belirleyecek 5 Kriter

Claude'un işi tamamlandı kabul etmemesi gereken kriterler:

1. **Spatial continuity** — UI öğeleri state değiştirirken nereden nereye gittikleri anlaşılmalı.
2. **Tactility** — Button/card gerçekten fiziksel tepki vermeli.
3. **Hierarchy** — Her şey aynı anda hareket etmemeli.
4. **Restraint** — Animasyon marka karakterini bastırmamalı.
5. **Accessibility** — Reduced Motion aktifken deneyim hâlâ anlaşılır olmalı.

---

## 27. Global Benchmark Sonucu

Güncel Motion/Framer yaklaşımında premium web motion artık yalnızca fade in / slide up / hover üçlüsünden oluşmuyor.

Öne çıkan yaklaşım: **Gesture + Spring + Shared Layout + Scroll + Micro-interaction + Spatial Transition + Accessibility** kombinasyonudur.

Motion'ın güncel React API'si bu alanların tamamı için `AnimatePresence`, `layoutId`, `useScroll`, `useSpring`, `useTransform`, `useReducedMotion` gibi yapı taşlarını sağlıyor.

Ancak Bowlera için bunların hepsini kullanmak hedef değildir. Hedef:

> Doğru yerde doğru motion.

---

## 28. Sonuç — Bowlera Premium Motion Hedefi

Mevcut `Static UI + occasionally animation` yerine:

```
BOWLERA MOTION SYSTEM

                         │
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
       PRESENCE       INTERACTION     CONTINUITY
          │              │              │
       Reveal          Tactile       layoutId
          │              │              │
          └──────────────┼──────────────┘
                         ↓
                  SPATIAL TRANSITION
                         │
                  Drawer / Page
                         │
                         ↓
                   AMBIENT MOTION
                         │
                  Hero / imagery
                         ↓
                  REDUCED MOTION
                         +
                    PERFORMANCE
```

kurulmalı.

Bu yaklaşım Bowlera'yı "animasyon eklenmiş bir Next.js sitesi" görünümünden çıkarıp kendi motion language'ına sahip premium bir dijital marka deneyimine yaklaştırır.

Ve önemli nokta şu: **Mevcut Design System çöpe atılmıyor.** Tam tersine, mevcut 500–600ms reveal, 250ms page transition, 200ms card hover, transform/opacity ve reduced-motion kuralları korunup üstlerine daha gelişmiş spatial + tactile + shared-motion katmanı ekleniyor.

### Claude İçin Uygulama Sırası

**P0**
1. CartDrawer ✅ *(bu proje kapsamında tamamlandı — bkz. SESSION_INDEX.md #105)*
2. MenuCard
3. CategoryNav / layoutId

**P1**
4. AccountMenu
5. Header scroll
6. Hero orchestration
7. Page transitions *(token değeri 500ms'ye güncellendi, bileşen henüz kodlanmadı)*

**P2**
8. Cart badge
9. Customizer
10. VisualPreview

**P3**
11. Ambient/Instagram motion

Bu sırayla uygulanırsa, ilk üç değişiklik bile sitenin algılanan premium seviyesinde ciddi fark yaratır; sonraki katmanlar ise bunu bütün siteye yayar.

---

### Değişiklik Notu — v1.0 → v1.1

**Gerekçe:** v1.0, 677 satır boyunca "mobil"/"touch"/"pointer" kelimelerini hiç geçirmemişti;
tüm Level 2 (Tactile Interaction) koreografisi `whileHover` üzerine kurulmuştu. Bowlera trafiği
neredeyse tamamen dokunmatik olduğu için, MenuCard P0-2 uygulamasında bu efektlerin mobilde HİÇ
görünmediği canlıda tespit edildi (kod+test PASS olmasına rağmen).

**Eklenenler:**
- §1a (YENİ) — Dokunmatik Öncelik: raporun geri kalanına uygulanan zorunlu ön koşul
- §2 (Level 2) — hover/tap/release üçlüsü "aynı hedefe giden farklı giriş yolları" olarak netleştirildi
- §3 — `springs.cardRelease` (`duration: 0.45, bounce: 0.15`) token'ı eklendi, canlı kullanıcı testiyle kalibre edildi
- §6/§7 (MenuCard/CTA) — `whileTap="hover"` + variant propagation + giriş/çıkış transition ayrımı işlendi

**Henüz işlenmeyenler (P1+ katmanlarda aynı denetim gerekli):** AccountMenu (§9), Header (§10),
Hero (§11), Page transitions (§14), Add to Cart (§16), Cart badge (§17) — bu bölümlerin hiçbiri
kod olarak henüz uygulanmadığı için dokunma-tetikleyici denetimi P0 katmanıyla (CartDrawer,
MenuCard, CategoryNav) sınırlı tutuldu. CategoryNav (§8) `layoutId` zaten seçim-bazlı olduğu için
(hover'a bağımlı değil) bu denetimden muaf.
