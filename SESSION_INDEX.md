# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Çekirdek üçlü (CORE.md + AGENT.md + SESSION_INDEX.md) onaylandı.
          Kullanıcı isteğiyle üretim temposu "üçer üçer" olarak değiştirildi.
          İlk üçlü referans paketi üretildi: ARCHITECTURE.md (Next.js App
          Router yapısı, modül kontratları — API route/store/component
          interface'leri, BowlItem/CartItem veri modeli, deploy/performans/
          rollback), DESIGN_SYSTEM.md (renk sistemi WCAG tablosu, logo
          degrade sınırlı kullanım kuralı, tipografi, ikonografi, fotoğraf
          direktifi, tam animasyon tablosu + erişilebilirlik kuralları),
          CUSTOMIZER_SPEC.md ("Kâseni Yarat" tam kontratı — 4 adım state
          makinesi, adım geçiş guard'ı, canlı fiyat/kalori hesaplama,
          VisualPreview katmanlı CSS/SVG mantığı, mobil sticky çekmece UX,
          BSC-6 race condition korumalı sepete ekleme).
Faz:      Oturum 0 — Ajan Altyapısı Kurulumu (kod yazımı henüz başlamadı)
Gerekçe:  Kullanıcı NEXUS_OS metodolojisini örnek alarak Bowlera'ya özgü ajan
          yürütme dosyalarının üretilmesini istedi; onay temposu tek tek
          dosyadan üçlü gruplara güncellendi.
Çıktı:    MASTER_PLAN.md + CORE.md + AGENT.md + SESSION_INDEX.md ONAYLANDI.
          ARCHITECTURE.md + DESIGN_SYSTEM.md + CUSTOMIZER_SPEC.md üretim
          aşamasında — onay bekliyor.
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
| ARCHITECTURE.md | 🟡 Üretim aşamasında | Session 1 | v1.0 — Next.js yapısı, modül kontratları, veri modeli, deploy/rollback — onay bekliyor |
| DESIGN_SYSTEM.md | 🟡 Üretim aşamasında | Session 1 | v1.0 — Renk/tipografi/animasyon/fotoğraf standartları (MASTER_PLAN §4) — onay bekliyor |
| CUSTOMIZER_SPEC.md | 🟡 Üretim aşamasında | Session 1 | v1.0 — "Kâseni Yarat" akışı tam kontratı (MASTER_PLAN §3.3, §5.2) — onay bekliyor |
| CONTENT_GUIDE.md | ⬜ Bekliyor | — | Marka sesi, SEO, JSON-LD (MASTER_PLAN §6, §7) |
| INTEGRATIONS.md | ⬜ Bekliyor | — | Adisyo/SepetTakip, WhatsApp, QR menü (MASTER_PLAN §5.6) |
| DEPENDENCIES.md | ⬜ Bekliyor | — | Dosya/bileşen bağımlılık haritası |
| FAILURE_PATTERNS.md | ⬜ Bekliyor | — | Sepet/checkout/entegrasyon hata kalıpları |
| ROADMAP.md | ⬜ Bekliyor | — | 5 oturumluk inşa sırası + kabul kriterleri (MASTER_PLAN §8) |
| TEST_MATRIX.md | ⬜ Bekliyor | — | Modül bazlı test takibi |
| CONFIG_SCHEMA.md | ⬜ Bekliyor | — | `.env.local` şeması |

> **4/14 dosya onaylandı** (MASTER_PLAN + CORE + AGENT + SESSION_INDEX). 3 dosya daha onay bekliyor
> (ARCHITECTURE + DESIGN_SYSTEM + CUSTOMIZER_SPEC) — onaylanırsa 7/14 olacak.

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
| 3 | SESSION_INDEX.md üretimi | 🔴 | ✅ |
| 4 | ARCHITECTURE.md üretimi | 🔴 | 🟡 Onay bekliyor |
| 5 | DESIGN_SYSTEM.md üretimi | 🟠 | 🟡 Onay bekliyor |
| 6 | CUSTOMIZER_SPEC.md üretimi | 🟠 | 🟡 Onay bekliyor |
| 7 | CONTENT_GUIDE.md üretimi (sıradaki üçlü) | 🟡 | ⬜ |
| 8 | INTEGRATIONS.md üretimi (sıradaki üçlü) | 🟡 | ⬜ |
| 9 | DEPENDENCIES.md üretimi (sıradaki üçlü) | 🟡 | ⬜ |
| 10 | FAILURE_PATTERNS.md üretimi | 🟡 | ⬜ |
| 11 | ROADMAP.md üretimi | 🟠 | ⬜ |
| 12 | TEST_MATRIX.md üretimi | 🟡 | ⬜ |
| 13 | CONFIG_SCHEMA.md üretimi | 🟡 | ⬜ |
| 14 | Ajan altyapısı tamamlandıktan sonra: Next.js proje iskeleti (Oturum 1) | 🔴 | ⬜ |

---

*BOWLERA SESSION_INDEX.md — güncellendi, Session 1 — 2026-07-17*
