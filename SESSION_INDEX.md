# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 2 DEVAM EDİYOR. MenuCard bileşen ailesi + app/menu/page.tsx
          üretildi, test edildi (15/15 ✅) VE Vercel'de GÖRSEL OLARAK doğrulandı:
          /menu sayfası grid halinde render oluyor, kalori/protein/fiyat doğru,
          allergen satırı ("İçerir: Soya" vb.) ve "Süper Gıda" rozeti çalışıyor.
          Kırık resim ikonları bekleniyordu (gerçek fotoğraflar henüz yüklenmedi).
Faz:      Oturum 2 — Menü sayfası, filtreleme, MenuCard, statik menü verisi.
          Tamamlanan: MenuCard ailesi + app/menu/page.tsx + deploy doğrulaması.
          Kalan: CategoryNav.tsx (sticky kategori nav) + FilterPanel.tsx (tag filtre).
Gerekçe:  MenuCard container hatası düzeltildi → npm peer-dependency çakışması
          çözüldü → app/menu/page.tsx yazıldı → Vercel build'de tsconfig type-check
          hatası çıktı (vitest.config.ts'in iki farklı vite paketi arasında tip
          çakışması) → tsconfig exclude düzeltmesiyle çözüldü → build başarılı,
          site canlı ve doğrulandı.
Çıktı:    Repo: github.com/Sovereign34/Bowlera_site (main dalı, son commit
          tsconfig fix). Deploy: Vercel — /menu sayfası canlı ve doğrulanmış.
