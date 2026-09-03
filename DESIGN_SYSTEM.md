# BOWLERA — DESIGN_SYSTEM.md
> Bu belge Bowlera'nın tasarım kontrat dosyasıdır.
> Renk, tipografi, ikonografi, fotoğraf ve animasyon kararları burada tanımlanır.
> UI kodu yazılmadan önce Claude bu dosyayı okumak zorundadır.
> Kaynak: MASTER_PLAN.md §4 (Tasarım Sistemi) + §2 (Rakip/İlham Analizi)

---

## 1. TASARIM FELSEFESİ

Site genelinde **toprak tonu (olive/bronze/espresso/cream)** paleti hakimdir.
Logodaki mor-pembe-turuncu degrade yalnızca **dönüşüm noktalarında** (CTA, sepet,
özelleştirici adımları, hover) sınırlı bir vurgu olarak kullanılır. Bu, marka
tutarlılığını korurken logo enerjisini dijital deneyime taşır.

**Referans markalar:** DIG ve Sweetgreen'in organik güvenilirlik stratejisi
(toprak tonu) + CAVA'nın adım adım görselleştirilmiş özelleştirme sihirbazı
(customizer UX referansı). Detaylı rakip tablosu: MASTER_PLAN §2.

---

## 2. RENK SİSTEMİ (WCAG Doğrulamalı)

> Kaynak: MASTER_PLAN §4.1

| Renk | Hex | Rol | Kontrast (Cream üzerinde) | WCAG | Tailwind Token |
|---|---|---|---|---|---|
| Warm Cream | `#F4F0E7` | Sayfa arka planı | — | — | `bg-cream` |
| Charcoal Black | `#1F1A18` | Ana metin/başlık | 15.14:1 | AAA | `text-charcoal` |
| Espresso Brown | `#38221D` | İkincil metin, fiyatlar | 13.05:1 | AAA | `text-espresso` |
| Primary Olive | `#53502A` | Birincil CTA/buton | 7.24:1 | AAA | `bg-olive-primary` |
| Deep Olive | `#6A6541` | İkincil buton/ikon | 5.20:1 | AA | `bg-olive-deep` |
| Bronze | `#816E44` | Dekoratif, büyük başlık (18px+) | 4.35:1 | AA Large only | `text-bronze` |

> ⚠️ **Bronze küçük gövde metninde kullanılmaz** — sadece 18px+ kalın başlıklarda
> veya dekoratif sınır/illüstrasyonlarda (AGENT.md YASAK LİSTE).

### 2.2 Personel Paneli İstisnası — Kırmızı (DAR KAPSAMLI)

> **[BU TURDA EKLENDİ, 2026-08-11]** `/personel/*` altındaki dahili araçlarda (müşteri
> ASLA görmez) "acil aksiyon bekliyor" anlamı taşıyan rozet/uyarılarda standart Tailwind
> `red-700`/`red-800` kullanımına izin verilir — Bölüm 2'deki toprak tonu paletin
> **dışında**, SADECE bu dar kapsamda.

```
Kapsam:     SADECE /personel/* rotaları (sekme rozetleri, GelAlOrderCard şüpheli-eşik
            rozeti gibi dahili uyarılar). Müşteri yüzü sayfalarda (menü, sepet,
            customizer, /siparis vb.) HÂLÂ YASAK — Bölüm 7.3 aynen geçerli.
Renkler:    bg-red-700, text-red-800, border-red-700/40 (Tailwind standart, yeni hex
            icat edilmedi)
Gerekçe:    Kırmızı, personel için evrensel "acil/bekliyor" konvansiyonu — dahili araç
            olduğu için marka tutarlılığı riski yok. Ayrıca GelAlOrderCard.tsx'teki
            şüpheli-deneme rozeti bu kuraldan ÖNCE zaten kırmızı kullanıyordu (fark
            edilmemiş bir tutarsızlıktı) — bu ekleme o kullanımı GERİYE DÖNÜK olarak
            resmileştiriyor, yeni bir sapma YARATMIYOR.
```

