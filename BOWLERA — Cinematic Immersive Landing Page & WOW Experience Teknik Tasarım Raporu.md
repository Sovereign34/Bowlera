# BOWLERA
## Cinematic Immersive Landing Page & WOW Experience
### Teknik Tasarım ve Uygulama Raporu

**Versiyon:** 1.0  
**Tarih:** Ağustos 2026  
**Hedef:** Bowlera'yı standart bir online food-ordering sitesinden, premium ve global ölçekte algılanabilecek dijital-first bir food brand deneyimine dönüştürmek.

---

# 1. YÖNETİCİ ÖZETİ

Bowlera'nın mevcut teknik altyapısı, sinematik bir landing page oluşturmak için yeterli temel bileşenlere zaten sahiptir.

Mevcut projede:

- Next.js 14 App Router
- React 18
- TypeScript
- Tailwind CSS
- Framer Motion
- Zustand
- NextAuth
- Menü veri modeli
- Ürün customizer
- Sepet
- Sipariş akışı
- Personel operasyon ekranları
- Responsive yapı

bulunmaktadır.

Ancak mevcut ana sayfa şu anda yalnızca temel bir Hero bileşeninden oluşmaktadır ve ana ürün görseli placeholder durumundadır.

Bu nedenle önerilen strateji:

> **Mevcut ticari sistemi değiştirmek yerine, üzerine premium bir cinematic brand experience katmanı eklemek.**

Landing page'in amacı yalnızca güzel görünmek değildir.

Üç hedef aynı anda gerçekleştirilmelidir:

1. İlk 3–5 saniyede güçlü WOW etkisi.
2. Bowlera'nın premium ve güvenilir bir marka olarak algılanması.
3. Kullanıcıyı mümkün olan en kısa yoldan ürün seçimine ve siparişe taşımak.

---

# 2. ANA TASARIM FELSEFESİ

Landing page:

**"animasyonlu web sitesi"**

olarak tasarlanmamalıdır.

Doğru hedef:

> **Dijital bir yemek reklamı + interaktif marka deneyimi + satış arayüzü**

kombinasyonudur.

Kullanıcı siteye girdiğinde geleneksel:

Logo → başlık → fotoğraf → buton

yapısını görmek yerine Bowlera'nın ürününün oluşumunu deneyimlemelidir.

Ana fikir:

> **From ingredients to your bowl.**

Yani:

**Malzeme → hazırlık → birleşme → final bowl → sipariş**

hikâyesi.

---

# 3. HEDEF GERÇEKLİK SEVİYESİ

Animasyonun hedef gerçeklik seviyesi:

## 9/10 Photorealistic

Ancak amaç hiper-gerçekçi CGI göstermek değildir.

Hedef:

> "Bu gerçek bir premium food commercial çekimi mi, yoksa CGI mı?"

sorusunu oluşturacak kadar gerçekçi bir görüntüdür.

### 3.1 Tavuk

Tavukta:

- doğal lif yapısı
- pişmiş yüzey
- hafif kızarma
- gerçekçi yağ yansımaları
- küçük yüzey düzensizlikleri
- doğal parça geometrisi

olmalıdır.

### 3.2 Sebzeler

Sebzeler:

- tamamen geometrik olmamalı
- doğal renk farklılıklarına sahip olmalı
- hafif yüzey kusurları bulunmalı
- gerçek ışık yansımaları göstermeli
- hareket sırasında gerçek fizik kurallarına uymalıdır.

### 3.3 Sos

Sos kritik bir gerçeklik testidir.

Sos:

- gerçek viskozite
- doğal akış
- yüzey gerilimi
- küçük damlacıklar
- kontrollü sıçrama
- gerçek ışık yansıması

göstermelidir.

Sosun matematiksel bir çizgi gibi hareket etmesi engellenmelidir.

### 3.4 Bowl

Bowl:

