# BOWLERA — CORE

> Bu dosya her session başında verilen TEK başlangıç dosyasıdır.
> Ajan bu dosyadan hareketle neye ihtiyacı olduğunu kendisi belirler.
> NEXUS_OS metodolojisi esas alınarak Bowlera'ya (marka web sitesi / e-ticaret) uyarlanmıştır.
> MASTER_PLAN.md (Bowlera Master Teknik Referans v2.0) — bu dosyanın temelidir, değiştirilmez.

---

## 1. SESSION AÇILIŞ PROTOKOLÜ

Her session'da şu sırayı takip et — adım atlanamaz, sıra değiştirilemez:

```
1.  SESSION_INDEX.md oku
    → Anlık durum, açık sorunlar, sıradaki görevler, kritik teknik kararlar

2.  Arşiv dosyalarını ASLA otomatik isteme
    → Arşiv birden fazla parçaya ayrılmış olabilir (session_arşiv.md,
      session_arşiv_1.md, session_arşiv_2.md, ...). Hangi parçanın AKTİF
      (yeni taşıma bloklarının eklendiği) parça olduğunu SESSION_INDEX.md'nin
      üst notundan teyit et. Sadece kullanıcı geçmişe bakmak isterse veya
      ilgili session numarasını/parça dosyasını belirtince o bloğu iste

3.  Sağlık Kontrolü yap (Bölüm 10)
    → Sonucu tek cümleyle söyle, sorun varsa 🔴 ile işaretle

4.  Kullanıcıya şunu söyle (tek cümle):
    "Son durum: [özet]. Sıradaki görev: [liste]. Nereden başlayalım?"

5.  Kullanıcı görevi belirtince → Tetikleyici Tablosuna bak (Bölüm 3)
    → Hangi dosyalar gerekiyor? Listele.

6.  Eksik dosyaları iste — eksik veriyle ASLA çözüm üretme

7.  AGENT.md → Self-Check listesini uygula

8.  Çözüm üret → Risk Analizi + Confidence belirle

9.  Her büyük görev sonrası Checkpoint sor (Bölüm 7.2)

10. Session kapanış protokolünü uygula (Bölüm 7.1)
```

> ⚠️ Re-injection: Her 20 mesajda bir yeni sohbete geçiş önerilir. → Bölüm 11
> ⚠️ Self-Correction: Kural sapması fark edilince cevap üretilmeden durdurulur. → AGENT.md

---

## 2. PROJE KİMLİĞİ

| Alan | Değer |
|---|---|
| Proje | BOWLERA |
| Tam İsim | Bowlera — "Healthy Bowls" |
| Amaç | Fast-casual sağlıklı bowl markası — global kalitede kurumsal web sitesi |
| Hedef Pazar | Türkiye (İstanbul öncelikli), çoklu şube yapısı |
| Mimari Referans | MASTER_PLAN.md — Bowlera Master Teknik Referans v2.0 |
| Web Stack | Next.js (App Router) + Tailwind CSS + TypeScript |
| State Yönetimi | Zustand (`persist` middleware — sepet kalıcılığı) |
| Animasyon | Framer Motion (orkestrasyon: sayfa geçişi, scroll-reveal, customizer adımları) + sade CSS `transition` (basit hover) |
| İkonografi | Lucide React (genel arayüz) + özel SVG (logo yaprak/zeytin motifi — imza desen) |
| Tipografi | Cormorant Garamond (başlık) + Nunito/Raleway (gövde) |
| Veri Modeli — MVP | Statik `menu-data.json`, Next.js API Route (`/api/menu`) üzerinden servis |
| Veri Modeli — Büyüme | Headless CMS (Sanity.io veya Contentful) + Next.js ISR |
| Deploy | Netleşmedi — kullanıcıya sorulmalı (Vercel muhtemel, Next.js native) |
| Üçüncü Parti | Adisyo/SepetTakip (pazaryeri toplama), WhatsApp (`wa.me` köprüsü), QR menü, SMS/e-posta (ör. Twilio) |
| Repo | Tek repo — Next.js full-stack (frontend + API routes) |
| Versiyon | v1.0 |
| Son Session | — |

---

## 3. TETİKLEYİCİ TABLOSU — Hangi Görev → Hangi Dosya

> Kullanıcı görevi söyleyince bu tablodan eşleştir.
> Listelenen dosyaları iste, fazlasını isteme.

