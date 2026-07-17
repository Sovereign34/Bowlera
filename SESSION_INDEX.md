# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Ajan yürütme altyapısının 14/14 dosyası üretildi (nihai onay bekliyor —
          detaylı içerik dökümü aşağıda GEÇMİŞ/ARŞİV bölümünde).
          Oturum 1 kod üretimi tamamlandı: Next.js iskeleti + Header/Footer/Hero
          (staggered başlık animasyonu + placeholder görsel) + testler.
          Kullanıcı Codespaces üzerinden repoya push etti (commit 1ff9e52),
          npm install + npm run dev başarıyla çalıştı ("Ready in 2.1s").
          Port 3000 forward adresi bulundu (https://supreme-...app.github.dev).
          Tarayıcıda görsel doğrulama YAPILMADI — kullanıcı linke tıkladı ama
          sonucu paylaşmadan sohbeti kapattı.
Faz:      Oturum 1 — Next.js Kurulumu (kod push edildi, görsel doğrulama bekliyor)
Gerekçe:  Kullanıcı başka bir sohbete geçeceğini bildirdi — kapanış protokolü
          (CORE.md §7.1) uygulanıyor.
Çıktı:    bowlera-oturum1.zip GitHub'a push edildi (main dalı, commit 1ff9e52).
          Sunucu Codespaces'te çalışır durumda bırakıldı.
```

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 1 — 2026-07-17 |
| Son Eylem | Oturum 1 kod push edildi, `npm install`+`npm run dev` başarılı, port 3000 forward linki bulundu |
| Blocker | Yok — sadece görsel doğrulama (screenshot) bekleniyor |
| Devam Noktası | Yeni sohbette önce `https://supreme-...app.github.dev` linkinin açtığı sayfanın ekran görüntüsü istenmeli — Header/Footer/Hero doğru render oluyor mu kontrol edilecek. Sorun yoksa Oturum 2'ye (Menü sayfası) geçilecek. |

---

## GENEL DURUM

| Alan | Değer |
|---|---|
| Proje | Bowlera — Healthy Bowls |
| Aktif Oturum | Oturum 1 — Next.js Kurulumu |
| Toplam Session | 1 |
| Sistem Durumu | 🟢 Kod push edildi, sunucu çalışıyor — görsel doğrulama bekliyor |
| Deploy Durumu | ⬜ Belirlenmedi — Vercel muhtemel, kullanıcıyla netleştirilecek |
| Next.js Proje İskeleti | ✅ Kuruldu, GitHub'a push edildi (main, commit 1ff9e52) |
| Repo | `github.com/Sovereign34/Bowlera_site` |
| Codespace | Aktif — `npm run dev` port 3000'de çalışıyor |
| Menü Veri Kaynağı | ⬜ `menu-data.json` henüz üretilmedi — Oturum 2 |
| Görsel/Fotoğraf İçeriği | ⬜ Hâlâ bekleniyor — Hero'da placeholder kullanıldı |
| Üçüncü Parti Anahtarları | ⬜ Adisyo/SepetTakip, WhatsApp, Twilio — henüz temin edilmedi, ayrı faz |

---

## AÇIK SORUNLAR

| # | Öncelik | Açıklama | Oturum | Referans |
|---|---|---|---|---|
| 1 | 🔴 | Oturum 1 kodu tarayıcıda GÖRSEL OLARAK doğrulanmadı — sonraki sohbette ilk iş bu | Oturum 1 | — |
| 2 | 🟡 | Deploy platformu netleşmedi | Oturum 1 | CORE.md §2 |
| 3 | 🟡 | Gerçek menü/görsel verisi yok — Hero'da placeholder kullanıldı | Oturum 2 | MASTER_PLAN §8 |
| 4 | 🟡 | Üçüncü parti API anahtarları temin edilmedi | Sonraki Faz | MASTER_PLAN §8 |
| 5 | 🟢 | ARCHITECTURE.md §2.4 `calculateTotals`/`getTotals` isim tutarsızlığı — düzeltme bekliyor | Oturum 0 | DEPENDENCIES.md §1 |
| 6 | 🟢 | `next-env.d.ts` ve `package-lock.json` Codespaces'te otomatik üretildi, henüz commit edilmedi (2 değişiklik) | Oturum 1 | — |

---

## BOWLERA OTURUM DURUMU

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (14 dosya) | ✅ Üretildi — son onay bekliyor |
| **Oturum 1** | Next.js+Tailwind, font/renk, Header/Footer, Hero | 🟡 Kod push edildi — görsel doğrulama bekliyor |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard, statik menü verisi | ⬜ Bekliyor |
| **Oturum 3** | Zustand store + BowlCustomizer (4 adım, masaüstü) | ⬜ Bekliyor |
| **Oturum 4** | VisualPreview, mobil özelleştirici, sepet | ⬜ Bekliyor |
| **Kontrol Noktası** | Kullanıcı testi (5-10 kişi) | ⬜ Bekliyor |
| **Oturum 5** | Hakkımızda, Şubeler, İletişim, SEO, son kontrol | ⬜ Bekliyor |

---

## DOKÜMANTASYON DOSYA DURUMU

| Dosya | Durum | Son Güncelleme | Notlar |
|---|---|---|---|
| MASTER_PLAN.md | ✅ Onaylandı | 11 Temmuz 2026 (v2.0) | Kullanıcının Bowlera Master Teknik Referans belgesi v2.0 |
| CORE.md | ✅ Onaylandı | Session 1 | v1.0 — 11 bölüm |
| AGENT.md | ✅ Onaylandı | Session 1 | v1.0 — Kod kalitesi kuralları + BSC (8 güvenlik kuralı) |
| SESSION_INDEX.md | ✅ Onaylandı | Session 1 | Bu dosya |
| session_log.md | ⬜ Bekliyor | — | Çekirdek üçlü onaylandıktan sonra ilk blok açılacak |
| ARCHITECTURE.md | 🟡 Onay bekliyor | Session 1 | §2.4 isim düzeltmesi bekliyor (Açık Sorun #5) |
| DESIGN_SYSTEM.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| CUSTOMIZER_SPEC.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| DEPENDENCIES.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| ROADMAP.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| TEST_MATRIX.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| CONTENT_GUIDE.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| INTEGRATIONS.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| FAILURE_PATTERNS.md | 🟡 Onay bekliyor | Session 1 | v1.0 |
| CONFIG_SCHEMA.md | 🟡 Onay bekliyor | Session 1 | v1.0 |

> **14/14 dosya üretildi**, 4/14 onaylı. İçerik detayları için aşağıdaki GEÇMİŞ/ARŞİV bölümüne bakınız.

---

## ÜRETİLEN KOD DOSYALARI

| Dosya | Durum | Test | Repo |
|---|---|---|---|
| `app/layout.tsx`, `app/page.tsx`, `app/globals.css` | ✅ Üretildi | — | ✅ Push edildi |
| `tailwind.config.ts`, `lib/fonts.ts` | ✅ Üretildi | — | ✅ Push edildi |
| `components/layout/Header.tsx` | ✅ Üretildi | ✅ happy/edge/failure | ✅ Push edildi |
| `components/layout/Footer.tsx` | ✅ Üretildi | ✅ happy/edge/failure | ✅ Push edildi |
| `components/home/Hero.tsx` + alt bileşenler | ✅ Üretildi | ✅ happy/edge/failure | ✅ Push edildi |

---

## SIRADAKİ GÖREVLER

| Sıra | Görev | Öncelik | Durum |
|---|---|---|---|
| 1 | Çalışan sitenin ekran görüntüsüyle görsel doğrulama | 🔴 | ⬜ |
| 2 | `next-env.d.ts` + `package-lock.json` değişikliklerini commit et | 🟡 | ⬜ |
| 3 | ARCHITECTURE.md §2.4 isim düzeltmesi | 🟡 | ⬜ |
| 4 | Oturum 2 — Menü sayfası + `menu-data.json` (placeholder) | 🔴 | ⬜ |

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

---

*BOWLERA SESSION_INDEX.md — güncellendi, Session 1 — 2026-07-17*
