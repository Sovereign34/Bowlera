# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 2 DEVAM EDİYOR. MenuCard bileşen ailesi (MenuCard, MenuCardImage,
          MenuCardBadges, MenuCardInfo) ve types/index.ts (BowlItem/CartItem) ile
          menu-data.json üretildi, test edildi, repoya push edildi. ANCAK bu
          bileşenler henüz hiçbir sayfaya bağlanmadı — app/menu/page.tsx yok,
          CategoryNav.tsx ve FilterPanel.tsx henüz yazılmadı. Vercel deploy'unda
          hâlâ sadece Oturum 1'in Hero sayfası görünüyor, bu BEKLENEN bir durum.
Faz:      Oturum 2 — Menü sayfası, filtreleme, MenuCard, statik menü verisi.
          Alt görev tamamlandı: MenuCard bileşen ailesi + testler (13/13 ✅).
          Kalan: app/menu/page.tsx + CategoryNav.tsx + FilterPanel.tsx.
Gerekçe:  MenuCard container dosyasında yanlış içerik commit edilmiş bulundu ve
          düzeltildi; ardından test altyapısında npm peer-dependency çakışması
          bulunup çözüldü. Şimdi bileşenler doğrulanmış durumda, sayfaya
          bağlanmayı bekliyor.
Çıktı:    Repo: github.com/Sovereign34/Bowlera_site (main dalı). Deploy: Vercel
          (görsel olarak henüz değişmedi — beklenen, çünkü sayfa bağlantısı yapılmadı).