| Görev Türü | Zorunlu Dosyalar | Opsiyonel |
|---|---|---|
| Header / Footer / genel layout | `ARCHITECTURE.md` | `DESIGN_SYSTEM.md` |
| Ana Sayfa (hero, değer önerisi, öne çıkanlar) | `MASTER_PLAN.md §3.1` + `DESIGN_SYSTEM.md` | `ARCHITECTURE.md` |
| Menü sayfası / filtreleme / MenuCard | `MASTER_PLAN.md §3.2` + `ARCHITECTURE.md` | `DESIGN_SYSTEM.md` |
| "Kâseni Yarat" özelleştirme akışı | `CUSTOMIZER_SPEC.md` + `ARCHITECTURE.md` | `DESIGN_SYSTEM.md` |
| "Sandviçini Oluştur" özelleştirme akışı | `SANDWICH_SPEC.md` + `ARCHITECTURE.md` | `DESIGN_SYSTEM.md` |
| Sepet (cart) / Zustand store | `ARCHITECTURE.md §Veri Modeli` + `CUSTOMIZER_SPEC.md` | `FAILURE_PATTERNS.md` |
| Renk / tipografi / animasyon kararı | `DESIGN_SYSTEM.md` | — |
| Motion sistemi (Framer Motion mimarisi, spring/stagger/tactile) | `BOWLERA_MOTION_SYSTEM_RAPORU.md` + `DESIGN_SYSTEM.md §6` | `lib/motion/tokens.ts` |
| Fotoğraf / görsel direktifi / adlandırma | `DESIGN_SYSTEM.md` | — |
| Marka sesi / metin yazımı / CTA | `CONTENT_GUIDE.md` | — |
| SEO / JSON-LD / yerel görünürlük | `CONTENT_GUIDE.md` | `ARCHITECTURE.md` |
| Yemeksepeti / Getir / Trendyol entegrasyonu | `INTEGRATIONS.md` | `FAILURE_PATTERNS.md` |
| WhatsApp sipariş köprüsü | `INTEGRATIONS.md` | — |
| QR menü / masaya sipariş | `INTEGRATIONS.md` | `ARCHITECTURE.md` |
| Sipariş bildirimi (SMS/e-posta) | `INTEGRATIONS.md` | `CONFIG_SCHEMA.md` |
| Menü veri modeli / CMS geçişi | `ARCHITECTURE.md` | `DEPENDENCIES.md` |
| Env değişkeni / API key yönetimi | `CONFIG_SCHEMA.md` | — |
| Performans / Core Web Vitals | `ARCHITECTURE.md` + `DESIGN_SYSTEM.md §Animasyon` | `TEST_MATRIX.md` |
| Responsive / mobil uyarlama | `ARCHITECTURE.md` + `CUSTOMIZER_SPEC.md §Mobil UX` | — |
| Şubeler / konum bulucu | `ARCHITECTURE.md` + `CONTENT_GUIDE.md §SEO` | — |
| Bug fix (geçmiş kayıt lazımsa) | AKTİF arşiv parçasındaki ilgili taşınmış blok (SESSION_INDEX üst notundan hangi parça olduğunu teyit et) | `FAILURE_PATTERNS.md` |
| Rollback / deploy geri alma | `ARCHITECTURE.md §Deploy` | AKTİF arşiv parçası |
| Test / doğrulama / çalışıyor mu | `TEST_MATRIX.md` | — |
| Yol haritası / önceliklendirme / faz durumu | `ROADMAP.md` | — |
| Hangi dosya neyi etkiler | `DEPENDENCIES.md` | — |
| Secret/gizli veri, ödeme mantığı, eşzamanlılık (concurrency), KVKK/kişisel veri işleyen görev | `RISK_DOMAINS.md` | `FAILURE_PATTERNS.md` (geçmiş örnek varsa) |

---

## 4. DOSYA HARİTASI

