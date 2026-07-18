# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 2 DEVAM EDİYOR. MenuCard bileşen ailesi + app/menu/page.tsx
          üretildi, test edildi (15/15 ✅) VE Vercel'de GÖRSEL OLARAK doğrulandı.
          Bu oturumun kod tarafı değişmedi — ancak Oturum 3'ü önceden hazırlayan
          KRİTİK BİR MİMARİ KARAR alındı: "Kâseni Yarat" akışı 4 adımdan 5 adıma
          çıkarıldı (bkz. 📌 KRİTİK TEKNİK/TASARIM KARARLARI). Bu, henüz kod
          üretimi gerektirmiyor — MASTER_PLAN.md, CUSTOMIZER_SPEC.md, CORE.md
          kanon dosyaları güncellendi, Oturum 3 bu yeni kontratla başlayacak.
Faz:      Oturum 2 — Menü sayfası, filtreleme, MenuCard, statik menü verisi.
          Tamamlanan: MenuCard ailesi + app/menu/page.tsx + deploy doğrulaması.
          Kalan: CategoryNav.tsx (sticky kategori nav) + FilterPanel.tsx (tag filtre).
Gerekçe:  MenuCard container hatası düzeltildi → npm peer-dependency çakışması
          çözüldü → app/menu/page.tsx yazıldı → Vercel build'de tsconfig type-check
          hatası çıktı → tsconfig exclude düzeltmesiyle çözüldü → build başarılı,
          site canlı ve doğrulandı. Ardından kullanıcı "Kâseni Yarat" marka
          anlayışını sorguladı → gurme mutfak mantığına dayalı 5 adımlı öneri
          getirdi → 3 turlu netleştirme (adım sayısı / dil / ücretlendirme) →
          resmi şema değişikliği olarak onaylandı ve kanon dosyalara işlendi.