```

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 2 — 2026-07-17 |
| Son Eylem | Vercel build başarılı, `/menu` sayfası ekran görüntüsüyle görsel olarak doğrulandı |
| Blocker | Yok |
| Devam Noktası | Yeni sohbette doğrudan `CategoryNav.tsx` + `FilterPanel.tsx` ile Oturum 2'nin geri kalanına başlanabilir |

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
| Veri Modeli | ✅ `types/index.ts` — `BowlItem`/`CartItem` |
| MenuCard Bileşen Ailesi | ✅ Üretildi, test edildi, canlıda görsel doğrulandı |
| Menü Sayfası (`app/menu/page.tsx`) | ✅ Üretildi, test edildi (2 test), canlıda görsel doğrulandı |
| Kategori/Filtre UI | ⬜ `CategoryNav.tsx`, `FilterPanel.tsx` henüz yazılmadı |
| Görsel/Fotoğraf İçeriği | ⬜ Hâlâ bekleniyor — hem Hero'da hem MenuCard'larda placeholder/kırık ikon |
| Üçüncü Parti Anahtarları | ⬜ Adisyo/SepetTakip, WhatsApp, Twilio — henüz temin edilmedi, ayrı faz |

---

## AÇIK SORUNLAR

| # | Öncelik | Açıklama | Oturum | Referans |
|---|---|---|---|---|
| 4 | 🟡 | Üçüncü parti API anahtarları temin edilmedi | Sonraki Faz | MASTER_PLAN §8 |
| 5 | 🟢 | ARCHITECTURE.md §2.4 `calculateTotals`/`getTotals` isim tutarsızlığı — düzeltme bekliyor | Oturum 0 | DEPENDENCIES.md §1 |
| 6 | 🟢 | `next-env.d.ts` (Oturum 1'den kalan) hâlâ untracked görünüyor, commit edilmemiş | Oturum 1 | — |
| 7 | 🟡 | **Allergen gösterimi DESIGN_SYSTEM.md onayı bekliyor.** `MenuCard.tsx`'e geçici bir satırla eklendi ve canlıda görsel olarak çalıştığı doğrulandı ("İçerir: Soya", "İçerir: Kabuklu Deniz Ürünü"), ama DESIGN_SYSTEM.md'de tanımlı resmi bir stil/bileşen olup olmadığı hâlâ teyit edilmedi. | Oturum 2 | DESIGN_SYSTEM.md §2 (doğrulanmadı) |
| 9 | 🟢 | `vitest.config.ts`'deki `@vitejs/plugin-react` ile Next.js'in kendi `vite` sürümü arasında TS tip çakışması vardı — `tsconfig.json`'ın `exclude` listesine `vitest.config.ts`, `vitest.setup.ts`, `**/*.test.tsx`, `**/*.test.ts` eklenerek çözüldü. Kalıcı bir workaround, ileride `vitest`/`vite` sürümleri güncellenirse tekrar kontrol edilmeli. | Oturum 2 | — |

> Kapatılan sorunlar: #1 (görsel doğrulama), #2 (deploy platformu), #3 (menü verisi artık var — sadece fotoğraflar hâlâ eksik, bu kısım #3 kapsamında açık kalmaya devam ediyor), #8 (vitest.config.ts commit+push+build doğrulandı).

---

## BOWLERA OTURUM DURUMU

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (14 dosya) | ✅ Üretildi — son onay bekliyor |
| **Oturum 1** | Next.js+Tailwind, font/renk, Header/Footer, Hero | ✅ Tamamlandı — görsel doğrulama yapıldı |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard, statik menü verisi | 🟡 Devam ediyor — MenuCard+page.tsx tamam ve doğrulandı, CategoryNav/FilterPanel kaldı |
| **Oturum 3** | Zustand store + BowlCustomizer (4 adım, masaüstü) | ⬜ Bekliyor |
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

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 2 Detaylı Kayıt

### MenuCard Container Hatası ve Düzeltmesi
- `components/menu/MenuCard.tsx` dosyası GitHub'da incelendiğinde, dosya adı doğru
  olmasına rağmen içeriğinin yanlışlıkla `MenuCardImage.tsx`'in birebir kopyası
  olduğu tespit edildi. Gerçek container yazılıp düzeltildi. Bu sırada `allergens`
  alanının hiçbir alt bileşende render edilmediği (bkz. Açık Sorun #7) bulundu ve
  geçici bir satırla kapatıldı.

### Test Altyapısı — npm Peer-Dependency Çakışması
- İlk `npm test` denemesinde 4 test dosyasının tamamı `ReferenceError: React is not
  defined` hatasıyla çöktü — `vitest.config.ts`'de `@vitejs/plugin-react` hiç
  tanımlı değildi. Versiyon belirtmeden yapılan kurulum denemesi npm'in en son
  sürümü (6.0.3, `vite@^8` istiyor) çekmesine ve mevcut `vite@^5` (vitest 1.6
  üzerinden) ile çakışmasına yol açtı. `rm -rf node_modules package-lock.json &&
  npm install` ile temiz kurulum + `@vitejs/plugin-react@^4.3.0` sabit sürüm
  kurulumuyla çözüldü — 13/13 test geçti.

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
  tip uyuşmazlığı. Kök sebep: Next.js'in production type-check'i `vitest.config.ts`'i
  de kapsıyordu, ama bu dosya build'de hiç kullanılmıyor.
- Çözüm: `tsconfig.json`'ın `exclude` dizisine `vitest.config.ts`, `vitest.setup.ts`,
  `**/*.test.tsx`, `**/*.test.ts` eklendi (Açık Sorun #9 olarak kayıtlı — kalıcı
  workaround, `vitest`/`vite` sürüm güncellemesinde tekrar gözden geçirilmeli).
  Build başarılı oldu, `/menu` sayfası canlıda görsel olarak doğrulandı: grid,
  kalori/protein/fiyat, allergen satırı ve "Süper Gıda" rozeti çalışıyor. Kırık
  resim ikonları beklenen durum (gerçek fotoğraflar henüz yok).

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
  esas alınıyor, düzeltme bekliyor (Açık Sorun #5).
- **DESIGN_SYSTEM.md** — Renk sistemi WCAG tablosu, logo degrade sınırlı kullanım kuralı
  (yalnızca 4 izinli yer), tipografi (Cormorant Garamond + Nunito), ikonografi (Lucide React
  + özel SVG imza deseni), fotoğraf direktifi + adlandırma standardı, tam animasyon tablosu
  + erişilebilirlik kuralları (prefers-reduced-motion, transform/opacity only).
- **CUSTOMIZER_SPEC.md** — "Kâseni Yarat" tam kontratı: 4 adım state makinesi, adım geçiş
  guard'ı (`maxReachedStep`), canlı fiyat/kalori hesaplama (`getTotals`), VisualPreview
  katmanlı CSS/SVG mantığı (z-index: kase→taban→protein→topping→sos), mobil sticky çekmece
  UX, BSC-6 race condition korumalı sepete ekleme.

### İkinci Üçlü (Session 1)
- **DEPENDENCIES.md** — Dosya→dosya, bileşen→store, veri modeli ve üçüncü parti entegrasyon
  bağımlılık haritaları.
- **ROADMAP.md** — 5 oturumluk inşa sırası + her oturum için kabul kriterleri + lansman
  sonrası kapsam dışı faz listesi.
- **TEST_MATRIX.md** — Modül bazlı test senaryoları (veri/API, customizer, sepet, tasarım/
  erişilebilirlik, performans, üçüncü parti) — durum sembolleriyle takip.

### Üçüncü Üçlü (Session 1)
- **CONTENT_GUIDE.md** — Marka sesi tablosu, hero başlık kalıpları, ürün açıklama kalıbı,
  alt-text üretim kuralı, SEO anahtar kelimeleri, JSON-LD şema şablonu.
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

*BOWLERA SESSION_INDEX.md — güncellendi, Session 2 — 2026-07-17*