> ⚠️ Bu istisna Bölüm 8 Self-Check'teki "Yeni renk kullanılıyor mu?" sorusunu geçersiz
> KILMAZ — kontrol ederken "personel rotası mı?" sorusu da eklenmiş sayılmalı.

### 2.1 Logo Degradesi — Sınırlı Kullanım

```css
background: linear-gradient(135deg, #8A2387 0%, #E94057 50%, #F27121 100%);
```

**Yalnızca şu 4 yerde kullanılır:**
1. Özelleştirici aktif adım göstergesi
2. Sepet rozeti (badge)
3. CTA hover kenarlığı (2px)
4. "Süper Gıda" etiket arka planı

> ⚠️ **Site arka planlarında ASLA kullanılmaz.** İhlali AGENT.md Self-Check'te
> otomatik yakalanır ("Logo degrade site arka planında mı kullanılıyor?").

---

## 3. TİPOGRAFİ

| Kullanım | Font | Ağırlık | Tailwind Token |
|---|---|---|---|
| Başlık (h1-h3) | Cormorant Garamond (serif, logoyla uyumlu) | 700 | `font-display` |
| Gövde / UI | Nunito veya Raleway (sans-serif, mobilde okunabilir) | 400 / 600 | `font-body` |

**Uygulama notu:** `next/font` ile self-host edilir (performans + layout shift önleme).

---

## 4. İKONOGRAFİ

