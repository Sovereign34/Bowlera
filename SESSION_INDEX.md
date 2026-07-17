# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Session 1'de ajan yürütme sistemi kuruluyor. MASTER_PLAN.md (kullanıcının
          Bowlera Master Teknik Referans v2.0 belgesi) proje köküne referans olarak
          yerleştirildi. CORE.md üretildi ve onaylandı — session açılış protokolü,
          proje kimliği, tetikleyici tablosu, dosya haritası, kritik tasarım/ürün
          varsayımları tanımlandı. AGENT.md üretildi ve onaylandı — kod kalitesi
          kuralları (Next.js/React'e uyarlanmış) + BSC (Bowlera Secure Code) 8
          kural: XSS sanitizasyonu, secret yönetimi, girdi doğrulama, hata yönetimi,
          sahte veri yasağı, sepet/customizer race condition koruması, üçüncü parti
          rate limit, entegrasyon kopmasında graceful degradation. Şimdi bu dosya
          (SESSION_INDEX.md) üretiliyor — çekirdek üçlü tamamlanıyor.
Faz:      Oturum 0 — Ajan Altyapısı Kurulumu (kod yazımı henüz başlamadı)
Gerekçe:  Kullanıcı NEXUS_OS metodolojisini örnek alarak Bowlera'ya özgü ajan
          yürütme dosyalarının sırayla (çekirdek önce, sonra referans dosyalar
          tek tek onaylı) üretilmesini istedi. Çekirdek üçlü (CORE+AGENT+
          SESSION_INDEX) bu sırada tamamlanıyor.
Çıktı:    MASTER_PLAN.md yerleştirildi. CORE.md ve AGENT.md ONAYLANDI.
          SESSION_INDEX.md üretim aşamasında — onay bekliyor.
```

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 1 — 2026-07-17 |
| Son Eylem | CORE.md ve AGENT.md üretildi, kullanıcı tarafından onaylandı. SESSION_INDEX.md üretiliyor. |
| Blocker | Yok |
| Devam Noktası | SESSION_INDEX.md onaylandıktan sonra referans dosyalara sırayla geçilecek: önce `ARCHITECTURE.md`. |

---

## GENEL DURUM

| Alan | Değer |
|---|---|
| Proje | Bowlera — Healthy Bowls |
| Aktif Oturum | Oturum 0 — Ajan Altyapısı Kurulumu |
| Toplam Session | 1 |
| Sistem Durumu | 🟡 Henüz kod yazılmadı — dokümantasyon/ajan altyapısı aşamasında |
| Deploy Durumu | ⬜ Belirlenmedi — Vercel muhtemel, kullanıcıyla netleştirilecek |
| Next.js Proje İskeleti | ⬜ Henüz oluşturulmadı |
| Menü Veri Kaynağı | ⬜ `menu-data.json` henüz üretilmedi — gerçek ürün/fiyat/kalori verisi bekleniyor |
| Görsel/Fotoğraf İçeriği | ⬜ Kullanıcıdan bekleniyor (MASTER_PLAN §8 notu) |
| Üçüncü Parti Anahtarları | ⬜ Adisyo/SepetTakip, WhatsApp, Twilio — henüz temin edilmedi, ayrı faz |

---

## AÇIK SORUNLAR

| # | Öncelik | Açıklama | Oturum | Referans |
|---|---|---|---|---|
| 1 | 🟡 | Deploy platformu netleşmedi (Vercel varsayımı doğrulanmalı) | Oturum 0 | CORE.md §2 |
| 2 | 🟡 | Gerçek menü verisi (fiyat, kalori, fotoğraf) henüz yok — `menu-data.json` placeholder ile kurulacak, TODO işaretli | Oturum 2 | MASTER_PLAN §8 |
| 3 | 🟡 | Üçüncü parti entegrasyon API anahtarları (Adisyo/SepetTakip, Twilio) henüz temin edilmedi — ayrı faz olarak planlı | Sonraki Faz | MASTER_PLAN §8 |

---

## BOWLERA OTURUM DURUMU

> MASTER_PLAN.md §8'deki 5 oturumluk inşa planına dayanır. Detaylı görev/kabul
> kriterleri ROADMAP.md onaylandığında bu tablo o dosyayla senkronize edilecek.

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (CORE/AGENT/SESSION_INDEX + referans dosyalar) | 🟡 Devam ediyor |
| **Oturum 1** | Next.js + Tailwind kurulumu, font/renk sistemi, Header/Footer, Ana Sayfa hero | ⬜ Bekliyor |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard (kalori/alerjen dahil), statik menü verisi | ⬜ Bekliyor |
| **Oturum 3** | Zustand store kurulumu + BowlCustomizer akışı (4 adım, masaüstü) | ⬜ Bekliyor |
| **Oturum 4** | VisualPreview (katmanlı CSS/SVG), mobil özelleştirici uyarlaması, sepet | ⬜ Bekliyor |
| **Kontrol Noktası** | Kullanıcı testi (5-10 kişi) — customizer akışı canlıya alınmadan önce | ⬜ Bekliyor |
| **Oturum 5** | Hakkımızda, Şubeler, İletişim + JSON-LD/SEO + performans/responsive son kontrol | ⬜ Bekliyor |

---

## DOKÜMANTASYON DOSYA DURUMU

| Dosya | Durum | Son Güncelleme | Notlar |
|---|---|---|---|
| MASTER_PLAN.md | ✅ Mevcut | 11 Temmuz 2026 (v2.0) | Kullanıcının Bowlera Master Teknik Referans belgesi — referans, tam okundu |
| CORE.md | ✅ Onaylandı | Session 1 | v1.0 — 11 bölüm, NEXUS_OS'tan Bowlera'ya uyarlandı |
| AGENT.md | ✅ Onaylandı | Session 1 | v1.0 — Kod kalitesi kuralları + BSC modülü (8 güvenlik kuralı) |
| SESSION_INDEX.md | 🟡 Üretim aşamasında | Session 1 | Bu dosya — onay bekliyor |
| session_log.md | ⬜ Bekliyor | — | Çekirdek üçlü onaylandıktan sonra ilk blok açılacak |
| ARCHITECTURE.md | ⬜ Bekliyor | — | Sırada — Next.js yapısı, komponent kontratları, veri modeli |
| DESIGN_SYSTEM.md | ⬜ Bekliyor | — | Renk/tipografi/animasyon/fotoğraf standartları (MASTER_PLAN §4) |
| CUSTOMIZER_SPEC.md | ⬜ Bekliyor | — | "Kâseni Yarat" akışı tam kontratı (MASTER_PLAN §3.3, §5.2) |
| CONTENT_GUIDE.md | ⬜ Bekliyor | — | Marka sesi, SEO, JSON-LD (MASTER_PLAN §6, §7) |
| INTEGRATIONS.md | ⬜ Bekliyor | — | Adisyo/SepetTakip, WhatsApp, QR menü (MASTER_PLAN §5.6) |
| DEPENDENCIES.md | ⬜ Bekliyor | — | Dosya/bileşen bağımlılık haritası |
| FAILURE_PATTERNS.md | ⬜ Bekliyor | — | Sepet/checkout/entegrasyon hata kalıpları |
| ROADMAP.md | ⬜ Bekliyor | — | 5 oturumluk inşa sırası + kabul kriterleri (MASTER_PLAN §8) |
| TEST_MATRIX.md | ⬜ Bekliyor | — | Modül bazlı test takibi |
| CONFIG_SCHEMA.md | ⬜ Bekliyor | — | `.env.local` şeması |

> **3/14 dosya tamamlandı** (MASTER_PLAN + CORE + AGENT). SESSION_INDEX onayla 4/14 olacak.

---

## ÜRETİLEN KOD DOSYALARI

> Henüz kod üretimi başlamadı — bu bölüm Oturum 1'den itibaren doldurulacak.

*(Boş — ilk kod dosyası ARCHITECTURE.md onaylandıktan ve Oturum 1 başladıktan sonra burada listelenecek.)*

---

## SIRADAKİ GÖREVLER

| Sıra | Görev | Öncelik | Durum |
|---|---|---|---|
| 1 | CORE.md üretimi | 🔴 | ✅ |
| 2 | AGENT.md üretimi | 🔴 | ✅ |
| 3 | SESSION_INDEX.md üretimi | 🔴 | 🟡 Onay bekliyor |
| 4 | ARCHITECTURE.md üretimi | 🔴 | ⬜ |
| 5 | DESIGN_SYSTEM.md üretimi | 🟠 | ⬜ |
| 6 | CUSTOMIZER_SPEC.md üretimi | 🟠 | ⬜ |
| 7 | CONTENT_GUIDE.md üretimi | 🟡 | ⬜ |
| 8 | INTEGRATIONS.md üretimi | 🟡 | ⬜ |
| 9 | DEPENDENCIES.md üretimi | 🟡 | ⬜ |
| 10 | FAILURE_PATTERNS.md üretimi | 🟡 | ⬜ |
| 11 | ROADMAP.md üretimi | 🟠 | ⬜ |
| 12 | TEST_MATRIX.md üretimi | 🟡 | ⬜ |
| 13 | CONFIG_SCHEMA.md üretimi | 🟡 | ⬜ |
| 14 | Ajan altyapısı tamamlandıktan sonra: Next.js proje iskeleti (Oturum 1) | 🔴 | ⬜ |

---

*BOWLERA SESSION_INDEX.md — güncellendi, Session 1 — 2026-07-17*