- gerçek malzeme hissi
- mikro yansımalar
- hafif yüzey kusurları
- gerçekçi gölge
- ambient occlusion

ile oluşturulmalıdır.

---

# 4. LANDING PAGE MASTER FLOW

Önerilen kullanıcı deneyimi:

```text
ENTRY
  ↓
CINEMATIC HERO
  ↓
INGREDIENTS
  ↓
ASSEMBLY
  ↓
BOWL REVEAL
  ↓
BRAND MESSAGE
  ↓
SIGNATURE BOWLS
  ↓
BUILD YOUR BOWL
  ↓
NUTRITION / TRUST
  ↓
ORDER CTA
```

Ancak bu bölümler klasik ayrı section'lar gibi görünmemelidir.

Scroll sırasında tek bir sinematik hikâyenin devamı hissedilmelidir.

---

# 5. SAHNE 01 — THE HOOK

## Süre

İlk deneyimin hedef süresi:

**5–8 saniye**

İlk saniyelerde kullanıcıdan uzun bir intro izlenmesi beklenmemelidir.

### Görsel

Karanlık / sıcak cream tonlu premium bir sahne.

Ortada boşluk.

Bir tavuk parçası kadraja girer.

Ardından:

- yeşillik
- sebze
- grain/base
- sos
- topping

farklı yönlerden kontrollü şekilde gelir.

Ancak her malzeme aynı anda gelmez.

### Kamera

Başlangıç:

**macro close-up**

Sonra:

**slow cinematic pull-back**

Final:

**top-down / 3/4 hero shot**

---

# 6. SAHNE 02 — INGREDIENT ORCHESTRATION

Bu bölüm Bowlera'nın en önemli WOW alanlarından biridir.

Malzemeler sadece ekranda belirmemelidir.

Her malzemenin karakteri olmalıdır.

Örnek:

### Tavuk

Kamera yakınında geçer.

### Sebzeler

Daha hafif ve hızlı hareket eder.

### Sos

Akışkan şekilde sahneye girer.

### Grain/Base

Daha ağır ve kontrollü hareket eder.

Bu farklı hareket karakterleri sayesinde görüntü "AI tarafından sırayla eklenmiş objeler" gibi görünmez.

---

# 7. SAHNE 03 — THE ASSEMBLY

Tüm malzemeler bowl çevresinde orbit hareketi yapar.

Bowl henüz tamamen görünmez.

Kamera:

```text
45° angle
↓
slow orbit
↓
micro push-in
↓
top-down transition
```

Malzemeler bowl içine yerleşir.

Burada fizik çok önemlidir.

Objeler:

- birbirinin içinden geçmemeli
- aşırı simetrik dizilmemeli
- aynı hızda hareket etmemeli
- aynı rotayı kullanmamalı.

---

# 8. SAHNE 04 — HERO BOWL REVEAL

Bütün malzemeler birleşir.

Kamera yavaşça geri çekilir.

Final bowl tam kadrajda görülür.

Bu anda animasyonun en güçlü frame'i oluşturulmalıdır.

### Final kompozisyon

Bowl:

- merkezde
- hafif 3/4 açı
- premium soft lighting
- doğal shadow
- hafif depth-of-field

ile gösterilir.

Arka plan Bowlera'nın:

- Warm Cream
- Deep Olive
- Espresso

paleti ile uyumlu olmalıdır.

---

# 9. SAHNE 05 — BRAND REVEAL

Bowl final pozisyonuna geldikten sonra:

**BOWLERA**

ve slogan ortaya çıkar.

Önerilen ana mesaj:

# BOWL BETTER

Alt mesaj:

**Daha iyi beslen. Daha iyi yaşa.**

Burada sloganın kendisini animasyonla aşırı hareket ettirmek yerine minimal motion kullanılmalıdır.

Çünkü ürün artık ana kahramandır.

---

# 10. HERO CTA

İki ana CTA önerilmektedir:

### Primary