| Kullanım | Kaynak | Not |
|---|---|---|
| Genel arayüz ikonları | **Lucide React** | Hafif, tutarlı çizgi stili, React native entegrasyon |
| Yaprak/zeytin motifi (logo imza deseni) | Özel SVG (Lucide'da yok) | İnce çizgisel (outline), Primary Olive renginde, 2px stroke — Lucide ile aynı kalınlık |

**İmza deseni kullanım yerleri:** yükleme ekranları, bölüm ayraçları, "Sağlıklı Tercih" rozetleri.

---

## 5. FOTOĞRAF DİREKTİFİ

> Kaynak: MASTER_PLAN §4.4, §4.8

| Kural | Detay |
|---|---|
| Ana kase çekimleri | 90° tam üstten (flat-lay) |
| Destekleyici görseller | 45° stüdyo açısı |
| Işık | Yumuşak gölgeli, sıcak-doğal (5000–5500K), sert flaş yok |
| Zemin | Mat traverten, açık meşe veya Warm Cream tonlu beton — parlak/yansıtıcı yüzey yok |

### 5.1 Dosya Adlandırma Standardı

```
[kategori]-[ürün-adı-kebab-case].webp

Örnek: signature-teriyaki-tavuk-kase.webp
       build-your-own-kinoa-taban.webp
```

> Tutarlı dosya yönetimi ve SEO alt-text üretimi için zorunludur (CONTENT_GUIDE.md
> bu adlandırmayı otomatik alt-text üretiminde kaynak olarak kullanır).

---

## 6. ANİMASYON VE MİKRO-ETKİLEŞİM SİSTEMİ

> Kaynak: MASTER_PLAN §4.7

**Felsefe:** Animasyon dekorasyon değil, yönlendirmedir. Her hareket bir şeyi
açıklamalı (seçim yapıldı, sayfa değişti, öğe eklendi) — amaçsız "gösteriş"
animasyonundan kaçınılmalı. Toprak tonu paletin sakinliğiyle tezat oluşturmayacak
şekilde **yumuşak, organik easing** kullanılmalı.

**Kütüphane seçimi:**
- **Framer Motion** → yalnızca orkestrasyon gerektiren yerlerde: sayfa geçişi, scroll-reveal, özelleştirici adım geçişleri, sepet çekmecesi, ürün kartı tactile katmanı
- **Sade CSS `transition`** → basit hover geçişleri (kütüphane yükü gereksiz)

> **[2026-09-03 — bkz. BOWLERA_MOTION_SYSTEM_RAPORU.md v1.1]** Framer Motion mimari
> yükseltmesi (11 adımlık P0-P3 sırası) sürüyor. Merkezi token kaynağı `lib/motion/tokens.ts`
> — bu bölümdeki süre/easing/spring değerleri o dosyayla senkron TUTULMALI, biri değişirse
> diğeri aynı turda güncellenir.

### 6.1 Animasyon Tablosu

| Bileşen/Alan | Animasyon | Süre & Easing | Tetikleyici |
|---|---|---|---|
| Hero başlık | Alttan yukarı fade+slide (staggered, kelime/satır bazlı) | 600ms, `ease-out`, 80ms stagger | Sayfa yüklenince |
| Hero arka plan görseli | Hafif Ken Burns efekti (yavaş zoom) | 8-12s, `linear`, sonsuz döngü | Sayfa yüklenince |
| Bölüm başlıkları/kartlar (scroll reveal) | Alttan fade+slide, %10 viewport'a girince | 500ms, `ease-out` | Scroll (Intersection Observer) |
| MenuCard hover/dokunma (kart+CTA+görsel) | Kart `y: 0→-4` + gölge derinleşmesi; CTA `y: 0→-1` (sadece özelleştirilebilir); görsel `scale: 1→1.045` — **üçü de tek variant state'inden (variant propagation) besleniyor.** **[2026-09-03 güncellendi]** Giriş (rest→hover) ve çıkış (hover→rest) AYRI: giriş süre/easing aynı kaldı, çıkış `springs.cardRelease`'e (bkz. 6.1a) çevrildi — hem `mouse-leave` hem `tap-release` bu spring'i kullanır. | Giriş: 200ms, `ease-in-out` · Çıkış: `springs.cardRelease` (spring, `duration:0.45/bounce:0.15`) | **[2026-09-03 güncellendi]** Hover VE dokunma (`whileHover` + `whileTap="hover"`, AYNI hedef — bkz. §6.3) |
| Sepete Ekle butonu | Tıklamada kısa "scale bounce" (0.95→1.05→1) | 300ms, `spring` | Click |
| Sepet rozeti (badge) | Sayı değiştiğinde logo-degrade renkli "pulse" | 400ms, `springs.badge` (VARSAYIM — bkz. 6.1a, onay bekliyor) | Sepete ürün eklenince |
| Sepet çekmecesi (CartDrawer) | **[YENİ, 2026-09-03]** Backdrop fade + panel `springs.drawer` slide + içerik `drawerContentStagger` ile sıralı giriş | Backdrop: fade · Panel: `springs.drawer` (spring, VARSAYIM) · İçerik: `drawerContentStagger` (VARSAYIM) — bkz. 6.1a | Açılış/kapanış (`isOpen` state, `AnimatePresence`) |
| Özelleştirici adım geçişi | Yatay slide (mevcut adım sola çıkar, yeni adım sağdan girer) | 350ms, `ease-in-out` | "Sonraki Adım" tıklanınca |
| VisualPreview katmanı | Yeni malzeme seçilince ilgili katman fade-in + hafif scale (0.9→1) | 250ms, `ease-out` | Malzeme seçimi |
| Özet panel (sticky) fiyat/kalori güncelleme | Sayı değişiminde kısa vurgu rengi flaşı (logo-degrade) | 300ms | Değer değişince |
| Sayfa geçişleri | Hafif fade (crossfade) | 500ms, `ease-in-out` **[2026-09-03 güncellendi — önceki: 250ms, kullanıcı isteğiyle yavaşlatıldı]** ⚠️ **[BU TURDA TESPİT EDİLDİ]** Bu değişiklik hiçbir sohbette/SESSION_INDEX'te loglanmamış — bkz. dosya sonu not | Route değişimi (Next.js) |
| Instagram galeri / sosyal kanıt | Yatay kayan (marquee) şerit, hover'da durur | 30-40s tam döngü, `linear` | Sayfa görünür olunca |
| CategoryNav aktif sekme göstergesi | **[HENÜZ KODLANMADI — P0-3]** `layoutId` tabanlı kayan pill | Netleşmedi | Seçim (tıklama/dokunma) — `layoutId` zaten state-bazlı, §6.3'ten ETKİLENMEZ |

### 6.1a Spring/Stagger Token Sözlüğü

> `lib/motion/tokens.ts`'teki `springs` objesiyle bire bir eşleşmesi gerekir. Bu tablo
> DESIGN_SYSTEM tarafındaki resmi kayıt — ⚠️ işaretli olanlar `tokens.ts` dosyasının
> kendisi bu turda da görülmeden, kod tarafındaki import'lardan çıkarılan VARSAYIMDIR;
> `tokens.ts` paylaşılınca kesin teyit edilmeli.

> **[2026-09-03, bu turda]** `tokens.ts` nihayet görüldü. Yapı çelişkisi ÇÖZÜLDÜ: gerçek kod
> düz `durations`/`easings`/`springs`/`drawerContentStagger` export'ları kullanıyor (raporun
> önerdiği nested `motionTokens.*` yapısı DEĞİL) — bu tablo artık kod teyitli, rapor
> spesifikasyonu değil.