```
── ÇEKİRDEK (Her session başında verilir) ────────────────
CORE.md                    ← Sen buradasın
AGENT.md                   ← Ajan davranış kuralları
SESSION_INDEX.md           ← Anlık durum pusulası — TEK aktif hafıza dosyası

session_arşiv.md,          ← Uzak/değiştirilemez hafıza, PARÇALARA AYRILABİLİR.
session_arşiv_1.md,          İki BAĞIMSIZ tetikleyici vardır, karıştırılmaz:
session_arşiv_2.md,          (A) SESSION_INDEX.md 400 satırı geçince, kapanmış
session_arşiv_3.md ★ AKTİF   içerik AKTİF arşiv parçasına taşınır (Bölüm 7.1).
... (N)                       (B) AKTİF arşiv parçasının KENDİSİ hacimce
                              yönetilemez hale gelirse (kullanıcı bunu belirtir/
                              talep eder), yeni bir sonraki parça (`_N+1`) açılır
                              — bu, SESSION_INDEX'in 400 satır kuralından AYRIDIR.
                              Her iki tetikleyici de "Ayrı bir 'session kaydı'
                              mekanizması" YARATMAZ — tek işlev hâlâ SESSION_INDEX'in
                              (veya bir önceki arşiv parçasının) boyutunu küçük
                              tutmaktır. Parçalama (B) yapıldığı ANDA, aynı turda
                              bu bölüm (Dosya Haritası) ve VERSİYON GEÇMİŞİ
                              güncellenir — atlanamaz (bkz. Bölüm 7.1 Adım 1.7).
                              SESSION_INDEX.md'nin üst notunda HER ZAMAN hangi
                              parçanın şu an AKTİF olduğu tek satırla belirtilir.

── REFERANS ──────────────────────────────────────────────
MASTER_PLAN.md              ← Bowlera Master Teknik Referans v2.0
                             §1 Yönetici Özeti
                             §2 Rakip ve İlham Analizi
                             §3 Site Mimarisi (Sitemap + sayfa bileşenleri)
                             §4 Tasarım Sistemi (renk/tipografi/animasyon/fotoğraf)
                             §5 Teknik Karar (Next.js/Tailwind/Zustand) + Entegrasyonlar
                             §6 Marka Sesi ve Örnek Metinler
                             §7 SEO ve Yerel Görünürlük
                             §8 Sonraki Adımlar (5 Oturumluk Plan)

ROADMAP.md                  ← 5 oturumluk inşa sırası, görevler, kabul kriterleri,
                             session bazlı milestone takibi

── TEKNİK MİMARİ ─────────────────────────────────────────
ARCHITECTURE.md            ← Next.js App Router mimarisi, komponent kontratları,
                             veri modeli, Zustand store yapısı, deploy/performans

DEPENDENCIES.md            ← Dosya ve modül bağımlılık haritası
                             (bir dosya değişince ne etkilenir)

CUSTOMIZER_SPEC.md         ← "Kâseni Yarat" akışının tam kontratı:
                             4 adım state makinesi, canlı fiyat/kalori hesabı,
                             VisualPreview katman mantığı, mobil UX

SANDWICH_SPEC.md           ← "Sandviçini Oluştur" akışının tam kontratı (v1.1,
                             2026-08-23) — CUSTOMIZER_SPEC.md desenlerini
                             kullanan AYRI/İZOLE store (useSandwichStore.ts,
                             Seçenek A), 6 adım state makinesi (Size→Bread→
                             Protein→Cheese→Veggies→Sauce&Toast&Extras),
                             UX sırasından bağımsız getPrepOrder() (mutfak
                             hazırlık sırası). ⚠️ Yapısal iskelet ONAYLANDI,
                             6 açık soru (S1-S6, malzeme verisi dahil) kod
                             aşamasından önce netleşmeli.

DESIGN_SYSTEM.md           ← Renk kullanım tablosu (WCAG), logo degrade kuralı,
                             tipografi, ikonografi, fotoğraf direktifi, animasyon sistemi

CONTENT_GUIDE.md           ← Marka sesi, örnek metinler, SEO anahtar kelimeler,
                             JSON-LD şema kalıbı

INTEGRATIONS.md            ← Adisyo/SepetTakip, WhatsApp köprüsü, QR menü,
                             SMS/e-posta bildirimi kontratları

BOWLERA_MOTION_SYSTEM_RAPORU.md ← Framer Motion mimari yükseltme raporu (v1.1,
                             2026-09-03) — 11 adımlık P0-P3 sırası (CartDrawer→
                             MenuCard→CategoryNav→...). §1a Dokunmatik Öncelik:
                             tüm tactile katman hover VE tap'e (aynı hedef)
                             gitmeli — Bowlera trafiği neredeyse tamamen
                             dokunmatik. ⚠️ Sadece P0-1 (CartDrawer) ve P0-2
                             (MenuCard) kodlandı, push/canlı doğrulama BEKLİYOR.

── TAKİP ─────────────────────────────────────────────────
FAILURE_PATTERNS.md        ← Projeye özgü hata kalıpları: sepet state kaybı,
                             checkout race condition, üçüncü parti entegrasyon
                             kopması, mobil responsive bugları

RISK_DOMAINS.md            ← YENİ (2026-09-22) — henüz yaşanmamış ama yaşanması
                             muhtemel hata sınıfları: gizli veri/secret dosyası,
                             fiyat/ödeme mantığı, eşzamanlılık, KVKK kapsamlı veri.
                             FAILURE_PATTERNS.md'den farkı: geçmişe değil geleceğe
                             bakar. Bir olay gerçekten yaşanırsa buradan
                             FAILURE_PATTERNS.md'ye FP-N olarak taşınır.

TEST_MATRIX.md             ← Modül bazlı test senaryoları ve durum
CONFIG_SCHEMA.md           ← Env değişkenleri şeması (.env.local kontratı)

── PROJE DOSYA YAPISI (Next.js App Router) ───────────────
app/
├── layout.tsx              ← Root layout (Header/Footer/font/tema)
├── page.tsx                ← Ana Sayfa
├── menu/
│   ├── page.tsx             ← Menü sayfası (filtre + grid)
│   └── customize/[id]/
│       └── page.tsx         ← Kâseni Yarat akışı
├── siparis/
│   └── page.tsx             ← Paket Servis / Gel Al
├── hakkimizda/page.tsx
├── subeler/page.tsx          ← Konum bulucu
├── iletisim/page.tsx
└── api/
    └── menu/route.ts        ← Menü verisi servis endpoint'i (MVP)

components/
├── layout/
│   ├── Header.tsx
│   └── Footer.tsx
├── home/
│   ├── Hero.tsx
│   ├── ValueProps.tsx
│   ├── FeaturedItems.tsx
│   └── InstagramFeed.tsx
├── menu/
│   ├── MenuCard.tsx          ← kalori ZORUNLU alan olarak render edilir; whileHover+
│   │                            whileTap="hover" (aynı hedef, §1a) — springs.cardRelease
│   ├── MenuCardImage.tsx     ← image zoom, variant propagation ile MenuCard'a bağlı
│   ├── FilterPanel.tsx
│   └── CategoryNav.tsx       ← sticky — motion yükseltmesi HENÜZ yapılmadı (P0-3)
├── customizer/
│   ├── StepBase.tsx / StepProtein.tsx / StepToppings.tsx / StepSauce.tsx
│   ├── SummaryPanel.tsx      ← sabit özet panel — kalori/fiyat her zaman görünür
│   └── VisualPreview.tsx     ← katmanlı CSS/SVG önizleme
├── cart/
│   ├── CartDrawer.tsx
│   └── CartBadge.tsx         ← logo-degrade pulse animasyonu
└── ui/                       ← paylaşılan buton/ikon/kart bileşenleri

store/
├── useCartStore.ts           ← Zustand + persist
└── useCustomizerStore.ts     ← Zustand (adım/seçim state'i)

lib/
├── menu-data.json            ← MVP statik veri kaynağı
├── motion/
│   └── tokens.ts             ← YENİ (2026-09-03) — durations/easings/springs
│                                merkezi kaynağı (springs.cardRelease dahil).
│                                DESIGN_SYSTEM.md §6.1 ile senkron olmalı,
│                                bazı değerler VARSAYIM (onay bekliyor)
├── integrations/
│   ├── whatsapp.ts
│   └── marketplace.ts        ← Adisyo/SepetTakip köprüsü
└── seo/
    └── schema.ts             ← JSON-LD üretici

public/
└── images/
    └── [kategori]-[ürün-adı-kebab-case].webp
```