**Kaseni Oluştur**

→ `/menu/customize/...`

### Secondary

**Menüyü Keşfet**

→ `/menu`

Mevcut projede bu iki CTA zaten bulunmaktadır.

Dolayısıyla yeni landing page mevcut ticari akışla doğrudan bağlanabilir.

---

# 11. SIGNATURE BOWLS SECTION

Hero'dan sonra kullanıcıya Bowlera'nın gerçek ürünleri gösterilmelidir.

Mevcut `menu-data.json` içerisinde örneğin:

- Teriyaki Tavuklu Kase
- Somonlu Akdeniz Kase
- Füme Antrikot Kase
- Vegan Falafel Kase
- Sıcak Tahıllı Kinoa Kase
- Akdeniz Humuslu Sıcak Kase

gibi gerçek ürün veri yapısı bulunmaktadır.

Bu bölümün amacı:

> "Bu sadece güzel bir marka sitesi değil, gerçekten sipariş verebileceğim bir marka."

algısını oluşturmak.

---

# 12. ÜRÜN KARTLARI

Klasik grid yerine premium editorial layout önerilir.

Örneğin:

```text
        LARGE HERO BOWL
             ↓
     Product information

SMALL BOWL       SMALL BOWL
```

Hover sırasında:

- hafif scale
- shadow transition
- nutrition metadata
- CTA reveal

kullanılabilir.

Ancak agresif animasyonlardan kaçınılmalıdır.

---

# 13. BUILD YOUR BOWL EXPERIENCE

Landing page'in ikinci büyük WOW alanı burasıdır.

Kullanıcı:

**Kaseni Oluştur**

dediğinde mevcut customizer sistemine geçer.

Mevcut projede:

- StepBase
- StepMain
- StepGarden
- StepSignatureFlavor
- StepFinish
- VisualPreview

gibi component'ler zaten bulunmaktadır.

Bu büyük avantajdır.

Landing page ile customizer arasında görsel süreklilik kurulmalıdır.

Örneğin landing page'deki bowl:

**base → protein → garden → sauce → finish**

mantığıyla oluşuyorsa customizer da aynı terminolojiyi kullanmalıdır.

Böylece marka deneyimi tek bir sistem gibi görünür.

---

# 14. INTERACTIVE SCROLL EXPERIENCE

Ana landing page için önerilen teknik model:

## Scroll-driven storytelling

Kullanıcı scroll yaptıkça:

```text
scroll progress 0%
    ↓
ingredient entrance

20%
    ↓
ingredient orbit

40%
    ↓
bowl reveal

60%
    ↓
brand message

80%
    ↓
product reveal

100%
    ↓
CTA
```

Burada scroll animasyonları tamamen sürekli çalıştırılmamalıdır.

Animasyonlar:

**scroll progress → animation progress**

şeklinde bağlanmalıdır.

---

# 15. FRAMER MOTION KULLANIMI

Projede zaten:

`framer-motion`

bulunduğu için ilk aşamada yeni bir animasyon framework'ü eklenmesine gerek yoktur.

Framer Motion:

- opacity
- transform
- scale
- rotate
- spring
- layout
- viewport triggers

için kullanılmalıdır.

Ancak ağır 3D sahneler için her şeyi React DOM üzerinden yapmak doğru değildir.

---

# 16. 3D VE VIDEO STRATEJİSİ

En ideal sistem hibrit olmalıdır.

## Layer 1 — HTML / CSS

- typography
- buttons
- UI
- CTA
- navigation

## Layer 2 — Framer Motion

- UI transitions
- scroll reveal
- text animation
- product card interaction

## Layer 3 — Video

Higgsfield ile oluşturulan:

- cinematic food shots
- hero animation
- ingredient movement
- bowl reveal

video olarak kullanılabilir.

## Layer 4 — WebGL / Canvas

Gerekirse:

- interactive bowl
- particle effects
- advanced parallax
- realtime 3D