| Token | `tokens.ts`'teki gerçek değer | Kullanıldığı Yer | Durum |
|---|---|---|---|
| `springs.cardRelease` | `{ type: "spring", stiffness: 300, damping: 24 }` | MenuCard/MenuCardImage çıkış (hover→rest, tap-release) | 🔴 **ÇELİŞKİ — KOD GÜNCEL DEĞİL.** Bu satır daha önce canlı testte "çok sert" bulunup `duration:0.45/bounce:0.15`'e kalibre edildiği notuyla kayıtlıydı — ama `tokens.ts`'te hâlâ eski stiffness/damping değeri duruyor, kalibrasyon koda hiç yansımamış. **Karar (bu turda, kullanıcı adına):** canlı kullanıcı testi kod varsayılanından üstündür → `tokens.ts` satır 61 `duration: 0.45, bounce: 0.15` olarak DÜZELTİLMELİ. Aksiyon SESSION_INDEX'e işlendi. |
| `springs.drawer` | `{ type: "spring", stiffness: 320, damping: 32 }` | CartDrawer panel slide | ✅ TEYİT EDİLDİ — rapor §4 ile birebir eşleşiyor |
| `springs.tactile` | `{ type: "spring", stiffness: 400, damping: 30 }` | Genel dokunsal tepki | ✅ TEYİT EDİLDİ — rapor §3 ile birebir eşleşiyor |
| `springs.badge` | `{ type: "spring", stiffness: 300, damping: 26 }` | Sepet rozeti pulse | ✅ TEYİT EDİLDİ — daha önce hiç sayısal değer yoktu, artık kesin |
| `drawerContentStagger` | `0.05` (50ms) | CartDrawer içerik sıralı giriş | ✅ TEYİT EDİLDİ — rapor §5'teki 40-60ms aralığının ortası, `tokens.ts` yorumunda da böyle belirtilmiş |

### 6.2 Performans ve Erişilebilirlik Kuralları

```
1. Tüm animasyonlar prefers-reduced-motion: reduce medya sorgusunu kontrol etmeli
   → Aktifse animasyonlar devre dışı, anında geçiş yapılmalı
2. Yalnızca transform ve opacity animasyonlu
   → width/height/top gibi layout tetikleyen özellikler ASLA animasyonlu bırakılmaz (CLS riski)
3. Scroll-reveal animasyonları tek seferlik olmalı
   → Her scroll'da tekrar tetiklenmemeli (performans + "rahatsız edici" his riski)
4. [YENİ, 2026-09-03] Tactile (kart/CTA/görsel lift-zoom benzeri) etkileşimler SADECE
   whileHover ile tanımlanamaz — dokunma (whileTap) AYNI hedef variant'a gitmeli
   → Bowlera trafiği neredeyse tamamen dokunmatik; hover-only bir katman mobil
     kullanıcının büyük çoğunluğu için hiç var olmaz (bkz. §6.3, kaynak:
     BOWLERA_MOTION_SYSTEM_RAPORU.md §1a — MenuCard P0-2'de canlıda tespit edildi)
```

> Bu 4 kural AGENT.md Self-Check'te otomatik denetlenir.

### 6.3 Dokunmatik Öncelik (Touch-First)

> **[YENİ, 2026-09-03]** Kaynak: BOWLERA_MOTION_SYSTEM_RAPORU.md §1a — MenuCard P0-2
> uygulamasında canlıda tespit edilen bulgu üzerine eklendi.

