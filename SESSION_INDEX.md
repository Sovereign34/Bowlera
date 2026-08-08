# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> **Şişmeyi önleme yöntemi:** Bu dosya SADECE anlık durumu tutar — tamamlanmış görevler
> Açık Sorunlar tablosundan silinir. Turn-by-turn geçmiş (📜 GEÇMİŞ/ARŞİV) burada TUTULMAZ,
> `session_arşiv.md` / `session_arşiv_1.md`'ye taşınır. Bu, arşivi SİLMEK değil DOĞRU
> DOSYAYA TAŞIMAK'tır. **[Session 12 devamı, 2026-08-08]:** Arşiv artık İKİ dosyaya
> bölünmüştür — Session 0-10 → `session_arşiv.md`, Session 11'den itibaren →
> `session_arşiv_1.md` (ilişki notu o dosyanın başlığında). Bölünme sadece hacim
> nedeniyledir, kural değişmedi.
> ⚠️ GEÇMİŞ İHLAL KAYDI (ders çıkarıldı, hâlâ geçerli):
> 2026-07-20'de üretilen bir "v2 sıkıştırılmış" SESSION_INDEX dosyası, kapanış notu
> olmadan 7 açık sorunu (#4,7,15,16,20,22,34) ve 2 kararı (#11,#12) tablolardan düşürmüştü.
> Bu, aynı gün içindeki bir sonraki sohbette fark edilip geri eklenmiş, ve BU sohbette
> tek tek dosyayla teyit edilerek gerçek sonuçlarına kavuşturulmuştur. Kural teyit edildi:
> tamamlanmış görev silinirken MUTLAKA kapanış gerekçesi session_arşiv.md'ye yazılmalı;
> aksi halde "tamamlandı" iddiası doğrulanamaz hale geliyor.
> ⚠️ İKİNCİ DERS (2026-08-02): AGENT.md/CORE.md'deki "400 satır eşiği" kuralı bu sohbette
> kısa süreliğine kaldırılmış, kullanıcı aynı gün içinde bunun yanlış anlaşılma olduğunu
> belirtmiş ve kural AYNEN eski hâline döndürülmüştür (AGENT.md v1.5, CORE.md v1.4).
> Net etki: kural DEĞİŞMEDİ. Governance dosyalarında büyük kural değişikliği istenirse
> önce açıkça onay alınmalı, geri dönüşü kolay olmayan varsayımlar yapılmamalı.
> ⚠️ ÜÇÜNCÜ DERS (2026-08-06/07, Session 8): Session 7'de #57 "kod+test tamam" olarak
> kapanış notuyla işaretlenmişti — ama kod hiçbir sayfaya bağlanmamıştı. Kullanıcı canlı
> production'da eski/kırık Twilio giriş akışıyla karşılaşana kadar bu fark edilmedi.
> Kural: bir görev "tamamlandı" işaretlenmeden önce SADECE kod+test yeterli değildir —
> kullanıcının o akışa GERÇEKTEN erişebildiği (route bağlı, buton/link çalışıyor) ayrıca
> doğrulanmalı. "Dokümantasyon tamam" ile "kullanıcı deneyimi tamam" AYRI kontrol noktaları.
> ⚠️ DÖRDÜNCÜ DERS (2026-08-07, Session 11): Session 10'un kapanış notunda "konuşma
> giriş/kayıt akışlarına geçti, içeriği sağlanmadı, bir sonraki güncellemede eklenecek"
> denmişti — ama o sohbet kapandığında SESSION_INDEX GÜNCELLENMEDEN kaldı. Kullanıcı,
> kapanan sohbetin tam metnini yeni bir sohbete taşıyarak bu güncellemeyi GERİYE DÖNÜK
> yaptırdı. Kural teyit edildi: "bir sonraki güncellemede eklenecek" notu bırakmak,
> güncellemenin GERÇEKTEN yapılacağının garantisi değildir. Mümkünse görev, sohbet
> kapanmadan ÖNCE işlenmeli; bu mümkün değilse not AÇIK SORUN olarak da ayrıca loglanmalı.

---

## 🎯 CURRENT FOCUS

> **[Session 12 devamı, 2026-08-08 — ARCHITECTURE.md v1.7 senkronu]** Ayrı bir sohbette
> (bu sohbetin dışında) ARCHITECTURE.md, KARAR BİLDİRİMİ + kullanıcı onayıyla v1.7'ye
> güncellenmişti: **Masaya Sipariş, genel giriş/kayıt akışından (§2.7a) TAMAMEN AYRILDI**
> ve ayrı, auth gerektirmeyen bir QR yüzeyine (`/masaya-siparis/*`) taşındı — yeni §2.7b.
> Bu sohbette SESSION_INDEX.md o kararla senkronize edildi:
> - **#65 KAPANDI** — gerekçe: middleware'in matcher'ı zaten `/menu/customize/:path*`
>   ile sınırlı; `/masaya-siparis/*` bu prefix'in DIŞINDA olduğu için Masaya Sipariş'e
>   özel bir guest-istisnası eklemeye HİÇ gerek kalmadı. Sorunun kendisi mimari kararla
>   ortadan kalktı (kod hâlâ yazılmadı, ama artık "istisna eklenmeli" görevi geçersiz).
> - **3 yeni açık soru** (#67/#68/#69) eklendi — ARCHITECTURE.md §2.7b'de kasıtlı olarak
>   AÇIK bırakılmış, tahmin edilmemiş sorular (bkz. AÇIK SORUNLAR tablosu).
> - **SIRADAKİ GÖREVLER 1b** güncellendi — middleware istisnası alt-kalemi kaldırıldı,
>   yerine `/masaya-siparis/*` yüzeyinin kodlanması görevi eklendi (henüz başlanamaz,
>   #67/#68/#69 netleşmeli).
> - **Sepet kararı teyidi:** `useCartStore` Masaya ile Gel Al arasında PAYLAŞILACAK (ayrı
>   state kurulmayacak) — gerekçe: Katman Kuralı §1 madde 7'de zaten teyitli olan
>   "`useCartStore` auth durumuna göre dallanmaz" ilkesiyle tutarlı, ayrıca zaten test
>   edilmiş fiyat/kalori hesaplama mantığının tekrarını önlüyor (Sahte Veri Yasağı ruhu).
> - **400 satır eşiği bu turda tetiklendi** (dosya 399 satırdaydı) — kullanıcı onayıyla
>   taşıma BÜYÜK tutuldu: Session 11 + Session 12'nin tam CURRENT FOCUS anlatı blokları
>   VE eski versiyon dipnot paragrafları `session_arşiv_1.md`'ye taşındı (bkz. dosya sonu).
> **Bu turda kod ÜRETİLMEDİ** — sadece dokümantasyon senkronu (Kural #6 gereği, kod
> aşamasına geçilmeden önce bu KARAR BİLDİRİMİ + onay adımı tamamlanmalı).

> **[Aynı sohbetin devamı] #67 KAPANDI.** İki seçenek (A: bağımsız mini-checkout, B:
> `/siparis`'in varyantı) Claude tarafından karşılaştırmalı analiz edildi, **Seçenek A**
> önerildi ve kullanıcı tarafından AYNEN ONAYLANDI: `/masaya-siparis` kendi bağımsız
> mini-checkout'unu kullanacak, `/siparis`'e (§2.9, Gel Al'a özel) bağlanmayacak. Gerekçe:
> Masaya'nın auth/kanal-seçimi mimarisinden tam izolasyonu — `/siparis`'e bağlanmak Gel
> Al'a özel mantığın (hesap girişi, ilk-sipariş manuel onay) sızma riskini taşıyordu.
> Fiyat/özet GÖSTERİMİ paylaşılabilir, checkout AKIŞI paylaşılmayacak. ARCHITECTURE.md
> v1.8'e işlendi. **Bu turda da kod ÜRETİLMEDİ** — sadece mimari karar netleşti.

> 📦 **[Bu turda taşındı — Session 12 devamı]** Session 11 ve Session 12'nin tam CURRENT
> FOCUS anlatı blokları (genel giriş/kayıt akışı netleşmesi, #62 kapsam genişlemesi, #64
> kapanışı, Session 12 retroaktif middleware doğrulaması — ~135 satır) `session_arşiv_1.md`'ye
> taşındı — hepsi kapanmış/geçmiş anlatı, SESSION ÖZET tablosunda (Session 11/12 satırları)
> ve KRİTİK KARARLAR/AÇIK SORUNLAR tablolarında özleri zaten korunuyordu. Tam metin
> gerekirse `session_arşiv_1.md`, Taşıma Bloğu #1'e bakılmalı.

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
| 🆕 | **[Session 11, KRİTİK]** "Kasa paneli" = Personel Sipariş Paneli (#62), TEK panel — Masaya gerçek-zamanlı akışı + Gel Al ilk-sipariş manuel onay kuyruğu | 🔴 Kapsam netleşti, mimari tasarım HENÜZ YAPILMADI |
| 🆕 | **[Session 11 devamı, #64 KAPANDI]** Gel Al onayı SADECE ilk siparişte — doğrulama durumu alanı (`pending`/`confirmed`) tutulur | ✅ Karar netleşti, #62 tasarımına eklendi, henüz KODLANMADI |
| 🆕 | **[Session 12 devamı, KRİTİK — ARCHITECTURE.md v1.7]** Masaya Sipariş genel giriş/kayıt akışından TAMAMEN AYRILDI, ayrı `/masaya-siparis/*` yüzeyine taşındı (auth gerektirmez, guest-istisnası mekanizması yerine mimari izolasyon). `useCartStore` PAYLAŞILIR (ayrı state kurulmadı). Middleware'e YENİ istisna GEREKMİYOR — bu nedenle #65 KAPANDI. | ✅ Karar netleşti (ARCHITECTURE.md v1.7), henüz KODLANMADI — 2 açık soru kaldı (#68/#69) |
| 🆕 | **[Session 12 devamı, #67 KAPANDI — ARCHITECTURE.md v1.8]** `/masaya-siparis` KENDİ BAĞIMSIZ mini-checkout'unu kullanacak — `/siparis`'in (§2.9, Gel Al'a özel) varyantı OLMAYACAK. Gerekçe: Gel Al'a özel mantığın (hesap girişi, ilk-sipariş manuel onay) Masaya'ya sızma riskini önlemek. Fiyat/özet gösterimi paylaşılabilir, checkout akışı paylaşılmayacak. | ✅ Karar netleşti (ARCHITECTURE.md v1.8), henüz KODLANMADI |
| 🗄️ | **[Session 12 devamı, #68 KAPANDI — ARCHITECTURE.md v1.9]** `RegistrationChannel`'dan `"masaya-siparis"` ÇIKARILDI (`FulfillmentChannel`'a taşınmadı). `20260808000000_registration_channel_masaya_siparis_cikarildi.md` | ✅ `types/index.ts` düzenlendi, migration gerekmedi (DB sütunu enum değil) |
| 🆕 | **[Session 12 devamı, #69 KAPANDI — ARCHITECTURE.md v1.10]** `order_history.channel` Masaya/Gel Al ayrımı için yeterli bulundu, ek alan eklenmedi. §2.7b'nin açık soru listesi tamamen kapandı. | ✅ Karar netleşti, kod HENÜZ YAZILMADI (1b bekliyor) |

*(Tam gerekçe/tarih dökümü için: `session_arşiv.md` [Session 0-10], `session_arşiv_1.md` [Session 11+].)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor | `ARCHITECTURE.md` §2.4 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi | `lib/customizer-data.ts` |
| 27 | 🟢 | Hero.tsx KAPANDI. StepBase.tsx hâlâ â içeriyor | `components/customizer/StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — PARKLI | `lib/auth/send-otp.ts` |
| 34 | 🟢 | `VisualPreview.tsx`'in `className` davranışı — tam repo taraması eksik | `components/customizer/VisualPreview.tsx` |
| 38 | 🟢 | `ProfileForm.tsx`/`RegistrationForm.tsx` Tailwind sınıfları TAM teyit edilmedi | `components/account/ProfileForm.tsx` |
| 39 | 🟠 | `/hesap` akışı Twilio kısıtı yüzünden canlıda test edilemedi | `app/hesap/page.tsx` |
| 50 | 🟢 | `AddToCartButton.tsx` hiç görülmedi — BSC-6 teyit edilmedi | `components/customizer/AddToCartButton.tsx` |
| 51 | 🟢 | `useCartStore.ts` tam dosya/persist davranışı hâlâ uçtan uca teyit edilmedi | `store/useCartStore.ts` |
| 52 | 🟡 | VisualPreview.tsx görsel katman klasörü boş | `components/customizer/VisualPreview.tsx` |
| 53 | 🟢 | CONTENT_GUIDE.md §1/§2 â→a kararına göre güncellenmedi | `CONTENT_GUIDE.md` §1, §2 |
| 54 | 🟡 | Gerçek şube adresi Şubeler/Footer.tsx/JSON-LD'ye işlenmedi — aciliyet var | `Footer.tsx` |
| 55 | 🟢 | `AboutValues.tsx` ile `ValueProps.tsx` senkronu teyit edilmedi | `components/about/AboutValues.tsx` |
| 56 | 🟢 | Twilio WhatsApp Business Sender onayı — PARKLI | `lib/auth/send-otp.ts` |
| 57 | 🟡 | Rıza esaslı kayıt — kod+test+canlı BAĞLANDI. KAPANMADI: `/online-siparis` sayfası yok | `app/kayit-ol/page.tsx` |
| 58 | 🟡 | Gel-al WhatsApp yönlendirme henüz kodlanmadı — #62 ile iç içe geçti | `lib/integrations/whatsapp.ts` |
| 59 | 🟡 | Kayıt sonrası kullanıcı adı/oturum durumu hiçbir yerde görünmüyor | `components/layout/Header.tsx` |
| 60 | 🟠 | Neon DB şifresi 3 kez açığa çıktı — Reset password HENÜZ ONAYLANMADI | Neon console, `.env.local` |
| 61 | 🟢 | `app/kayit-ol/page.tsx` alt başlığı uydurmaydı — kullanıcı karar bekliyor | `app/kayit-ol/page.tsx` |
| 62 | 🔴 | Personel Sipariş Paneli — Masaya gerçek-zamanlı akışı + Gel Al ilk-sipariş onay kuyruğu, TEK panel. Personel auth + real-time teknoloji + doğrulama durumu alanı HÂLÂ YAPILMADI. **[Session 12 devamı]:** artık §2.7b'den (Masaya) gelen veri ile §2.9a arasındaki bağlantı da #69'a bağlı. | `order_history`, personel auth sistemi (yok), real-time katman (yok) |
| 63 | 🟠 | `npm install`: 12 açık/3 kritik güvenlik açığı — `npm audit fix --force` bilinçli KOŞULMADI | `package.json` |
| 66 | 🟢 | İmza kase "Sepete Ekle" butonu (customize'a girmeden direkt ekleme) guest gate middleware'i tarafından YAKALANMIYOR — component-seviyesi guard gerekiyor. **[Session 12 devamı, kapsam teyidi]:** bu, `/menu/customize/*` (Gel Al) bağlamına özgüdür — Masaya artık ayrı `/masaya-siparis/*` yüzeyinde olduğu ve zaten auth gerektirmediği için bu sorunla kesişmiyor. AÇIK KARAR (kullanıcıdan teyit bekliyor): 1b'nin ayrı alt-görevi mi, bilinçli açık mı? | `components/customizer/AddToCartButton.tsx` |
| 68 | 🟢 | **[KAPANDI, Session 12 devamı, ARCHITECTURE.md v1.9]** `RegistrationChannel` tipinden `"masaya-siparis"` ÇIKARILDI, `FulfillmentChannel`'a taşınmadı. `types/index.ts` ve `lib/db/schema.ts` bu turda görüldü — `consentRegistrations.channel` sütunu enum değil düz `text`, migration gerekmedi. Şema notu: `docs/schema-changes/20260808000000_registration_channel_masaya_siparis_cikarildi.md`. | `types/index.ts` |
| 69 | 🟢 | **[KAPANDI, Session 12 devamı, ARCHITECTURE.md v1.10]** `order_history.channel` (`"dine-in"\|"pickup"`) Masaya/Gel Al ayrımı için YETERLİ — ek alan gerekmedi. Online Platform bu tabloya hiç yazmıyor, Gel Al onay durumu zaten `users.verificationStatus`'ta (kişi bazlı). §2.7b'nin açık soru listesi tamamen kapandı. | `order_history` şeması, §2.9a |

> **KAPANDI (bu turda):** #65 — Masaya Sipariş'in guest-girişi istisnasının middleware'e
> eklenmesi görevi, ARCHITECTURE.md v1.7 kararıyla (Masaya'nın middleware kapsamı dışına,
> ayrı `/masaya-siparis/*` yüzeyine taşınması) GEÇERSİZ hale geldi — istisnaya hiç gerek
> kalmadı. Kod hâlâ yazılmadı (bkz. SIRADAKİ GÖREVLER 1b).
> **#67** — Checkout varyantı sorusu, kullanıcı onayıyla Seçenek A (bağımsız mini-checkout)
> olarak çözüldü, ARCHITECTURE.md v1.8'e işlendi. Kod hâlâ yazılmadı.
>
> **KAPANDI (önceki turlar):** #4, #7, #15, #16, #20, #22/Karar #11, #35, #43, #44, #49, #64 —
> detaylar `session_arşiv.md` ve `session_arşiv_1.md`'de.

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
| 12 | 2026-08-08 | ⚠️ Retroaktif: guest-gate middleware'i zip ile doğrulandı (confidence HIGH), #65/#66 açıldı. **Devamında:** ARCHITECTURE.md v1.7'ye güncellendi (Masaya Sipariş ayrı `/masaya-siparis/*` yüzeyine taşındı), bu turda SESSION_INDEX o kararla senkronize edildi — #65 KAPANDI, #67/#68/#69 açıldı, 400 satır eşiği tetiklendi ve büyük bir taşıma yapıldı. | 🟡 1b kısmen tamamlandı; #67/#68/#69 netleşmeden §2.7b kodlanamaz |

*(Tam turn-by-turn detay: `session_arşiv.md` [0-10], `session_arşiv_1.md` [11+].)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel, Vercel Production'da deploy'lar Ready. |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 kod ile hizalı. **[Session 12 devamı]:** ARCHITECTURE.md v1.7'ye güncellendi, henüz koda yansımadı. |
| Test Suite | 🟢 `guest-gate.test.ts` (8 — kullanıcı tarafından koşuldu, PASS doğrulandı). Genel `npm test` hâlâ tekrar çalıştırılmadı. |
| Auth | 🟡 Twilio/Netgsm PARKLI. Genel giriş/kayıt akışı karar olarak netleşti, guest gate middleware'i KODLANDI ve repoda doğrulandı. **[Session 12 devamı]:** Masaya Sipariş kanalı artık middleware'in kapsamı dışında AYRI bir yüzeyde (`/masaya-siparis/*`) yaşayacak — bu yüzey henüz kodlanmadı. Gel Al akışı için "Sepete Ekle" bypass guard'ı (#66) hâlâ eksik. |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Kullanıcı Kaydı (rıza esaslı) | 🟡 Backend+Frontend TAMAM, canlı test BAŞARILI. Oturum göstergesi eksik (#59). Kanal seçimi zorunlu adımı henüz KODLANMADI. |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı, SADECE Gel Al'a özel (§2.9). **[Session 12 devamı, #67 KAPANDI]:** Masaya kendi bağımsız mini-checkout'unu kullanacak (ARCHITECTURE.md v1.8) — henüz KODLANMADI. |
| Veritabanı | 🟢 Neon Postgres çalışıyor. `consentRegistrations` ve `order_history` migrate edildi. ⚠️ DB şifresi reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik (#63). |
| Personel Sipariş Paneli (#62) | 🔴 Masaya gerçek-zamanlı akışı + Gel Al ilk-sipariş onay kuyruğu, TEK panel. Personel auth, real-time teknoloji VE onay kuyruğu tasarımı HÂLÂ YAPILMADI. **[Session 12 devamı]:** #68/#69 KAPANDI — mimari önü açık, tasarım/kod HENÜZ YAPILMADI. |
| Mimari Dokümantasyon | 🟢 **[Session 12 devamı]** ARCHITECTURE.md v1.7 — Masaya Sipariş §2.7a'dan ayrılıp §2.7b'ye taşındı, §1/§2.9/§2.9a/§3 senkron edildi. SESSION_INDEX.md v26 bu kararla senkron. |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | #62 Personel Sipariş Paneli mimari tasarımı — personel auth yöntemi, real-time teknoloji, onay kuyruğu UI/veri modeli, `pending`/`confirmed` şeması. **[Session 12 devamı]:** #68/#69 KAPANDI, tasarıma başlanabilir. | 🔴 |
| 1b | [GÜNCELLENDİ, Session 12 devamı, #67/#68/#69 KAPANDI] Genel giriş/kayıt akış kararlarını koda dök: (i) `/menu/customize/*` guest gate middleware'i TAMAMLANDI (repoda doğrulandı); (ii) ~~Masaya Sipariş guest istisnası middleware'e eklenmeli~~ — ARTIK GEÇERSİZ, bkz. #65 KAPANDI; (iii) `/masaya-siparis/*` yüzeyi (`page.tsx` + `customize/[id]/page.tsx` + **kendi mini-checkout'u**, #67 kararınca) HENÜZ KODLANMADI — mimari önü açık, başlanabilir; (iv) "Sepete Ekle" bypass component-guard'ı (#66 — eklensin mi kararı bekliyor); (v) kayıt sayfasında zorunlu kanal seçimi adımı hâlâ kodlanmadı | 🔴 |
| 2 | #57'yi TAM kapat — `/online-siparis` sayfası (marketplace linkleri) | 🔴 |
| 3 | Kayıt sonrası oturum/kullanıcı adı gösterimini araştır ve çöz (#59) | 🟡 |
| 4 | Neon DB şifresini resetle, `.env.local`'i güncelle (#60, güvenlik) | 🟠 |
| 4b | `npm audit fix` — 12 açık/3 kritik güvenlik açığını ayrı, sakin bir oturumda ele al (#63) | 🟠 |
| 5 | `app/kayit-ol/page.tsx` alt başlığı kararı — sil ya da CONTENT_GUIDE.md ile yeniden yaz (#61) | 🟢 |
| 6 | `/kvkk` sayfasını hukuk danışmanına incelettir (kullanıcı eylemi) | 🟡 |
| 7 | #58 Gel-al WhatsApp yönlendirme — artık #62 mimarisiyle birlikte tasarlanmalı | 🟡 |
| 8 | Twilio/Netgsm kararı — PARKLI (#32/#56) | ⚪ |
| 9 | Gerçek şube adresini Şubeler/Footer.tsx/JSON-LD şemasına işle (#54) | 🟡 |
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
| 23 | [Session 12 devamı, TAMAMLANDI] `types/index.ts` görüldü, #68 (RegistrationChannel/FulfillmentChannel tip etkisi) netleşti ve kodlandı | ✅ |

---

*BOWLERA SESSION_INDEX.md — v27 (v26'dan: aynı sohbetin devamında #67 KAPANDI —
`/masaya-siparis` checkout kararı: Seçenek A [bağımsız mini-checkout] kullanıcı tarafından
onaylandı, ARCHITECTURE.md v1.8'e işlendi. AÇIK SORUNLAR tablosundan #67 çıkarıldı, KAPANDI
notuna eklendi; #68/#69 §2.7b'nin artık 2 açık sorusu olarak yeniden numaralandırıldı
(Açık Soru #1/#2). KRİTİK KARARLAR tablosuna yeni satır eklendi. SIRADAKİ GÖREVLER 1b ve
madde 24 güncellendi — madde 24 (checkout kararı) #67'nin kapanmasıyla KAPANDI, listeden
çıkarıldı. GENEL DURUM'daki Checkout satırı senkron edildi. Bu turda da kod ÜRETİLMEDİ —
sadece mimari karar + dokümantasyon senkronu, KARAR BİLDİRİMİ + onay adımına uyuldu
(AGENT.md Kural #6). v26'daki 400 satır eşiği taşıması bu turda etkilenmedi, dosya hâlâ
eşiğin altında.
Güncellenme: 2026-08-08.*