için kullanılabilir.

Ancak başlangıçta WebGL zorunlu değildir.

---

# 17. HIGGSFIELD KULLANIM STRATEJİSİ

Higgsfield'de hazır karakterler kullanılmak zorunda değildir.

Bowlera için ana strateji:

> **Custom food assets + cinematic generation**

olmalıdır.

Üretilecek temel asset'ler:

1. Hero bowl
2. Chicken macro
3. Vegetable macro
4. Grain/base macro
5. Sauce macro
6. Topping macro
7. Bowl empty
8. Bowl final
9. Ingredient orbit shot
10. Final hero shot

Bu asset'ler aynı:

- kamera dili
- lens karakteri
- ışık
- renk
- materyal
- gerçekçilik

ile oluşturulmalıdır.

---

# 18. ASSET CONSISTENCY

En kritik teknik konulardan biridir.

Farklı AI generation'larda:

- tavuk rengi
- bowl geometrisi
- sebze şekli
- ışık yönü
- kamera açısı
- background

değişirse kullanıcı bunu fark eder.

Bu nedenle bir:

## Bowlera Visual Asset Bible

oluşturulmalıdır.

Her asset için:

```text
Object ID
Material
Color
Camera
Lens
Lighting
Background
Scale
Rotation
Shadow
Reference Image
```

tanımlanmalıdır.

---

# 19. FOTOĞRAF MI CGI MI?

En ideal yöntem:

## Hybrid Photorealism

Önce gerçek ürün fotoğrafı / yüksek kaliteli ürün render'ı oluşturulmalı.

Sonra AI video generation ile hareket verilmelidir.

Tamamen sıfırdan AI video üretmek yerine:

**Reference image → controlled motion**

yaklaşımı tercih edilmelidir.

Bu yöntem ürün tutarlılığını artırır.

---

# 20. KAMERA DİLİ

Bowlera için kamera dili:

### Macro

Malzeme detayları.

### 50mm equivalent

Premium food commercial görünümü.

### 85mm equivalent

Bowl hero.

### Top-down

Ingredient composition.

### 35mm equivalent

Environmental brand scene.

Kamera hareketleri:

- slow push-in
- slow pull-out
- controlled orbit
- macro rack focus
- subtle handheld micro movement

olmalıdır.

Aşırı hızlı kamera hareketlerinden kaçınılmalıdır.

---

# 21. IŞIK

Önerilen lighting:

## Key

Soft large-source light.

## Fill

Düşük yoğunlukta.

## Rim

Bowl ve malzemeleri background'dan ayıracak şekilde.

## Ambient

Sıcak, doğal ve düşük kontrastlı.

Hedef:

**premium food commercial**

görüntüsüdür.

---

# 22. RENK SİSTEMİ

Mevcut tasarım sistemindeki renkler korunmalıdır:

```text
Warm Cream    #F4F0E7
Charcoal      #1F1A18
Espresso      #38221D
Olive         #53502A
Deep Olive    #6A6541
Bronze        #816E44
```

Animasyonların renkleri bu palete göre color-grade edilmelidir.

AI generation sonucunda aşırı:

- neon green
- saturated red
- blue tint
- orange cinematic LUT

kullanılmamalıdır.

Bowlera'nın kendi marka paleti baskın kalmalıdır.

---

# 23. TYPOGRAPHY

Mevcut:

**Cormorant Garamond**

display fontu olarak kullanılabilir.

**Nunito**

body/UI için kullanılabilir.

Bu kombinasyon korunmalıdır.

Hero başlığında büyük tipografi kullanılmalı fakat ekranın tamamını kaplayan aşırı büyük typography kullanılmamalıdır.

---

# 24. NAVIGATION

Header tamamen kaybolmamalıdır.

Ancak cinematic hero sırasında daha minimal bir header kullanılabilir.

Öneri:

```text
BOWLERA
              MENU
              ACCOUNT
              CART
```