```
Kural:      Fare (whileHover) ve dokunma (whileTap) AYNI hedef state'e gitmeli.
            İki ayrı görsel dil icat edilmez.
Giriş:      rest → aktif — mevcut ease/duration tabanlı kararlar (§6.1) korunur.
Çıkış:      aktif → rest (hem mouse-leave hem tap-release) — fiziksel "geri sekme"
            hissi için duration/bounce tabanlı spring önerilir (elle stiffness/
            damping tahmini yerine, süre/sertlik hissini doğrudan ayarlar).
İstisna:    layoutId tabanlı geçişler (örn. CategoryNav aktif sekme) zaten bir
            state değişikliğine (tıklama/dokunma ile seçim) bağlı — bu kuraldan
            ETKİLENMEZ.
```

---

## 7. ALERJEN GÖSTERİM SİSTEMİ

> Kaynak: Açık Sorun #7 (SESSION_INDEX.md) — Session 4, 2026-07-21 onaylandı.
> Veri modeli (`menu-data.json`, `types/index.ts`) alerjen bilgisini zaten destekliyor;
> bu bölüm sadece UI gösterim kuralını tanımlar.

### 7.0 Zorunluluk Seviyesi

```
Kalori/protein ile AYNI statü: bir üründe alerjen verisi varsa
MenuCard / Customizer / SummaryPanel-Sepet'te GİZLENEMEZ, opsiyonel yapılamaz.
```

> ⚠️ Bu kural CORE.md §8 "Kalori/protein zorunlu alan" varsayımının alerjene
> genişletilmiş halidir. Alerjen verisi olmayan ürünlerde bölüm sessizce boş kalır
> (yanıltıcı "alerjen yok" ibaresi zorunlu değildir, sadece gösterilmez).

### 7.1 Gösterim Yerleri

| Yer | Biçim |
|---|---|
| `MenuCard.tsx` | Kalori satırının hemen altında küçük ikon şeridi (max 4 ikon, taşarsa `+N`) |
| Customizer (malzeme seçimi) | Her malzemenin yanında tekil ikon + tooltip/tap |
| `SummaryPanel` / Sepet | Kâsedeki TÜM malzemelerin birleşik/tekilleştirilmiş alerjen listesi (malzeme malzeme değil, konsolide tek liste) |

### 7.2 İkonografi

- Lucide React'te alerjen ikonu yok → imza yaprak/zeytin motifiyle aynı stil:
  ince çizgisel (outline), **2px stroke**, **Primary Olive (`#53502A`)** renginde,
  Bölüm 4'teki özel SVG setiyle aynı üretim kalıbı.
- Kapsanan alerjenler (MVP): **Gluten, Süt, Yumurta, Fındık/Kuruyemiş, Soya,
  Balık/Kabuklu Deniz Ürünü, Susam.**
- İkon dosya adlandırma: `allergen-icon-[ad].svg` (Bölüm 5.1 ile tutarlı kebab-case).

### 7.3 Renk Kararı

```
Logo degrade KULLANILMAZ (Bölüm 2.1'deki 4 izinli yer dışında bir yer daha açmaz).
Yeni bir "uyarı kırmızısı" YOK — palet toprak tonunda kalır.
İkon: Primary Olive · Metin/tooltip: Charcoal Black (birincil) veya Espresso Brown (ikincil)
```

> Gerekçe: alerjen bilgisi her zaman görünür ve gizlenemez olduğu için ayrı bir
> alarm rengine ihtiyaç yoktur; görünürlük zaten renkten değil, zorunluluk
> kuralından (7.0) gelir.

### 7.4 Etkileşim & Animasyon

- Masaüstü: hover'da tooltip (malzeme/ikon adı + "İçerir: [alerjen]")
- Mobil: tap'te genişleyen chip
- Animasyon: VisualPreview katmanıyla aynı desen — **250ms, `ease-out`, fade-in +
  hafif scale (0.9→1)** — Bölüm 6.2 kurallarına tabi (`prefers-reduced-motion`
  kontrolü zorunlu, yalnızca `transform`/`opacity`).

