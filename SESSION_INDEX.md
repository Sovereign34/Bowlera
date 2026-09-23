# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> **Şişmeyi önleme yöntemi:** Bu dosya SADECE anlık durumu tutar — tamamlanmış görevler
> Açık Sorunlar tablosundan silinir. Turn-by-turn geçmiş (📜 GEÇMİŞ/ARŞİV) burada TUTULMAZ,
> `session_arşiv.md` / `session_arşiv_1.md` / `session_arşiv_2.md`'ye taşınır. Bu, arşivi
> SİLMEK değil DOĞRU DOSYAYA TAŞIMAK'tır. **[Session 12 devamı, 2026-08-08]:** Arşiv önce
> İKİ dosyaya bölünmüştü — Session 0-10 → `session_arşiv.md`, Session 11'den 2026-08-10'a
> kadar → `session_arşiv_1.md`. **[2026-08-11 güncellemesi]:** `session_arşiv_1.md` da
> hacimce şişince ÜÇÜNCÜ bir dosya açıldı — 2026-08-11'den itibaren → `session_arşiv_2.md`
> (ilişki notu o dosyanın başlığında). Bölünme sadece hacim nedeniyledir, kural değişmedi.
> > ⚠️ **DERS ARŞİVİ NOTU (2026-09-23 güncellemesi):** Bu dosyanın başında önceden 7 ayrı "DERS" (İkinci-Yedinci) + birden fazla "TAŞIMA UYARISI/NOTU" bloğu (toplam ~87 satır) tutuluyordu. Hepsi zaten `session_arşiv_1.md`/`session_arşiv_2.md`'ye TAM metinle taşınmıştı (bkz. Arşiv Taşıma Kaydı tablosu) ve buradaki kopyaları sadece tekrar niteliğindeydi — 400 satır eşiğini (CORE.md §7.1 Adım 1) aşmanın başlıca nedeniydi. Bu turda tek satıra indirildi: ders özetleri (checkpoint sıklığı, "kod≠kullanıcı deneyimi", TAM DOSYA üretimi yarım bırakılmaz, vb.) hâlâ AGENT.md/CORE.md'ye işli ve geçerlidir, sadece bu dosyadaki tekrar kaldırıldı. Tam metin: `session_arşiv_2_EKLENTI_2026-09-23-ders-arsivi.md` (kullanıcı elle `session_arşiv_2.md`'nin sonuna ekleyecek).
---

## 🎯 CURRENT FOCUS

> **[GÜNCEL — 2026-09-07, 28. sohbet]** Admin panelde ilk gerçek kullanıcı testi yapıldı —
> yeni ürün ("Fogy") oluşturuldu. **2 bulgu ortaya çıktı:**
> 1. **Sitede görünmüyor — BEKLENEN, hata değil.** Canlı site hâlâ statik `menu-data.json`'dan
>    okuyor, `menu_items` DB'sine bağlanmadı (bilinçli olarak ayrı bırakılan bir görev).
> 2. **Admin listesinde de görünmüyordu — GERÇEK BUG, BULUNDU VE DÜZELTİLDİ.** Neon'da
>    `SELECT` ile kayıt DB'ye YAZILMIŞ olduğu doğrulandı (`fogy-izzbw`, 2026-09-07 03:34) —
>    yani sorun kayıtta değil, `app/admin/page.tsx`'in Next.js tarafından **build-anı statik
>    önbellek** olarak dondurulmasıydı (server component DB'den okuyor ama `dynamic` export'u
>    yoktu). `export const dynamic = 'force-dynamic'` hem liste sayfasına hem düzenleme
>    sayfasına eklendi — kullanıcı henüz repoya uygulayıp push ETMEDİ, canlı doğrulama
>    BEKLİYOR (bkz. Açık Sorun #114).
>
> **[ÖNCEKİ — 2026-09-06, 27. sohbet]** Admin Panel CANLIYA ALINDI. #110/#112 KAPANDI (4
> senkron dosya repoya uygulandı, `role='admin'` Neon'da atandı ve canlıda doğrulandı).
> Kullanıcı kararıyla admin artık `/personel`'e de erişiyor (middleware'in staff guard'ı
> `role !== 'staff' && role !== 'admin'` olarak genişletildi — `/admin` guard'ı hâlâ SADECE
> `admin`'e özel, tek-admin kararı korundu). #111/#113 KAPANDI — ilk CRUD (9 dosya: upload-
> image + menu-items list/create/update/delete route'ları + MenuItemForm + 3 admin sayfası)
> yazıldı, ImageKit hesabı açılıp entegre edildi. Yol boyunca 3 build hatası çıktı, hepsi
> çözüldü (eksik `imagekit` npm paketi, TS literal-tipi `.includes()` hatası, ilk pushta
> unutulan `app/admin/page.tsx`). `/admin` canlıda 8 gerçek ürünü doğru isim/fiyat/kategoriyle
> listeliyor. Kozmetik, önemsiz bir detay: admin listesindeki `<img>` önizlemeleri kırık ikon
> gösteriyor (`menu_items.image` alanı `/public`'ten okunan bir dosya adı, admin bu yola
> giremiyor).

> **[TAŞINDI, çeşitli tarihler]** 26., 22., 21., 20., 19. ve 18./17. sohbetlerin ayrıntılı anlatı blokları (Admin Panel planlaması, sandviç UI/checkout keşfi, CRM/çok-şubeli vizyon, SANDWICH_SPEC üretimi, güvenlik denetimi ve masaüstü sığdırma detayları) `session_arşiv_2.md`'ye taşındı — hepsi aşağıdaki Arşiv Taşıma Kaydı tablosunda ve ilgili Açık Sorun/Kritik Kararlar satırlarında (bkz. #90-#113) zaten tam özetli, aktif takip için gerekli değil.

### 📦 Arşiv Taşıma Kaydı (CORE.md §7.1 Adım 1.5 gereği tek satır/taşıma)

| Tarih | Taşınan | Hedef | Durum |
|---|---|---|---|
| 2026-08-09 | 6 blok (#62 kod kapanışı, BEŞİNCİ DERS, `users.role` migration, şema notu, masa no kararı, channel-options.ts kırığı) | `session_arşiv.md` | ✅ Kritik Kararlar/GENEL DURUM'da özetli |
| 2026-08-09 (devamı) | 2 blok (#74-78 açılışı, #76+#77 kapanışı) + eski kapanış anlatısı (#59/#72/users.role/1d) | `session_arşiv_1.md` | ✅ Açık Sorunlar/Kritik Kararlar'da özetli |
| 2026-08-10 | 3 blok (#74 çıkış butonu, #62 Masaya tam kapanış, #79 masaüstü fix) | `session_arşiv_1.md` | ✅ özetli. ⚠️ Eklenti (`session_arsiv_1_EKLENTI_2026-08-10.md`, 4 blok) HÂLÂ `session_arşiv_1.md`'nin sonuna eklenmemiş |
| 2026-08-11 | #85 bloğu (İLK taşıma, session_arşiv_2.md'yi açan blok) | `session_arşiv_2.md` | ✅ Açık Sorun #85/Kritik Kararlar'da özetli, TAM dosya olarak verildi |
| 2026-08-11 (3. kez) | Sekme rozetleri + DESIGN_SYSTEM.md §2.2 istisnası | `session_arşiv_2.md` (eklenti: `..._EKLENTI_2026-08-11.md`) | ✅ Açık Sorun #88'de özetli |
| 2026-08-11 (devamı) | 1b(ii) kapsam-dışı kararı | `session_arşiv_2.md` (iddia edilen) | ⚠️ **DOĞRULANAMADI** — 2026-08-13 taramasında bu blok `session_arşiv_2.md` içinde bulunamadı, muhtemelen eklenti hiç üretilmedi/eklenmedi. Karar Kritik Kararlar tablosunda ve Açık Sorun #66'da özetli, içerik kaybı değil, sadece turn-by-turn anlatı eksik |
| 2026-08-11 (devamı, 4. kez) | #86 Kayıt Onayları (build doğrulandı notu) | `session_arşiv_2.md` (eklenti: `..._EKLENTI_2026-08-11-devam4.md`) | ✅ Açık Sorun #86'da özetli |
| 2026-08-12 | #89 bloğu (IP delili + engellenen deneme logu) | `session_arşiv_2.md` (eklenti: `..._EKLENTI_2026-08-12.md`) | ✅ Kritik Kararlar/#89'da özetli |
| 2026-08-12 (3. kez) | #38 bloğu (RegistrationForm kod+push) | `session_arşiv_2.md` (eklenti: `..._EKLENTI_2026-08-12-devam3.md`) | ✅ Açık Sorun #38'de özetli |
| 2026-08-12 (devamı) | Gel Al 3-durumlu revizyon (KARAR A) | `session_arşiv_2.md` (eklenti: `..._EKLENTI_2026-08-12-devam2.md`) | ✅ Kritik Kararlar/#62/GENEL DURUM'da özetli |
| 2026-09-03 | 3 blok (19. sohbet CRM keşfi, 20. sohbet SANDWICH_SPEC üretimi, 22. sohbet geriye-dönük sandviç UI/checkout bulgusu) | `session_arşiv_2.md` (eklenti: `session_arsiv_2_EKLENTI_2026-09-03.md`) | ⚠️ TAM metinle üretildi, kullanıcı henüz `session_arşiv_2.md`'nin sonuna eklemedi — Açık Sorunlar #92/#93/#94/#95/#99-104'te özetli |
| 2026-08-23 | 2 blok (18. sohbet #91 detayı, 17. sohbet #90 detayı) + 5 "KAPANDI (BU TURDA)" anlatı bloğu (#82/83/84, #74, #79/75/80, #50, #76/77) | `session_arşiv_2.md` (eklenti: `session_arsiv_2_EKLENTI_2026-08-23.md`, 2 blok halinde) | ✅ Açık Sorunlar/Kritik Kararlar'da özetli, TAM metinle taşındı |
| 2026-08-23 (22. sohbet, 2. taşıma) | SEKİZİNCİ DERS (21. sohbet) tam anlatı bloğu | `session_arşiv_2.md` (eklenti: `session_arsiv_2_EKLENTI_2026-08-23-devam2.md`) | ✅ Açık Sorunlar #95/#96/#97/#98'de özetli, TAM metinle taşındı |
| 2026-09-05 (25. sohbet) | 23. sohbet devamı — MOTION SYSTEM Mobil Tactile Düzeltmesi anlatısı (MenuCard whileTap kararı) | `session_arşiv_2.md` (eklenti: `session_arsiv_2_EKLENTI_2026-09-05.md`) | ⚠️ TAM metinle üretildi, kullanıcı henüz `session_arşiv_2.md`'nin sonuna eklemedi — #107 (KAPANDI) ve Motion System P0 bölümünde özetli |
| 2026-09-07 (28. sohbet) | 26. sohbetin Admin Panel planlaması tam anlatısı | `session_arşiv_2.md` (eklenti: `session_arsiv_2_EKLENTI_2026-09-07.md`) | ⚠️ TAM metinle üretildi, kullanıcı henüz `session_arşiv_2.md`'nin sonuna eklemedi — Kritik Kararlar ve Açık Sorunlar #108-#113'te özetli |
| 2026-09-23 (bu turda) | Header ders/taşıma-uyarı bloğu (7 DERS + çoklu TAŞIMA NOTU, 87 satır) + CURRENT FOCUS'taki çoklu TAŞINDI anlatısı + v75-v79 footer sürüm notları (toplam ~150 satır) | `session_arşiv_2.md` (eklenti: `session_arsiv_2_EKLENTI_2026-09-23-ders-arsivi.md` + `..._versiyon-notlari.md`) | ⚠️ TAM metinle üretildi, kullanıcı henüz `session_arşiv_2.md`'nin sonuna eklemedi — ders özetleri AGENT.md/CORE.md'de geçerliliğini koruyor, kayıp yok |

> ⚠️ **Bekleyen eklemeler (kullanıcı elle eklemeli):** `session_arsiv_1_EKLENTI_2026-08-10.md`,
> `session_arsiv_2_EKLENTI_2026-08-11.md`, `..._EKLENTI_2026-08-11-devam4.md`,
> `..._EKLENTI_2026-08-12.md`, `..._EKLENTI_2026-08-12-devam2.md`, `..._EKLENTI_2026-08-12-devam3.md`,
> `session_arsiv_2_EKLENTI_2026-08-23.md`, `..._EKLENTI_2026-08-23-devam2.md`,
> `..._EKLENTI_2026-09-03.md`, `..._EKLENTI_2026-09-05.md`
> — bunların hangileri fiilen ilgili arşiv dosyasının sonuna eklendi, teyit edilmeli.

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI (özet — hâlâ etkili olanlar + yeniden teyit edilmesi gerekenler)

| # | Karar | Durum |
|---|---|---|
| 1 | Customizer 5 adım: Base → Main → Garden → Signature Flavor → Finish | ✅ Uygulandı |
| 3-4 | Garden: ilk 4 ücretsiz + avokado her zaman ücretli / Finish: ilk 1 ücretsiz | ✅ Uygulandı |
| 5 | "Make it Yours" → Finish'e entegre, "Double Main" → `mainPortion` yeniden kullanır | ✅ Uygulandı |
| 6 | Slogan: "Sağlıklı Beslen, Sağlıklı Yaşa, Gücünü Hisset" | ✅ |
| 13 | `FulfillmentChannel`: `"pickup"` \| `"dine-in"` (delivery yok), sepet/oturum seviyesinde tek alan | ✅ Canlıda doğrulandı. |
| 14-16 | `â` karakteri kaldırıldı (menu-data.json, CartDrawer). Hero.tsx/StepBase.tsx bilinçli ertelendi (#27) | ✅ |
| 18 | CartDrawer portal fix (`createPortal` → `document.body`) | ✅ Canlıda doğrulandı |
| 19→20 | Auth: Twilio Verify + Auth.js JWT. DB: Neon Postgres, `users` tablosu | ✅ Kurulum tamam, build yeşil. |
| 21-22 | Auth kod + görünür giriş UI | 🟡 **[Session 8]** Eski `/giris` KALDIRILDI, `/kayit-ol`'a redirect ediyor. |
| 23 | Adres/profil modeli: adres SADECE profil/sadakat verisi, checkout'u bloklamaz | ✅ Kod üretildi VE repo varlığı doğrulandı |
| 🆕 | Alerjen gösterimi: kalori/protein ile aynı zorunluluk statüsü | ✅ (#7 ve #44 kapandı) |
| 🆕 | **[Session 7]** `consentRegistrations` tablosu, `users`'tan AYRI | ✅ Kod+şema+test tamam, migration canlıda ÇALIŞTIRILDI. |
| 🆕 | **[Session 7]** `RegistrationChannel` tipi (`masaya-siparis`\|`gel-al`\|`online-platform`), `FulfillmentChannel`'DAN AYRI | ✅ Kod+şema+test tamam. |
| 🆕 | **[Session 11]** Genel giriş akışı: girişsiz gezinme → ürün SEÇİNCE giriş sayfası → giriş/kayıt seçimi | ✅ Karar netleşti, henüz KODLANMADI |
| 🆕 | **[Session 11]** Kayıtta bilgi+KVKK sonrası, giriş sağlanmadan ÖNCE kanal seçimi ZORUNLU | ✅ Karar netleşti, henüz KODLANMADI |
| 🆕 | **[Session 11, KRİTİK]** "Kasa paneli" = Personel Sipariş Paneli (#62), TEK panel — Masaya gerçek-zamanlı akışı + Gel Al ilk-sipariş manuel onay kuyruğu | 🟡 Kapsam + mimari kararlar netleşti, kod HENÜZ YAZILMADI |
| 🆕 | **[Session 11 devamı, #64 KAPANDI]** Gel Al onayı SADECE ilk siparişte — doğrulama durumu alanı (`pending`/`confirmed`) tutulur | ✅ Karar netleşti, #62 tasarımına eklendi, henüz KODLANMADI |
| 🆕 | **[Session 12 devamı, KRİTİK — ARCHITECTURE.md v1.7]** Masaya Sipariş genel giriş/kayıt akışından TAMAMEN AYRILDI, ayrı `/masaya-siparis/*` yüzeyine taşındı (auth gerektirmez, guest-istisnası mekanizması yerine mimari izolasyon). `useCartStore` PAYLAŞILIR (ayrı state kurulmadı). Middleware'e YENİ istisna GEREKMİYOR — bu nedenle #65 KAPANDI. | ✅ Karar netleşti (ARCHITECTURE.md v1.7), henüz KODLANMADI |
| 🆕 | **[Session 12 devamı, #67 KAPANDI — ARCHITECTURE.md v1.8]** `/masaya-siparis` KENDİ BAĞIMSIZ mini-checkout'unu kullanacak — `/siparis`'in (§2.9, Gel Al'a özel) varyantı OLMAYACAK. Gerekçe: Gel Al'a özel mantığın (hesap girişi, ilk-sipariş manuel onay) Masaya'ya sızma riskini önlemek. Fiyat/özet gösterimi paylaşılabilir, checkout akışı paylaşılmayacak. | ✅ Karar netleşti (ARCHITECTURE.md v1.8), henüz KODLANMADI |
| 🗄️ | **[Session 12 devamı, #68 KAPANDI — ARCHITECTURE.md v1.9]** `RegistrationChannel`'dan `"masaya-siparis"` ÇIKARILDI (`FulfillmentChannel`'a taşınmadı). `20260808000000_registration_channel_masaya_siparis_cikarildi.md` | ✅ `types/index.ts` düzenlendi, migration gerekmedi (DB sütunu enum değil) |
| 🆕 | **[Session 12 devamı, #69 KAPANDI — ARCHITECTURE.md v1.10]** `order_history.channel` Masaya/Gel Al ayrımı için yeterli bulundu, ek alan eklenmedi. §2.7b'nin açık soru listesi tamamen kapandı. | ✅ Karar netleşti, kod HENÜZ YAZILMADI (1b bekliyor) |
| 🗄️ | **[2026-08-08, KRİTİK — ARCHITECTURE.md v1.11]** Masa numarası TUTULACAK — terk edilmeyecek. Route: `/masaya-siparis/[tableId]` (path segment). `useCartStore`'a `tableId`+`setTableId()` eklendi (§2.3). `order_history`'ye nullable `table_number` eklenecek (SADECE dine-in) — şema notu: `20260808010000_order_history_tablenumber_eklendi.md`. #69'un kapsamı genişletildi (KAPALI kalıyor, gerekçesiz düşürülmedi). | ✅ Karar netleşti + doküman güncellendi, kod/migration HENÜZ YAZILMADI/KOŞULMADI |
| 🗄️ | **[2026-08-08, KRİTİK — ARCHITECTURE.md v1.12]** #62'nin 3 mimari sorusu KAPANDI: (1) Personel auth = `users.role` alanıyla mevcut Auth.js'e rol bazlı yetki (2) Real-time = basit polling (3) Onay kuyruğu UI = iki ayrı sekme/panel (Masaya / Gel Al). | ✅ Karar netleşti + doküman güncellendi |
| 🗄️✅ | **[önceki tur — `users.role` MIGRATION KOŞULDU]** `lib/db/schema.ts`'e `role` sütunu eklendi (`text`, `NOT NULL`, `DEFAULT 'customer'`), kullanıcı GitHub'a manuel kaydetti. `ALTER TABLE` Neon SQL Editor'de koşuldu, `role text` sütunu Tables görünümünde DOĞRULANDI. `users` tablosu 0 satır (Twilio #32 kısıtı) — regresyon test edilemedi ama risk de fiilen yok. | ✅ DB tarafı TAMAM |
| 🆕 | **[BU TURDA — #75 mimari kararı]** "Sepete Ekle" kilidi SÜRE-bazlı (500ms debounce) değil, DURUM-bazlı (`selectionKey` + `Set<string> addedKeys`) olacak — bir kombinasyon eklenince kalıcı "Eklendi ✓", SADECE seçim değişince yeniden aktif. Aynı kombinasyona geri dönülürse kilit KORUNUR (bilinçli, tekrar eklemeyi önler). | ✅ Karar netleşti, kod üretildi, TEST/BUILD/PUSH/canlı doğrulama BEKLİYOR |
| 🗄️✅ | **[önceki tur — `/personel/*` guard'ı UÇTAN UCA TAMAMLANDI]** `types/index.ts` (`AuthenticatedUser.role`), `auth.ts` (JWT/session callback'leri, `normalizeRole()`), `middleware.ts` (`/personel/*` role guard — oturumsuz→`/kayit-ol`, `role!=='staff'`→403), `types/next-auth.d.ts` (Session/User/JWT augmentation) — 4 dosya senkron, kullanıcı 403 kararını onayladı, Vercel build YEŞİL (kullanıcı doğruladı). Açık Sorun #72 (eski yorum) da kapandı. | ✅ Kod TAMAM, canlı build YEŞİL |
| 🆕 | **[BU TURDA, 19. sohbet — henüz ONAYLANMADI, sadece öneri]** Çok şubeli mimari yönü: `branches` tablosu açılıp `order_history`+`consent_registrations`'a nullable `branch_id` FK eklenmesi öneriliyor. `users` ASLA şubeye bağlanmayacak (CRM şubeler üstü kalmalı — çapraz-şube LTV mantığı buna dayanıyor). Detay: `BOWLERA_COK_SUBELI_CRM_VIZYON.md` §6. | 🟡 Öneri aşamasında, bkz. Açık Sorun #92 |
| 🆕 | **[BU TURDA, 19. sohbet — henüz ONAYLANMADI, sadece öneri]** CRM metrik alanları (`order_count`/`total_spend`/`days_to_repeat`) `users` tablosuna KOLON olarak eklenmeyecek, `order_history` üzerinden SQL VIEW olarak hesaplanacak — senkron kayma riskini (iptal/düzeltme senaryoları) önlemek için. Pazarlama attribution alanları (`acquisition_source` vb.) mevcut `channel` (fulfillment) alanlarıyla İSİM ÇAKIŞMASI yaratmayacak şekilde AYRI isimlendirilecek. | 🟡 Öneri aşamasında, bkz. Açık Sorun #94 |
| 🆕 | **[YENİ, 26. sohbet — Admin Panel]** Görsel depolama: **ImageKit** (Cloudinary'ye karşı — sınırsız dönüşüm + geniş ücretsiz bant genişliği gerekçesiyle). Entegrasyon HENÜZ YAPILMADI. | 🟡 Karar netleşti, kod YOK |
| 🗄️✅ | **[YENİ, 26. sohbet — Admin Panel, DB TARAFI TAMAMLANDI]** `menu_items` tablosu (`lib/menu-data.json`'dan taşındı) — `id` bilinçli `text` (uuid değil), `calories`/`protein` NOT NULL, `tags`/`allergens` DB'de kısıtsız (sadece admin form UI kısıtlar), `build-your-own-kasem` DAHİL EDİLMEDİ (grep ile doğrulandı). Migration+seed Neon'da koşuldu ve doğrulandı (13 kolon, 8 satır). Şema notu: `docs/schema-changes/20260905090000_menu_items_tablosu_eklendi.md`. | ✅ DB tarafı TAMAM |
| 🆕 | **[YENİ, 26. sohbet — Admin Panel]** Admin yetkisi `users.role`'e AYRI bir `"admin"` değeri olarak eklendi (`"customer"\|"staff"\|"admin"`) — `"staff"`'a BAĞLANMADI (gerekçe: "tek admin hesabı" kararının staff panelinin ileride çoğalma ihtimaliyle çakışmaması). `schema.ts`/`auth.ts`/`middleware.ts`/`types/next-auth.d.ts` dört dosyada senkron güncellendi. | 🟡 Kod üretildi, kullanıcıya verildi — REPO'YA UYGULANDIĞI TEYİT EDİLMEDİ |
| 🗄️ | **[YENİ, 26. sohbet — Admin Panel]** `/admin`+`/api/admin` middleware guard'ı — `/personel` guard'ı ile AYNI desen (fail-closed, taze DB rol okuması), ama `role==='admin'` katı şartı — `staff` bu bloktan GEÇEMİYOR (bilinçli, "tek admin" kararı). | 🟡 Kod üretildi, canlı doğrulama BEKLİYOR |

---

## 🔴 AÇIK SORUNLAR (numaralı, kronolojik değil — öncelik/bağlam gruplu)

| # | Öncelik | Açıklama | Etkilenen Dosya(lar) |
|---|---|---|---|
| 39 | 🟢 | **[Bu turda ÇÖZÜLDÜ]** `/hesap` akışı artık rıza esaslı kayıt (OTP'siz) üzerinden canlıda test edildi ve DOĞRULANDI — Twilio kısıtı bu akışı artık engellemiyor. | — |
| 50 | ✅ | **[BU TURDA KAPANDI]** `AddToCartButton.tsx` görüldü, BSC-6 (çift ekleme race condition) doğrudan ele alındı ve seçim-kimliği bazlı kilitle çözüldü — bkz. #75. | `components/customizer/AddToCartButton.tsx` |
| 51 | 🟢 | `useCartStore.ts` tam dosya/persist davranışı hâlâ uçtan uca teyit edilmedi | `store/useCartStore.ts` |
| 52 | 🟡 | VisualPreview.tsx görsel katman klasörü boş | `components/customizer/VisualPreview.tsx` |
| 53 | 🟢 | CONTENT_GUIDE.md §1/§2 â→a kararına göre güncellenmedi | `CONTENT_GUIDE.md` §1, §2 |
| 54 | 🟡 | Gerçek şube adresi Şubeler/Footer.tsx/JSON-LD'ye işlenmedi — aciliyet var | `Footer.tsx` |
| 55 | 🟢 | `AboutValues.tsx` ile `ValueProps.tsx` senkronu teyit edilmedi | `components/about/AboutValues.tsx` |
| 56 | 🟢 | Twilio WhatsApp Business Sender onayı — PARKLI | `lib/auth/send-otp.ts` |
| 57 | 🟡 | Rıza esaslı kayıt — kod+test+canlı BAĞLANDI. KAPANMADI: `/online-siparis` sayfası yok | `app/kayit-ol/page.tsx` |
| 58 | 🟡 | Gel-al WhatsApp yönlendirme henüz kodlanmadı — #62 ile iç içe geçti | `lib/integrations/whatsapp.ts` |
| 60 | 🟠 | Neon DB şifresi 3 kez açığa çıktı — Reset password HENÜZ ONAYLANMADI | Neon console, `.env.local` |
| 61 | 🟢 | `app/kayit-ol/page.tsx` alt başlığı uydurmaydı — kullanıcı karar bekliyor | `app/kayit-ol/page.tsx` |
| 91 | 🟠 | **[CURRENT FOCUS]** Güvenlik denetimi SEC-01 (rol revocation) + SEC-02 (login rate-limit) — kod+test (33/33 PASS)+build+tsc TAMAM. **KALAN:** (a) canlıda bir staff hesabının role'ünü DB'de elle `customer`'a çekip eski JWT ile `/personel`'e girip 403 aldığını GÖZLE görmek; (b) aynı telefonla 6 kez yanlış şifre deneyip 6.'nın reddedildiğini GÖZLE görmek. İkisi de mock'lu testlerle DOLAYLI kanıtlandı ama GERÇEK ortamda hiç denenmedi (ÜÇÜNCÜ DERS). | `middleware.ts`, `auth.ts`, `lib/auth/rate-limit.ts` |
| 90 | 🟡 | **[YENİ, bu turda]** `/menu/customize/[id]` masaüstünde tek ekrana sığmıyordu — `VisualPreview` görseli (`aspect-square`) masaüstünde tavansız büyüyüp adım alanını görünür alanın dışına itiyordu. `page.tsx`'te 4 satırlık düzeltme kodlandı (görsel tavanı `md:max-w-[280px]`, `<main>` `md:h-screen md:overflow-hidden`, sol kolon `md:overflow-y-auto`, `SummaryPanel` `md:sticky`) ve kullanıcıya verildi. **KALAN:** Codespaces'te build koşulmadı, GitHub'a push edilmedi, canlıda/yerelde masaüstünde tek ekrana sığdığı GÖZLE doğrulanmadı. | `app/menu/customize/[id]/page.tsx` |
| 62 | 🟡 | Personel Sipariş Paneli — Masaya sekmesi TAMAMLANDI + canlı doğrulandı. Gel Al onay kuyruğu: #85 KAPANDI (önceki tur). **[BU TURDA]** Canlı bulgu üzerine 3-durumlu revizyon (KARAR A) — `confirmed` terminal olmaktan çıkarıldı, yeni `completed` durumu eklendi. 7 kaynak + 5 test dosyası (2'si YENİ — projedeki ilk API route testleri, emsal yoktu) kodlandı, Codespaces'te 37/37 PASS. **KALAN:** SADECE canlı ortamda "Teslim Edildi" butonunun tıklanıp gerçekten `completed`'e geçtiğinin ve Hazırlanıyor listesinden düştüğünün doğrulanması. | ARCHITECTURE.md §2.9a |
| 85 | ✅ | **[BU TURDA KAPANDI]** Gel Al kod incelemesi bulgularının 5'i de ele alındı: (1) BSC-4 sessiz catch → structured log + kullanıcı mesajı; (2) reduced-motion → `motion-safe:` varyantı; (3) bayat yorumlar temizlendi; (4) `recordFailedContactAttempt` atomik SQL UPDATE'e çevrildi (confirm/reject kısmı bilinçli MVP-dışı bırakıldı, bkz. #87); (5) 3 test dosyası yazıldı, Codespaces'te 15/15 PASS doğrulandı, GitHub'a push edildi. | `components/personel/GelAlPanel.tsx`, `GelAlOrderCard.tsx`, `lib/personel/gel-al-queries.ts` + 3 test dosyası |
| 87 | 🟢 | **[YENİ, bu turda]** Gel Al'da `confirmPickupOrder`/`rejectPickupOrder` eşzamanlı-güncelleme/optimistic-lock korumasız (#81'in Gel Al karşılığı) — bilinçli MVP-dışı bırakıldı (kullanıcı: tek personel/tek masaüstü panel, pratik risk düşük). Kullanım yoğunlaşırsa ele alınmalı. | `lib/personel/gel-al-queries.ts` |
| 88 | 🟢 | **[YENİ, bu turda]** Sekme rozetleri (Şifre Talepleri/Gel Al/Kayıt Onayları) kod+push tamam ama test yazılmadı, canlı ortamda hiç görsel kontrol edilmedi. Ayrıca Gel Al/Kayıt Onayları sekmesi aktifken ilgili endpoint 5sn'de 2 kez sorgulanıyor (rozet + panel ayrı hook, bilinçli trade-off) — kullanım yoğunlaşırsa state page.tsx'e taşınıp panellere prop geçirilmesi düşünülebilir. | `app/personel/page.tsx`, `hooks/usePersonelPasswordResetQueue.ts` |
| 86 | 🟡 | **[Bu turda, build DOĞRULANDI]** Kayıt Onayları (4. sekme) — 8 dosya kodlandı, tam repo zip'inden statik incelendi, Gel Al deseniyle tutarlı. Kullanıcı Codespaces'te `tsc --noEmit` (hatasız) VE `npm run build` (route tablosu/size özeti başarıyla üretildi — Next.js bu tabloyu SADECE derleme başarılıyken yazdırır) çalıştırdı, GitHub'a push edildi. **Build tarafı KAPANDI.** **KALAN:** test seti (Kural #6) yok, canlı ortamda Teyit Et/Reddet-Sil hiç test edilmedi (ÜÇÜNCÜ DERS — kod+build ≠ kullanıcı deneyimi doğrulandı). | `lib/personel/kayit-onaylari-queries.ts`, `app/api/personel/kayit-onaylari/*`, `components/personel/KayitOnaylariPanel.tsx` |
| 89 | 🟢 | **[YENİ, bu turda — 2 açık madde]** #89 IP delili + engellenen deneme logu KOD/MİGRASYON/TEST tarafı TAMAMLANDI (bkz. CURRENT FOCUS + Kritik Kararlar). Kapsam dışı bırakılan 2 madde: (a) KVKK aydınlatma metnine "güvenlik amacıyla IP adresiniz kaydedilir" maddesi eklenmeli (madde 6'ya bağlı); (b) `route.ts POST` fonksiyonu AGENT.md Kural #1'deki 20 satır sınırını (bu değişiklikten önce de) aşıyor — ayrı refactor turu önerildi (`handleRateLimitExceeded()` gibi bir yardımcıya çıkarılabilir). Ayrıca `registration_blocked_attempts` için retention/pruning YOK (bilinçli, kapsam dışı) — yoğun saldırı senaryosunda disk kullanımı izlenmeli. | `lib/db/schema.ts`, `app/api/registration/consent/route.ts`, `/kvkk` sayfası |
| 63 | 🟠 | `npm install`: 12 açık/3 kritik güvenlik açığı — `npm audit fix --force` bilinçli KOŞULMADI | `package.json` |
| 66 | 🟢 | İmza kase "Sepete Ekle" butonu (customize'a girmeden direkt ekleme) guest gate middleware'i tarafından YAKALANMIYOR — component-seviyesi guard gerekiyor. **[Session 12 devamı, kapsam teyidi]:** bu, `/menu/customize/*` (Gel Al) bağlamına özgüdür. **[2026-08-11 güncellemesi]:** 1b(ii) (`/masaya-siparis`) kapsam dışı bırakıldığı için bu sorunun "1b'nin alt-görevi mi" ikilemi ORTADAN KALKTI — artık sadece kendi başına bir karar: component-guard eklensin mi, yoksa bilinçli açık mı bırakılsın? Hâlâ kullanıcı kararı bekliyor. | `components/customizer/AddToCartButton.tsx` |
| 70 | ✅ | **[BU TURDA KAPANDI]** `order_history.table_number` tipi `text` olarak kararlaştırıldı (masa adları sayısal olmayabilir), index sadece `status` üzerine eklendi (`table_number` filtrelenmeyecek). Migration Neon'da koşuldu ve DOĞRULANDI. | `docs/schema-changes/20260809140000_order_history_status_tablenumber_customernotes_eklendi.md` |
| 71 | 🟠 | DEPENDENCIES.md, `RegistrationChannel`'ın tüketicisi olarak `channel-options.ts`'i (ve muhtemelen görülmemiş başka dosyaları) listelemiyor — #68 kapanırken bu dosya atlandığı için canlı build kırılmıştı (düzeltildi, 1d KAPANDI). DEPENDENCIES.md bu sohbette paylaşıldı ama v1.1 (Session 3) — genel olarak ESKİ, `RegistrationChannel` tüketicileri dahil yeni alan/tablo/store değişiklikleri (tableId, order_history, users.role, vb.) hiç yansımamış. Ayrı bir turda kapsamlı güncellenmeli. **[26. sohbet notu]:** `menu_items` tablosu da bu listeye eklenmeli. | `DEPENDENCIES.md` |
| 73 | 🟠 | `tailwind.config.ts`'teki `extend.colors` custom token'ları (`olive-primary` doğrulandı, muhtemelen `olive-deep`/`bronze`/`espresso` de) `bg-*` sınıfı olarak KULLANILDIĞINDA derlenmiyor — `bg-red-500` (standart) çalışıyor, `bg-olive-primary` (custom) çalışmıyor, `bg-[#53502A]` (arbitrary) çalışıyor. Kök neden BULUNAMADI. **[Bu turda ek kanıt]:** `AddToCartButton.tsx`'te de AYNI kırık pattern görüldü (#50'de "hiç görülmedi" idi), aynı `bg-[#53502A]` workaround'ıyla düzeltildi — üçüncü dosyada doğrulanan tekrar, sistematik tarama gerekliliğini pekiştiriyor. `text-olive-primary`'nin çalışıp çalışmadığı hâlâ TEYİT EDİLMEDİ. | `tailwind.config.ts`, tüm `bg-{custom-token}` kullanan dosyalar |
| 81 | 🟢 | **[YENİ, bu turda — bilinçli erteleme]** Masaya Paneli'nde (1) iki personelin aynı siparişi eşzamanlı güncellemesine karşı optimistic lock yok (son yazan kazanır), (2) `usePersonelOrders` polling'i sekme arka plandayken duraklamıyor (Page Visibility API kullanılmadı). İkisi de MVP kapsamı dışı bırakıldı, kullanım yoğunlaşırsa ele alınmalı. | `hooks/usePersonelOrders.ts`, `app/api/personel/orders/[id]/route.ts` |
| 80 | 🟢 | **[YENİ — kullanıcı kararıyla, 2026-08-09]** #79/#75 kapatıldı (mobil canlıda doğrulandı: "Sepete Ekle sorunu çözüldü"). Masaüstü (`SummaryPanel.tsx`) fix'i AYRICA canlıda doğrulanmadı — kod+test tarafı aynı (`isReadyToAddToCart()`), risk düşük görülüyor ama not olarak açık bırakılıyor. #75'in orijinal çift-tık/duplicate senaryosu da bu turda ayrıca test edilmedi. | `components/customizer/SummaryPanel.tsx` |
| 78 | 🟢 | **[Kaynak bileşen bu turda teyit edildi — UX çözümü hâlâ AÇIK]** Customizer'da collapsed sticky özet panel (fiyat/kalori satırı + ▲ ikonu) seçim anında "Sepete Ekle" butonunu ve Base/Main/Flavor özetini GİZLİYOR — panel manuel genişletilmeden görünmüyor. Kaynak bileşenin `MobileSummaryDrawer.tsx` olduğu bu turda doğrulandı (bkz. #75) — SADECE o dosyadaki build-kırığı prop eksikliği düzeltildi, panel-görünürlüğü UX çözümüne bilinçli olarak DOKUNULMADI (Kural #5, ayrı karar). CORE.md §8 mimari varsayımı "Özet panel her zaman görünür... asla gizlenmez" ile çelişiyor. Çözüm yönü henüz kararlaştırılmadı (varsayılan yarı-açık / mikro-metin / otomatik ilk-açılış seçenekleri konuşuldu). | `components/customizer/MobileSummaryDrawer.tsx` |
| 92 | 🟠 | **[YENİ, bu turda (19. sohbet) — sadece analiz+öneri, KOD YOK]** Çok şubeli mimari: `branches` tablosu şemada HİÇ YOK. Kullanıcı 2./3. şubenin "herhangi an" açılabileceğini belirtti. `order_history` ve `consent_registrations`'da hangi siparişin/kaydın hangi şubeye ait olduğunu tutan bir alan yok — şu an TEK ŞUBE varsayımıyla kurulu. Geriye dönük eklemek, mevcut kayıtlara hangi şube olduğu konusunda varsayım atamayı gerektirir (veri belirsizliği riski). **Önerilen yön (ONAYLANMADI):** `branches` tablosu tek satırla (mevcut şube) şimdiden açılsın, `order_history.branch_id` + `consent_registrations.branch_id` nullable FK olarak eklensin; `users` ASLA şubeye bağlanmasın (CRM şubeler üstü kalmalı). Detay: `BOWLERA_COK_SUBELI_CRM_VIZYON.md` §3-4-6. **Açık karar:** 2. şube yaklaşık ne zaman planlanıyor — bu, işin bu turda mı yoksa ayrı sırada mı yapılacağını belirler. | `lib/db/schema.ts` (henüz dokunulmadı) |
| 93 | ✅ | **[BU TURDA (26. sohbet) KAPANDI]** Menü verisinin gerçek konumu doğrulandı: `lib/menu-data.json` (imza kaseler+içecekler), `lib/sandwich-data.json` (sandviçler, TEST VERİSİ, #95), `lib/customizer-data.ts` (build-your-own malzeme kataloğu). `menu-data.json`'daki 8 gerçek ürün `menu_items` DB tablosuna taşındı, migration+seed Neon'da doğrulandı. Şube-bazlı menü önerisi (branch_menu_items eşleme tablosu) HÂLÂ ONAYLANMADI, ayrı bir karar — bu turun kapsamı SADECE tek-şube admin panel ön koşuluydu. | `lib/menu-data.json`, `lib/db/schema.ts` |
| 94 | 🟢 | **[YENİ, bu turda (19. sohbet) — sadece analiz+öneri, KOD YOK]** CRM/attribution katmanı eksik: `consent_registrations`/`order_history`'de pazarlama kaynağı (Instagram/TikTok/Marketplace/Google/UTM) hiç tutulmuyor. **İsim çakışması riski:** mevcut `channel` alanları (her iki tabloda da var) FULFILLMENT kanalı (gel-al/masaya) anlamında — pazarlama kanalı DEĞİL. Yeni alanlar eklenirse `channel` yeniden kullanılmamalı, `acquisition_source`/`utm_campaign`/`utm_medium` gibi AYRI isimler kullanılmalı. Ayrıca `order_count`/`total_spend`/`days_to_repeat` gibi CRM metrikleri `users`'a KOLON olarak eklenmemeli — `order_history` üzerinden SQL VIEW olarak hesaplanmalı (senkron kayma riski). Kullanıcının "bu yapı ileride birçok modül/uygulamanın temel iskeleti olacak" vizyonuyla bağlantılı — PUSULA OS değerlendirmesindeki "event log yok, policy engine yok" bulgusuyla örtüşüyor (tam çözüm bu turun kapsamı dışı, sadece isim/yön kararı). Detay: `BOWLERA_COK_SUBELI_CRM_VIZYON.md` §5-6-7. | `lib/db/schema.ts` (henüz dokunulmadı) |
| 95 | 🟡 | **[YENİ, bu turda (21. sohbet)]** Sandviç akışı `lib/sandwich-data.json` TEST VERİSİ ile çalışıyor — S1 (gerçek fiyat/kalori/ürün isimleri), S2 (ücretsiz sebze kotası — şu an placeholder 4), S5 ("Mike's Way" preset içeriği — şu an placeholder sebze+sos) hâlâ gerçek veri bekliyor. Launch öncesi MUTLAKA değiştirilmeli, aksi halde sahte fiyat/kalori canlıya çıkar. | `lib/sandwich-data.json` |
| 96 | ✅ | **[BU TURDA KAPANDI]** Sandviç bileşen testleri (`SandwichCustomizer` + 6 adım bileşeni) yazıldı ve Codespaces'te doğrulandı: 7/7 dosya, 27/27 test PASS (2026-08-23 18:28). Yol boyunca 2 sorun çıktı, ikisi de çözüldü: `act()` eksikliği ve unutulan `StepSauceToastExtras.test.tsx` pushu. | `components/sandwich/*.test.tsx` |
| 97 | 🟠 | **[YENİ, bu turda (21. sohbet)]** CORE.md Dosya Haritası bu turda eklenen dosyaları yansıtmıyor: `StepBread/StepSize/StepProtein/StepCheese/StepVeggies/StepSauceToastExtras.tsx`, `app/sandwich/customize/[id]/page.tsx`, 7 test dosyası, `Hero.tsx` CTA değişikliği. **[26. sohbet notu]:** ayrıca `middleware.ts`/`auth.ts`/`types/next-auth.d.ts` admin guard değişiklikleri ve `lib/db/schema.ts`'e `menuItems` de eklenmeli. Ayrı bir turda CORE.md güncellenmeli. | `CORE.md` |
| 98 | 🟢 | **[YENİ, bu turda (21. sohbet) — kapsam dışı bırakıldı]** Genel proje `npm test` çalıştırıldığında (sandviç kapsamı DIŞINDA) 7 dosya/9 test başarısız çıktı, `Header.test.tsx` dahil (kritik: "Çıkış Yap"a tıklayınca signOut callbackUrl="/" ile çağrılır" testi). Bu turda kasıtlı dokunulmadı — Kural #5 izolasyon. Ayrı bir turda ele alınmalı. | `components/layout/Header.test.tsx` + 6 diğer dosya (henüz listelenmedi) |
| 99 | 🔴 | **[YENİ, 22. sohbet — GERİYE DÖNÜK loglandı, sohbet kesildi]** Sandviç checkout'u BLOKLU: "Siparişi Onayla" adımında fiyat ne olursa olsun kırmızı "fiyatlandırılamadı" hatası çıkıyor, sipariş tamamlanamıyor. Kök neden ŞÜPHESİ (doğrulanmadı): `FulfillmentGate.tsx`/`ConfirmPickupOrderButton.tsx`'teki fiyatlandırma kontrolü sadece Bowl'un `bowlItem`/`customization` alanlarını tanıyor, `sandwichCustomization`'ı bilmiyor. Kullanıcıdan `grep -rn "fiyatlandırılamadı" --include="*.tsx" --include="*.ts" .` çıktısı istendi, YANIT GELMEDEN sohbet kesildi. | `components/checkout/FulfillmentGate.tsx` veya `ConfirmPickupOrderButton.tsx` (kesin dosya DOĞRULANMADI) |
| 100 | 🟡 | **[YENİ, 22. sohbet — kod üretildiği İDDİA EDİLDİ, push/test TEYİT EDİLMEDİ]** 4 UI düzeltmesi: (a) `Hero.tsx` buton düzeni `flex-wrap`→`grid grid-cols-2`, mobilde yan yana kalıcı; (b) `SandwichSummaryPanel.tsx`'e TEST VERİSİ rozeti eklendi; (c) `HeroImagePlaceholder.tsx` `aspect-square`→`aspect-[4/3]`+`max-h-72`, mobil taşma düzeltildi; (d) `SandwichCustomizer.tsx` sepete ekleme sonrası artık `/siparis`'e yönlendiriyor (`useRouter`, önceden `store.reset()`+aynı sayfa). | `components/home/Hero.tsx`, `components/sandwich/SandwichSummaryPanel.tsx`, `components/home/HeroImagePlaceholder.tsx`, `components/sandwich/SandwichCustomizer.tsx` |
| 101 | ✅ | **[BU TURDA KAPANDI, 2026-09-03, 23. sohbet]** 22. sohbetteki "Özel Kase" fallback bug'u (`item.bowlItem?.name ?? "Özel Kase"` sandviçlerde hep "Özel Kase" yazdırıyordu) `CartDrawer.tsx`'in bu turdaki motion yükseltmesiyle YENİDEN yazıldı VE test edildi — `CartDrawer.test.tsx`'teki "bowlItem null + sandwichCustomization dolu → Özel Sandviç; ikisi de null → Özel Kase" testi Codespaces'te PASS (8/8, 2026-09-03 06:16, ekran görüntüsü). Bowl davranışı da (`bowlItem?.name` önceliği) happy-path testinde doğrulandı. **KALAN:** push + canlı/production doğrulaması — bkz. #105. | `components/cart/CartDrawer.tsx` |
| 102 | 🟢 | **[YENİ, 22. sohbet — push/test TEYİT EDİLMEDİ]** `OrderSummary.tsx` satır 20 — CartDrawer'daki (#101) BİREBİR AYNI "Özel Kase" fallback bug'u burada da bulundu, aynı desenle genişletildi ("Özel Sandviç"). | `components/order/OrderSummary.tsx` |
| 103 | 🟢 | **[YENİ, 22. sohbet — push/test TEYİT EDİLMEDİ]** `OrderSummary.tsx`'e CartDrawer'daki gibi "Kaldır" butonu eklendi — eski fiyat düzeltmesinden ÖNCE sepete girmiş 0₺'lik test ürünlerini temizlemek için. | `components/order/OrderSummary.tsx` |
| 104 | 🟡 | **[YENİ, 22. sohbet — çözülmeden kaldı]** #100(d) fix'i sonrası `SandwichCustomizer.test.tsx`'in sepete-ekleme testleri artık `router.push` çağıracak — `next/navigation`'ın `useRouter`'ı test ortamında mock'lanmadıysa testler kırılabilir. Kullanıcıya "şimdi düzelteyim mi yoksa `npx vitest run components/sandwich` çalıştırıp kırmızı çıkanı mı paylaşırsın" soruldu, YANIT GELMEDEN sohbet kesildi. | `components/sandwich/SandwichCustomizer.test.tsx` |
| 106 | 🟢 | **[GÜNCELLENDİ, bu turda — kısmen açıklandı]** DESIGN_SYSTEM.md §6.1'deki "Sayfa geçişleri" satırında `"[2026-09-03 güncellendi — önceki: 250ms, kullanıcı isteğiyle yavaşlatıldı]"` notu var (250ms→500ms) — bu değişiklik bu sohbette hiç konuşulmadı, SESSION_INDEX.md'nin hiçbir yerinde loglanmamıştı. **Kısmi açıklama bulundu:** kullanıcının paylaştığı rapor v1.1'in §28 sonunda "Page transitions *(token değeri 500ms'ye güncellendi, bileşen henüz kodlanmadı)*" notu var — yani token değeri değiştirilmiş ama SAYFA GEÇİŞİ BİLEŞENİNİN KENDİSİ HENÜZ KODLANMADI. Hâlâ belirsiz: (a) bu notu kullanıcı mı ekledi yoksa başka bir kaynaktan mı geldi (kullanıcıya bu turda soruldu); (b) `tokens.ts`'teki gerçek değer 500ms mi. | `DESIGN_SYSTEM.md` §6.1, `BOWLERA_MOTION_SYSTEM_RAPORU.md` §28, sayfa geçiş bileşeni (dosya adı doğrulanmadı) |
| 107 | ✅ | **[KAPANDI]** `tokens.ts` paylaşıldı, yapı çelişkisi çözüldü — gerçek kod düz `durations/easings/springs` export'ları kullanıyor. | `lib/motion/tokens.ts` |
| 105 | 🟡 | **[2026-09-03, 23. sohbet — Motion System, kullanıcı kararıyla #99/#91'in PARALELİNDE]** Rapor P0-1 (CartDrawer) kod+test TAMAM. P0-2 MenuCard kod TAMAM. **KALAN:** push edilmedi, canlı/production'da GÖZLE doğrulanmadı. Detay `session_arşiv_2.md`/Motion System P0 özetinde. | `lib/motion/tokens.ts`, `components/cart/CartDrawer.tsx`, `components/menu/MenuCard.tsx` |
| 108 | 🟠 | **[YENİ, 26. sohbet — Admin Panel]** `DESIGN_SYSTEM.md` §7.2'nin alerjen listesi (7 değer: Gluten/Süt/Yumurta/Fındık-Kuruyemiş/Soya/Balık-Kabuklu Deniz Ürünü/Susam) kodda (`types/index.ts`'teki `BowlItem.allergens`) ve canlı filtre ekranında SADECE 5 değerle karşılığı var (gluten/dairy/nuts/soy/shellfish — Yumurta ve Susam hiç kodlanmamış). Kod+canlı davranış esas alınıp `menu_items` DB şeması 5 değere göre kuruldu — DESIGN_SYSTEM.md'nin GÜNCEL OLMADIĞI değerlendirildi, ama doküman henüz düzeltilmedi. | `DESIGN_SYSTEM.md` §7.2, `types/index.ts` |
| 109 | 🟡 | **[YENİ, 26. sohbet — Admin Panel]** Canlı `/menu` filtre ekranı "Diyet & Kalori" bölümünde **Keto** seçeneği gösteriyor ama gerçek `menu-data.json` verisinde HİÇBİR üründe bu tag yok. Ayrıca gerçek veride kullanılan **glutensiz** ve **sıcak-tahıl** etiketleri filtre ekranında HİÇ YOK — bu iki tag'e sahip ürünler filtrelenemiyor. Admin panel formu gerçek veriye göre 5 doğru değeri (yüksek protein/glutensiz/vegan/sıcak-tahıl/düşük kalori) kullanacak şekilde kararlaştırıldı, ama canlı filtre ekranının KENDİSİ bu turda düzeltilmedi — ayrı bir görev. | `/menu` filtre bileşeni (kesin dosya adı bu turda doğrulanmadı) |
| 110 | 🟠 | **[YENİ, 26. sohbet — Admin Panel]** ARCHITECTURE.md ve DEPENDENCIES.md `menu_items` tablosunun eklendiğini, `users.role`'e `"admin"` değerinin eklendiğini ve `/admin`+`/api/admin` middleware guard'ının varlığını YANSITMIYOR — bu turda SADECE `docs/schema-changes/20260905090000_menu_items_tablosu_eklendi.md` şema notu üretildi, mimari dokümanlar güncellenmedi. | `ARCHITECTURE.md`, `DEPENDENCIES.md` |
| 111 | 🟡 | **[YENİ, 26. sohbet — Admin Panel]** `types/index.ts`'teki `BowlItem` tipi bu turda GÖRÜLMEDİ ve GÜNCELLENMEDİ — `menu_items` DB şemasıyla (calories/protein NOT NULL, tags/allergens array) senkron olduğu VARSAYILDI (ARCHITECTURE.md'de daha önce görülen tip tanımına dayanarak) ama bu turda dosyanın kendisi paylaşılmadı, TAM teyit edilmedi. | `types/index.ts` |
| 112 | ✅ | **[BU TURDA (27. sohbet) KAPANDI]** 4 dosya (`schema.ts`/`auth.ts`/`middleware.ts`/`types/next-auth.d.ts`) repoya uygulandı, `npx tsc --noEmit` + `npm run build` temiz, push edildi. Neon'da `+905431615778` numarası `role='admin'` yapıldı VE canlıda doğrulandı (`SELECT` ile teyit edildi). **YENİ KARAR (kullanıcı isteğiyle):** bu hesabın hem `/personel` hem `/admin`'e erişmesi istendiği için `middleware.ts`'teki `/personel` guard'ı `role !== 'staff' && role !== 'admin'` olarak GENİŞLETİLDİ (admin artık staff'ın süperkümesi, ama `/admin` guard'ı hâlâ SADECE `role==='admin'` — tek admin kararı bozulmadı). Canlıda hem `/personel` hem `/admin` (o an 404 — sayfa yoktu ama 403 YOKTU) doğrulandı. | `middleware.ts` |
| 113 | ✅ | **[BU TURDA (27. sohbet) KAPANDI]** Admin panelinin ilk CRUD'u yazıldı ve DEPLOY EDİLDİ: `lib/imagekit.ts`, `lib/admin/menu-item-constants.ts`, `app/api/admin/upload-image/route.ts`, `app/api/admin/menu-items/route.ts` (GET+POST), `app/api/admin/menu-items/[id]/route.ts` (GET+PATCH+DELETE), `components/admin/MenuItemForm.tsx`, `app/admin/page.tsx` (liste), `app/admin/menu-items/new/page.tsx`, `app/admin/menu-items/[id]/page.tsx`. ImageKit hesabı açıldı (Public Key/Private Key/URL Endpoint alındı, `.env.local`+Vercel env'e eklendi), `imagekit` npm paketi kuruldu. Yol boyunca 3 build hatası çıktı, hepsi çözüldü: (1) `imagekit` paketi package.json'a hiç eklenmemişti — `npm install imagekit --save`; (2) `MENU_ITEM_TAGS.includes()` TS literal-tipi hatası — `as readonly string[]` cast'iyle çözüldü; (3) `app/admin/page.tsx`'in kendisi ilk pushta unutulmuştu (sadece alt sayfalar gitmişti) — ayrıca eklenip push edildi. **CANLIDA DOĞRULANDI:** `/admin` artık 8 gerçek ürünü doğru isim/fiyat/kategoriyle listeliyor. | `app/admin/*`, `app/api/admin/*`, `lib/imagekit.ts`, `components/admin/MenuItemForm.tsx` |
| 114 | 🔴 | **[YENİ, 28. sohbet]** Admin panelde yeni ürün oluşturuldu ("Fogy"), Neon'da DB'ye yazıldığı DOĞRULANDI — ama `app/admin/page.tsx` build-anı statik önbelleğe alındığı için (server component'te `dynamic` export'u yoktu) liste sayfasında hiç görünmedi. `export const dynamic = 'force-dynamic'` hem liste hem düzenleme sayfasına eklendi — kullanıcı henüz repoya uygulayıp push ETMEDİ, canlı doğrulama BEKLİYOR. Ayrıca kalan (önceki turdan devam eden, henüz test edilmeyen): düzenleme formunun dolu geldiği + gerçek ImageKit yüklemesinin uçtan uca çalıştığı hâlâ canlıda doğrulanmadı; liste sayfasındaki `<img>` önizlemelerinin kırık ikon göstermesi kozmetik, ayrı görev. | `app/admin/page.tsx`, `app/admin/menu-items/[id]/page.tsx` |

> **KAPANDI (ayrıntı `session_arşiv_2.md`'de, taşıma: 2026-08-23):** #82, #83, #84, #74, #79,
> #75 (kullanıcı kararıyla, #80 not olarak açık kaldı), #50, #76, #77 — hepsi Kritik Kararlar
> tablosunda ve/veya GENEL DURUM'da hâlâ özet olarak duruyor; turn-by-turn kapanış anlatısı
> arşive taşındı (400 satır eşiği).

> **KAPANDI (önceki turlar, ayrıntı `session_arşiv_1.md`'de):** #59, #72, `users.role`
> migration, 1d (Vercel build), #4, #7, #15, #16, #20, #22/Karar #11, #35, #43, #44, #49,
> #64, #65, #67, #68, #69 — hepsi Kritik Kararlar tablosunda ve/veya GENEL DURUM'da hâlâ
> özet olarak duruyor; turn-by-turn anlatı arşive taşındı (2026-08-09, 400 satır eşiği).

---

## SESSION ÖZET (tümü — 0'dan 12'ye)

| Session | Tarih | Ana içerik | Durum |
|---|---|---|---|
| 0 | — | Ajan altyapısı (14 dosya) | ✅ Tamamlandı |
| 1 | 2026-07-1x | Next.js+Tailwind kurulum, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| 2 | 2026-07-18 | Menü sayfası, filtreleme, MenuCard, customizer 4→5 adım kararı | ✅ Tamamlandı |
| 3 | 2026-07-18 | Zustand store + pricing + customizer data (kesintiye uğradı) | ✅ Büyük ölçüde tamam |
| 4 (devam) | 2026-07-18→07-22 | Sepet/kanal seçimi, auth mimarisi+kod+DB+UI, ARCHITECTURE.md v1.4, vb. | 🟡 Devam ediyor |
| 5 | 2026-08-01→08-02 | VisualPreview denetimi (#52), Hakkımızda sayfası, 400 satır eşiği kaldırılıp geri getirildi | 🟡 Devam ediyor |
| 6 | 2026-08-05 | WhatsApp OTP kodlandı/test edildi. Twilio/Netgsm PARKLANDI, rıza esaslı kayıt+WhatsApp yönlendirme kararlaştırıldı (#57/#58 açıldı) | 🟡 Devam ediyor |
| 7 | 2026-08-06 | #57 uçtan uca kodlandı (17/17 PASS). `consentRegistrations`, `RegistrationChannel` tipleri eklendi. **#57 kapanmadı** — kod sayfaya bağlanmadı. | 🟡 Devam ediyor |
| 8 | 2026-08-06/07 | Kırık Twilio akışı keşfedildi, `/kayit-ol`+`/kvkk` bağlandı, migration koşuldu, canlı test BAŞARILI. #59/#60/#61 yeni açıldı. | 🟡 Devam ediyor |
| 9 | 2026-08-07 | Masaya Sipariş kanalı canlıda doğrulandı. Personel Sipariş Paneli ihtiyacı keşfedildi → #62 açıldı. `session_log.md` ismi/mekanizması netleştirildi. | 🟡 Devam ediyor — #62 yeni sohbette |
| 10 | 2026-08-07 | ⚠️ Geriye dönük tamamlandı. `order_history` tablosu migrate edildi. #63 (npm audit) yeni. | 🟡 Devam ediyor |
| 11 | 2026-08-07 | ⚠️ Geriye dönük tamamlandı. Genel giriş/kayıt akışı netleşti (kanal bazlı tablo), #62 kapsamı genişledi ("kasa paneli" = Personel Sipariş Paneli), #64 kapandı (doğrulama durumu alanı kararı). | 🔴 Devam ediyor — #62 mimarisi bekliyor |
| 12 | 2026-08-08 | ⚠️ Retroaktif: guest-gate middleware'i zip ile doğrulandı (confidence HIGH), #65/#66 açıldı. ARCHITECTURE.md v1.7'ye güncellendi (Masaya Sipariş ayrı `/masaya-siparis/*` yüzeyine taşındı), #65 KAPANDI, #67/#68/#69 açıldı+kapandı, 400 satır eşiği tetiklendi. Masa numarası kararı: TUTULACAK, ARCHITECTURE.md v1.11'e işlendi (`CartState.tableId`, path segment route, `order_history.table_number` şema notu), #69 kapsamı genişletildi (#70 yeni açıldı). Canlı build kırığı bulunup düzeltildi (`channel-options.ts`), #71 yeni açıldı. | 🟡 §2.7b kod üretimine hazır; #70/#71 netleşmeli |
| 12 (devamı) | 2026-08-08 | 1d KAPANDI (Vercel build yeşil, kullanıcı doğruladı). #62'nin 3 mimari sorusu (personel auth, real-time, onay kuyruğu UI) kullanıcı onayıyla kapandı, ARCHITECTURE.md v1.12'ye işlendi. `users.role` için CORE.md §7.4 şema notu üretildi. `lib/db/schema.ts` diff'i + migration SQL'i üretildi, sunuldu. **Kullanıcı migration'ı Neon'da koşturdu ve Tables görünümünde `role` sütununu doğruladı.** `users.role` DB tarafı TAM kapandı — kod tarafı (`types/index.ts`/`auth.ts`/`middleware.ts`) bir sonraki tur. | 🟢 DB tamam; kod tarafı bekliyor |
| 12 (devamı, 2026-08-09) | 2026-08-09 | #70 kapandı (`order_history` şema genişletmesi: status/table_number/customer_notes, migration koşuldu+doğrulandı). `middleware.ts`'teki `/api/personel/*` guard açığı kapatıldı. #62'nin Masaya sekmesi 10 dosyayla uçtan uca kodlandı VE canlıda test siparişiyle doğrulandı (PATCH→durum makinesi→DB→polling→UI zinciri). Yol boyunca `users.role` düzeltmesi (staff'a manuel `UPDATE`) ve JWT-cache nedeniyle yeniden giriş gerekliliği yaşandı — #74 (çıkış butonu eksikliği) bu yüzden önceliği yükseltilerek tekrar gündeme geldi. | 🟢 Masaya TAMAM; Gel Al + #74 + ARCHITECTURE.md güncellemesi bekliyor |
| 26 | 2026-09-05 | **Admin Panel planlaması başladı.** ImageKit kararı, menü verisinin gerçek konumu doğrulandı (#93 KAPANDI), `menu_items` DB tablosu migration+seed Neon'da koşuldu ve doğrulandı, `"admin"` rolü `schema.ts`/`auth.ts`/`middleware.ts`/`types/next-auth.d.ts` dört dosyada senkron kodlandı ve kullanıcıya verildi. **KALAN:** 4 dosyanın repoya uygulanıp push edilmesi (#112), `app/admin/page.tsx` (henüz başlanmadı). | 🟡 DB+yetki katmanı hazır; repo entegrasyonu + sayfa/CRUD kodu bekliyor |

*(Tam turn-by-turn detay: `session_arşiv.md` [0-10], `session_arşiv_1.md` [11+].)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel. `lib/db/schema.ts` (users.role eklendi) kullanıcı tarafından manuel push edildi. ✅ Önceki turdaki `channel-options.ts` build kırığı düzeltildi, Vercel deploy YEŞİL (1d KAPANDI). ⚠️ **[26. sohbet]** `schema.ts`/`middleware.ts`/`auth.ts`/`types/next-auth.d.ts` — admin rolü için TAM DOSYA üretildi, kullanıcıya verildi, REPO'YA UYGULANDIĞI/PUSH EDİLDİĞİ TEYİT EDİLMEDİ (bkz. #112). |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 kod ile hizalı — ⚠️ ROADMAP.md'ye #62 (Personel Sipariş Paneli) hiç işlenmemiş, ayrı bir oturum/kalem olarak eklenmesi gerekebilir. ARCHITECTURE.md v1.12'ye güncellendi, henüz koda tam yansımadı (DB var, kod yok). ⚠️ **[19. sohbet]** `BOWLERA_COK_SUBELI_CRM_VIZYON.md` adlı YENİ, ayrı bir taslak vizyon belgesi üretildi (ARCHITECTURE.md'nin YERİNE geçmiyor) — çok şubeli mimari + CRM/attribution önerisi içeriyor, henüz resmi dosyalara (ARCHITECTURE.md) işlenmedi, sadece Açık Sorunlar #92/#94'te özetlendi. ⚠️ **[26. sohbet, YENİ]** Admin Panel için ROADMAP.md'ye HENÜZ bir kalem eklenmedi (kullanıcıya bu şekilde önerilmişti, teyit edilmedi). |
| Test Suite | 🟢 `guest-gate.test.ts` (8 — kullanıcı tarafından koşuldu, PASS doğrulandı). `rate-limit.test.ts` (11) + `middleware.test.ts` (10) + `auth.test.ts` (13) = 33/33 PASS, Codespaces'te kullanıcı tarafından koşuldu ve doğrulandı — SEC-01/SEC-02 kapsamı. Genel `npm test` (TÜM proje, tüm dosyalar) hâlâ hiç çalıştırılmadı. ⚠️ `users.role` migration'ı için TEST_MATRIX.md güncellemesi BEKLEMEDE (dosya paylaşılmadı). ⚠️ **[26. sohbet, YENİ]** `middleware.test.ts`/`auth.test.ts` admin guard'ı için hiç test yazılmadı — sadece `/personel` guard'ının mevcut testleri var, `/admin` guard'ı test edilmedi. |
| Auth | 🟡 Twilio/Netgsm PARKLI. Genel giriş/kayıt akışı karar olarak netleşti, guest gate middleware'i KODLANDI ve repoda doğrulandı. Masaya Sipariş kanalı middleware'in kapsamı dışında AYRI bir yüzeyde (`/masaya-siparis/*`) yaşayacak — bu yüzey henüz kodlanmadı. Gel Al akışı için "Sepete Ekle" bypass guard'ı (#66) hâlâ eksik. `/personel/*` role bazlı guard'ı ✅ TAMAMLANDI — 4 dosya senkron, canlı build yeşil doğrulandı. Telefon+şifre girişi (#82) VE şifre sıfırlama (#83) canlıda TAM doğrulandı — ikisi de KAPANDI. Login sonrası isim gösterme sorunu (#84) de canlıda düzelmiş görüldü, KAPANDI. Güvenlik denetimi SEC-01+SEC-02 kod+test+build+tsc TAMAM — canlı manuel doğrulama BEKLİYOR (#91). ⚠️ **[26. sohbet, YENİ]** `/admin`+`/api/admin` role guard'ı (`role==='admin'`, staff giremiyor) kodlandı, 4 dosya senkron üretildi — repo entegrasyonu VE canlı doğrulama BEKLİYOR (#112). |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE canlıda test edildi (#39 KAPANDI). ⚠️ Kaydet butonu `bg-olive-600` (kırık) → `bg-[#53502A]` (arbitrary value, çalışıyor) — kök neden #73'te açık. |
| Kullanıcı Kaydı (rıza esaslı) | 🟢 Backend+Frontend TAMAM, canlı test BAŞARILI, oturum+isim gösterimi DOĞRULANDI (#59 KAPANDI). Kanal seçimi zorunlu adımı henüz KODLANMADI (bkz. 1b). |
| Checkout (`/siparis`) | 🟢 Bowl için kod tamam VE repoda doğrulandı, SADECE Gel Al'a özel (§2.9). Masaya kendi bağımsız mini-checkout'unu kullanacak (ARCHITECTURE.md v1.8) — henüz KODLANMADI. 🔴 **[22. sohbet]** Sandviç için checkout BLOKLU — fiyat ne olursa olsun "fiyatlandırılamadı" hatası çıkıyor, sipariş tamamlanamıyor, kök neden DOĞRULANMADI (bkz. #99). |
| Veritabanı | 🟢 Neon Postgres çalışıyor. `consentRegistrations` ve `order_history` migrate edildi. `users.role` (`text`, `NOT NULL`, `DEFAULT 'customer'`) migrate edildi ve DOĞRULANDI. `consentRegistrations.ipAddress` (nullable) + `registrationBlockedAttempts` tablosu (#89) migrate edildi, 6 sorguyla DOĞRULANDI. `users` tablosu hâlâ 0 satır (#32 Twilio kısıtı). ⚠️ DB şifresi reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik (#63). ✅ **[26. sohbet, YENİ]** `menu_items` tablosu (6. tablo) migrate edildi ve DOĞRULANDI — 13 kolon (tipler teyitli), 8 satır (`SELECT COUNT(*)` ile doğrulandı). `build-your-own-kasem` bilinçli olarak DAHİL EDİLMEDİ (grep ile doğrulandı). `branches` veya çok-şubeli menü tablosu HÂLÂ YOK (bkz. #92/#93). |
| Personel Sipariş Paneli (#62) | 🟢 Masaya sekmesi TAMAMLANDI + canlı doğrulandı. `/personel/*` + `/api/personel/*` guard'ı ikisi de canlı build yeşil. 🟡 Gel Al onay kuyruğu — 3-durumlu revizyon (KARAR A), 7 kaynak+5 test dosyası kodlandı, Codespaces'te 37/37 PASS. **SADECE canlı ortamda "Teslim Edildi" tıklama testi BEKLİYOR.** 🟡 Kayıt Onayları (4. sekme, #86) — 8 dosya kodlandı, build YEŞİL, test seti + canlı doğrulama BEKLİYOR. 🟢 Sekme rozetleri eklendi, push edildi. |
| Admin Panel (menü/fiyat/kalori/görsel CRUD) | 🟡 **[YENİ, 26. sohbet]** Planlama+DB katmanı TAMAMLANDI: `menu_items` tablosu migrate+doğrulandı, admin yetkisi (`users.role="admin"`) + `/admin` middleware guard'ı 4 dosyada senkron kodlandı. **KALAN:** 4 dosyanın (`schema.ts`/`middleware.ts`/`auth.ts`/`types/next-auth.d.ts`) repoya uygulanıp push edilmesi (#112), `app/admin/page.tsx` (placeholder önerisi henüz onaylanmadı), CRUD API route'ları+formlar, ImageKit entegrasyonu — hiçbiri başlanmadı. Menü verisinin geri kalanı (`sandwich-data.json`, `customizer-data.ts`) bu turun kapsamı DIŞINDA. |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| A1 | **[YENİ, 26. sohbet, EN ÖNCELİKLİ]** `schema.ts`/`middleware.ts`/`auth.ts`/`types/next-auth.d.ts` dosyalarını repoya uygulayıp GitHub'a push et, Vercel build'in yeşil olduğunu doğrula (#112) | 🔴 |
| A2 | **[YENİ, 26. sohbet]** Kendi hesabına Neon'dan elle `role='admin'` ata | 🔴 |
| A3 | **[YENİ, 26. sohbet]** `app/admin/page.tsx` — basit placeholder sayfa, middleware guard'ının canlıda çalıştığını (staff/customer 403, admin giriyor) GÖZLE doğrula | 🟠 |
| A4 | **[YENİ, 26. sohbet]** Admin panel CRUD API route'ları (`/api/admin/menu-items`) + formlar kodlanmalı | 🟡 |
| A5 | **[YENİ, 26. sohbet]** ImageKit entegrasyonu (upload akışı) | 🟡 |
| A6 | **[YENİ, 26. sohbet]** `/menu` canlı filtre ekranındaki Keto/glutensiz/sıcak-tahıl tag uyuşmazlığı düzeltilmeli (#109) | 🟡 |
| A7 | **[YENİ, 26. sohbet]** DESIGN_SYSTEM.md §7.2 alerjen listesi (7→5) kod ile senkron güncellenmeli (#108) | 🟢 |
| A8 | **[YENİ, 26. sohbet]** ARCHITECTURE.md + DEPENDENCIES.md — `menu_items`/`admin` rolü/`/admin` guard'ı işlenmeli (#110) | 🟢 |
| 1e | DEPENDENCIES.md'yi kapsamlı güncelle — `RegistrationChannel`'ın TÜM tüketicileri taransın (#71), ayrıca `useCartStore.tableId`, `order_history`, `users.role` gibi bu sohbetlerde eklenen alan/tablo/store değişiklikleri haritaya işlensin | 🟠 |
| 1f | TEST_MATRIX.md paylaşılınca `users.role` doğrulama testini işle: sütun var/`NOT NULL`/default doğru, mevcut kullanıcı kırılmadı (şu an 0 satır olduğu için gerçek regresyon testi #32 çözülünce yapılabilir) | 🟡 |
| 1g | SANDWICH_SPEC.md §8'deki 6 açık soru (S1-S6) netleştirilmeli — özellikle S1 (gerçek `sandwich-data.json`) BLOKLAYICI | 🟡 |
| 2 | #57'yi TAM kapat — `/online-siparis` sayfası (marketplace linkleri) | 🔴 |
| 3 | #73 kök neden araştırması: `tailwind.config.ts extend.colors` custom token'ları neden `bg-*` sınıfı olarak derlenmiyor | 🟠 |
| 4 | Neon DB şifresini resetle, `.env.local`'i güncelle (#60, güvenlik) | 🟠 |
| 4b | `npm audit fix` — 12 açık/3 kritik güvenlik açığını ayrı, sakin bir oturumda ele al (#63) | 🟠 |
| 5 | `app/kayit-ol/page.tsx` alt başlığı kararı — sil ya da CONTENT_GUIDE.md ile yeniden yaz (#61) | 🟢 |
| 6 | `/kvkk` sayfasını hukuk danışmanına incelettir (kullanıcı eylemi) | 🟡 |
| 7 | #58 Gel-al WhatsApp yönlendirme — artık #62 mimarisiyle birlikte tasarlanmalı | 🟡 |
| 8 | Twilio/Netgsm kararı — PARKLI (#32/#56) | ⚪ |
| 9 | Gerçek şube adresini Şubeler/Footer.tsx/JSON-LD şemasına işle (#54) | 🟡 |
| 91 | Güvenlik denetimi (#91) — canlıda GÖZLE doğrulama (role-revocation 403 + 6. yanlış şifre reddi) | 🔴 |
| 90 | #90 masaüstü sığdırma düzeltmesi — build+push+canlı doğrulama | 🟠 |
| 62 | #62 Gel Al "Teslim Edildi" canlı doğrulama | 🟠 |
| 86 | #86 Kayıt Onayları test seti + canlı doğrulama | 🟡 |
| 99 | #99 Sandviç checkout blokajı kök neden — `grep -rn "fiyatlandırılamadı"` çıktısı bekleniyor | 🔴 |
| 105 | Motion System — CartDrawer/MenuCard push + canlı doğrulama, CategoryNav (P0-3) | 🟡 |
| 10 | DESIGN_SYSTEM.md paylaşılırsa `ProfileForm.tsx`+`RegistrationForm.tsx` Tailwind sınıflarını TAM teyit et (#38) | 🟢 |
| 11 | CONTENT_GUIDE.md §1/§2 â örnekleri ve StepBase.tsx güncelle (#53) | 🟢 |
| 12 | AboutValues.tsx ile ValueProps.tsx senkronunu teyit et (#55) | 🟢 |
| 13 | Vektörel ikon seti üretimi (25-30 malzeme) (#52) | 🟡 |
| 14 | PHOTOGRAPHY_GUIDE.md §8 notu düzeltilmeli (#52 ile bağlantılı) | 🟢 |
| 15 | Boostfeel/QR tabanlı sadakat çözümü değerlendirilmeli | 🟡 |
| 16 | `AddToCartButton.tsx` + `useCartStore.ts` tam dosya teyidi (#50/#51) | 🟢 |
| 17 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a güncelle (#10) | 🟡 |
| 18 | Alerjen gösterimini MenuCard/Customizer/SummaryPanel'de fiilen uygula | 🟡 |
| 19 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 20 | VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat | 🟢 |
| 21 | Customizer adım başlıklarını Türkçeleştir / spec ile senkronla (#28/29) | 🟢 |
| 22 | Genel `npm test` (tüm proje) çalıştırıp güncel geçen/kalan sayıyı teyit et | 🟢 |
| 23 | [TAMAMLANDI] `types/index.ts` görüldü, #68 (RegistrationChannel/FulfillmentChannel tip etkisi) netleşti ve kodlandı | ✅ |
| 24 | [TAMAMLANDI] Vercel build yeşil doğrulandı (1d) | ✅ |
| 25 | [TAMAMLANDI] #62'nin 3 mimari sorusu kapandı — ARCHITECTURE.md v1.12 | ✅ |
| 26 | ROADMAP.md'ye #62 (Personel Sipariş Paneli) için ayrı bir oturum/kalem eklenmesi düşünülmeli — şu an hiç yer almıyor | 🟢 |
| 27 | [TAMAMLANDI, önceki tur] `users.role` migration'ı Neon'da koşuldu, `role text` sütunu Tables görünümünde doğrulandı | ✅ |
| 28 | [TAMAMLANDI, önceki tur] #70 kapandı — `order_history.table_number`/`status`/`customer_notes` migration'ı Neon'da koşuldu ve doğrulandı | ✅ |
| 29 | [TAMAMLANDI, önceki tur] #62 Masaya sekmesi (10 dosya) uçtan uca kodlandı, build+deploy yeşil, canlıda gerçek test siparişiyle doğrulandı | ✅ |
| 30 | [TAMAMLANDI, önceki tur] #89 IP delili + engellenen deneme logu — 4 dosya kodlandı, migration Neon'da koşuldu+6 sorguyla doğrulandı, test 6/6 PASS (Codespaces), Vercel deploy yeşil | ✅ |
| 31 | [TAMAMLANDI, 26. sohbet] `menu_items` tablosu migration+seed Neon'da koşuldu ve doğrulandı (13 kolon, 8 satır) | ✅ |
| -13 | **[TAMAMLANDI, 25. sohbet, 2026-09-05 ✅]** Motion System rapor P2 — VisualPreview Layer entrance. Kod ZATEN vardı, sadece hardcoded değerler yerine merkezi `durations.visualPreviewLayer`+`easings.easeOut` token'larına bağlandı. Görsel değişiklik YOK. | ✅ |
| -6a | **[YENİ, 24. sohbet]** `git add .` ile ilgisiz/istenmeyen dosyalar commit'e karışmış: `tsconfig.tsbuildinfo`, `test-tutarsizlik-callback.js`. `.gitignore`'a `*.tsbuildinfo` eklenmesi ve o test dosyasının kasıtlı mı yanlışlıkla mı eklendiğinin teyit edilmesi gerekiyor. | 🟠 |
| -6b | **[YENİ, 24. sohbet — YEDİNCİ DERS adayı]** Dosya var/yok iddiaları kullanıcının "emin değilim" cevabına rağmen kesin ifadeyle sunulmamalı, "kontrol edin" ile sınırlı kalmalı. | 🟢 (ders notu) |
| -5 | **[YENİ, 22. sohbet]** #99 — Sandviç checkout'u BLOKLU. **AYRICA:** #100-#104'teki 7 dosya değişikliğinin hangilerinin fiilen push/test edildiği kullanıcıdan tek tek teyit alınmalı. | 🔴 |
| -4b | **[YENİ, 2026-09-03]** Motion System rapor P0-2/P0-3: MenuCard, CategoryNav. P0-1 (CartDrawer) TAMAMLANDI (#105) — push/canlı doğrulama + DESIGN_SYSTEM.md/CORE.md senkronu hâlâ bekliyor. | 🟡 |
| -4 | **[YENİ, bu turda]** #92/#93/#94 — Çok şubeli mimari + şube-bazlı menü + CRM/attribution katmanı — SADECE analiz+öneri yapıldı, kod YOK. Kullanıcı kararıyla #91'DEN SONRAYA alındı. | 🟡 |
| -3 | **[YENİ, bu turda]** #91 — Güvenlik denetimi SEC-01/SEC-02 kod+test+build+tsc TAMAM. **KALAN:** canlıda (a) role-revocation 403 testi, (b) 6. yanlış şifre denemesinin reddi — ikisi de GÖZLE doğrulanmalı, sonra 5 dosya GitHub'a push edilmeli. | 🔴 |
| -2 | **[YENİ, bu turda]** #90 — `/menu/customize/[id]` masaüstü tek-ekrana-sığma düzeltmesi kodlandı. **KALAN:** build koşulmalı, GitHub'a push edilmeli, masaüstünde GÖZLE doğrulanmalı. | 🟠 |
| -1 | **[TAMAMLANDI ✅]** #84 — isim gösterme sorunu kullanıcı tarafından canlıda doğrulandı. | ✅ |
| 0 | **[TAMAMLANDI ✅]** #83 — "Sıfırla" → üretilen geçici kodla giriş canlıda BAŞARILI test edildi. | ✅ |
| 0b | **[TAMAMLANDI ✅]** #82 — orijinal kayıt şifresiyle çıkış→giriş döngüsü canlıda BAŞARILI test edildi. | ✅ |
| 0a | #80 — masaüstünde (`SummaryPanel.tsx`) #79 fix'inin canlı doğrulaması notu (düşük öncelik) | 🟢 |
| 0c | #78 — Customizer sticky özet panelin collapsed halde "Sepete Ekle"yi gizlemesi için UX çözümü kararlaştırılıp uygulanmalı | 🟢 |
| 1 | #62 Masaya sekmesi TAMAMLANDI + canlı doğrulandı. Gel Al onay kuyruğu #85 KAPANDI. 3-durumlu revizyon (KARAR A) kodlandı, 37/37 PASS. **KALAN:** canlı "Teslim Edildi" doğrulaması. | 🟠 |
| 1c | #86 Kayıt Onayları (4. sekme) — kod+build tarafı KAPANDI. **KALAN:** test seti yazılmalı, canlı doğrulanmalı. | 🟡 |
| 1b | Genel giriş/kayıt akış kararları: (i) guest gate middleware'i TAMAMLANDI; (ii) `/masaya-siparis` KAPSAM DIŞI BIRAKILDI (kullanıcı kararı); (iii) "Sepete Ekle" bypass component-guard'ı (#66 — karar bekliyor); (iv) KAPANDI — kayıt sayfasında zorunlu kanal seçimi zaten kodluymuş, uçtan uca teyit edildi. | 🟡 (iii) hâlâ açık |
| 1d | ARCHITECTURE.md §4.1'deki `users.role` notu güncellenmeli; §2.9a'ya Masaya kısmının TAMAMLANDIĞI + `order_history` şema genişletmesi işlenmeli | 🟡 |

*BOWLERA SESSION_INDEX.md — v85 (v82'den: **[bu turda, 2026-09-23]** 400 satır eşiği altıncı kez aşıldı (485 satır) — bu kez tablo hücreleri değil, ÇOK SATIRLI bloklar (header ders/taşıma-uyarı bloğu, CURRENT FOCUS TAŞINDI anlatıları, v75-v79 footer sürüm notları) tek satıra indirilip arşive taşındı; 485→334 satıra indi. Kayıp yok, hepsi Arşiv Taşıma Kaydı tablosunda ve ilgili Açık Sorun/Kritik Kararlar satırlarında özetli.)*

*BOWLERA SESSION_INDEX.md — v82 (v81'den: **[28. sohbet, 2026-09-07]** İLK GERÇEK KULLANICI
TESTİ VE CACHE BUG'I. Admin panelde yeni ürün ("Fogy") oluşturuldu — Neon'da DB'ye yazıldığı
DOĞRULANDI ama liste sayfasında hiç görünmedi. Kök neden bulundu: `app/admin/page.tsx`
`dynamic` export'u olmadığı için Next.js tarafından build-anı statik önbelleğe alınıyordu.
`export const dynamic = 'force-dynamic'` hem liste hem düzenleme sayfasına eklendi — canlı
doğrulama BEKLİYOR (#114, YENİ). Ayrıca netleşti: sitenin kendisinin `menu_items`'a hiç
bağlanmadığı (bilinçli, ayrı görev) bu turda kullanıcıya AÇIKÇA hatırlatıldı, bir "hata"
sanılmasın diye. 400 satır eşiği beşinci kez aşıldığı için 26. sohbetin ayrıntılı planlama
anlatısı arşive taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-07.md`) — içerik Kritik
Kararlar/Açık Sorunlar'da zaten tam özetli, kayıp yok.)*

*BOWLERA SESSION_INDEX.md — v81 (v80'den: **[27. sohbet, 2026-09-06]** ADMIN PANEL CANLIYA
ALINDI. #112 KAPANDI — 4 senkron dosya (schema/auth/middleware/next-auth.d.ts) repoya
uygulandı, tsc+build temiz, push edildi, Neon'da `role='admin'` atandı ve canlıda
doğrulandı. **YENİ KARAR:** admin hesabının aynı zamanda staff paneline de erişmesi
istendi — `middleware.ts`'teki `/personel` guard'ı `admin`'i de kabul edecek şekilde
genişletildi (`/admin` guard'ı hâlâ sadece `admin`'e özel, tek-admin kararı korundu).
#113 KAPANDI — Admin panelinin ilk CRUD'u (9 dosya: upload-image route, menu-items
list+create+update+delete route'ları, MenuItemForm, admin sayfaları) yazıldı, ImageKit
hesabı açılıp entegre edildi, 3 build hatası (eksik npm paketi, TS literal-tipi hatası,
unutulan app/admin/page.tsx) sırayla bulunup düzeltildi. **CANLIDA DOĞRULANDI:** `/admin`
8 gerçek ürünü doğru listeliyor. **KALAN:** düzenleme formu + yeni ürün oluşturma + gerçek
ImageKit yüklemesi ucu ucuna henüz canlıda test edilmedi (bkz. #113 detayı) — sıradaki
oturumun ilk işi bu olmalı. Görsel önizlemenin admin listesinde kırık ikon göstermesi
kozmetik bir detay, gerçek bir hata değil.)*

*BOWLERA SESSION_INDEX.md — v80 (v79'dan: **[26. sohbet, 2026-09-05]** ADMIN PANEL
PLANLAMASI BAŞLADI. Görsel depolama ImageKit olarak kararlaştırıldı. Menünün gerçek konumu
doğrulandı (#93 KAPANDI). `menu_items` DB tablosu migration+seed Neon'da koşuldu ve
doğrulandı (13 kolon, 8 satır). `"admin"` rolü `schema.ts`/`auth.ts`/`middleware.ts`/
`types/next-auth.d.ts` dört dosyada senkron kodlandı, `/admin`+`/api/admin` middleware
guard'ı `/personel` deseniyle aynı şekilde (fail-closed, role==='admin' katı şartı)
eklendi — DÖRDÜ DE kullanıcıya verildi ama REPOYA UYGULANDIĞI/PUSH EDİLDİĞİ TEYİT EDİLMEDİ
(YENİ Açık Sorun #112, en yüksek öncelik). 2 yeni doküman-kod uyuşmazlığı bulundu: alerjen
listesi DESIGN_SYSTEM.md'de 7, kodda 5 (#108); canlı filtre ekranında Keto/glutensiz/
sıcak-tahıl tag'leri gerçek veriyle uyuşmuyor (#109). `build-your-own-kasem` test kaydının
tabloya dahil edilmemesi kararı `grep` ile KODDA DOĞRULANDI. Bu güncelleme dosyayı 400 satır
eşiğinin ÜZERİNE çıkardı — bir sonraki sohbette arşivleme/taşıma ele alınmalı (bu turda
arşiv dosyasının güncel hâli görülmediği için taşıma yapılamadı, bkz. dosya başındaki YENİ
TAŞIMA UYARISI).)*

*BOWLERA SESSION_INDEX.md — v75-v79 sürüm notları (2026-09-04/05 arası, Motion System P0-P2 kapanışı + AccountMenu/CartBadge/Customizer spatial transition detayları) `session_arsiv_2_EKLENTI_2026-09-23-versiyon-notlari.md`'ye taşındı — içerik zaten Kritik Kararlar/Açık Sorunlar tablosunda (#105-#107, Motion System P0 bölümü) özetli.*