Scroll sonrası normal header state'e geçilebilir.

---

# 25. LOADING EXPERIENCE

Landing page ağır video nedeniyle bekletilmemelidir.

Önerilen yapı:

```text
Initial render
    ↓
Static hero poster
    ↓
Critical UI
    ↓
Low-resolution video
    ↓
High-resolution cinematic video
```

Video yüklenene kadar poster frame gösterilmelidir.

---

# 26. PERFORMANCE MİMARİSİ

Ana hedefler:

### LCP

Mümkün olduğunca düşük tutulmalıdır.

### CLS

Hero yüklenirken layout değişmemelidir.

### INP

Scroll ve interaction işlemleri ana thread'i kilitlememelidir.

Video:

- lazy load
- compressed
- mobile-specific
- desktop-specific

varyantlarla sunulmalıdır.

---

# 27. VIDEO TEKNİK FORMAT

Master:

**4K**

Web delivery:

**1080p**

Mobile:

**720p veya optimize edilmiş 1080p**

Codec:

- H.264 fallback
- modern browser için WebM/VP9 veya AV1 uygunluğu test edilebilir.

Video:

- muted
- autoplay
- playsInline
- loop

olarak çalışabilir.

Ancak kritik brand reveal video üzerinden değil HTML olarak da oluşturulmalıdır.

---

# 28. MOBILE STRATEJİSİ

Desktop animasyonun aynısı mobile taşınmamalıdır.

Mobile'da:

```text
Hero poster
↓
short video
↓
Bowl reveal
↓
CTA
```

kullanılabilir.

Scroll sırasında çok büyük video canvas kullanmak yerine daha kısa sequence kullanılmalıdır.

---

# 29. ACCESSIBILITY

`prefers-reduced-motion` desteği korunmalıdır.

Mevcut projede global olarak bu düşünülmüş durumdadır.

Reduced-motion kullanıcılarında:

- video poster
- static bowl
- fade transition

kullanılmalıdır.

Animasyon hiçbir zaman içeriğe erişim için zorunlu olmamalıdır.

---

# 30. SEO

Cinematic landing page SEO'nun yerine geçmemelidir.

HTML içerisinde gerçek:

```text
<h1>
<h2>
<p>
<Product>
```

içeriği bulunmalıdır.

Video içindeki yazılar SEO içeriği olarak kullanılmamalıdır.

Metadata mevcut Next.js metadata sistemi üzerinden geliştirilmelidir.

---

# 31. CONVERSION ARCHITECTURE

WOW etkisi tek başına yeterli değildir.

Landing page'in dönüşüm yolu:

```text
WOW
 ↓
DESIRE
 ↓
TRUST
 ↓
CHOICE
 ↓
ORDER
```

olmalıdır.

Hero:

**WOW**

Signature products:

**DESIRE**

Nutrition information:

**TRUST**

Menu/customizer:

**CHOICE**

CTA:

**ORDER**

---

# 32. NUTRITION TRUST SECTION

Mevcut ürün veri modelinde:

- calories
- protein
- carbs
- fat
- allergens
- tags

zaten tutulmaktadır.

Bu veri landing page'de kullanılmalıdır.

Örneğin:

**High Protein**

**38g Protein**

**540 kcal**

gibi bilgiler premium bir editorial tasarımla gösterilebilir.

Bu Bowlera'yı sıradan fast-food markalarından ayırabilecek önemli bir özelliktir.

---

# 33. SOSYAL KANIT

Landing page'in ilerleyen bölümünde:

- müşteri yorumları
- sipariş sayısı
- rating
- kullanıcı fotoğrafları

gibi gerçek veriler kullanılabilir.

Ancak gerçek veri oluşmadan sahte testimonial kullanılmamalıdır.

---

# 34. FINAL CTA

Landing page'in sonunda tekrar büyük bir ürün görüntüsü.

Metin:

# BOWL BETTER