```

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 2 — 2026-07-17 |
| Son Eylem | `npm test` → 13/13 test geçti (MenuCard, Hero, Footer, Header), `@vitejs/plugin-react@^4.3.0` sabitlendi |
| Blocker | Yok — ancak `package.json`/`package-lock.json` değişikliğinin commit+push edildiği teyit edilmedi (kullanıcıya son adım olarak verildi) |
| Devam Noktası | Yeni sohbette: (1) önce commit/push teyidi al, (2) sonra `app/menu/page.tsx` + `CategoryNav.tsx` + `FilterPanel.tsx` ile Oturum 2'yi tamamla |

---

## GENEL DURUM

| Alan | Değer |
|---|---|
| Proje | Bowlera — Healthy Bowls |
| Aktif Oturum | Oturum 2 devam ediyor |
| Toplam Session | 2 |
| Sistem Durumu | 🟢 Test altyapısı sağlıklı, bileşenler doğrulanmış — 🟡 sayfa bağlantısı eksik |
| Deploy Durumu | ✅ Vercel canlı (henüz Oturum 2 içeriği görünmüyor — beklenen) |
| Repo | `github.com/Sovereign34/Bowlera_site` |
| Codespace | Aktif (workspace adı: Bowlera_si...) |
| Menü Veri Kaynağı | ✅ `lib/menu-data.json` üretildi (6 signature + 2 içecek, gerçek kalori/protein/fiyat) |
| Veri Modeli | ✅ `types/index.ts` — `BowlItem`/`CartItem` ilk kez codify edildi |
| MenuCard Bileşen Ailesi | ✅ `MenuCard.tsx` + `MenuCardImage/Badges/Info.tsx` — 13/13 test geçti |
| Menü Sayfası | ⬜ `app/menu/page.tsx` henüz yazılmadı |
| Kategori/Filtre UI | ⬜ `CategoryNav.tsx`, `FilterPanel.tsx` henüz yazılmadı |
| Görsel/Fotoğraf İçeriği | ⬜ Hâlâ bekleniyor — placeholder kullanılıyor |
| Üçüncü Parti Anahtarları | ⬜ Adisyo/SepetTakip, WhatsApp, Twilio — henüz temin edilmedi, ayrı faz |

---

## AÇIK SORUNLAR

| # | Öncelik | Açıklama | Oturum | Referans |
|---|---|---|---|---|
| 4 | 🟡 | Üçüncü parti API anahtarları temin edilmedi | Sonraki Faz | MASTER_PLAN §8 |
| 5 | 🟢 | ARCHITECTURE.md §2.4 `calculateTotals`/`getTotals` isim tutarsızlığı — düzeltme bekliyor | Oturum 0 | DEPENDENCIES.md §1 |
| 6 | 🟢 | `next-env.d.ts` ve `package-lock.json` (Oturum 1'den kalan) commit edilmiş mi teyit edilmedi | Oturum 1 | — |
| 7 | 🟡 | **Allergen gösterimi DESIGN_SYSTEM.md onayı bekliyor.** `MenuCard.tsx`'e geçici bir satırla (`İçerir: ...`) eklendi çünkü `allergens` alanı hiçbir alt bileşende render edilmiyordu — bu bir güvenlik/sağlık gap'iydi (alerjen bilgisi kullanıcıya hiç gösterilmiyordu). DESIGN_SYSTEM.md'de tanımlı bir stil/bileşen varsa ona göre değiştirilmeli. | Oturum 2 | DESIGN_SYSTEM.md §2 (doğrulanmadı) |
| 8 | 🟡 | `package.json`/`package-lock.json`'daki `@vitejs/plugin-react@^4.3.0` sabitlemesinin commit+push edildiği teyit edilmedi (son mesajda kullanıcıya görev olarak verildi, sonucu görülmedi) | Oturum 2 | — |

> Kapatılan sorunlar: #1 (görsel doğrulama), #2 (deploy platformu), #3 (MenuCard için menü verisi artık var — placeholder fotoğraf hâlâ geçerli, bkz. yeni #9 değil, aynı kapsamda kalıyor).

---

## BOWLERA OTURUM DURUMU

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (14 dosya) | ✅ Üretildi — son onay bekliyor |
| **Oturum 1** | Next.js+Tailwind, font/renk, Header/Footer, Hero | ✅ Tamamlandı — görsel doğrulama yapıldı |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard, statik menü verisi | 🟡 Devam ediyor — MenuCard ailesi tamam, sayfa bağlantısı kaldı |
| **Oturum 3** | Zustand store + BowlCustomizer (4 adım, masaüstü) | ⬜ Bekliyor |
| **Oturum 4** | VisualPreview, mobil özelleştirici, sepet | ⬜ Bekliyor |
| **Kontrol Noktası** | Kullanıcı testi (5-10 kişi) | ⬜ Bekliyor |
| **Oturum 5** | Hakkımızda, Şubeler, İletişim, SEO, son kontrol | ⬜ Bekliyor |

---

## ÜRETİLEN KOD DOSYALARI

| Dosya | Durum | Test | Repo |
|---|---|---|---|
| `app/layout.tsx`, `app/page.tsx`, `app/globals.css` | ✅ Üretildi | — | ✅ Push edildi |
| `tailwind.config.ts`, `lib/fonts.ts` | ✅ Üretildi | — | ✅ Push edildi |
| `components/layout/Header.tsx` | ✅ Üretildi | ✅ 3 test geçti | ✅ Push edildi — görsel doğrulandı |
| `components/layout/Footer.tsx` | ✅ Üretildi | ✅ 3 test geçti | ✅ Push edildi — görsel doğrulandı |
| `components/home/Hero.tsx` + alt bileşenler | ✅ Üretildi | ✅ 3 test geçti | ✅ Push edildi — görsel doğrulandı |
| `public/images/logo-bowlera.png` | ✅ Eklendi (base64 → decode) | — | ✅ Push edildi — görsel doğrulandı |
| `types/index.ts` (BowlItem/CartItem) | ✅ Üretildi | — | ✅ Push edildi |
| `lib/menu-data.json` | ✅ Üretildi (6 signature + 2 içecek) | — | ✅ Push edildi |
| `components/menu/MenuCardImage.tsx` | ✅ Üretildi | ✅ dahil | ✅ Push edildi |
| `components/menu/MenuCardBadges.tsx` | ✅ Üretildi | ✅ dahil | ✅ Push edildi |
| `components/menu/MenuCardInfo.tsx` | ✅ Üretildi | ✅ dahil | ✅ Push edildi |
| `components/menu/MenuCard.tsx` | ✅ Düzeltildi (bkz. GEÇMİŞ) | ✅ 4/4 test geçti | ✅ Push edildi |
| `components/menu/MenuCard.test.tsx` | ✅ Üretildi | ✅ happy/edge/failure | ✅ Push edildi |
| `vitest.config.ts` | 🟡 Düzeltildi (`react()` plugin eklendi) | — | ⬜ Push teyidi yok |
| `app/menu/page.tsx` | ⬜ Henüz yazılmadı | — | — |
| `components/menu/CategoryNav.tsx` | ⬜ Henüz yazılmadı | — | — |
| `components/menu/FilterPanel.tsx` | ⬜ Henüz yazılmadı | — | — |

---

## SIRADAKİ GÖREVLER

| Sıra | Görev | Öncelik | Durum |
|---|---|---|---|
| 1 | `git add package.json package-lock.json && git commit && git push` — `@vitejs/plugin-react` sabitlemesini kalıcı hale getir | 🔴 | ⬜ |
| 2 | `app/menu/page.tsx` yaz — `menu-data.json`'ı okuyup `MenuCard` grid'i render etsin | 🔴 | ⬜ |
| 3 | `CategoryNav.tsx` (sticky kategori nav, MASTER_PLAN §3.2) | 🔴 | ⬜ |
| 4 | `FilterPanel.tsx` (tag bazlı filtreleme) | 🟡 | ⬜ |
| 5 | Vercel'e deploy + görsel doğrulama (menü sayfası) | 🔴 | ⬜ |
| 6 | Allergen gösterim satırını DESIGN_SYSTEM.md ile teyit et (Açık Sorun #7) | 🟡 | ⬜ |
| 7 | `next-env.d.ts` + `package-lock.json` (Oturum 1 kalıntısı) commit teyidi | 🟢 | ⬜ |
| 8 | ARCHITECTURE.md §2.4 isim düzeltmesi | 🟢 | ⬜ |

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 2 Detaylı Kayıt

### MenuCard Container Hatası ve Düzeltmesi
- `components/menu/MenuCard.tsx` dosyası GitHub'da incelendiğinde, dosya adı doğru
  olmasına rağmen içeriğinin yanlışlıkla `MenuCardImage.tsx`'in birebir kopyası
  olduğu tespit edildi (1. satırdaki yorum `// components/menu/MenuCardImage.tsx`
  yazıyordu). Gerçek container hiç yazılmamıştı — test dosyası (`./MenuCard`'ı
  `item: BowlItem` prop'uyla import eden) bu yüzden çalışamazdı.
- Doğru `MenuCard.tsx` üretildi: üç alt bileşeni (`MenuCardImage`, `MenuCardBadges`,
  `MenuCardInfo`) `item` prop'undan besleyen bir container. Bu sırada ayrı bir gap
  daha bulundu: `allergens` alanı (BowlItem'da mevcut, menu-data.json'da dolu) hiçbir
  alt bileşende render edilmiyordu — `MenuCardBadges.tsx`'in kod yorumu alerjen
  riskinden bahsediyordu ama sadece `tags`'i render ediyordu. Geçici bir çözümle
  (`İçerir: ...` satırı) kapatıldı, DESIGN_SYSTEM.md onayı bekliyor (Açık Sorun #7).
- Kullanıcı GitHub web arayüzünden `MenuCard.tsx` içeriğini manuel olarak düzeltip
  push etti (Codespaces heredoc yöntemi yerine).

### Test Altyapısı — npm Peer-Dependency Çakışması
- İlk `npm test` denemesinde 4 test dosyasının tamamı (13/13) aynı hatayla çöktü:
  `ReferenceError: React is not defined`. Kök sebep: `vitest.config.ts`'de
  `@vitejs/plugin-react` plugin'i hiç tanımlı değildi, sadece `resolve.alias` vardı.
- `npm install -D @vitejs/plugin-react` (versiyon belirtmeden) çalıştırıldığında npm
  en son sürümü (6.0.3) kurmaya çalıştı — bu sürüm `vite@^8.0.0` istiyordu, ama
  proje `vitest@^1.6.0` üzerinden `vite@^5` kullanıyordu. Peer-dependency çakışması
  nedeniyle kurulum reddedildi (`MODULE_NOT_FOUND` zinciri ile sonraki testlerde
  tekrar tekrar ortaya çıktı).
- `--legacy-peer-deps` ile zorlanan bir ara deneme `esbuild` seviyesinde farklı bir
  çöküşe yol açtı (native binary/paket sürüm uyumsuzluğu).
- Kalıcı çözüm: `rm -rf node_modules package-lock.json && npm install` ile temiz
  kurulum yapıldı, ardından `npm install -D @vitejs/plugin-react@^4.3.0` (vite 5 /
  vitest 1.x ile uyumlu sabit sürüm) ile plugin doğru kuruldu. Sonuç: **13/13 test
  geçti** (`MenuCard.test.tsx` 4, `Hero.test.tsx` 3, `Footer.test.tsx` 3,
  `Header.test.tsx` 3).
- Bu düzeltme, ileride aynı hatanın tekrar yaşanmaması için FAILURE_PATTERNS.md'ye
  yeni bir kalıp (FP-11 adayı: "vitest/@vitejs-plugin-react sürüm sabitleme")
  olarak eklenmeyi bekliyor — henüz o dosyaya işlenmedi.

### Sayfa Bağlantısı Henüz Yapılmadı
- Vercel deploy'unda site kontrol edildiğinde Hero sayfasının Oturum 1'deki haliyle
  aynı kaldığı görüldü. Bu bir regresyon değil — MenuCard bileşenleri henüz hiçbir
  route'a bağlanmadı (`app/menu/page.tsx` yok). Kullanıcıya bu netleştirildi.

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 0 Detaylı Kayıt

> Tamamlanan görevlerin üstteki bölümlerden silinen ayrıntıları — dosya şişmemesi için
> buraya taşındı (bu dosyanın kendi kuralı).

### Çekirdek Üçlü (Session 1)
- **CORE.md** — 11 bölüm: session açılış protokolü, proje kimliği, tetikleyici tablosu,
  dosya haritası, context kuralı, session kapanış protokolü, checkpoint protokolü, log
  tetikleyicileri, veri şeması değişiklik protokolü, mimari varsayımlar, mutlak yasaklar,
  sağlık kontrol listesi, re-injection protokolü. NEXUS_OS metodolojisinden Bowlera'ya
  (marka web sitesi/e-ticaret) uyarlandı.
- **AGENT.md** — Kod kalitesi kuralları (bileşen boyutu disiplini, niyet yorumu zorunluluğu,
  edge case önce/kod sonra, sahte veri yasağı, bağımlılık disiplini, test yazım standardı,
  context kaybı koruması) + BSC (Bowlera Secure Code) modülü, 8 güvenlik kuralı: XSS
  sanitizasyonu, secret yönetimi, girdi doğrulama, hata yönetimi, sahte veri yasağı,
  sepet/customizer race condition koruması (BSC-6), üçüncü parti rate limit (BSC-7),
  entegrasyon kopmasında graceful degradation (BSC-8). Kural #9: üretilen her dosya
  artifact olarak verilir.

### Referans Üçlüsü (Session 1)
- **ARCHITECTURE.md** — Next.js App Router yapısı, modül kontratları (API route/store/
  component interface'leri), BowlItem/CartItem veri modeli, deploy/performans/rollback.
  ⚠️ §2.4'te `calculateTotals`/`getTotals` isim tutarsızlığı tespit edildi — CUSTOMIZER_SPEC.md
  esas alınıyor, düzeltme bekliyor.
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
