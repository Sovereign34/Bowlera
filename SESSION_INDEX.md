# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## ⚠️ BU GÜNCELLEME HAKKINDA NOT

Bu güncelleme, önceki bir sohbette üretildiği bildirilen `CategoryNav.tsx` /
`FilterPanel.tsx` kodunun **bu oturumda yeniden görülmeden**, kullanıcının
sağladığı 7 ekran görüntüsüne dayanarak yapılmıştır. Ekran görüntüleri şunları
doğruluyor: (1) `npm test` çıktısı — 8 test dosyası / 34 test, tümü ✅; (2)
Vercel canlı ortamda 4 kategori sekmesi (İmza Kaseler, Sıcak Tahıl Kaseleri,
Vegan, İçecekler) arasında geçiş; (3) Alerjen + Diyet&Kalori filtre paneli
render oluyor; (4) "Sonuç yok" boş durum mesajı çalışıyor. Kodun kendisi
(dosya içerikleri) bu sohbette incelenmedi — sadece çalışan sonuç görsel
olarak doğrulandı.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 2 TAMAMLANDI. MenuCard bileşen ailesi + app/menu/page.tsx +
          CategoryNav.tsx + FilterPanel.tsx üretildi, test edildi (34/34 ✅,
          8 test dosyası) VE Vercel'de GÖRSEL OLARAK doğrulandı — kategori
          sekmeleri (İmza/Sıcak Tahıl/Vegan/İçecekler), alerjen+diyet filtre
          paneli ve "Sonuç yok" boş durum mesajı canlıda çalışıyor.
Faz:      Oturum 2 — Menü sayfası, filtreleme, MenuCard, statik menü verisi.
          TAMAMLANDI. Bir sonraki oturum Oturum 3 (Zustand store + 5 adımlı
          BowlCustomizer) ile başlayabilir.
Gerekçe:  MenuCard container hatası düzeltildi → npm peer-dependency çakışması
          çözüldü → app/menu/page.tsx yazıldı → Vercel build hatası (tsconfig)
          çözüldü → CategoryNav.tsx + FilterPanel.tsx + lib/menu-filters.ts
          üretildi → 34/34 test geçti → Vercel'de 4 kategori sekmesi ve
          filtre paneli görsel olarak doğrulandı (boş durum dahil).
Çıktı:    Repo: github.com/Sovereign34/Bowlera_site (main dalı). Deploy:
          Vercel — /menu sayfası kategori nav + filtre paneliyle birlikte
          canlı ve doğrulanmış. "Kâseni Yarat" 5-adım mimari kararı bir
          önceki oturumda kanon dosyalara işlendi, kodu henüz Oturum 3'te
          yazılacak.