Alt:

**Kendin için daha iyi bir kase oluştur.**

CTA:

**Kaseni Oluştur**

İkinci:

**Menüyü Keşfet**

---

# 35. ÖNERİLEN SAYFA YAPISI

```text
/
│
├── CinematicHero
│
├── BrandStatement
│
├── IngredientStory
│
├── BowlAssembly
│
├── SignatureBowls
│
├── NutritionTrust
│
├── BuildYourBowl
│
├── BrandStory
│
├── SocialProof
│
└── FinalCTA
```

---

# 36. COMPONENT MİMARİSİ

Mevcut:

```text
components/home/
```

altında sistem genişletilebilir.

Önerilen:

```text
components/home/
│
├── CinematicHero.tsx
├── HeroVideo.tsx
├── HeroPoster.tsx
├── HeroHeadline.tsx
├── HeroCTA.tsx
│
├── IngredientStory.tsx
├── IngredientScene.tsx
├── BowlAssembly.tsx
│
├── SignatureBowls.tsx
├── SignatureBowlCard.tsx
│
├── NutritionSection.tsx
├── BuildYourBowlCTA.tsx
├── SocialProof.tsx
└── FinalCTA.tsx
```

---

# 37. VIDEO STATE MİMARİSİ

Video ve scroll interaction doğrudan component state'e bağlanmamalıdır.

Önerilen abstraction:

```text
scrollProgress
      ↓
animationProgress
      ↓
scene state
      ↓
visual layer
```

Örneğin:

```ts
type HeroSceneState =
  | 'intro'
  | 'ingredients'
  | 'assembly'
  | 'reveal'
  | 'brand'
```

Bu ileride animasyonların değiştirilmesini kolaylaştırır.

---

# 38. PRELOAD STRATEJİSİ

Sadece kritik asset'ler preload edilmelidir.

Öncelik:

```text
Logo
Hero poster
Hero font
Critical CSS
Primary CTA
```

Sonra:

```text
Hero video
Product images
Secondary assets
```

yüklenebilir.

---

# 39. AI ASSET PIPELINE

Önerilen üretim pipeline:

```text
Real Product Reference
        ↓
Image cleanup / consistency
        ↓
Master reference image
        ↓
Higgsfield image-to-video
        ↓
Shot selection
        ↓
Color grading
        ↓
Compression
        ↓
Web delivery
```

Her video üretiminden önce master reference kullanılmalıdır.

---

# 40. HIGGSFIELD PROMPT MANTIĞI

Her sahnede prompt sadece:

"beautiful food commercial"

gibi genel ifadelerden oluşmamalıdır.

Prompt yapısı:

```text
SUBJECT
+
MATERIAL
+
PHYSICAL BEHAVIOR
+
CAMERA
+
LENS
+
LIGHTING
+
ENVIRONMENT
+
MOTION
+
REALISM
+
COLOR GRADE
```

Örneğin:

```text
Photorealistic grilled chicken pieces,
natural cooked texture,
subtle surface moisture,
premium food commercial lighting,
85mm macro lens,
shallow depth of field,
slow controlled cinematic movement,
physically plausible motion,
warm cream background,
olive and bronze color grading,
natural imperfections,
high-end commercial food photography realism.
```

Bu yapı tüm asset'lerde standardize edilmelidir.

---

# 41. AI HALLUCINATION KONTROLÜ

AI video production sırasında özellikle şu problemler kontrol edilmelidir:

- ekstra malzeme oluşması
- tavuk şeklinin değişmesi
- bowl geometrisinin değişmesi
- çatal/kaşık deformasyonu
- sosun fizik dışı hareketi
- ingredient duplication
- background morphing
- logo deformasyonu

Logo hiçbir zaman AI video içinde kritik şekilde oluşturulmamalıdır.

Logo HTML/image layer olarak eklenmelidir.

---