### 7.5 Alerjen Self-Check

```
[ ] Üründe alerjen verisi var mı?        → MenuCard/customizer/sepette gösteriliyor mu?
[ ] Alerjen bilgisi gizleniyor/opsiyonel mi? → EVET: kesinlikle yasak — DUR (7.0)
[ ] Yeni bir alarm rengi/logo degrade mi kullanıldı? → EVET: yasak — Primary Olive'e çevir (7.3)
[ ] SummaryPanel'deki liste konsolide mi, malzeme malzeme mi? → Malzeme malzeme ise DUR, birleştir (7.1)
```

> Not: AGENT.md'deki genel SELF-CHECK/YASAK LİSTE tablosuna karşılık gelen satırın
> eklenmesi ayrı bir onay gerektirir (Kural #5 — tek problem, tek çözüm), bu
> değişikliğin kapsamı dışındadır.

---

## 8. KALİTE KONTROL — DESIGN_SYSTEM SELF-CHECK

```
[ ] Yeni renk kullanılıyor mu?          → Bölüm 2 tablosunda var mı? Değilse: /personel/* rotası mı (Bölüm 2.2 istisnası) yoksa gerçek ihlal mi?
[ ] Logo degrade kullanılıyor mu?        → Sadece 4 izinli yerden biri mi? (Bölüm 2.1)
[ ] Bronze rengi kullanılıyor mu?        → 18px+ başlık/dekoratif mi?
[ ] Yeni animasyon ekleniyor mu?         → prefers-reduced-motion kontrolü var mı?
[ ] Animasyon width/height/top mu tetikliyor? → transform/opacity'e çevrildi mi?
[ ] Yeni görsel ekleniyor mu?            → Adlandırma standardına uygun mu? (Bölüm 5.1)
[ ] Alerjen gösterimi eklendi/değişti mi? → Bölüm 7 Self-Check'i geçti mi?
[ ] [YENİ] Tactile animasyon (kart/CTA/görsel) sadece whileHover mi? → EVET: whileTap="hover" (aynı hedef) eksik — DUR (6.3)
```

**Format:** `"Tasarım skoru: 7/8 — [eksik kriter] nedeniyle 1 puan düştü."`

---

*BOWLERA DESIGN_SYSTEM.md — v1.5 — Session 1 (2026-07-17), Session 4 (2026-07-21),
Session 14 (2026-08-11), 23. sohbet (2026-09-03, üç alt-tur)*
*Kaynak: MASTER_PLAN.md §2, §4 · CORE.md §6 (Kritik Tasarım/Ürün Varsayımları)*
*v1.1: §7 "Alerjen Gösterim Sistemi" eklendi (Açık Sorun #7 kapatıldı, Session 4,
2026-07-21). Eski §7 (Kalite Kontrol) §8'e kaydı, self-check listesine alerjen
maddesi eklendi.*
*v1.2: §2.2 "Personel Paneli İstisnası — Kırmızı" eklendi (dar kapsamlı, SADECE
/personel/* rotaları, müşteri yüzü sayfalarda yasak aynen sürüyor). Bölüm 8
Self-Check'e personel-rotası kontrolü eklendi. GelAlOrderCard.tsx'teki önceden
var olan kırmızı kullanımını geriye dönük resmileştiriyor.*
*v1.3: §6.1'e CartDrawer (P0-1) ve MenuCard hover/dokunma (P0-2) satırları işlendi,
yeni §6.1a "Spring/Stagger Token Sözlüğü" eklendi (springs.cardRelease/drawer/tactile/badge
+ drawerContentStagger — çoğu ⚠️ VARSAYIM, `tokens.ts` görülmeden teyit edilemedi). §6.2'ye
4. kural + yeni §6.3 "Dokunmatik Öncelik" eklendi: tactile animasyonlar SADECE whileHover
ile tanımlanamaz, dokunma (whileTap) aynı hedefe gitmeli — MenuCard P0-2'de canlıda tespit
edilen bulgu (rapor v1.0 tamamen hover-merkezliydi, Bowlera trafiği neredeyse tamamen
dokunmatik). Bölüm 8 Self-Check'e karşılık gelen madde eklendi. Kaynak: BOWLERA_MOTION_
SYSTEM_RAPORU.md v1.1 §1a, CORE.md v1.7, AGENT.md v1.6 ile eşleştirildi.
⚠️ **TUTARSIZLIK TESPİTİ (bu turda, geriye dönük):** "Sayfa geçişleri" satırındaki
250ms→500ms değişikliği (etiketli "2026-09-03 güncellendi") bu sohbette hiç konuşulmadı ve
SESSION_INDEX.md'de hiçbir yerde loglanmamış — muhtemelen başka bir sohbette yapılıp
SESSION_INDEX'e hiç işlenmedi (ÇALIŞMA AKIŞI ihlali). İçeriğe dokunulmadı, sadece SESSION_INDEX'e
yeni bir Açık Sorun olarak eklendi, kullanıcıya bu turda ayrıca bildirildi.
⚠️ **DAHA CİDDİ TUTARSIZLIK (bu turda tespit edildi):** BOWLERA_MOTION_SYSTEM_RAPORU.md §3'ün
önerdiği token mimarisi (tek nested `motionTokens.{duration,ease,spring}` objesi, örn.
`motionTokens.spring.cardRelease`) ile gerçek kodun (`MenuCard.tsx`) kullandığı yapı
(`durations`/`easings`/`springs` — üç ayrı top-level export, `durations.menuCardHover` gibi
raporda hiç geçmeyen anahtarlarla) BİRBİRİYLE ÇELİŞİYOR. İkisi aynı `tokens.ts` dosyası olamaz.
`tokens.ts` görülmeden hangisinin (ya da üçüncü bir yapının) gerçek olduğu belirlenemez — bu
bölümdeki tüm §6.1a değerleri bu çelişki çözülene kadar RAPOR SPESİFİKASYONU olarak okunmalı,
kod teyidi olarak DEĞİL.*
*v1.4: Kullanıcı rapor v1.1'in tam metnini paylaştı. §6.1a'daki `springs.drawer`
(`stiffness:320/damping:32`, rapor §4) ve `drawerContentStagger` (40-60ms, rapor §5) "hiç
paylaşılmadı" durumundan "rapor spesifikasyonu var, kod teyidi yok" durumuna güncellendi.
Kritik bulgu: rapor §3'ün önerdiği token mimarisi (`motionTokens.duration/ease/spring`) ile
`MenuCard.tsx`'in gerçekte import ettiği yapı (`durations`/`easings`/`springs`,
`durations.menuCardHover` dahil) BİRBİRİYLE ÇELİŞİYOR — `tokens.ts` görülmeden çözülemez, not
olarak işlendi. Ayrıca raporun §28 sonundaki "Page transitions (token değeri 500ms'ye
güncellendi, bileşen henüz kodlanmadı)" notu, SESSION_INDEX Açık Sorun #106'daki (250ms→500ms,
kaynağı belirsiz değişiklik) sorunun kısmi açıklaması olarak SESSION_INDEX'e işlendi.*
*v1.5: `tokens.ts` paylaşıldı. §6.1a TAM kod-teyitli hale getirildi — yapı çelişkisi (#107)
ÇÖZÜLDÜ (gerçek kod düz `durations/easings/springs` export'ları kullanıyor, rapordaki nested
`motionTokens.*` DEĞİL). 4 değer teyit edildi (`drawer`, `tactile`, `badge`, `drawerContentStagger`).
🔴 YENİ BULGU: `springs.cardRelease` için `tokens.ts`'teki değer (`stiffness:300/damping:24`) ile
bu tablonun önceden kayıtlı canlı-kalibrasyon sonucu (`duration:0.45/bounce:0.15`) ÇELİŞİYOR —
kod eski değerde kalmış, kalibrasyon hiç commit edilmemiş görünüyor. Kullanıcı adına karar
verildi (bkz. tablo): canlı test sonucu esas alınır, `tokens.ts` düzeltilmeli — SESSION_INDEX'e
🔴 aksiyon olarak işlendi.*
