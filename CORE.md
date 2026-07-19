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

2.  session_log.md'yi ASLA otomatik isteme
    → Sadece kullanıcı geçmişe bakmak isterse veya
      ilgili session numarasını belirtince o bloğu iste

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
| Sepet (cart) / Zustand store | `ARCHITECTURE.md §Veri Modeli` + `CUSTOMIZER_SPEC.md` | `FAILURE_PATTERNS.md` |
| Renk / tipografi / animasyon kararı | `DESIGN_SYSTEM.md` | — |
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
| Bug fix | `session_log.md` ilgili blok | `FAILURE_PATTERNS.md` |
| Rollback / deploy geri alma | `ARCHITECTURE.md §Deploy` | `session_log.md` |
| Test / doğrulama / çalışıyor mu | `TEST_MATRIX.md` | — |
| Yol haritası / önceliklendirme / faz durumu | `ROADMAP.md` | — |
| Hangi dosya neyi etkiler | `DEPENDENCIES.md` | — |
| Session log yazma | Sadece bu session'ın bloğu | — |

---

## 4. DOSYA HARİTASI

```
── ÇEKİRDEK (Her session başında verilir) ────────────────
CORE.md                    ← Sen buradasın
AGENT.md                   ← Ajan davranış kuralları
SESSION_INDEX.md           ← Anlık durum pusulası
session_log.md             ← Tam geçmiş (sadece gerekince istenir)

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

DESIGN_SYSTEM.md           ← Renk kullanım tablosu (WCAG), logo degrade kuralı,
                             tipografi, ikonografi, fotoğraf direktifi, animasyon sistemi

CONTENT_GUIDE.md           ← Marka sesi, örnek metinler, SEO anahtar kelimeler,
                             JSON-LD şema kalıbı

INTEGRATIONS.md            ← Adisyo/SepetTakip, WhatsApp köprüsü, QR menü,
                             SMS/e-posta bildirimi kontratları

── TAKİP ─────────────────────────────────────────────────
FAILURE_PATTERNS.md        ← Projeye özgü hata kalıpları: sepet state kaybı,
                             checkout race condition, üçüncü parti entegrasyon
                             kopması, mobil responsive bugları

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
│   ├── MenuCard.tsx          ← kalori ZORUNLU alan olarak render edilir
│   ├── FilterPanel.tsx
│   └── CategoryNav.tsx       ← sticky
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
- Session log haritasına yeni satır ekle
- **TAM DOSYA olarak ver**
- ⚠️ "Şişmeyi önle" kuralı SADECE tamamlanmış/güncel-olmayan görev satırlarının silinmesini
  kapsar. Geçmiş oturumların **arşiv blokları** (📜 GEÇMİŞ / ARŞİV başlıklı bölümler) TAM
  içerikle korunur — özetlenip "önceki versiyona bakılmalı" gibi bir referansla DEĞİŞTİRİLMEZ.
  Bu, AGENT.md Kural #4'ün (Truncated çıktı yasak) doğrudan bir uzantısıdır.

**Adım 2 — session_log.md**
- Yapılanlar + Kararlar (neden alındı) + Teknik notlar
- **SADECE YENİ BLOK ver** — kullanıcı session_log.md'ye kendisi ekler

**Adım 3 — TEST_MATRIX.md**
- Bu session'da dokunulan bileşen/modül var mı?
- Varsa ilgili satırları güncelle: ❓ → ✅ veya ❌
- **TAM DOSYA olarak ver**

**Adım 4 — DEPENDENCIES.md**
- Yeni dosya/bileşen eklendi mi? Yeni bağımlılık oluştu mu?
- Değiştiyse **TAM DOSYA olarak ver**

**Adım 5 — ROADMAP.md**
- Bu session bir oturum/görev tamamladı mı?
- Tamamlandıysa checkbox işaretle, kabul kriteri güncelle
- Değiştiyse **TAM DOSYA olarak ver**

**Adım 6 — Kullanıcı Onayı**
- "Bu dosyaları onaylıyor musun?" diye sor
- "Evet" gelmeden session kapanmaz
- "Hayır" gelirse ilgili dosyayı düzelt, tekrar sun

---

### 7.2 — Checkpoint Protokolü (Ani Kesinti Koruması)

> Uzun sohbet aniden kesilebilir.
> Her büyük görev tamamlandığında — session bitmeden — checkpoint al.

**Ajan her büyük görev sonrası otomatik sorar:**
> "Checkpoint alayım mı? (Evet → SESSION_INDEX + session_log + TEST_MATRIX güncellenir)"

**Kullanıcı "Evet" derse:**
- SESSION_INDEX.md, session_log (yeni blok), TEST_MATRIX.md güncellenir
- TAM DOSYA olarak verilir
- Kullanıcı kopyalar — kesinti olsa bile buradan devam edilir

**Kullanıcı "Hayır" derse:**
- Devam edilir — bir sonraki görev sonrası tekrar sorulur

---

### 7.3 — Log Tetikleyicileri

Aşağıdakilerden biri gerçekleşince log + SESSION_INDEX + checkpoint ZORUNLU:

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
2. Session log'a `🗄️` sembolü + dosya adı yazılır
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
| session_log.md'yi TAM DOSYA olarak ver — SADECE YENİ BLOK |
| Üçüncü parti entegrasyonu (WhatsApp/Adisyo/QR) gerçek anahtar/test olmadan "tamamlandı" say |

---

## 10. SAĞLIK KONTROL LİSTESİ

Her session açılışında kontrol et, sonucu kullanıcıya söyle:

| # | Kontrol | Nasıl Kontrol Edilir |
|---|---|---|
| 1 | Açık 🔴 kritik sorun var mı? | SESSION_INDEX.md → Açık Sorunlar |
| 2 | Son deploy başarılı mı? | Kullanıcıya sor |
| 3 | Yarım kalan entegrasyon var mı? (WhatsApp/Adisyo/QR) | SESSION_INDEX.md → Açık Sorunlar |
| 4 | Son session log push edildi mi? | Kullanıcıya sor |
| 5 | TEST_MATRIX.md'de ❓ kritik test var mı? | TEST_MATRIX.md → kritik bileşenler |
| 6 | Açık oturum/faz görevi var mı? | ROADMAP.md → aktif oturum |
| 7 | Core Web Vitals hedefleri karşılanıyor mu? (LCP<2.5s, CLS<0.1) | SESSION_INDEX.md veya kullanıcıya sor |
| 8 | Kalori/alerjen verisi eksik ürün var mı? | menu-data.json veya kullanıcıya sor |

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