# 42. WOW ETKİSİ İÇİN EN ÖNEMLİ TASARIM KARARI

WOW etkisini:

**"çok fazla efekt"**

ile üretmek yanlış olur.

En güçlü WOW:

> **Sadelik + gerçekçilik + kontrollü hareket + ürünün beklenmedik şekilde oluşması**

kombinasyonundan gelir.

Dolayısıyla:

**less effects / more realism**

ilkesi kullanılmalıdır.

---

# 43. KAÇINILMASI GEREKENLER

Kesinlikle kaçınılmalı:

- aşırı neon renkler
- fazla particle
- gereksiz 3D objeler
- sürekli hareket eden text
- aşırı parallax
- hızlı kamera hareketleri
- her section'da farklı animation style
- generic AI characters
- stok yemek fotoğrafları
- sahte testimonial
- autoplay ses
- uzun intro
- loading ekranında kullanıcıyı bekletmek

---

# 44. KARAKTER KULLANIMI

Higgsfield'deki insan karakterleri ana landing page'in merkezine koymak önerilmemektedir.

Bowlera'nın ana karakteri:

# BOWL

olmalıdır.

İnsan karakterleri daha sonra:

- lifestyle campaign
- social media
- brand story
- advertisement

için kullanılabilir.

Ana landing page'de ürün merkezli storytelling daha güçlüdür.

---

# 45. LANDING PAGE'İN EN İDEAL WOW SENARYOSU

Önerilen final senaryo:

### 0.0–1.0 saniye

Cream/olive karanlık geçiş.

Çok yakın macro görüntü.

### 1.0–2.5 saniye

Tavuk hızlı ama kontrollü şekilde kadraja girer.

### 2.5–4.0 saniye

Sebzeler ve base ortaya çıkar.

### 4.0–5.5 saniye

Bowl görünür.

Malzemeler orbit hareketi yapar.

### 5.5–6.5 saniye

Sos gerçekçi şekilde akar.

### 6.5–7.5 saniye

Final bowl.

Kamera geri çekilir.

### 7.5–8.5 saniye

Logo:

**BOWLERA**

### 8.5+ saniye

**BOWL BETTER**

CTA:

**Kaseni Oluştur**

Bu ilk deneyim kullanıcıya:

> "Bu sıradan bir yemek sipariş sitesi değil."

mesajını vermelidir.

---

# 46. MEVCUT PROJEYE ENTEGRASYON

Mevcut:

```text
app/page.tsx
```

şu anda yalnızca:

```tsx
<Hero />
```

render etmektedir.

Bu nedenle landing page'in ana giriş noktası zaten hazırdır.

Mevcut:

```text
components/home/Hero.tsx
```

yeniden tasarlanabilir.

`HeroImagePlaceholder.tsx` ise gerçek asset/video sistemi ile değiştirilmelidir.

Mevcut CTA'lar korunmalıdır.

---

# 47. MEVCUT ALTYAPININ KORUNMASI

Landing page yapılırken aşağıdaki sistemlere dokunulmamalıdır:

- authentication
- cart
- order APIs
- customizer state
- personnel system
- menu data
- database
- checkout/order logic

Landing page yalnızca mevcut ticari sistemin üst katmanıdır.

Bu mimari yaklaşım teknik riskleri ciddi şekilde azaltır.

---

# 48. TEKNİK ÖNCELİK SIRASI

## Phase 1 — Visual Foundation

- gerçek bowl görselleri
- ingredient assets
- master reference
- lighting standard
- camera standard
- color grade

## Phase 2 — Cinematic Hero

- Higgsfield shots
- hero video
- poster
- mobile variant
- fallback

## Phase 3 — Interactive Story

- scroll progress
- ingredient scenes
- bowl assembly
- reveal

## Phase 4 — Product Integration

- signature bowls
- menu data
- product cards
- nutrition

## Phase 5 — Conversion

- customizer CTA
- menu CTA
- final CTA
- analytics