---

## 5. CONTEXT KURALI

```
✅ Her seferinde minimum dosya iste
✅ Bir session'da maksimum 3 ana dosya aktif
✅ Kullanıcı yeni konuya geçince yeni dosya iste
✅ Asla tüm sistemi belleğe yükleme
✅ Eksik veriyle çözüm üretme — önce dosyayı iste
✅ MASTER_PLAN.md'nin ilgili bölümünü §numarasıyla referans ver
```

---

## 6. KRİTİK TASARIM/ÜRÜN VARSAYIMLARI

> Bu varsayımlar sistemin değiştirilemez çalışma kurallarıdır.
> Her Claude instance bunları bilmek ve uygulamak zorundadır.

| Kural | Açıklama |
|---|---|
| Kalori bilgisi zorunlu alan | MenuCard, customizer özet panel, sepette her zaman görünür — opsiyonel değil (MASTER_PLAN §5.5) |
| Logo degrade sınırlı kullanım | Yalnızca customizer adım göstergesi, sepet rozeti, CTA hover kenarlığı, "Süper Gıda" etiketi — site arka planında ASLA (MASTER_PLAN §4.2) |
| Bronze rengi küçük metinde yasak | Sadece 18px+ kalın başlık veya dekoratif kullanım (MASTER_PLAN §4.1) |
| 3 tıklama hedefi | Kullanıcı en fazla 3 tıklamayla siparişini tamamlamalı (MASTER_PLAN §3) |
| Animasyon = yönlendirme, dekorasyon değil | Her hareket bir anlam taşımalı; amaçsız "gösteriş" animasyonu yasak (MASTER_PLAN §4.7) |
| `prefers-reduced-motion` zorunlu kontrol | Tüm animasyonlar bu tercihe uymalı, aksi halde devre dışı bırakılmalı |
| Yalnızca `transform`/`opacity` animasyonlu | `width`/`height`/`top` gibi layout tetikleyen özellikler animasyonsuz (CLS riski) |
| API key / secret client'a gitmez | CMS, Adisyo/SepetTakip, Twilio anahtarları yalnızca server-side (API Route / env) |
| Mobil özet panel sticky çekmece | Masaüstü yan panel, mobilde sabit alt çekmeceye dönüşür (MASTER_PLAN §5.2) |
| Görsel adlandırma standardı | `[kategori]-[ürün-adı-kebab-case].webp` — SEO alt-text tutarlılığı için (MASTER_PLAN §4.8) |

---

## 7. SESSION KAPANIŞ PROTOKOLÜ

> ⚠️ ZORUNLUDUR. Adım atlanamaz. Kullanıcı onayı gelmeden session kapanmaz.

### 7.1 — Kapanış Adımları (Sırayla)

**Adım 1 — SESSION_INDEX.md**
- Açık sorunlar güncelle — çözülenler kaldır, yeniler ekle
- Sıradaki görevler güncelle
- Kritik teknik kararlar güncelle — yeni karar varsa ekle
- **TAM DOSYA olarak ver**
- ⚠️ "Şişmeyi önle" kuralı SADECE tamamlanmış/güncel-olmayan görev satırlarının silinmesini
  kapsar. Geçmiş oturumların **arşiv blokları** (SESSION ÖZET tablosu, 📜 GEÇMİŞ/ARŞİV başlıklı
  bölümler) TAM içerikle korunur — özetlenip "önceki versiyona bakılmalı" gibi bir referansla
  DEĞİŞTİRİLMEZ. Bu, AGENT.md Kural #4'ün (Truncated çıktı yasak) doğrudan bir uzantısıdır.