Çıktı:    Repo: github.com/Sovereign34/Bowlera_site (main dalı, son commit
          tsconfig fix — bu oturumdaki mimari karar henüz repoya push edilmedi,
          kullanıcı dosyaları kendisi taşıyacak). Deploy: Vercel — /menu sayfası
          canlı ve doğrulanmış (customizer henüz canlı değil, Oturum 3'te gelecek).
```

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI

| # | Karar | Tarih | Kaynak/Gerekçe |
|---|---|---|---|
| 1 | "Kâseni Yarat" akışı 4 adımdan **5 adıma** çıkarıldı: Base → Main → Garden → Signature Flavor → Finish | Oturum 2 — 2026-07-18 | Kullanıcı önerisi ("şefin düşünme sırası": temel→ana ürün→tazelik→lezzet karakteri→son dokunuş). Şema değişiklik notu: `20260718001123_customizer_5_adim_gecisi.md` |
| 2 | Adım/malzeme isimleri **tamamen İngilizce** — CONTENT_GUIDE.md §1 Türkçe marka sesi kuralına bilinçli istisna, yalnızca customizer'ı kapsar | Oturum 2 — 2026-07-18 | Premium/global algı kararı, kullanıcı onaylı |
| 3 | Garden: ilk 4 seçim ücretsiz, Avokado miktarı fark etmeksizin **her zaman ücretli** | Oturum 2 — 2026-07-18 | Kullanıcının orijinal önerisinde Avokado "+" işaretliydi; mevcut Toppings kuralıyla tutarlılık için Claude önerdi, kullanıcı onayladı |
| 4 | Finish: ilk 1 seçim ücretsiz, sonrası ücretli | Oturum 2 — 2026-07-18 | Kullanıcı seçimi |
| 5 | "Make it Yours" (Extra Avocado/Sauce/Crunch) **ayrı adım değil**, Finish adımına entegre alt-bileşen; "Double Main" mevcut `mainPortion` mekanizmasını yeniden kullanır | Oturum 2 — 2026-07-18 | Kullanıcı seçimi + AGENT.md Kural #5 (bağımlılık/duplikasyon önleme) |

> Etkilenen dosyalar: `CORE.md` §8, `MASTER_PLAN.md` v2.1 (§3.3, §5.2, §6, §8),
> `CUSTOMIZER_SPEC.md` v1.1 (tüm dosya). Henüz etkilenmeyen (Oturum 3'te
> işlenecek): `store/useCustomizerStore.ts`, `types/index.ts`, `lib/menu-data.json`,
> `ARCHITECTURE.md` §2.4, `DEPENDENCIES.md`.

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 2 — 2026-07-18 |
| Son Eylem | Customizer akışı 4→5 adıma çıkarıldı; CORE.md/MASTER_PLAN.md/CUSTOMIZER_SPEC.md kanon dosyaları güncellendi |
| Blocker | Yok |
| Devam Noktası | Yeni sohbette CORE.md + AGENT.md + bu SESSION_INDEX ile CategoryNav.tsx/FilterPanel.tsx'e (Oturum 2'nin kalanı) VEYA doğrudan Oturum 3'e (yeni 5 adımlı customizer state kurulumu) başlanabilir |

---

## GENEL DURUM

| Alan | Değer |
|---|---|
| Proje | Bowlera — Healthy Bowls |
| Aktif Oturum | Oturum 2 devam ediyor |
| Toplam Session | 2 |
| Sistem Durumu | 🟢 Test altyapısı sağlıklı (15/15), build sağlıklı, `/menu` canlı |
| Deploy Durumu | ✅ Vercel — `/menu` sayfası görsel olarak doğrulandı |
| Repo | `github.com/Sovereign34/Bowlera_site` |
| Codespace | Aktif (workspace adı: Bowlera_si...) |
| Menü Veri Kaynağı | ✅ `lib/menu-data.json` — 6 signature + 2 içecek, canlıda doğru render oluyor |
| Veri Modeli | ✅ `types/index.ts` — `BowlItem`/`CartItem`. ⬜ `CustomizerSelection` tipi henüz kodda yok (Oturum 3) |
| MenuCard Bileşen Ailesi | ✅ Üretildi, test edildi, canlıda görsel doğrulandı |
| Menü Sayfası (`app/menu/page.tsx`) | ✅ Üretildi, test edildi (2 test), canlıda görsel doğrulandı |
| Kategori/Filtre UI | ⬜ `CategoryNav.tsx`, `FilterPanel.tsx` henüz yazılmadı |
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
| 7 | 🟡 | **Allergen gösterimi DESIGN_SYSTEM.md onayı bekliyor.** `MenuCard.tsx`'e geçici bir satırla eklendi ve canlıda görsel olarak çalıştığı doğrulandı, ama DESIGN_SYSTEM.md'de tanımlı resmi bir stil/bileşen olup olmadığı hâlâ teyit edilmedi. | Oturum 2 | DESIGN_SYSTEM.md §2 (doğrulanmadı) |
| 9 | 🟢 | `vitest.config.ts`'deki `@vitejs/plugin-react` ile Next.js'in kendi `vite` sürümü arasında TS tip çakışması vardı — `tsconfig.json`'ın `exclude` listesine ekleyerek çözüldü. Kalıcı workaround, ileride tekrar kontrol edilmeli. | Oturum 2 | — |
| 10 | 🟡 | **YENİ** — `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md`, customizer'ın 5 adıma çıkması nedeniyle güncel değil (henüz bu görev kapsamına alınmadı — Oturum 3 açılışında ele alınmalı) | Oturum 2 | `20260718001123_customizer_5_adim_gecisi.md` |

> Kapatılan sorunlar: #1 (görsel doğrulama), #2 (deploy platformu), #3 (menü verisi artık var — sadece fotoğraflar hâlâ eksik), #8 (vitest.config.ts commit+push+build doğrulandı).

---

## BOWLERA OTURUM DURUMU

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (14 dosya) | ✅ Üretildi — son onay bekliyor |
| **Oturum 1** | Next.js+Tailwind, font/renk, Header/Footer, Hero | ✅ Tamamlandı — görsel doğrulama yapıldı |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard, statik menü verisi | 🟡 Devam ediyor — MenuCard+page.tsx tamam ve doğrulandı, CategoryNav/FilterPanel kaldı; customizer 5 adım kararı bu oturumda alındı |
| **Oturum 3** | Zustand store + BowlCustomizer (**5 adım** — v2.1, masaüstü) | ⬜ Bekliyor — kontrat hazır (`CUSTOMIZER_SPEC.md` v1.1) |
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
| `components/menu/MenuCard.test.tsx` | ✅ | ✅ happy/edge/failure | ✅ Push | — |
| `vitest.config.ts` | ✅ | — | ✅ Push | ✅ (build kırmadığı doğrulandı) |
| `tsconfig.json` (exclude fix) | ✅ | — | ✅ Push | ✅ Build başarılı |
| `app/menu/page.tsx` | ✅ | ✅ 2 test | ✅ Push | ✅ Doğrulandı |
| `app/menu/page.test.tsx` | ✅ | ✅ happy/edge | ✅ Push | — |
| `components/menu/CategoryNav.tsx` | ⬜ Henüz yazılmadı | — | — | — |
| `components/menu/FilterPanel.tsx` | ⬜ Henüz yazılmadı | — | — | — |
| `store/useCustomizerStore.ts` | ⬜ Henüz yazılmadı (Oturum 3, kontrat v1.1 hazır) | — | — | — |

---

## SIRADAKİ GÖREVLER

| Sıra | Görev | Öncelik | Durum |
|---|---|---|---|
| 1 | `CategoryNav.tsx` (sticky kategori nav, MASTER_PLAN §3.2 — dosya bende yok, istenmeli) | 🔴 | ⬜ |
| 2 | `FilterPanel.tsx` (tag bazlı filtreleme) | 🟡 | ⬜ |
| 3 | Vercel'e deploy + görsel doğrulama (kategori/filtre) | 🔴 | ⬜ |
| 4 | Allergen gösterim satırını DESIGN_SYSTEM.md ile teyit et (Açık Sorun #7) | 🟡 | ⬜ |
| 5 | `next-env.d.ts` commit teyidi (Açık Sorun #6) | 🟢 | ⬜ |
| 6 | ARCHITECTURE.md §2.4 isim düzeltmesi (Açık Sorun #5) | 🟢 | ⬜ |
| 7 | **YENİ** — `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md`'yi 5 adımlı customizer kontratıyla senkronize et (Açık Sorun #10) | 🟡 | ⬜ |

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 2 Detaylı Kayıt

### Customizer 4→5 Adım Geçişi (bu oturumun ikinci yarısı)
- Kullanıcı, kategori/filtre çalışmasına başlamadan önce marka anlayışının
  netleşmediğini belirtti ve "Kâseni Yarat" akışı için 5 adımlı, gurme
  mutfak mantığına dayalı bir öneri getirdi (Base/Main/Garden/Signature
  Flavor/Finish + "Make it Yours" ek seçenekleri).
- MASTER_PLAN.md, CUSTOMIZER_SPEC.md, CONTENT_GUIDE.md okunarak öneri
  mevcut kanonla karşılaştırıldı; 3 doğrudan çelişki tespit edildi: adım
  sayısı (4 vs 5), dil (Türkçe vs İngilizce), veri şeması (toppings/sauce
  vs garden/signatureFlavor/finish).
- 3 turlu netleştirme yapıldı: (1) adım sayısı → 5 adıma geçildi, (2) dil →
  tamamen İngilizce, (3) resmi şema değişikliği mi / sadece konsept mi →
  resmi değişiklik. Ardından Garden/Finish ücretlendirme kuralları ve "Make
  it Yours" konumlandırması netleştirildi (Garden: sen öner → mevcut
  Toppings kuralıyla tutarlı 4-ücretsiz + avokado her zaman ücretli önerisi
  kabul edildi; Finish: 1 ücretsiz; Make it Yours → Finish'e entegre).
- Şema değişiklik notu (`20260718001123_customizer_5_adim_gecisi.md`)
  CORE.md §7.4 formatına uygun üretildi. `CORE.md` §8, `MASTER_PLAN.md`
  (v2.0→v2.1), `CUSTOMIZER_SPEC.md` (v1.0→v1.1) tam dosya olarak güncellendi.
- `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md` bu kararı henüz yansıtmıyor —
  bu dosyalar bu oturumda sağlanmadığı için güncellenemedi, Açık Sorun #10
  olarak kaydedildi.

### MenuCard Container Hatası ve Düzeltmesi
- `components/menu/MenuCard.tsx` dosyası GitHub'da incelendiğinde, dosya adı
  doğru olmasına rağmen içeriğinin yanlışlıkla `MenuCardImage.tsx`'in birebir
  kopyası olduğu tespit edildi. Gerçek container yazılıp düzeltildi. Bu
  sırada `allergens` alanının hiçbir alt bileşende render edilmediği (bkz.
  Açık Sorun #7) bulundu ve geçici bir satırla kapatıldı.

### Test Altyapısı — npm Peer-Dependency Çakışması
- İlk `npm test` denemesinde 4 test dosyasının tamamı `ReferenceError: React is
  not defined` hatasıyla çöktü — `vitest.config.ts`'de `@vitejs/plugin-react`
  hiç tanımlı değildi. Versiyon belirtmeden yapılan kurulum denemesi npm'in
  en son sürümü (6.0.3, `vite@^8` istiyor) çekmesine ve mevcut `vite@^5`
  (vitest 1.6 üzerinden) ile çakışmasına yol açtı. `rm -rf node_modules
  package-lock.json && npm install` ile temiz kurulum + `@vitejs/plugin-react@^4.3.0`
  sabit sürüm kurulumuyla çözüldü — 13/13 test geçti.

### app/menu/page.tsx — Dosya Oluşturma Sorunları
- İlk `git commit` denemesi "nothing to commit" döndü — `app/menu/page.tsx` ve
  `page.test.tsx` heredoc'ları hiç çalıştırılmamıştı, sadece komut olarak
  yapıştırılmıştı. `ls app/menu/` ile teyit edilip dosyalar doğru şekilde
  oluşturuldu. Düşük insertion sayısı endişesi test sonucunun (15/15 ✅) dosya
  bütünlüğünü dolaylı doğrulamasıyla giderildi.

### Vercel Build Hatası — tsconfig/vitest Tip Çakışması
- `git push` sonrası Vercel build'i `next build`'in tip kontrolü aşamasında
  `vitest.config.ts:6:13`'te çöktü: `node_modules` içindeki iki farklı `vite`
  paketi (kök + `vitest`'in kendi gömülü kopyası) arasında `Plugin`/`PluginOption`
  tip uyuşmazlığı. Kök sebep: Next.js'in production type-check'i
  `vitest.config.ts`'i de kapsıyordu, ama bu dosya build'de hiç kullanılmıyor.
- Çözüm: `tsconfig.json`'ın `exclude` dizisine `vitest.config.ts`,
  `vitest.setup.ts`, `**/*.test.tsx`, `**/*.test.ts` eklendi (Açık Sorun #9
  olarak kayıtlı — kalıcı workaround, `vitest`/`vite` sürüm güncellemesinde
  tekrar gözden geçirilmeli). Build başarılı oldu, `/menu` sayfası canlıda
  görsel olarak doğrulandı: grid, kalori/protein/fiyat, allergen satırı ve
  "Süper Gıda" rozeti çalışıyor. Kırık resim ikonları beklenen durum (gerçek
  fotoğraflar henüz yok).

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 0 Detaylı Kayıt

> Tamamlanan görevlerin üstteki bölümlerden silinen ayrıntıları — dosya şişmemesi için
> buraya taşındı (bu dosyanın kendi kuralı).

### Çekirdek Üçlü (Session 1)
- **CORE.md** — 11 bölüm: session açılış protokolü, proje kimliği, tetikleyici tablosu,
  dosya haritası, context kuralı, session kapanış protokolü, checkpoint protokolü, log
  tetikleyicileri, veri şeması değişiklik protokolü, mimari varsayımlar, mutlak yasaklar,
  sağlık kontrol listesi, re-injection protokolü.
- **AGENT.md** — Kod kalitesi kuralları + BSC (Bowlera Secure Code) modülü, 8 güvenlik
  kuralı (XSS, secret yönetimi, girdi doğrulama, hata yönetimi, sahte veri yasağı,
  BSC-6/7/8). Kural #9: üretilen her dosya artifact olarak verilir.

### Referans Üçlüsü (Session 1)
- **ARCHITECTURE.md** — Next.js App Router yapısı, modül kontratları (API route/store/
  component interface'leri), BowlItem/CartItem veri modeli, deploy/performans/rollback.
  ⚠️ §2.4'te `calculateTotals`/`getTotals` isim tutarsızlığı tespit edildi — CUSTOMIZER_SPEC.md
  esas alınıyor, düzeltme bekliyor (Açık Sorun #5). ⚠️ Oturum 2 itibarıyla ayrıca 5 adımlı
  customizer kontratıyla senkronize edilmeli (Açık Sorun #10).
- **DESIGN_SYSTEM.md** — Renk sistemi WCAG tablosu, logo degrade sınırlı kullanım kuralı
  (yalnızca 4 izinli yer), tipografi (Cormorant Garamond + Nunito), ikonografi (Lucide React
  + özel SVG imza deseni), fotoğraf direktifi + adlandırma standardı, tam animasyon tablosu
  + erişilebilirlik kuralları (prefers-reduced-motion, transform/opacity only).
- **CUSTOMIZER_SPEC.md** — "Kâseni Yarat" tam kontratı: Oturum 2'de v1.0'dan v1.1'e
  güncellendi (4 adımdan 5 adıma). Güncel içerik için bkz. yukarıdaki "Oturum 2 Detaylı
  Kayıt" ve dosyanın kendisi.

### İkinci Üçlü (Session 1)
- **DEPENDENCIES.md** — Dosya→dosya, bileşen→store, veri modeli ve üçüncü parti entegrasyon
  bağımlılık haritaları. ⚠️ Oturum 2 itibarıyla 5 adımlı customizer kararını yansıtmıyor
  (Açık Sorun #10).
- **ROADMAP.md** — 5 oturumluk inşa sırası + her oturum için kabul kriterleri + lansman
  sonrası kapsam dışı faz listesi.
- **TEST_MATRIX.md** — Modül bazlı test senaryoları (veri/API, customizer, sepet, tasarım/
  erişilebilirlik, performans, üçüncü parti) — durum sembolleriyle takip.

### Üçüncü Üçlü (Session 1)
- **CONTENT_GUIDE.md** — Marka sesi tablosu, hero başlık kalıpları, ürün açıklama kalıbı,
  alt-text üretim kuralı, SEO anahtar kelimeleri, JSON-LD şema şablonu. Oturum 2'de
  customizer adım isimleri için bilinçli İngilizce istisnası tanımlandı (bkz. MASTER_PLAN
  v2.1 §6) — CONTENT_GUIDE.md dosyasının kendisi henüz bu istisnayı içermiyor, bu görev
  kapsamına alınmadı.
- **INTEGRATIONS.md** — Adisyo/SepetTakip (rate limit + graceful degradation), WhatsApp
  köprüsü (mesaj şablonu + edge case'ler), QR menü (masa parametresi), SMS/e-posta bildirimi
  (gelecek faz iskeleti).
- **FAILURE_PATTERNS.md** — 10 bilinen hata kalıbı (FP-1 – FP-10): sepet/state, customizer,
  üçüncü parti entegrasyon, tasarım/performans kategorilerinde — her biri belirti/kök neden/
  çözüm/önleme formatında.
- **CONFIG_SCHEMA.md** — `.env.local` şeması, ortam bazlı kapsam (dev/preview/production),
  `.env.local.example` şablonu, yeni değişken ekleme protokolü.

### Oturum 1 — Görsel Doğrulama Süreci (Session 1)
- Logo dosyası GitHub mobil arayüzünde binary drag-and-drop desteklenmediği için
  base64 metne çevrilip Codespaces terminalinde `cat > ... << 'EOF'` heredoc yöntemiyle
  aktarıldı. İlk iki denemede heredoc kapanış satırı (`'EOF'` tırnaklı yazılması) hatalı
  olduğu için terminal takılı kaldı ve komutlar dosyanın içine metin olarak karıştı —
  üçüncü denemede tırnaksız `EOF` ile düzgün kapatıldı, `base64 -d` hatasız tamamlandı.
- İlk push denemesi yanlışlıkla NEXSUS (trading sistemi) reposuna yapılmıştı —
  `git push` "rejected" hatası vermesi sayesinde uzak repoya hiçbir şey gitmedi;
  `git reset HEAD~1` ile local commit geri alındı, dosya o repodan temizlendi.
  Doğru Codespace (Bowlera_site) açılarak işlem baştan yapıldı.
- Doğru repoda `git push` "rejected (fetch first)" hatası verdi (uzak repoda
  Header.tsx/Footer.tsx'te local'de olmayan değişiklikler vardı) — `git pull --no-rebase`
  ile merge yapıldı, ardından push başarılı oldu (d4eb85d..5806160).
- Site Vercel'e deploy edildi, ekran görüntüsüyle doğrulandı: Header/Footer'da logo
  doğru render oluyor, Hero başlık+CTA butonları çalışıyor, placeholder alanlar
  ("Kase fotoğrafı yakında", "Şube bilgileri yakında Oturum 5'te") bilinçli ve etiketli.

---

*BOWLERA SESSION_INDEX.md — güncellendi, Session 2 — 2026-07-18*