```

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI

| # | Karar | Tarih | Kaynak/Gerekçe |
|---|---|---|---|
| 1 | "Kâseni Yarat" akışı 4 adımdan **5 adıma** çıkarıldı: Base → Main → Garden → Signature Flavor → Finish | Oturum 2 — 2026-07-18 | Kullanıcı önerisi ("şefin düşünme sırası"). Şema değişiklik notu: `20260718001123_customizer_5_adim_gecisi.md` |
| 2 | Adım/malzeme isimleri **tamamen İngilizce** — CONTENT_GUIDE.md §1 Türkçe marka sesi kuralına bilinçli istisna, yalnızca customizer'ı kapsar | Oturum 2 — 2026-07-18 | Premium/global algı kararı, kullanıcı onaylı |
| 3 | Garden: ilk 4 seçim ücretsiz, Avokado miktarı fark etmeksizin **her zaman ücretli** | Oturum 2 — 2026-07-18 | Toppings kuralıyla tutarlılık, kullanıcı onaylı |
| 4 | Finish: ilk 1 seçim ücretsiz, sonrası ücretli | Oturum 2 — 2026-07-18 | Kullanıcı seçimi |
| 5 | "Make it Yours" ayrı adım değil, Finish adımına entegre alt-bileşen; "Double Main" mevcut `mainPortion` mekanizmasını yeniden kullanır | Oturum 2 — 2026-07-18 | Kullanıcı seçimi + AGENT.md Kural #5 |

> Etkilenen dosyalar: `CORE.md` §8, `MASTER_PLAN.md` v2.1, `CUSTOMIZER_SPEC.md` v1.1.
> Henüz etkilenmeyen (Oturum 3'te işlenecek): `store/useCustomizerStore.ts`,
> `types/index.ts`, `lib/menu-data.json`, `ARCHITECTURE.md` §2.4, `DEPENDENCIES.md`.

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 2 — 2026-07-18 |
| Son Eylem | CategoryNav.tsx + FilterPanel.tsx + lib/menu-filters.ts üretildi, 34/34 test geçti, Vercel'de kategori sekmeleri/filtre paneli/boş durum görsel olarak doğrulandı |
| Blocker | Yok |
| Devam Noktası | Yeni sohbette CORE.md + AGENT.md + bu SESSION_INDEX ile doğrudan **Oturum 3**'e (Zustand store + 5 adımlı BowlCustomizer, kontrat `CUSTOMIZER_SPEC.md` v1.1 hazır) başlanabilir. Alternatif: Açık Sorun #5, #6, #7, #10'daki küçük temizlik görevleri önce kapatılabilir. |

---

## GENEL DURUM

| Alan | Değer |
|---|---|
| Proje | Bowlera — Healthy Bowls |
| Aktif Oturum | Oturum 2 tamamlandı |
| Toplam Session | 2 |
| Sistem Durumu | 🟢 Test altyapısı sağlıklı (34/34, 8 test dosyası), build sağlıklı, `/menu` + kategori/filtre canlı |
| Deploy Durumu | ✅ Vercel — `/menu` sayfası, kategori nav (4 sekme) ve filtre paneli görsel olarak doğrulandı |
| Repo | `github.com/Sovereign34/Bowlera_site` |
| Codespace | Aktif (workspace adı: Bowlera_si...) |
| Menü Veri Kaynağı | ✅ `lib/menu-data.json` — İmza Kaseler, Sıcak Tahıl Kaseleri, Vegan, İçecekler kategorilerinde ürünler canlıda doğru render oluyor |
| Veri Modeli | ✅ `types/index.ts` — `BowlItem`/`CartItem`. ⬜ `CustomizerSelection` tipi henüz kodda yok (Oturum 3) |
| MenuCard Bileşen Ailesi | ✅ Üretildi, test edildi, canlıda görsel doğrulandı |
| Menü Sayfası (`app/menu/page.tsx`) | ✅ Üretildi, test edildi, canlıda görsel doğrulandı |
| Kategori/Filtre UI | ✅ `CategoryNav.tsx`, `FilterPanel.tsx` üretildi, test edildi (8 test), canlıda 4 sekme + alerjen/diyet filtreleri + boş durum mesajı doğrulandı |
| Görsel/Fotoğraf İçeriği | ⬜ Hâlâ bekleniyor — hem Hero'da hem MenuCard'larda placeholder/kırık ikon |
| Customizer Kontratı | ✅ v1.1 — 5 adıma güncellendi (kod henüz yazılmadı, Oturum 3 kapsamında) |
| Üçüncü Parti Anahtarları | ⬜ Adisyo/SepetTakip, WhatsApp, Twilio — henüz temin edilmedi, ayrı faz |

---

## AÇIK SORUNLAR

| # | Öncelik | Açıklama | Oturum | Referans |
|---|---|---|---|---|
| 4 | 🟡 | Üçüncü parti API anahtarları temin edilmedi | Sonraki Faz | MASTER_PLAN §8 |
| 5 | 🟢 | ARCHITECTURE.md §2.4 `calculateTotals`/`getTotals` isim tutarsızlığı — düzeltme bekliyor | Oturum 0 | DEPENDENCIES.md §1 |
| 6 | 🟢 | `next-env.d.ts` (Oturum 1'den kalan) hâlâ untracked görünüyor, commit edilmemiş | Oturum 1 | — |
| 7 | 🟡 | **Allergen gösterimi DESIGN_SYSTEM.md onayı bekliyor.** `MenuCard.tsx`'e geçici bir satırla eklendi ve canlıda görsel olarak çalıştığı doğrulandı ("İçerir: Kuruyemiş" gibi satırlar görünüyor), ama DESIGN_SYSTEM.md'de tanımlı resmi bir stil/bileşen olup olmadığı hâlâ teyit edilmedi. | Oturum 2 | DESIGN_SYSTEM.md §2 (doğrulanmadı) |
| 9 | 🟢 | `vitest.config.ts`'deki `@vitejs/plugin-react` ile Next.js'in kendi `vite` sürümü arasındaki TS tip çakışması `tsconfig.json` exclude ile çözüldü. Kalıcı workaround, ileride tekrar kontrol edilmeli. | Oturum 2 | — |
| 10 | 🟡 | `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md`, customizer'ın 5 adıma çıkması nedeniyle güncel değil | Oturum 2 | `20260718001123_customizer_5_adim_gecisi.md` |

> Kapatılan sorunlar: #1 (görsel doğrulama), #2 (deploy platformu), #3 (menü verisi artık var),
> #8 (vitest.config.ts commit+push+build doğrulandı).
> **Bu oturumda kapatılan:** Sıradaki Görevler #1 (CategoryNav.tsx), #2 (FilterPanel.tsx),
> #3 (deploy + görsel doğrulama) — üçü de tamamlandı ve doğrulandı, aşağıya taşındı.

---

## BOWLERA OTURUM DURUMU

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (14 dosya) | ✅ Üretildi — son onay bekliyor |
| **Oturum 1** | Next.js+Tailwind, font/renk, Header/Footer, Hero | ✅ Tamamlandı — görsel doğrulama yapıldı |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard, statik menü verisi | ✅ **Tamamlandı** — MenuCard, page.tsx, CategoryNav, FilterPanel hepsi üretildi, test edildi (34/34) ve canlıda görsel doğrulandı; customizer 5 adım kararı bu oturumda alındı |
| **Oturum 3** | Zustand store + BowlCustomizer (**5 adım** — v2.1, masaüstü) | ⬜ Sırada — kontrat hazır (`CUSTOMIZER_SPEC.md` v1.1) |
| **Oturum 4** | VisualPreview, mobil özelleştirici, sepet | ⬜ Bekliyor |
| **Kontrol Noktası** | Kullanıcı testi (5-10 kişi) | ⬜ Bekliyor |
| **Oturum 5** | Hakkımızda, Şubeler, İletişim, SEO, son kontrol | ⬜ Bekliyor |

---

## ÜRETİLEN KOD DOSYALARI

| Dosya | Durum | Test | Repo | Deploy |
|---|---|---|---|---|
| `app/layout.tsx`, `app/page.tsx`, `app/globals.css` | ✅ | — | ✅ Push | ✅ Doğrulandı |
| `tailwind.config.ts`, `lib/fonts.ts` | ✅ | — | ✅ Push | ✅ Doğrulandı |
| `components/layout/Header.tsx` | ✅ | ✅ 3 test | ✅ Push | ✅ Doğrulandı |
| `components/layout/Footer.tsx` | ✅ | ✅ 3 test | ✅ Push | ✅ Doğrulandı |
| `components/home/Hero.tsx` + alt bileşenler | ✅ | ✅ 3 test | ✅ Push | ✅ Doğrulandı |
| `public/images/logo-bowlera.png` | ✅ | — | ✅ Push | ✅ Doğrulandı |
| `types/index.ts` (BowlItem/CartItem) | ✅ | — | ✅ Push | ✅ (dolaylı) |
| `lib/menu-data.json` | ✅ | — | ✅ Push | ✅ Doğrulandı |
| `components/menu/MenuCardImage.tsx` | ✅ | ✅ dahil | ✅ Push | ✅ Doğrulandı |
| `components/menu/MenuCardBadges.tsx` | ✅ | ✅ dahil | ✅ Push | ✅ Doğrulandı |
| `components/menu/MenuCardInfo.tsx` | ✅ | ✅ dahil | ✅ Push | ✅ Doğrulandı |
| `components/menu/MenuCard.tsx` | ✅ | ✅ 4 test | ✅ Push | ✅ Doğrulandı |
| `vitest.config.ts` | ✅ | — | ✅ Push | ✅ (build kırmadığı doğrulandı) |
| `tsconfig.json` (exclude fix) | ✅ | — | ✅ Push | ✅ Build başarılı |
| `app/menu/page.tsx` | ✅ | ✅ 2 test | ✅ Push | ✅ Doğrulandı |
| `lib/menu-filters.ts` | ✅ | ✅ 11 test | ✅ Push (varsayım) | ✅ Doğrulandı (test terminalinde görüldü) |
| `components/menu/CategoryNav.tsx` | ✅ | ✅ 4 test | ✅ Push (varsayım) | ✅ Doğrulandı (4 sekme canlıda çalışıyor) |
| `components/menu/FilterPanel.tsx` | ✅ | ✅ 4 test | ✅ Push (varsayım) | ✅ Doğrulandı (alerjen+diyet filtreleri ve boş durum çalışıyor) |
| `store/useCustomizerStore.ts` | ⬜ Henüz yazılmadı (Oturum 3, kontrat v1.1 hazır) | — | — | — |

> Not: `lib/menu-filters.ts`, `CategoryNav.tsx`, `FilterPanel.tsx` için "Repo: Push"
> durumu bu oturumda git log/GitHub üzerinden teyit edilmedi — sadece test terminali
> ve Vercel canlı ortamı görüldü (Vercel'in güncel olması dolaylı olarak push'un
> yapıldığını gösteriyor). Kesin teyit için sonraki oturumda `git log --oneline -5`
> istenmesi önerilir.

---

## SIRADAKİ GÖREVLER

| Sıra | Görev | Öncelik | Durum |
|---|---|---|---|
| 1 | Allergen gösterim satırını DESIGN_SYSTEM.md ile teyit et (Açık Sorun #7) | 🟡 | ⬜ |
| 2 | `next-env.d.ts` commit teyidi (Açık Sorun #6) | 🟢 | ⬜ |
| 3 | ARCHITECTURE.md §2.4 isim düzeltmesi (Açık Sorun #5) | 🟢 | ⬜ |
| 4 | `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md`'yi 5 adımlı customizer kontratıyla senkronize et (Açık Sorun #10) | 🟡 | ⬜ |
| 5 | **Oturum 3'ü başlat** — `store/useCustomizerStore.ts` + `types/index.ts`'e `CustomizerSelection` eklenmesi (kontrat: `CUSTOMIZER_SPEC.md` v1.1) | 🔴 | ⬜ |
| 6 | (Opsiyonel, düşük öncelik) `git log` ile CategoryNav/FilterPanel push'unun kesin teyidi | 🟢 | ⬜ |

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 2 Detaylı Kayıt

### CategoryNav.tsx + FilterPanel.tsx — Üretim ve Doğrulama (bu oturumun üçüncü bölümü)
- `lib/menu-filters.ts` (kategori/alerjen/diyet config + saf filtre fonksiyonları),
  `CategoryNav.tsx` (sticky kategori sekmeleri) ve `FilterPanel.tsx` (alerjen +
  diyet&kalori checkbox grupları) üretildi.
- `npm test` çalıştırıldı: 8 test dosyası, 34 test — tamamı ✅ (`menu-filters.test.ts`
  11, `FilterPanel.test.tsx` 4, `CategoryNav.test.tsx` 4, `MenuCard.test.tsx` 4,
  `Hero.test.tsx` 3, `Footer.test.tsx` 3, `Header.test.tsx` 3, `page.test.tsx` 2).
- Vercel'de görsel doğrulama yapıldı: İmza Kaseler / Sıcak Tahıl Kaseleri / Vegan /
  İçecekler sekmeleri arasında geçiş çalışıyor, her sekmede doğru ürünler ve
  etiketler (vegan, glutensiz, düşük kalori, yüksek protein, "İçerir: X") render
  oluyor. Alerjen ve Diyet&Kalori filtre paneli checkbox'ları görünüyor. Filtre
  kombinasyonu sonuç döndürmediğinde "Bu filtrelerle eşleşen ürün yok — filtreleri
  temizlemeyi dene." boş durum mesajı doğru şekilde tetikleniyor.
- Bu üretim ve doğrulama farklı bir sohbette/oturumda gerçekleşti; bu SESSION_INDEX
  güncellemesi kullanıcının sağladığı ekran görüntülerine dayanarak yapıldı, kod
  dosyalarının kendisi bu güncelleme sırasında incelenmedi.

### Customizer 4→5 Adım Geçişi
- Kullanıcı, kategori/filtre çalışmasına başlamadan önce marka anlayışının
  netleşmediğini belirtti ve "Kâseni Yarat" akışı için 5 adımlı, gurme
  mutfak mantığına dayalı bir öneri getirdi (Base/Main/Garden/Signature
  Flavor/Finish + "Make it Yours" ek seçenekleri).
- 3 turlu netleştirme yapıldı: (1) adım sayısı → 5 adıma geçildi, (2) dil →
  tamamen İngilizce, (3) resmi şema değişikliği mi / sadece konsept mi →
  resmi değişiklik. Şema değişiklik notu (`20260718001123_customizer_5_adim_gecisi.md`)
  üretildi. `CORE.md` §8, `MASTER_PLAN.md` (v2.0→v2.1), `CUSTOMIZER_SPEC.md`
  (v1.0→v1.1) tam dosya olarak güncellendi.
- `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md` bu kararı henüz yansıtmıyor —
  Açık Sorun #10 olarak kayıtlı.

### MenuCard Container Hatası ve Düzeltmesi
- `components/menu/MenuCard.tsx` dosyasının içeriğinin yanlışlıkla
  `MenuCardImage.tsx`'in birebir kopyası olduğu tespit edildi, gerçek container
  yazılıp düzeltildi. `allergens` alanının hiçbir alt bileşende render edilmediği
  bulundu ve geçici bir satırla kapatıldı (Açık Sorun #7).

### Test Altyapısı — npm Peer-Dependency Çakışması
- İlk `npm test` denemesinde `ReferenceError: React is not defined` hatası —
  `vitest.config.ts`'de `@vitejs/plugin-react` tanımlı değildi. Versiyon
  belirtmeden kurulum npm'in vite@^8 çekmesine ve mevcut vite@^5 ile çakışmasına
  yol açtı. Temiz kurulum + `@vitejs/plugin-react@^4.3.0` sabit sürümle çözüldü.

### Vercel Build Hatası — tsconfig/vitest Tip Çakışması
- `next build`'in tip kontrolü `vitest.config.ts:6:13`'te çöktü — iki farklı
  `vite` paketi arasında `Plugin`/`PluginOption` tip uyuşmazlığı. `tsconfig.json`
  exclude listesine `vitest.config.ts`, `vitest.setup.ts`, `**/*.test.tsx`,
  `**/*.test.ts` eklenerek çözüldü (Açık Sorun #9, kalıcı workaround).

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 0 Detaylı Kayıt

### Çekirdek Üçlü (Session 1)
- **CORE.md** — 11 bölüm: session açılış protokolü, proje kimliği, tetikleyici tablosu,
  dosya haritası, context kuralı, session kapanış protokolü, checkpoint protokolü, log
  tetikleyicileri, veri şeması değişiklik protokolü, mimari varsayımlar, mutlak yasaklar,
  sağlık kontrol listesi, re-injection protokolü.
- **AGENT.md** — Kod kalitesi kuralları + BSC (Bowlera Secure Code) modülü, 8 güvenlik
  kuralı. Kural #9: üretilen her dosya artifact olarak verilir.

### Referans Üçlüsü (Session 1)
- **ARCHITECTURE.md** — Next.js App Router yapısı, modül kontratları, BowlItem/CartItem
  veri modeli. ⚠️ §2.4'te isim tutarsızlığı (Açık Sorun #5), 5 adımlı customizer
  kontratıyla senkronize edilmeli (Açık Sorun #10).
- **DESIGN_SYSTEM.md** — Renk sistemi WCAG tablosu, logo kullanım kuralı, tipografi,
  ikonografi, fotoğraf direktifi, animasyon tablosu + erişilebilirlik kuralları.
- **CUSTOMIZER_SPEC.md** — "Kâseni Yarat" tam kontratı, Oturum 2'de v1.0→v1.1 (5 adım).

### İkinci Üçlü (Session 1)
- **DEPENDENCIES.md** — Bağımlılık haritaları. ⚠️ 5 adımlı customizer kararını
  yansıtmıyor (Açık Sorun #10).
- **ROADMAP.md** — 5 oturumluk inşa sırası + kabul kriterleri.
- **TEST_MATRIX.md** — Modül bazlı test senaryoları.

### Üçüncü Üçlü (Session 1)
- **CONTENT_GUIDE.md** — Marka sesi tablosu, hero başlık kalıpları, SEO, JSON-LD şablonu.
  Customizer İngilizce istisnası henüz dosyanın kendisine işlenmedi.
- **INTEGRATIONS.md** — Adisyo/SepetTakip, WhatsApp köprüsü, QR menü, SMS/e-posta.
- **FAILURE_PATTERNS.md** — 10 bilinen hata kalıbı (FP-1 – FP-10).
- **CONFIG_SCHEMA.md** — `.env.local` şeması, ortam bazlı kapsam.

### Oturum 1 — Görsel Doğrulama Süreci (Session 1)
- Logo base64 heredoc ile aktarıldı, ilk denemelerde `EOF` kapanışı hatalıydı,
  üçüncü denemede düzeldi.
- İlk push yanlışlıkla NEXSUS reposuna yapıldı, `git push` "rejected" sayesinde
  hiçbir şey uzağa gitmedi, geri alındı, doğru Codespace'te tekrarlandı.
- `git pull --no-rebase` ile merge, push başarılı (d4eb85d..5806160).
- Site Vercel'e deploy edildi, Header/Footer/Hero görsel olarak doğrulandı.

---

*BOWLERA SESSION_INDEX.md — güncellendi, Session 2 kapanışı — 2026-07-18*