- ⚠️ **400 SATIR EŞİĞİ — aktif arşiv parçasına taşıma zorunluluğu:**
  SESSION_INDEX.md ile aktif arşiv parçası arasındaki ilişki SADECE bu eşikle çalışır; ayrı,
  her-session-kapanışında-yazılan bir "log" mekanizması YOKTUR (kaldırıldı — bkz. VERSİYON
  GEÇMİŞİ, session_log→session_arşiv geçişi). Kapanışta güncellenmiş SESSION_INDEX.md
  **400 satırı geçerse**, dosya "sıkıştırılarak" küçültülemez. Bunun yerine:
  1. Artık aktif olmayan içerik (kapanmış Açık Sorunlar, süresi geçmiş/uygulanmış Kararlar,
     eski CURRENT FOCUS metinleri, en eski SESSION ÖZET satırları) o anki **AKTİF arşiv
     parçasına TAŞINIR** — silinmez, özetlenmez. Hangi parçanın aktif olduğu SESSION_INDEX
     üst notundan teyit edilir; belirsizse kullanıcıya sorulur.
  2. Taşınan HER madde için arşiv parçasına eklenen blokta en az 1-2 cümlelik **kapanış
     gerekçesi** bırakılır. Gerekçesiz "artık etkili değil" diyerek satırı silmek KESİNLİKLE
     YASAKTIR — bu, 2026-07-20'de yaşanan gerçek bir ihlaldi: bir "sıkıştırılmış" SESSION_INDEX
     sürümü 7 açık sorunu (#4/7/15/16/20/22/34) ve 2 kararı (#11/#12) hiçbir kapanış notu
     olmadan tablolardan düşürmüştü.
  3. Taşıma işlemi kendi başına bir session kapanışı gerektirir: SESSION_INDEX.md'nin
     400 satırın ALTINA inmiş TAM güncel hâli + aktif arşiv parçasına eklenen taşıma bloğu
     **aynı turda birlikte** verilir — biri verilip diğeri sonraya bırakılamaz.
  4. Arşiv parçasına eklenen taşıma bloğu **SADECE YENİ EKLEME olarak** verilir —
     hiçbir arşiv parçası (session_arşiv.md, _1, _2, ...) asla tam olarak yeniden
     üretilmez, kullanıcı kendi elinle ilgili parçanın sonuna ekler. (Bkz. Bölüm 9
     Mutlak Yasaklar.)
  5. SESSION_INDEX.md'nin en üstündeki uyarı notuna, taşımanın tarihi, kaç madde
     taşındığı VE hangi arşiv parçasına taşındığı tek satırla kaydedilir.
  6. Bu adım atlanırsa Self-Correction tetiklenir — bkz. AGENT.md SELF-CORRECTION tablosu,
     "SESSION_INDEX 400 satır eşiği atlandı" satırı.
  7. ⚠️ **ARŞİV PARÇALAMA (dosyanın kendisi bölündüğünde) — AYRI, BAĞIMSIZ tetikleyici:**
     Yukarıdaki 400 satır eşiği SESSION_INDEX.md içindir. Bundan tamamen ayrı olarak, eğer
     AKTİF arşiv parçasının (`session_arşiv_N.md`) kendisi hacimce yönetilemez hale geldiyse
     (kullanıcı bunu fark eder/talep eder), yeni bir `session_arşiv_(N+1).md` açılır. Bu
     durumda:
     - Yeni parçanın başına, önceki parça(lar)la kronolojik ilişkiyi açıklayan bir not
       yazılır (bkz. mevcut arşiv dosyalarındaki örnek üst notlar).
     - **Aynı turda, atlanmadan** CORE.md'nin Bölüm 4 (Dosya Haritası) ve VERSİYON GEÇMİŞİ
       güncellenir — yeni parça dosyasının varlığı ve hangi tarihten itibaren aktif olduğu
       CORE.md'ye işlenir. CORE.md güncellenmeden parçalama "tamamlanmış" sayılmaz.
     - SESSION_INDEX.md'nin üst notu, yeni AKTİF parçanın adını yansıtacak şekilde
       güncellenir.
     - Bu adım atlanırsa Self-Correction tetiklenir — bkz. AGENT.md SELF-CORRECTION tablosu,
       "Arşiv parçalandı ama CORE.md güncellenmedi" satırı.

**Adım 2 — TEST_MATRIX.md**
- Bu session'da dokunulan bileşen/modül var mı?
- Varsa ilgili satırları güncelle: ❓ → ✅ veya ❌
- **TAM DOSYA olarak ver**

**Adım 3 — DEPENDENCIES.md**
- Yeni dosya/bileşen eklendi mi? Yeni bağımlılık oluştu mu?
- Değiştiyse **TAM DOSYA olarak ver**

**Adım 4 — ROADMAP.md**
- Bu session bir oturum/görev tamamladı mı?
- Tamamlandıysa checkbox işaretle, kabul kriteri güncelle
- Değiştiyse **TAM DOSYA olarak ver**

**Adım 5 — Kullanıcı Onayı**
- "Bu dosyaları onaylıyor musun?" diye sor
- "Evet" gelmeden session kapanmaz
- "Hayır" gelirse ilgili dosyayı düzelt, tekrar sun

---

### 7.2 — Checkpoint Protokolü (Ani Kesinti Koruması)

> Uzun sohbet aniden kesilebilir.
> Her büyük görev tamamlandığında — session bitmeden — checkpoint al.

**Ajan her büyük görev sonrası otomatik sorar:**
> "Checkpoint alayım mı? (Evet → SESSION_INDEX + TEST_MATRIX güncellenir)"

**Kullanıcı "Evet" derse:**
- SESSION_INDEX.md ve TEST_MATRIX.md güncellenir
- TAM DOSYA olarak verilir
- Hiçbir arşiv parçasına BU ADIMDA dokunulmaz — sadece SESSION_INDEX 400 satırı geçerse
  (Bölüm 7.1 Adım 1) ya da aktif parça kendisi şişerse (Bölüm 7.1 Adım 1.7) devreye girer
- Kullanıcı kopyalar — kesinti olsa bile buradan devam edilir

**Kullanıcı "Hayır" derse:**
- Devam edilir — bir sonraki görev sonrası tekrar sorulur

---

### 7.3 — Log Tetikleyicileri

Aşağıdakilerden biri gerçekleşince SESSION_INDEX güncellemesi + checkpoint ZORUNLU:

| Durum | Sembol |
|---|---|
| Görev tamamlandı | ✅ |
| Blokaj / hata oluştu | 🔴 |
| Veri modeli / şema değişti | 🗄️ |
| Dosya/bileşen eklendi / silindi | 📁 |
| Mimari veya tasarım kararı verildi | 🔧 |
| Kritik bug çözüldü | 🐛 |
| Üçüncü parti entegrasyon sorunu (WhatsApp/Adisyo/QR) | 📡 |
| Deploy yapıldı / rollback edildi | 🚀 |

---

### 7.4 — Veri Şeması Değişiklik Protokolü

> ⚠️ ZORUNLUDUR. `menu-data.json` yapısı veya (büyüme fazında) CMS şeması değiştiğinde atlanamaz.

**Temel Kural:** Şema değişmeden ÖNCE değişiklik notu oluşturulur.

**Not formatı:**
```
YYYYMMDDHHMMSS_aciklama.md
Örnek: 20260717130000_bowlitem_alerjen_alani_eklendi.md
```

**İçerik (zorunlu):**
```md
## Session: [numara] — [tarih]
## Açıklama: [ne değişti, neden]

### ÖNCE
[eski BowlItem tipi / şema]

### SONRA
[yeni BowlItem tipi / şema]

### ETKİLENEN DOSYALAR
[MenuCard.tsx, ARCHITECTURE.md, menu-data.json vb.]

### GERİ ALMA
[eski şemaya dönüş adımı]
```

**Session kapanışında:**
1. Not, proje köküne `docs/schema-changes/` klasörüne kaydedilir (kullanıcı repo'ya taşır)
2. SESSION_INDEX.md'nin Kritik Kararlar tablosuna `🗄️` sembolü + dosya adı yazılır
3. `ARCHITECTURE.md` güncellenir

---

## 8. MİMARİ VARSAYIMLAR

> Bu varsayımlar sistemin temel çalışma mantığıdır.
> Çelişkili durum olunca bu bölüm referans alınır.

| Varsayım | Açıklama |
|---|---|
| Kalori/protein zorunlu alan | `BowlItem` tipinde `calories`/`protein` opsiyonel değil (MASTER_PLAN §5.5) |
| MVP → statik veri, Büyüme → CMS | Geçiş `/api/menu` sözleşmesi bozulmadan yapılmalı |
| Sepet state Zustand + persist | Tarayıcı kapansa da sepet korunur (`bowlera-cart-storage`) |
| Customizer 5 adım sırayla ilerler | Base → Main → Garden → Signature Flavor → Finish — sıra atlanamaz (v2.1, bkz. `20260718001123_customizer_5_adim_gecisi.md`) |
| Özet panel her zaman görünür | Masaüstünde sabit yan panel, mobilde sticky çekmece — asla gizlenmez |
| Animasyon estetiği paletle tutarlı | Yumuşak/organik easing — sert/mekanik animasyon yasak |
| Görsel önizleme CSS/SVG katmanlı | MVP'de gerçek fotoğraf kompozisyonu yok — ileride server-side image composition'a geçilebilir |
| API key sadece server-side | Route Handler / env üzerinden — istemci koduna asla gömülmez |
| Üçüncü parti entegrasyonlar ayrı faz | Adisyo/SepetTakip, WhatsApp, QR menü gerçek API anahtarı/iş ortaklığı gerektirir — ilk lansmandan sonra |
| Faz geçişi kabul kriteri zorunlu | Kabul kriteri karşılanmadan sonraki oturuma geçilmez (ROADMAP.md) |

---

## 9. MUTLAK YASAKLAR

> Detaylar AGENT.md'de — burada sadece bu projeye özgü kritikler:

| ❌ Asla yapma |
|---|
| Kalori bilgisini MenuCard/customizer/sepetten gizle veya opsiyonel yap |
| Logo degrade'ini site arka planında veya büyük yüzeylerde kullan |
| Bronze rengini küçük gövde metninde kullan |
| `prefers-reduced-motion` kontrolü olmadan animasyon ekle |
| `width`/`height`/`top` gibi layout tetikleyen özelliği animasyonlu bırak |
| API key / secret'ı client-side kodda, repo'da veya logda bırak |
| Customizer adım sırasını kullanıcı onayı olmadan değiştir |
| Onaysız birden fazla modülü aynı anda değiştir |
| Context eksikken HIGH confidence ver |
| Truncated dosya ver |
| Herhangi bir arşiv parçasını (session_arşiv.md, _1, _2, ...) TAM DOSYA olarak ver — SADECE 400 satır eşiğinde taşınan yeni blok verilir, dosyanın kendisi asla yeniden üretilmez |
| Arşiv parçalaması yapıp CORE.md'nin Dosya Haritası/Versiyon Geçmişini aynı turda güncellemeden geç |
| Üçüncü parti entegrasyonu (WhatsApp/Adisyo/QR) gerçek anahtar/test olmadan "tamamlandı" say |
| Tactile animasyon (kart/CTA lift, zoom vb.) SADECE `whileHover` ile tanımla, dokunma (`whileTap`) karşılığı bırakma — Bowlera trafiği neredeyse tamamen dokunmatik (BOWLERA_MOTION_SYSTEM_RAPORU.md §1a) |

---

## 10. SAĞLIK KONTROL LİSTESİ

Her session açılışında kontrol et, sonucu kullanıcıya söyle:

| # | Kontrol | Nasıl Kontrol Edilir |
|---|---|---|
| 1 | Açık 🔴 kritik sorun var mı? | SESSION_INDEX.md → Açık Sorunlar |
| 2 | Son deploy başarılı mı? | Kullanıcıya sor |
| 3 | Yarım kalan entegrasyon var mı? (WhatsApp/Adisyo/QR) | SESSION_INDEX.md → Açık Sorunlar |
| 4 | Son SESSION_INDEX güncellemesi push edildi mi? | Kullanıcıya sor |
| 5 | TEST_MATRIX.md'de ❓ kritik test var mı? | TEST_MATRIX.md → kritik bileşenler |
| 6 | Açık oturum/faz görevi var mı? | ROADMAP.md → aktif oturum |
| 7 | Core Web Vitals hedefleri karşılanıyor mu? (LCP<2.5s, CLS<0.1) | SESSION_INDEX.md veya kullanıcıya sor |
| 8 | Kalori/alerjen verisi eksik ürün var mı? | menu-data.json veya kullanıcıya sor |
| 9 | Arşiv parçalarının SESSION_INDEX üst notu ile CORE.md Dosya Haritası senkron mu? | SESSION_INDEX üst notu ↔ CORE.md Bölüm 4 karşılaştır |

**Format:**
> "Sağlık: ⚠️ [kaç sorun] açık — [kısa liste]. Devam edelim mi?"

Sorun yoksa:
> "Sağlık: ✅ Temiz. Sıradaki görev: [liste]. Nereden başlayalım?"

---

## 11. RE-INJECTION PROTOKOLÜ

Her 20 mesajda bir Claude otomatik şunu söyler:

> "⚠️ Re-injection noktası — Bu sohbet 20 mesaja ulaştı.
> Context hakimiyeti zayıflayabilir. Yeni sohbete geçmemi öneririm.
> Hazır paket sunayım mı?"

**Kullanıcı "Evet" derse — Claude şunu üretir:**
```
## YENİ SOHBET PAKETİ

### Bu sohbette yapılanlar:
[Tamamlanan görevler — madde madde]

### Alınan teknik/tasarım kararları:
[Kararlar ve gerekçeleri]

### Sıradaki görev:
[Tam olarak nerede kaldık]

### Yeni sohbete yapıştır:
CORE.md + AGENT.md + SESSION_INDEX.md (güncel) + bu özet
```

**Kullanıcı "Hayır" derse:**
Devam edilir. Bir sonraki 20 mesajda tekrar sorulur.

**Manuel tetikleme:**
Kullanıcı istediği zaman "Re-injection" veya "Yeni sohbet" diyebilir.
Claude hemen paketi hazırlar.

---

*BOWLERA — Bu dosya yaşayan bir referanstır. Her mimari/tasarım kararı SESSION_INDEX.md'ye,
her büyük değişiklik DEPENDENCIES.md'ye yansıtılmalıdır.*
*v1.1 — §7.1 Adım 1'e SESSION_INDEX arşiv koruma netleştirmesi eklendi (Session 4 — 2026-07-19,
AGENT.md v1.1 ile eşleştirildi).*
*v1.2 — §7.1 Adım 1'e "400 satır eşiği" kuralı eklendi: SESSION_INDEX.md 400 satırı geçince
sıkıştırılamaz, gerekçeli olarak session_log.md'ye taşınır. Gerekçe: 2026-07-20'de yaşanan
gerekçesiz madde kaybı (7 açık sorun + 2 karar) — AGENT.md v1.2 ile eşleştirildi (2026-07-21).*
*v1.3 — `session_log.md` ismi ve "her session kapanışında ayrı anlatı bloğu yaz" mekanizması
(eski §7.1 Adım 2 + §7.2'deki session_log referansı) TAMAMEN KALDIRILDI — isim ve çift-mekanizma
karışıklığı yarattığı kullanıcı tarafından tespit edildi (2026-08-07). Yerine `session_arşiv.md`
getirildi: TEK işlevi, SESSION_INDEX.md 400 satırı geçtiğinde kapanmış içeriği taşımak — amaç
SESSION_INDEX'in (aktif hafızanın) boyutunu küçük tutup sistemin hafif çalışmasını sağlamak.
"session_arşiv.md asla tam dosya olarak yeniden üretilmez, sadece yeni taşıma bloğu verilir"
güvenlik kuralı DEĞİŞMEDİ, sadece tek mekanizmaya indirgendi. AGENT.md v1.4 ile eşleştirildi.*
*v1.4 — Arşivin KENDİSİNİN de hacimce yönetilemez hale gelince parçalara ayrılabileceği
(session_arşiv.md → session_arşiv_1.md → session_arşiv_2.md → ...) resmen tanımlandı. Bu,
SESSION_INDEX'in 400 satır eşiğinden (Bölüm 7.1 Adım 1.1-1.6) AYRI, BAĞIMSIZ bir tetikleyicidir
(Adım 1.7). Bölüm 1 (Session Açılış), Bölüm 3 (Tetikleyici Tablosu), Bölüm 4 (Dosya Haritası),
Bölüm 9 (Mutlak Yasaklar) ve Bölüm 10 (Sağlık Kontrol Listesi, yeni madde 9) buna göre
güncellendi. Gerekçe: 2026-08-08 ve 2026-08-11'de fiilen `session_arşiv_1.md` ve
`session_arşiv_2.md` açılmıştı, kullanıcı tarafından onaylanmıştı, ama bu değişiklik hiçbir
zaman CORE.md'ye işlenmemişti — SESSION_INDEX.md ile CORE.md arasında senkron kopukluğu
oluşmuştu (kullanıcı tarafından fark edildi, 2026-08-12). Kural artık açık: bir arşiv parçası
açıldığı ANDA, aynı turda CORE.md güncellenir — aksi halde Self-Correction tetiklenir (bkz.
AGENT.md SELF-CORRECTION, "Arşiv parçalandı ama CORE.md güncellenmedi" satırı). AGENT.md v1.5
ile eşleştirildi.*
*v1.5 — Bölüm 3 (Tetikleyici Tablosu) ve Bölüm 4 (Dosya Haritası) güncellendi: yeni
`SANDWICH_SPEC.md` referansı eklendi — "Sandviçini Oluştur" akışının izole kontratı
(Seçenek A, bowl akışına dokunmaz). Gerekçe: yeni bir çekirdek referans dosyası eklenince
CORE.md'nin aynı turda güncellenmesi kuralı (arşiv parçalama dersinden genellenen prensip,
bkz. v1.4 notu) — kullanıcı talebiyle uygulandı (2026-08-23). SANDWICH_SPEC.md'nin 6 açık
sorusu (S1-S6) netleşmeden kod üretimine geçilemeyeceği not edildi. AGENT.md'ye HENÜZ
işlenmedi — sadece CORE.md tarafı bu turda güncellendi.*
*v1.6 — Bölüm 4'teki SANDWICH_SPEC.md referansı v1.0→v1.1'e güncellendi (adım sırası
düzeltmesi: Bread→Size→Protein→Cheese→Veggies→Sauce&Toast&Extras, kullanıcı onayı
2026-08-23). Küçük senkron güncellemesi — Bölüm 3 (Tetikleyici Tablosu) değişmedi.
⚠️ SELF-CORRECTION notu: v1.5 girdisi bu footer'a kronolojik sıranın DIŞINDA (v1.1'den
ÖNCE) eklenmişti — bu turda düzeltildi, doğru sıraya (v1.4'ten SONRA) taşındı. İçerik
kaybı yok, sadece sıralama hatası giderildi.*
*v1.7 — Bölüm 3 (Tetikleyici Tablosu) ve Bölüm 4 (Dosya Haritası) güncellendi: yeni
`BOWLERA_MOTION_SYSTEM_RAPORU.md` referansı (v1.1) + `lib/motion/tokens.ts` + `MenuCardImage.tsx`
eklendi. Bölüm 9 (Mutlak Yasaklar)'a "tactile animasyon sadece whileHover, dokunma karşılığı yok"
maddesi eklendi — gerekçe: MenuCard P0-2'de rapor v1.0'ın tamamen hover-merkezli yazılmış olması,
Bowlera trafiğinin neredeyse tamamen dokunmatik olmasına rağmen, canlıda kritik bir eksiklik
olarak tespit edildi (whileTap="hover" + springs.cardRelease ile düzeltildi, rapor v1.1'e işlendi).
Bu, yeni bir çekirdek referans dosyası eklenince CORE.md'nin aynı turda güncellenmesi kuralının
(bkz. v1.4/v1.5 notları) bir tekrarı. AGENT.md v1.6 ile eşleştirildi (2026-09-03).*
*v1.8 — Bölüm 3 (Tetikleyici Tablosu) ve Bölüm 4 (Dosya Haritası) güncellendi: yeni
`RISK_DOMAINS.md` referansı eklendi — FAILURE_PATTERNS.md'nin geçmişe bakan (olay oldu →
kaydedildi) mantığını tamamlayan, geleceğe bakan (bu alana dokunuyorsan → şu kontrol zorunlu)
bir dosya: secret/gizli veri, fiyat/ödeme mantığı, eşzamanlılık, KVKK kapsamlı veri. Gerekçe:
"hatayı ancak fark edildikten sonra kural haline getirme" döngüsünün, kullanıcı/geliştirici
tarafından fark edilmesi zor olan ("sessiz") hata sınıflarında yetersiz kalacağı tespit edildi —
bu sınıflar için önleyici, araç-tabanlı kontrol (AI'ın hatırlamasına değil) zorunlu kılındı. Yeni
bir çekirdek referans dosyası eklenince CORE.md'nin aynı turda güncellenmesi kuralının (bkz.
v1.4/v1.5/v1.7 notları) bir tekrarı. AGENT.md v1.7 ile eşleştirildi (2026-09-22).*
*v1.9 — Bölüm 4 (Dosya Haritası) güncellendi: `session_arşiv_2.md` (2201 satır / 188K)
hacimce yönetilemez hale geldiği için CORE.md §4 tetikleyici (B) tetiklendi, yeni
`session_arşiv_3.md` açıldı ve AKTİF parça olarak işaretlendi. Bölünme noktası: 2026-09-01
(27. sohbet, #118 Adım 3 turu) kapanışı — bu tarihe kadarki bloklar `session_arşiv_2.md`'de
kaldı, 2026-09-03'ten (23. sohbet devamı) itibaren taşınan bloklar `session_arşiv_3.md`'ye
geçti. **Ayrıca:** `session_arşiv_2.md` içinde "TAŞIMA BLOĞU — 2026-09-01 (5. taşıma)"dan
"TAŞIMA BLOĞU 6"ya kadar olan ~127 satırlık blok (SESSION ÖZET tablosu + Kritik Kararlar
Session 1-2 + Açık Sorunlar #107/#108, #101-104, #112-114, #39/#50) dosyada YANLIŞLIKLA
İKİ KEZ bulunduğu tespit edildi (muhtemelen bir eklenti yapıştırılırken tekrarlanmış);
birebir aynı olan ikinci kopya silindi — bu bir "sıkıştırma" değil, saf kopya temizliğidir,
kalan tek kopyada içerik kaybı YOKTUR. Gerekçe: kullanıcı arşivin hacmini küçültme yolu sordu
(2026-09-27, 37. sohbet) — CORE.md §4'ün zaten tanımladığı tetikleyici (B) mekanizması bu
turda fiilen uygulandı. **KALAN:** SESSION_INDEX.md'nin üst notu, yeni AKTİF parçanın
`session_arşiv_3.md` olduğunu yansıtacak şekilde AYRICA güncellenmeli (bu teslimatın
kapsamı dışında bırakıldı, kullanıcı isterse ayrıca üretilir).*
