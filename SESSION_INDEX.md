# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> **Şişmeyi önleme yöntemi:** Bu dosya SADECE anlık durumu tutar — tamamlanmış görevler
> Açık Sorunlar tablosundan silinir. Turn-by-turn geçmiş (📜 GEÇMİŞ/ARŞİV) burada TUTULMAZ,
> `session_log.md`'ye taşınır (CORE.md §1 Adım 2 — session_log.md zaten "sadece gerekince
> istenir" olarak tanımlı, otomatik her session'da yüklenmez). Bu, arşivi SİLMEK değil
> DOĞRU DOSYAYA TAŞIMAK'tır — arşiv hâlâ TAM içerikle, güvenilir tek kaynakta duruyor.
> ⚠️ Bu ayrım netleştirilmeden önce (2026-07-20) bir sürüm arşivi hem taşımadan hem
> silmeden "eski dosyaya bakılmalı" diyerek kırpmıştı — bu AGENT.md Kural #4 ihlaliydi ve
> düzeltildi. Farkı unutma: session_log.md'ye TAŞI, asla sadece REFERANS VERİP silme.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 4 devam ediyor. En son bilinen (özet düzeyinde) durum: Header hesap
          ikonu oturum-farkında hale getirildi (SessionProvider + useSession()), bu
          Header.test.tsx'i kırdı, vi.mock('next-auth/react') ile düzeltildi; aynı
          testte gizli kalmış eski bir stale-assertion sorunu da bulunup düzeltildi.
          Bu turda ayrıca #41, #37, #26, #36, #33, #40 "kapandı" olarak işaretlendi
          — ANCAK bu kapanışların turn-by-turn kaydı hiçbir dosyada yok (bkz. #42).
Blokaj:   🟠 Twilio TR SMS kısıtı (#32) — projenin TEK KALAN büyük darboğazı, kullanıcı
          ödemeyi henüz yapmadığı için bilinçli parklı. Auth + /hesap uçtan uca canlı
          test hâlâ bu kısıta takılıyor.
Sıradaki: (1) Twilio kararı (#32), (2) Beşinci Bölüm'ün eksik kaydını tamamla — #42,
          (3) ARCHITECTURE.md §2.4'ü 5 adıma güncelle (#10), (4) kategori enum
          uyuşmazlığı (#35), (5) ProfileForm Tailwind teyidi (#38).
```

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI (özet — sadece hâlâ etkili olanlar)

| # | Karar | Durum |
|---|---|---|
| 1 | Customizer 5 adım: Base → Main → Garden → Signature Flavor → Finish | ✅ Uygulandı |
| 3-4 | Garden: ilk 4 ücretsiz + avokado her zaman ücretli / Finish: ilk 1 ücretsiz | ✅ Uygulandı |
| 5 | "Make it Yours" → Finish'e entegre, "Double Main" → `mainPortion` yeniden kullanır | ✅ Uygulandı |
| 6 | Slogan: "Sağlıklı Beslen, Sağlıklı Yaşa, Gücünü Hisset" | ✅ |
| 13 | `FulfillmentChannel`: `"pickup"` \| `"dine-in"` (delivery yok), sepet/oturum seviyesinde tek alan | ✅ Canlıda doğrulandı |
| 14-16 | `â` karakteri kaldırıldı (menu-data.json, CartDrawer). Hero.tsx/StepBase.tsx bilinçli ertelendi (#27) | ✅ Canlıda doğrulandı |
| 15 | Customizer malzeme isimleri Türkçeye çevrildi (id'ler değişmedi) | ✅ Canlıda doğrulandı |
| 18 | CartDrawer portal fix (`createPortal` → `document.body`, backdrop-blur containing-block bug'ı için) | ✅ Canlıda doğrulandı |
| 19→20 | Auth: Twilio Verify + Auth.js JWT. DB: Neon Postgres (Vercel Marketplace), `users` tablosu (`phone`,`address`,`displayName`,`loyaltyPoints`,`verifiedAt`) | ✅ Kurulum tamam, build yeşil |
| 21-22 | Auth kod (route'lar, `auth.ts`, DB katmanı) + görünür giriş UI (`/giris`) | ✅ Kod tamam, `/giris` canlı doğrulandı; OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor |
| 23 | Adres/profil modeli: adres SADECE profil/sadakat verisi, checkout'u bloklamaz, `/hesap`'ta opsiyonel toplanır | ✅ Kod üretildi. ⚠️ Repo push durumu bir aşamada YANLIŞ raporlanmıştı (#41'in kökeni) — bkz. session_log.md, Dördüncü Bölüm |

*(Tam gerekçe/tarih dökümü ve kapanmış eski kararlar için: `session_log.md`.)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor — 5 adıma hiç güncellenmedi (bilinçli kapsam dışı) | `ARCHITECTURE.md` §2.4, `CUSTOMIZER_SPEC.md` §3.1 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi | `lib/customizer-data.ts`, `lib/menu-data.json` |
| 27 | 🟢 | Hero.tsx CTA'sı ve StepBase.tsx açıklaması hâlâ `â` içeriyor (bilinçli ertelendi) | `components/home/Hero.tsx`, `StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce; `CUSTOMIZER_SPEC.md` §2 senkron değil | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — hem auth hem `/hesap` akışını canlıda test edilemez kılıyor. Çözüm: ücretli plan veya Netgsm/İleti Merkezi. Kullanıcı kararıyla parklandı. | Twilio Console |
| 35 | 🟡 | `BowlItem.category` enum'ı MASTER_PLAN §3.2 ile uyuşmuyor | `types/index.ts`, `lib/menu-filters.ts` |
| 38 | 🟢 | `ProfileForm.tsx` Tailwind sınıfları (`bg-olive-600` vb.) DESIGN_SYSTEM.md ile teyit edilmedi | `components/account/ProfileForm.tsx` |
| 39 | 🟠 | `/hesap` akışı Twilio kısıtı yüzünden canlıda hiç fonksiyonel test edilemedi | `app/hesap/page.tsx` |
| 42 | 🟡 | Beşinci Bölüm'ün (#26/#33/#36/#37/#40/#41 kapanışları) turn-by-turn kaydı hiçbir dosyada yok — sadece özet var, teyit edilmeli | Bu dosya, `session_log.md` (Beşinci Bölüm notu) |

> **KAPANDI (özet düzeyinde, teyit bekliyor — bkz. #42):** #41 (repo/SESSION_INDEX
> tutarsızlığı), #37 (profile route rate-limit), #26 (teslimat kanalı checkout'ta zorunlu
> değildi → `app/siparis/page.tsx` vb.), #36 (ARCHITECTURE.md senkron değildi), #33 (Header
> hesap ikonu oturum-farkında değildi), #40 (Header.test.tsx, iki parça). Detaylar ve hangi
> bölümde neyin bulunduğu için: `session_log.md`.

---

## SESSION ÖZET (son 5)

| Session | Tarih | Ana içerik | Durum |
|---|---|---|---|
| 0 | — | Ajan altyapısı (14 dosya) | ✅ Tamamlandı |
| 1 | 2026-07-1x | Next.js+Tailwind kurulum, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| 2 | 2026-07-18 | Menü sayfası, filtreleme, MenuCard, statik veri, CategoryNav+FilterPanel, customizer 4→5 adım kararı | ✅ Tamamlandı |
| 3 | 2026-07-18 | Zustand store + pricing + customizer data, masaüstü UI bileşenleri (kesintiye uğradı) | ✅ Büyük ölçüde tamam |
| 4 (devam) | 2026-07-18 → 07-19 (5 bölüm) | Sepet/kanal seçimi, Türkçeleştirme, â düzeltmesi, CartDrawer bugfix, auth mimarisi+kod+DB+UI, adres/profil (#23), test triyajı, menü animasyonu, ARCHITECTURE.md v1.3, rate-limit üretimi, repo tutarsızlığı keşfi (#41), [özet düzeyinde] #26/#33/#36/#37/#40/#41 kapanışı | 🟡 Devam ediyor — Twilio (#32) tek darboğaz; Beşinci Bölüm kaydı eksik (#42) |

*(Tam turn-by-turn detay: `session_log.md`.)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — ⚠️ SESSION_INDEX'in fiili repo durumunu EN AZ BİR KEZ yanlış yansıttığı kanıtlandı (#41 kökeni). Yeni dosya varlığı iddiaları temkinli ele alınmalı. |
| Test Suite | 🟢 Özet düzeyinde: `Header.test.tsx` 3/3 canlı doğrulandı. Genel `npm test` bu aralıkta tekrar çalıştırılmadı — bir sonraki tam çalıştırmada teyit edilmeli. |
| Auth | 🟢 Kod tamam, `/giris` canlı doğrulandı. 🟠 OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor (#32) |
| Kullanıcı Profili/Adres | 🟢 Kod tamam. Özet düzeyinde repoda doğrulandı (#41 kapandı) — teyit gerekir (#42) |
| Checkout (`/siparis`) | Özet düzeyinde: kanal seçimi zorunlu kılındığı belirtiliyor (#26 kapandı) — üretim süreci hiç belgelenmemiş, teyit gerekir (#42) |
| Veritabanı | 🟢 Neon Postgres çalışıyor |
| ARCHITECTURE.md | v1.3 taslağı üretildi ama push edilmedi; özet düzeyinde sonradan "v1.4, senkron" denmiş (#36 kapandı) — ara adım belgelenmemiş, teyit gerekir (#42) |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | Twilio kararı: ücretli plan veya yerel sağlayıcı — TEK büyük darboğaz (#32, parklandı) | 🟠 |
| 2 | Beşinci Bölüm'ün eksik kaydını tamamla — #26/#33/#36/#37/#40/#41 kapanışlarını repo/canlı durumla yeniden teyit et (#42) | 🟡 |
| 3 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a güncelle (#10) | 🟡 |
| 4 | Kategori enum uyuşmazlığı (#35) | 🟡 |
| 5 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 6 | ProfileForm Tailwind sınıflarını DESIGN_SYSTEM.md ile teyit et (#38) | 🟢 |
| 7 | Genel `npm test` çalıştırıp güncel geçen/kalan sayıyı teyit et | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v3, arşiv `session_log.md`'ye taşındı (silinmedi). Sadece anlık
durum + açık borçlar tutulur. Tam geçmiş için `session_log.md`'ye bakılmalı (CORE.md §1,
Adım 2 — otomatik yüklenmez, sadece gerekince istenir). Güncellenme: 2026-07-21.*
