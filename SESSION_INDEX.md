# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> **Şişmeyi önleme yöntemi:** Bu dosya SADECE anlık durumu tutar — tamamlanmış görevler
> Açık Sorunlar tablosundan silinir. Turn-by-turn geçmiş (📜 GEÇMİŞ/ARŞİV) burada TUTULMAZ,
> `session_log.md`'ye taşınır. Bu, arşivi SİLMEK değil DOĞRU DOSYAYA TAŞIMAK'tır.
> ⚠️ GEÇMİŞ İHLAL KAYDI (ders çıkarıldı, hâlâ geçerli):
> 2026-07-20'de üretilen bir "v2 sıkıştırılmış" SESSION_INDEX dosyası, kapanış notu
> olmadan 7 açık sorunu (#4,7,15,16,20,22,34) ve 2 kararı (#11,#12) tablolardan düşürmüştü.
> Bu, aynı gün içindeki bir sonraki sohbette fark edilip geri eklenmiş, ve BU sohbette
> tek tek dosyayla teyit edilerek gerçek sonuçlarına kavuşturulmuştur. Kural teyit edildi:
> tamamlanmış görev silinirken MUTLAKA kapanış gerekçesi session_log.md'ye yazılmalı;
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

---

## 🎯 CURRENT FOCUS

```
Görev (GÜNCEL — 2026-08-06/07, Session 8):    Canlı production'da eski Twilio OTP
          `/giris` sayfasının hâlâ tek giriş noktası olduğu ve kırık olduğu keşfedildi
          (kullanıcı ekran görüntüsüyle bildirdi). #57'nin 2 açık ucu bu turda kapatıldı:
          (1) `/kayit-ol` route'u oluşturulup `RegistrationForm.tsx` bağlandı, `/giris`
          artık `/kayit-ol`'a redirect ediyor; Header.tsx'teki link güncellendi.
          (2) `/kvkk` sayfası, kullanıcıdan alınan gerçek şirket bilgileriyle (Bowlera
          şahıs şirketi, VKN 41905078374, Çağlayan Mah. Park Sokak No 30/B Kağıthane/
          İstanbul) oluşturuldu — hukuki taslak olarak işaretli, avukat incelemesi önerili.

          Ayrıca: `RegistrationForm.tsx`'teki "Kayıt Ol" butonu canlıda GÖRÜNMÜYORDU —
          kök neden `bg-olive-600` (Session 7'de tahmin edilmiş, geçersiz Tailwind
          rengi) idi, kanıtlanmış `bg-olive-primary` ile değiştirildi (nokta-atışı
          düzeltme, #38'in tam DESIGN_SYSTEM.md teyidini GEREKSİZ KILMAZ).

          `consentRegistrations` migration'ı hiç koşulmamıştı (Codespaces `.env.local`'de
          `DATABASE_URL` eksikti) — Neon connection string bulunup eklendi,
          `npx drizzle-kit push` BAŞARILI oldu. Kayıt formu canlıda uçtan uca test edildi:
          BAŞARILI (önceki "Kayıt şu an tamamlanamadı" hatası düzeldi).

          **#57 HÂLÂ TAM KAPANMADI — 1 açık uç kaldı:** `/online-siparis` sayfası yok
          (online-platform kanalı seçildiğinde yönlendirilen rota).

          **YENİ AÇIK UÇ (Session 8 keşfi, araştırılmadı):** Kayıt sonrası kullanıcı
          adı/oturum durumu hiçbir yerde görünmüyor — Header hesap ikonu giriş-yapılmamış
          görünümünde kalıyor. Bu akışta gerçek bir session/cookie kuruluyor mu, yoksa
          sadece DB'ye satır mı düşüyor — netleşmedi. → #61 (yeni).

          **Tam gerekçe, adım adım DB/env sorun giderme süreci, kullanıcı onaylarının tam
          metni → `session_log.md`, Session 8.**

Blokaj/Sıradaki için hâlâ bekleyen:
          Neon DB şifresi (`npg_8baAZqWogI1u`) süreç içinde 3 kez ekran görüntüsünde açığa
          çıktı — Reset password önerisi kullanıcıya 2 kez yapıldı, HENÜZ ONAYLANMADI.
          `app/kayit-ol/page.tsx` alt başlığı ("Bilgilerini bırak, seni arayalım.") Claude
          tarafından CONTENT_GUIDE.md görülmeden uydurulmuştu — kullanıcı karar bekliyor
          (sil / CONTENT_GUIDE.md'ye göre yeniden yaz). `INTEGRATIONS.md` §0 ve gerçek
          merkezi WhatsApp numarası (#58 için) hâlâ gelmedi.

Blokaj:   🟡 Twilio TR SMS kısıtı (#32) + Netgsm esnaf odası engeli (#56, 9000 TL) — İKİSİ DE
          PARKLI (silinmedi, öncelik değil).
Sıradaki: (0) #57'yi TAM kapatmak için kalan tek açık uç:
          (0i) `/online-siparis` sayfası (marketplace linkleri: Yemeksepeti/Getir/Trendyol),
          (0l) [YENİ, Session 8] Kayıt sonrası oturum/kullanıcı adı gösterimi araştır —
          gerçek bir session mekanizması var mı, yoksa sadece DB kaydı mı? Header'da nasıl
          yansıtılmalı? (#61)
          (0m) [YENİ, Session 8] Neon DB şifresini resetle (güvenlik, kullanıcı onayı
          bekliyor) ve `.env.local`'i yeni şifreyle güncelle.
          (0n) [YENİ, Session 8] `app/kayit-ol/page.tsx` alt başlığı kararı — sil ya da
          CONTENT_GUIDE.md ile uyumlu yeniden yaz.
          (0j) DESIGN_SYSTEM.md görülünce RegistrationForm.tsx + ProfileForm.tsx Tailwind
          sınıflarını TAM kapsamlı birlikte teyit et (#38 — Session 8'deki buton fix'i bunu
          GEREKSİZ KILMADI, sadece tek bir noktayı acil düzeltti).
          (0-2) #58 Gel-al WhatsApp yönlendirme: `wa.me` linki + sipariş özeti ön-doldurma,
          `lib/integrations/whatsapp.ts` içinde — `INTEGRATIONS.md` §0 + gerçek numara bekliyor.
          (0-ARŞİV) WhatsApp Sender (#56) ve Netgsm (9000 TL, #32) — PARKLANDI.
          (1) Şubeler/Footer.tsx/JSON-LD'ye gerçek adresi işle (#54, öncelikli —
          "yayına vereceğiz" ifadesiyle aciliyet belirtildi),
          (2) CONTENT_GUIDE.md'deki â örneklerini ve StepBase.tsx'i güncelle (#53, yeni),
          (3) AboutValues.tsx ile ValueProps.tsx senkronunu teyit et (#55, yeni),
          (4) ARCHITECTURE.md §2.4'ü 5 adıma (+ Bitkisel Protein) güncelle (#10),
          (5) customizerCatalog + "Benim Kâsem" fiyatı — fotoğraf çekimine bağlı (#24),
          (6) Customizer adım başlıklarının Türkçeleştirilmesi/spec senkronu (#28/29),
          (7) VisualPreview.tsx çağıranlarının tam repo taraması (#34),
          (8) AddToCartButton.tsx — hiç görülmedi, BSC-6 (çift tıklama koruması) teyit
          edilmeli (#50).
```

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI (özet — hâlâ etkili olanlar + yeniden teyit edilmesi gerekenler)

| # | Karar | Durum |
|---|---|---|
| 1 | Customizer 5 adım: Base → Main → Garden → Signature Flavor → Finish | ✅ Uygulandı |
| 3-4 | Garden: ilk 4 ücretsiz + avokado her zaman ücretli / Finish: ilk 1 ücretsiz | ✅ Uygulandı |
| 5 | "Make it Yours" → Finish'e entegre, "Double Main" → `mainPortion` yeniden kullanır | ✅ Uygulandı |
| 6 | Slogan: "Sağlıklı Beslen, Sağlıklı Yaşa, Gücünü Hisset" | ✅ |
| 11 | "Bitkisel Protein" tek Main kartı + 2 alt-varyant, inline genişleme, flavor filtreleme | ✅ Uygulandı, canlıda doğrulandı, spec tam senkron. MASTER_PLAN'a bilinçli taşınmadı (spec referansı korundu). |
| 12 | "Kâseni Yarat" sadece "Benim Kâsem" (`build-your-own-kasem`) ürününde | ⚠️ Bağlayıcı kapsam kuralı, ayrıca test edilmedi — hâlâ geçerli varsayılıyor. `loyaltyPoints` mekaniği hâlâ netleşmedi — muhtemelen QR-tabanlı fiziksel kayıt akışına (Boostfeel model) dayanmalı. |
| 13 | `FulfillmentChannel`: `"pickup"` \| `"dine-in"` (delivery yok), sepet/oturum seviyesinde tek alan | ✅ Canlıda doğrulandı. Session 7'de Session 6'nın 3-kanal kararına rağmen BİLİNÇLİ olarak DEĞİŞMEDİ — bkz. Karar #24. |
| 14-16 | `â` karakteri kaldırıldı (menu-data.json, CartDrawer). Hero.tsx/StepBase.tsx bilinçli ertelendi (#27) | ✅ `menu-data.json` içeriği görülüp `â` yokluğu doğrulandı |
| 15 | Customizer malzeme isimleri Türkçeye çevrildi (id'ler değişmedi) | ✅ Canlıda doğrulandı |
| 18 | CartDrawer portal fix (`createPortal` → `document.body`, backdrop-blur containing-block bug'ı için) | ✅ Canlıda doğrulandı |
| 19→20 | Auth: Twilio Verify + Auth.js JWT. DB: Neon Postgres, `users` tablosu (`phone`,`address`,`displayName`,`loyaltyPoints`,`verifiedAt`) | ✅ Kurulum tamam, build yeşil. |
| 20 | AuthenticatedUser tipi `address` alanıyla genişletildi, DB'de kalıcı saklanıyor | ✅ `types/index.ts`'te doğrulandı |
| 21-22 | Auth kod (route'lar, `auth.ts`, DB katmanı) + görünür giriş UI | 🟡 **[Session 8]** Eski `/giris` (Twilio OTP UI) KALDIRILDI, artık `/kayit-ol`'a redirect ediyor — Twilio/Netgsm PARKLI olduğu için bu UI zaten kullanılamaz durumdaydı. |
| 23 | Adres/profil modeli: adres SADECE profil/sadakat verisi, checkout'u bloklamaz, `/hesap`'ta opsiyonel toplanır | ✅ Kod üretildi VE repo varlığı doğrulandı |
| 🆕 | CategoryNav sekmeleri `BowlItem.category` enum'unu genişletmez — "vegan"/"sicak-tahil" sekmeleri `tags[]` üzerinden sanal filtrelenir | ✅ (#35 kapandı) |
| 🆕 | Alerjen gösterimi: kalori/protein ile aynı zorunluluk statüsü, gizlenemez/opsiyonel yapılamaz | ✅ (#7 ve #44 kapandı) |
| 🆕 | Site-geneli "kâse"→"kase" yazım kararı (â kaldırıldı) | ⚠️ Kısmen uygulandı: Hero.tsx tamam. CONTENT_GUIDE.md örnekleri, StepBase.tsx henüz güncellenmedi (#53). |
| 🆕 | Gerçek şube adresi: Çağlayan Park Sokak No:30, Kağıthane, İstanbul | ⚠️ Kısmen uygulandı: AboutStory.tsx'e işlendi. Şubeler/Footer/JSON-LD'ye henüz işlenmedi (#54). |
| 🆕 | **[DENEME AŞAMASI, kesin değil]** Twilio/Netgsm yerine geçici olarak: rıza (KVKK) esaslı, doğrulamasız telefon+adres toplama + gel-al siparişlerinde WhatsApp'a yönlendirme | 🟡 Mimari kararlaştırıldı, kod yazıldı VE **[Session 8]** kısmen CANLIYA BAĞLANDI (`/kayit-ol` route'u, `/kvkk` sayfası). `/online-siparis` hâlâ eksik. |
| 🆕 | **[Session 7]** Rıza kaydı `users` tablosundan AYRI, yeni `consentRegistrations` tablosunda tutulur | ✅ Kod+şema+test tamam. **[Session 8]:** Migration canlı Neon DB'sinde ÇALIŞTIRILDI, tablo artık gerçekten var. |
| 🆕 | **[Session 7]** Yeni `RegistrationChannel` tipi (`masaya-siparis`\|`gel-al`\|`online-platform`), `FulfillmentChannel`'DAN AYRI ve onu DEĞİŞTİRMEDEN eklendi | ✅ Kod+şema+test tamam. Kayıt sonrası seçim `fulfillmentChannel`'i ön-doldurur (dine-in/pickup); `online-platform` sepete hiç girmez. |
| 🆕 | **[Session 7]** `/siparis`'teki `FulfillmentGate` (2 kanal) SİLİNMEDİ — kayıt sonrası kanal seçimi bir ÖN-TERCİH, checkout'taki gate SON ONAY olarak kalıyor | ✅ Kod tarafında `FulfillmentGate`'e hiç dokunulmadı. |
| 🆕 | **[Session 8]** `RegistrationForm.tsx` buton rengi `bg-olive-600`'dan (tahmin, geçersiz) `bg-olive-primary`'ye (kanıtlanmış, `app/giris/page.tsx`'ten) düzeltildi | ✅ Canlıda doğrulandı — buton artık görünür. #38'in TAM DESIGN_SYSTEM.md teyidi hâlâ ayrı ve açık. |

*(Tam gerekçe/tarih dökümü için: `session_log.md`.)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor — 5 adıma hiç güncellenmedi | `ARCHITECTURE.md` §2.4, `CUSTOMIZER_SPEC.md` §3.1 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi | `lib/customizer-data.ts`, `lib/menu-data.json` |
| 27 | 🟢 | Hero.tsx KAPANDI. StepBase.tsx hâlâ â içeriyor — site-geneli karar kısmen uygulandı | `components/customizer/StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce; `CUSTOMIZER_SPEC.md` §2 senkron değil | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — PARKLI, #57/#58 mimarisi öncelikli hale geldi | Twilio Console, `lib/auth/send-otp.ts` |
| 34 | 🟢 | `VisualPreview.tsx`'in `className` davranışı — kısmi teyit edildi, tam repo taraması eksik | `components/customizer/VisualPreview.tsx` |
| 38 | 🟢 | `ProfileForm.tsx` VE `RegistrationForm.tsx` Tailwind sınıfları DESIGN_SYSTEM.md ile TAM teyit edilmedi — Session 8'de sadece buton rengi nokta-atışı düzeltildi, kapsamlı teyit hâlâ açık | `components/account/ProfileForm.tsx`, `components/registration/RegistrationForm.tsx` |
| 39 | 🟠 | `/hesap` akışı Twilio kısıtı yüzünden canlıda hiç fonksiyonel test edilemedi | `app/hesap/page.tsx` |
| 50 | 🟢 | `AddToCartButton.tsx` hiç görülmedi — BSC-6 ve disabled davranışı teyit edilmedi | `components/customizer/AddToCartButton.tsx` |
| 51 | 🟢 | `useCartStore.ts` — Session 7'de kısmen görüldü (`fulfillmentChannel`/`setFulfillmentChannel` teyit edildi), ama tam dosya/persist davranışı hâlâ uçtan uca teyit edilmedi | `store/useCartStore.ts` |
| 52 | 🟡 | VisualPreview.tsx + `lib/customizer-visual-layers.ts` görsel katman klasörü boş — vektörel ikon seti üretimi bekleniyor | `components/customizer/VisualPreview.tsx`, `PHOTOGRAPHY_GUIDE.md` §8 |
| 53 | 🟢 | CONTENT_GUIDE.md §1/§2'deki "Kâseni Yarat" örnekleri â→a kararına göre güncellenmedi | `CONTENT_GUIDE.md` §1, §2 |
| 54 | 🟡 | Gerçek şube adresi Şubeler/Footer.tsx/JSON-LD'ye henüz işlenmedi — kullanıcı aciliyet belirtti | `Footer.tsx`, Şubeler sayfası, JSON-LD şeması |
| 55 | 🟢 | `AboutValues.tsx` ile `ValueProps.tsx` senkronu teyit edilmedi | `components/about/AboutValues.tsx`, `components/home/ValueProps.tsx` |
| 56 | 🟢 | Twilio WhatsApp Business Sender onayı — PARKLI ($20 Upgrade gerekiyor) | Twilio Console, `lib/auth/send-otp.ts` |
| 57 | 🟡 | Rıza (KVKK) esaslı kayıt — kod+test TAMAM, canlıya BAĞLANDI (`/kayit-ol`, `/kvkk`), migration KOŞULDU, uçtan uca canlı test BAŞARILI. **KAPANMADI, 1 açık uç kaldı:** `/online-siparis` sayfası yok (online-platform kanalı seçildiğinde yönlendirilen rota). | `components/registration/*`, `app/api/registration/consent/route.ts`, `app/kayit-ol/page.tsx`, `app/kvkk/page.tsx` |
| 58 | 🟡 | Gel-al WhatsApp yönlendirme (`wa.me` linki) henüz kodlanmadı — `INTEGRATIONS.md` §0 + gerçek numara bekliyor. `WhatsAppOrderButton.tsx` zaten repoda var (disabled iskelet), sıfırdan yazılmayacak. | `lib/integrations/whatsapp.ts` (henüz yok), `components/order/WhatsAppOrderButton.tsx` |
| 59 | 🟡 | [YENİ, Session 8] Kayıt sonrası kullanıcı adı/oturum durumu hiçbir yerde görünmüyor — Header hesap ikonu giriş-yapılmamış görünümünde kalıyor. Bu akışta gerçek session/cookie var mı, kök neden araştırılmadı. | `components/layout/Header.tsx`, kayıt akışı auth mekanizması (araştırılacak) |
| 60 | 🟠 | [YENİ, Session 8] Neon DB şifresi (`npg_8baAZqWogI1u`) sorun giderme sürecinde 3 kez ekran görüntüsünde açığa çıktı — Reset password önerisi 2 kez yapıldı, HENÜZ ONAYLANMADI/YAPILMADI. | Neon console, `.env.local` |
| 61 | 🟢 | [YENİ, Session 8] `app/kayit-ol/page.tsx` alt başlığı ("Bilgilerini bırak, seni arayalım.") Claude tarafından CONTENT_GUIDE.md görülmeden uydurulmuştu — kullanıcı karar bekliyor (sil / yeniden yaz). | `app/kayit-ol/page.tsx`, `CONTENT_GUIDE.md` |

> **KAPANDI (önceki turlar):** #4, #7, #15, #16, #20, #22/Karar #11, #35, #43, #44, #49 —
> detaylar önceki SESSION_INDEX sürümlerinde ve `session_log.md`'de.
>
> Detaylı gerekçe/dosya alıntıları `session_log.md`'de (Session 0'dan Session 8'e tam).

---

## SESSION ÖZET (tümü — 0'dan 8'e)

| Session | Tarih | Ana içerik | Durum |
|---|---|---|---|
| 0 | — | Ajan altyapısı (14 dosya) | ✅ Tamamlandı |
| 1 | 2026-07-1x | Next.js+Tailwind kurulum, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| 2 | 2026-07-18 | Menü sayfası, filtreleme, MenuCard, statik veri, CategoryNav+FilterPanel, customizer 4→5 adım kararı | ✅ Tamamlandı |
| 3 | 2026-07-18 | Zustand store + pricing + customizer data, masaüstü UI bileşenleri (kesintiye uğradı) | ✅ Büyük ölçüde tamam |
| 4 (devam) | 2026-07-18 → 07-22 (11 bölüm) | Sepet/kanal seçimi, Türkçeleştirme, â düzeltmesi, CartDrawer bugfix, auth mimarisi+kod+DB+UI, adres/profil (#23), test triyajı, menü animasyonu, ARCHITECTURE.md v1.3→v1.4, rate-limit üretimi, repo tutarsızlığı keşfi (#42 kapandı), DESIGN_SYSTEM.md §7 (#7 kapandı), Bitkisel Protein uçtan uca, MobileSummaryDrawer konsolidasyonu (#43), AGENT.md v1.3 alerjen self-check (#44), CUSTOMIZER_SPEC.md §3.5 (#49), MASTER_PLAN/ROADMAP tutarlılık denetimi (#50/#51 yeni) | 🟡 Devam ediyor |
| 5 | 2026-08-01 → 08-02 (3 tur) | VisualPreview.tsx mimari denetimi (#52 açıldı), pazaryeri müşteri verisi araştırması (Boostfeel/QR model), Hakkımızda sayfası oluşturuldu, Hero.tsx â→a uygulandı, "400 satır eşiği" kuralı kaldırılıp geri getirildi, AGENT.md dosya karışıklığı çözüldü | 🟡 Devam ediyor — #53/#54/#55 yeni açıldı |
| 6 | 2026-08-05 (uzun, çok turlu) | Netgsm'in de esnaf odası/marka tescili istediği keşfedildi. WhatsApp OTP birincil+SMS fallback kodlandı, test edildi (3/3 PASS), push edildi. Twilio Upgrade denendi ($20), Netgsm alternatifinin de ~9000 TL gerektirdiği netleşti. Google/online platform sosyal girişi elendi. **Büyük mimari karar:** Twilio/Netgsm PARKLANDI, rıza (KVKK) esaslı toplama + WhatsApp yönlendirme kararlaştırıldı (#57/#58 açıldı). `WhatsAppOrderButton.tsx`'in zaten repoda var olduğu keşfedildi. | 🟡 Devam ediyor — #57/#58 kodlanacak |
| 7 | 2026-08-06 | #57 uçtan uca kodlandı ve test edildi (17/17 PASS). Zip ile gerçek repo incelendi, 3 kritik çelişki (checkout auth kuralı, users.phone şema çakışması, FulfillmentChannel kanal sayısı) kullanıcı onayıyla çözüldü: ayrı `consentRegistrations` tablosu, ayrı `RegistrationChannel` tipi, `FulfillmentGate` korunması kararları alındı. 11 dosya üretildi (şema, validasyon+test, DB sorgusu, rate-limit+test, API route, form hook+bileşen). 2 kez 20-satır kuralı ihlali kendi kendine düzeltildi. **#57 kapanmadı** — kod hiçbir sayfaya bağlanmadı. | 🟡 Devam ediyor |
| 8 | 2026-08-06/07 | Kullanıcı canlıda kırık Twilio giriş akışını keşfetti (ekran görüntüsü). `/kayit-ol` ve `/kvkk` route'ları oluşturulup bağlandı, Header.tsx güncellendi, eski `/giris` redirect'e çevrildi. `RegistrationForm.tsx`'teki görünmez buton bug'ı (`bg-olive-600`→`bg-olive-primary`) düzeltildi. `consentRegistrations` migration'ı (DATABASE_URL eksikliği giderilerek) canlı Neon DB'sinde koşuldu. Kayıt formu canlıda uçtan uca test edildi, BAŞARILI. Yeni açık uçlar keşfedildi: kayıt sonrası oturum/kullanıcı adı gösterimi eksik (#59), Neon şifresi 3 kez açığa çıktı/reset bekliyor (#60), Claude'un kendi uydurduğu alt başlık karar bekliyor (#61). **#57 hâlâ kapanmadı** — sadece `/online-siparis` kaldı. | 🟡 Devam ediyor — #57'nin son açık ucu + 3 yeni madde |

*(Tam turn-by-turn detay: `session_log.md`.)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel, Vercel Production'da deploy'lar Ready. Kullanıcı GitHub Codespaces (`3rw9.github.dev`) üzerinden de çalışıyor. |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 kod ile hizalı |
| Test Suite | 🟢 Header.test.tsx, customizer-summary-format.test.ts, menu-filters.test.ts, hakkimizda/page.test.tsx (2/2), send-otp.test.ts (3/3), `lib/registration/validation.test.ts` (9), `lib/auth/rate-limit.test.ts` (5), `lib/auth/rate-limit.registration.test.ts` (3). Genel `npm test` (tüm proje) hâlâ tekrar çalıştırılmadı. |
| Auth | 🟡 Twilio/Netgsm PARKLI (#32/#56). **[Session 8]:** Eski `/giris` (Twilio OTP) UI'ı kaldırıldı, rıza esaslı kayıt (`/kayit-ol`) birincil akış oldu. Oturum/kullanıcı adı gösterimi hâlâ netleşmedi (#59). |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Kullanıcı Kaydı (rıza esaslı) | 🟡 **[Session 8]** Backend + Frontend TAMAM, `/kayit-ol`'a BAĞLANDI, DB migration KOŞULDU, canlı uçtan uca test BAŞARILI. Kayıt sonrası oturum göstergesi eksik (#59). |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı — kanal seçimi zorunlu, `FulfillmentGate` dokunulmadan doğrulandı |
| Veritabanı | 🟢 Neon Postgres çalışıyor. **[Session 8]:** `consentRegistrations` tablosu migration'ı BAŞARIYLA koşuldu, tablo canlıda var. ⚠️ DB şifresi 3 kez açığa çıktı, reset bekliyor (#60). |
| ARCHITECTURE.md | 🟢 v1.4 güncel. §2.4 (#10) bilinçli kapsam dışı |
| Menü Filtreleme | 🟢 `lib/menu-filters.ts` — kod+test ile doğrulandı |
| Customizer Özet Formatlama | ✅ `lib/customizer-summary-format.ts` — kod+test ile doğrulandı |
| Alerjen Gösterim Sistemi | ✅ Tasarım tam. 🟡 UI implementasyonu henüz yazılmadı. |
| Bitkisel Protein (Main alt-varyant) | ✅ Kod + spec + canlı doğrulama tam. |
| Sepet (`useCartStore.ts`, `AddToCartButton.tsx`) | 🟡 `fulfillmentChannel`/`setFulfillmentChannel` sözleşmesi doğrulandı. Tam dosya/persist davranışı ve `AddToCartButton.tsx` hâlâ teyit edilmedi (#50/#51) |
| Customizer Görsel Önizleme (VisualPreview) | 🔴 Görsel katmanlar eksik (#52) |
| Hakkımızda Sayfası (`/hakkimizda`) | 🟢 Kod tamam, test geçti (2/2). Şubeler/Footer/JSON-LD adres senkronu bekleniyor (#54) |
| KVKK Aydınlatma Metni | 🟢 **[Session 8]** `/kvkk` route'una çevrildi, gerçek şirket bilgileriyle dolduruldu. Hukuki taslak — avukat incelemesi henüz yapılmadı. |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | #57'yi TAM kapat — `/online-siparis` sayfası (marketplace linkleri: Yemeksepeti/Getir/Trendyol) | 🔴 |
| 2 | [YENİ] Kayıt sonrası oturum/kullanıcı adı gösterimini araştır ve çöz (#59) | 🟡 |
| 3 | [YENİ] Neon DB şifresini resetle, `.env.local`'i güncelle (#60, güvenlik) | 🟠 |
| 4 | [YENİ] `app/kayit-ol/page.tsx` alt başlığı kararı — sil ya da CONTENT_GUIDE.md ile yeniden yaz (#61) | 🟢 |
| 5 | `/kvkk` sayfasını hukuk danışmanına incelettir (kullanıcı eylemi, Claude'un kapsamı dışı) | 🟡 |
| 6 | #58 Gel-al WhatsApp yönlendirme (`wa.me` linki, `WhatsAppOrderButton.tsx` iskeletini tamamla) — `INTEGRATIONS.md` §0 + gerçek numara bekliyor | 🟡 |
| 7 | Twilio/Netgsm kararı — PARKLI, acil değil (#32/#56) | ⚪ |
| 8 | Gerçek şube adresini Şubeler sayfası/Footer.tsx/JSON-LD şemasına işle (#54 — kullanıcı aciliyet belirtti) | 🟡 |
| 9 | DESIGN_SYSTEM.md paylaşılırsa `ProfileForm.tsx` + `RegistrationForm.tsx` Tailwind sınıflarını TAM kapsamlı teyit et (#38) | 🟢 |
| 10 | CONTENT_GUIDE.md §1/§2'deki â örneklerini ve StepBase.tsx'i güncelle (#53) | 🟢 |
| 11 | AboutValues.tsx ile ValueProps.tsx senkronunu teyit et (#55) | 🟢 |
| 12 | Vektörel ikon seti üretimi (25-30 malzeme) (#52) | 🟡 |
| 13 | PHOTOGRAPHY_GUIDE.md §8 notu düzeltilmeli (#52 ile bağlantılı) | 🟢 |
| 14 | Boostfeel/QR tabanlı sadakat çözümü değerlendirilmeli (Karar #12) | 🟡 |
| 15 | `AddToCartButton.tsx` + `useCartStore.ts` tam dosya teyidi (#50/#51) | 🟢 |
| 16 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a güncelle (#10) | 🟡 |
| 17 | Alerjen gösterimini MenuCard/Customizer/SummaryPanel'de fiilen uygula | 🟡 |
| 18 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 19 | VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat | 🟢 |
| 20 | Customizer adım başlıklarını Türkçeleştir / spec ile senkronla (#28/29) | 🟢 |
| 21 | Genel `npm test` (tüm proje) çalıştırıp güncel geçen/kalan sayıyı teyit et | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v21. Session 8 (2026-08-06/07) işlendi: kullanıcı canlı
production'da kırık Twilio giriş akışını keşfetti; #57'nin 2 açık ucu (`/kayit-ol`
tetikleyici route'u, `/kvkk` sayfası) bu turda kapatıldı, sadece `/online-siparis` kaldı.
`RegistrationForm.tsx`'teki görünmez buton bug'ı (tahmin edilmiş geçersiz Tailwind rengi)
kanıta dayalı olarak düzeltildi. `consentRegistrations` migration'ı canlı DB'de koşuldu ve
kayıt akışı uçtan uca canlı doğrulandı. 3 yeni açık madde eklendi (#59 oturum gösterimi,
#60 DB şifre resetleme, #61 Claude'un uydurduğu alt başlık kararı). Yeni bir "GEÇMİŞ İHLAL
KAYDI" (Üçüncü Ders) eklendi: "kod+test tamam" ile "kullanıcı gerçekten erişebiliyor"
ayrı doğrulama noktaları olmalı. Diğer tüm içerik v20'den korundu, hiçbir madde
gerekçesiz silinmedi.
Dosya artık ~260 satır — 400 eşiğinin altında, arşivleme gerekmedi.
Tam turn-by-turn gerekçe/karar dökümü için: `session_log.md` (Session 8 yeni bloğu ayrı
artifact olarak verildi — kullanıcı session_log.md'nin SONUNA ekleyecek, dosya TAM olarak
yeniden üretilmedi, AGENT.md Kural #4/YASAK LİSTE gereği).
Güncellenme: 2026-08-07.*
