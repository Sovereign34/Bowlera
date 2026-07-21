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
- **Framer Motion** → yalnızca orkestrasyon gerektiren yerlerde: sayfa geçişi, scroll-reveal, özelleştirici adım geçişleri
- **Sade CSS `transition`** → basit hover geçişleri (kütüphane yükü gereksiz)

### 6.1 Animasyon Tablosu

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

### 6.2 Performans ve Erişilebilirlik Kuralları

```
1. Tüm animasyonlar prefers-reduced-motion: reduce medya sorgusunu kontrol etmeli
   → Aktifse animasyonlar devre dışı, anında geçiş yapılmalı
2. Yalnızca transform ve opacity animasyonlu
   → width/height/top gibi layout tetikleyen özellikler ASLA animasyonlu bırakılmaz (CLS riski)
3. Scroll-reveal animasyonları tek seferlik olmalı
   → Her scroll'da tekrar tetiklenmemeli (performans + "rahatsız edici" his riski)
```

> Bu 3 kural AGENT.md Self-Check'te otomatik denetlenir.

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
[ ] Yeni renk kullanılıyor mu?          → Bölüm 2 tablosunda var mı?
[ ] Logo degrade kullanılıyor mu?        → Sadece 4 izinli yerden biri mi? (Bölüm 2.1)
[ ] Bronze rengi kullanılıyor mu?        → 18px+ başlık/dekoratif mi?
[ ] Yeni animasyon ekleniyor mu?         → prefers-reduced-motion kontrolü var mı?
[ ] Animasyon width/height/top mu tetikliyor? → transform/opacity'e çevrildi mi?
[ ] Yeni görsel ekleniyor mu?            → Adlandırma standardına uygun mu? (Bölüm 5.1)
[ ] Alerjen gösterimi eklendi/değişti mi? → Bölüm 7 Self-Check'i geçti mi?
```

**Format:** `"Tasarım skoru: 6/7 — [eksik kriter] nedeniyle 1 puan düştü."`

---

*BOWLERA DESIGN_SYSTEM.md — v1.1 — Session 1 (2026-07-17), Session 4 (2026-07-21)*
*Kaynak: MASTER_PLAN.md §2, §4 · CORE.md §6 (Kritik Tasarım/Ürün Varsayımları)*
*v1.1: §7 "Alerjen Gösterim Sistemi" eklendi (Açık Sorun #7 kapatıldı, Session 4,
2026-07-21). Eski §7 (Kalite Kontrol) §8'e kaydı, self-check listesine alerjen
maddesi eklendi.*