## Phase 6 — Optimization

- video compression
- lazy loading
- LCP
- CLS
- mobile performance
- reduced motion
- accessibility

---

# 49. ANALYTICS

Landing page için event tracking kurulmalıdır.

Önerilen events:

```text
landing_view
hero_video_started
hero_video_completed
hero_cta_clicked
menu_clicked
customizer_clicked
product_viewed
customizer_started
add_to_cart
checkout_started
order_completed
```

Böylece WOW etkisinin gerçek ticari değeri ölçülebilir.

Özellikle:

```text
Hero → CTA conversion
Hero → Menu conversion
Hero → Customizer conversion
```

ölçülmelidir.

---

# 50. BAŞARI KRİTERLERİ

Landing page sadece estetik olarak değerlendirilmemelidir.

### Brand

Kullanıcı:

**"Premium bir marka."**

demeli.

### Product

Kullanıcı:

**"Yemek gerçekten iştah açıcı."**

demeli.

### Trust

Kullanıcı:

**"Ne yediğimi biliyorum."**

demeli.

### UX

Kullanıcı:

**"Sipariş vermek kolay."**

demeli.

### Performance

Site:

**"Hızlı."**

hissettirmeli.

---

# 51. SON TASARIM KARARI

Bowlera için önerilen nihai sistem:

> **Photorealistic cinematic food advertising + scroll-driven storytelling + real product data + direct commerce integration**

Bu, klasik:

**"restaurant landing page"**

modelinden daha ileri bir yapıdır.

Ancak gereksiz teknoloji eklemek yerine mevcut Next.js/React/Framer Motion altyapısının üzerine kurulmalıdır.

---

# 52. NİHAİ VİZYON

Bowlera açıldığında kullanıcı şunu görmemeli:

> "Bir restoran web sitesi."

Şunu hissetmeli:

> **"Bir marka deneyiminin içine girdim."**

Ve deneyimin sonunda:

> **"Bu kaseyi istiyorum."**

demelidir.

Bu nedenle en güçlü WOW unsuru animasyonun kendisi değil:

**animasyon + ürün gerçekçiliği + marka kimliği + kullanıcıyı siparişe taşıyan akışın tek bir deneyim gibi çalışmasıdır.**

---

# 53. UYGULAMA İÇİN MASTER PRENSİP

Uygulama sırasında bütün ekip için tek ana kural:

> **Bowlera'nın gerçek ürününü kahraman yap. Teknolojiyi gösterme; teknolojinin oluşturduğu deneyimi göster.**

Higgsfield araçtır.

Framer Motion araçtır.

Next.js araçtır.

WebGL gerekirse araçtır.

Kullanıcının gördüğü şey ise yalnızca:

# BOWLERA

## BOWL BETTER

olmalıdır.

---

# 54. SONUÇ

Mevcut Bowlera projesi bu yaklaşım için uygun bir teknik temele sahiptir.

Özellikle:

- mevcut Hero yapısı,
- Framer Motion,
- mevcut ürün veri modeli,
- customizer,
- menu sistemi,
- cart,
- order flow

landing page'in doğrudan ticari sisteme bağlanmasını mümkün kılmaktadır.

Bu nedenle öneri:

**Siteyi yeniden yapmak değil.**

**Mevcut sistemi cinematic brand experience ile yükseltmektir.**

İdeal sonuç:

```text
CINEMATIC BRAND EXPERIENCE
            +
REAL FOOD PRODUCT
            +
INTERACTIVE STORY
            +
NUTRITION TRUST
            +
CUSTOM BOWL
            +
DIRECT ORDER
            =
BOWLERA DIGITAL BRAND
```

Bu yapı doğru uygulanırsa landing page yalnızca görsel olarak etkileyici olmaz; Bowlera'nın **marka algısını, ürün iştahını ve dönüşüm potansiyelini aynı anda yükselten ana dijital yüzü** haline gelir.