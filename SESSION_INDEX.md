# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> **Şişmeyi önleme yöntemi:** Bu dosya SADECE anlık durumu tutar — tamamlanmış görevler
> Açık Sorunlar tablosundan silinir. Turn-by-turn geçmiş (📜 GEÇMİŞ/ARŞİV) burada TUTULMAZ,
> `session_arşiv.md`'ye taşınır. Bu, arşivi SİLMEK değil DOĞRU DOSYAYA TAŞIMAK'tır.
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
> giriş/kayıt akışları konusuna geçti, içeriği sağlanmadı, bir sonraki güncellemede
> eklenecek" denmişti — ama o sohbet kapandığında SESSION_INDEX GÜNCELLENMEDEN kaldı.
> Kullanıcı, kapanan sohbetin tam metnini yeni bir sohbete taşıyarak bu güncellemeyi
> GERİYE DÖNÜK yaptırdı. Kural teyit edildi: "bir sonraki güncellemede eklenecek" notu
> bırakmak, güncellemenin GERÇEKTEN yapılacağının garantisi değildir — kullanıcı takip
> etmezse içerik kaybolabilirdi. Mümkünse böyle bir not bırakılan görev, aynı sohbet
> kapanmadan ÖNCE işlenmeli; bu mümkün değilse not AÇIK SORUN olarak da ayrıca loglanmalı.
> ⚠️ 400 SATIR EŞİĞİ TAŞIMASI (2026-08-07, Session 11 devamı, checkpoint sırasında):
> CURRENT FOCUS'taki Session 8/9/10 "Görev (GÜNCEL...)" blokları (3 madde) — hepsi kapanmış/
> geçmiş anlatı, güncel değil, SESSION ÖZET tablosunda zaten özetleri mevcuttu — gerekçeli
> olarak `session_arşiv.md`'ye TAŞINDI. Aşağıda sadece Session 11'in GÜNCEL blokları kaldı.

---

## 🎯 CURRENT FOCUS

> **[Session 12, 2026-08-08 — RETROACTİF checkpoint, zip doğrulamalı]** Session 11'in
> kapanışında SIRADAKİ GÖREV 1b için kodlama başlamıştı; o sohbet de checkpoint onayı
> beklerken kapandı (SESSION_INDEX güncellenmeden). Kullanıcı önce kapanan sohbetin son
> mesajını (KARAR BİLDİRİMİ + checkpoint sorusu) yapıştırdı; Claude eksik veri nedeniyle
> (kod dosyaları görülmedi, "#65" referansı belirsizdi, "Sepete Ekle" kapsam sorusu
> cevapsızdı) üretmeyi reddedip 3 netleştirme istedi. Kullanıcı ardından GERÇEK REPO ZIP'İNİ
> yükledi — bu turda kod doğrudan repodan incelendi (tahmine dayanmadı):
> - `middleware.ts` + `lib/auth/guest-gate.ts` + `lib/auth/guest-gate.test.ts` repoda MEVCUT
>   ve zaten push edilmiş durumda görüldü.
> - `auth.ts`'in gerçek export şekli (`{ handlers, auth, signIn, signOut }`) doğrulandı —
>   `middleware.ts`'in `import { auth } from '@/auth'` çağrısıyla TAM uyumlu. Önceki turdaki
>   MEDIUM confidence gerekçesi (auth.ts export şekli görülmedi) bu turda ortadan kalktı →
>   **confidence HIGH'a yükseltildi.**
> - "#65" referansı `guest-gate.ts`/`middleware.ts` yorum bloklarında zaten belgeliydi:
>   Masaya Sipariş kanalının guest-girişi istisnası bu middleware'e BİLİNÇLİ OLARAK
>   eklenmemiş (kod yorumunda "kullanıcı onayı: B olmalı" notu var — bu onayın tam içeriği
>   bu turda görülmeyen bir önceki alt-turda verilmiş, sadece sonucu koda yazılmış).
> - "Sepete Ekle" bypass gap'i (component-seviyesi guard, #66) kullanıcıya hâlâ SORULMADI —
>   kod yorumunda "1b'nin bu turda ele alınmayan bir parçası" olarak dokümante edilmiş,
>   backlog'a eklenip eklenmeyeceği AÇIK karar olarak aşağıya işlendi.
> ⚠️ **Sınırlama:** Bu ortamda ağ erişimi yok, `npm test`/`vitest` ÇALIŞTIRILAMADI. Test
> dosyası (8 test: 2 happy + 4 edge + 2 failure) kod incelemesiyle doğrulandı, ama
> ÇALIŞTIRILARAK doğrulanmadı — bu ayrım kullanıcıya açıkça belirtildi, "PASS" iddia edilmedi.

> 📦 **[Session 11 checkpoint'inde taşındı]** Session 8, Session 9 ve Session 10'un
> CURRENT FOCUS anlatı blokları (Twilio→`/kayit-ol` geçişi, buton bug fix, migration
> koşumu; Masaya Sipariş fiziksel akış + #62'nin açılışı; `order_history` DB şeması
> alt-çalışması) 400 satır eşiği nedeniyle `session_arşiv.md`'ye taşındı — hepsi
> kapanmış/geçmiş anlatıydı, SESSION ÖZET tablosunda (Session 8/9/10 satırları) ve
> KRİTİK KARARLAR/AÇIK SORUNLAR tablolarında (#57–#63) özleri zaten korunuyor. Tam
> metin gerekirse `session_arşiv.md`, Session 8-9-10 bloklarına bakılmalı.

```
Görev (GÜNCEL — 2026-08-07, Session 11):    ⚠️ NOT: Bu güncelleme GERİYE DÖNÜK yapıldı —
          önceki sohbet (Session 10'un devamı) kapanmış ama SESSION_INDEX güncellenmemişti.
          Kullanıcı kapanan sohbetin tam metnini bu sohbete taşıdı, Claude ondan bu bloğu
          çıkardı (bkz. yukarıdaki DÖRDÜNCÜ DERS). Konu, Session 10'da "içeriği sağlanmadı"
          notuyla ertelenen **giriş/kayıt/sipariş kanalı akışı**ydı — bu turda tam olarak
          netleşti ve #62'nin kapsamı KRİTİK ŞEKİLDE GENİŞLEDİ:

          **Netleşen genel giriş/kayıt akışı (yeni, önceden kayıtlı değildi):**
          - Girişsiz kullanıcı menüde serbestçe gezinebilir; ama bir ürün SEÇTİĞİ an giriş
            sayfasına yönlendirilir.
          - Giriş sayfası her zaman iki seçenek sunar: **giriş** veya **kayıt**.
          - Kayıt seçilirse: kullanıcı bilgileri + KVKK metni okutulur → giriş sağlanmadan
            ÖNCE kanal seçimi (Masaya Servis / Gel Al / Online Platform) ZORUNLU.

          **Kanal bazlı netleşme (RECONCILE edildi — bkz. tablo):**
          | Kanal | Bilgi/Giriş gereksinimi | Sipariş tamamlama koşulu |
          |---|---|---|
          | Masaya Sipariş | YOK — kullanıcı kişisel bilgi vermek zorunda değil, **"Masaya Servis"** genel etiketiyle guest girişi yapar | Direkt tamamlanır, doğrulama yok |
          | Gel Al | Hesapla giriş (kayıt veya mevcut hesap), sepeti serbestçe doldurur | **İlk siparişte** Personel Sipariş Paneli'nden personel, telefon/WhatsApp üzerinden erişim teyidi yaptıktan sonra MANUEL ONAY vermeden sipariş tamamlanmaz |
          | Online Platform | — | `/online-siparis` (henüz yok) üzerinden Yemeksepeti/Getir/Trendyol'a yönlendirme — zaten kayıtlı karar (#57 açık ucu), bu turda DEĞİŞMEDİ, sadece teyit edildi |

          **KRİTİK KARAR — #62'nin kapsamı netleşti:** Sohbette bir çelişki ("QR'dan gelen
          kullanıcı bilgi vermeden de girebilir" ifadesi) ortaya çıktı, kullanıcıyla birlikte
          çözüldü: bu, genel "önce giriş/kayıt" kuralına istisna değil, SADECE Masaya
          Sipariş'in guest-girişi kuralıydı. Ardından kullanıcı "kasa paneli" ile #62'de
          tanımlı **Personel Sipariş Paneli**'nin AYNI ŞEY olduğunu teyit etti (tek panel,
          iki isim). Sonuç: Personel Sipariş Paneli artık SADECE Masaya Sipariş'in
          gerçek-zamanlı akışını değil, **Gel Al'ın ilk-sipariş manuel telefon/WhatsApp
          teyit+onay kuyruğunu da** yönetecek. Bu, #62'nin mimari tasarım kapsamını
          genişletiyor (personel auth + real-time katman kararı hâlâ yapılmadı, ama artık
          bu karar iki farklı iş akışını [anlık masa siparişi + bekleyen Gel-Al onayı]
          aynı panelde desteklemeli).

          ⚠️ **AÇIK, TEYİT EDİLMEMİŞ VARSAYIM (yeni, #64):** Kullanıcı "Gel Al'da bu onay
          adımı muhtemelen sadece İLK siparişte gerekiyor, sonrakilerde tekrarlanmıyor"
          dedi — ama bu netleşmiş bir karar DEĞİL, kullanıcının kendi ifadesiyle bile
          "muhtemelen". Claude bunu teyit etmek istediğini belirtti, sohbet kapandığı için
          teyit ALINAMADI. Bir sonraki sohbette netleştirilmeli.

          **Bu turda kod/dosya ÜRETİLMEDİ** — sadece akış netleştirildi ve SESSION_INDEX'e
          işlendi (Kural #6: her kod değişikliği öncesi KARAR BİLDİRİMİ + onay gerekir,
          burada henüz kod aşamasına geçilmedi).

Görev (GÜNCEL — 2026-08-07, Session 11 devamı):    **#64 KAPANDI.** Kullanıcı netleştirdi:
          Gel Al'da ilk siparişte yapılan manuel telefon/WhatsApp teyidi sırasında kullanıcı
          bilgileri zaten DB'ye yazılıyor — bu nedenle onay adımı SADECE ilk siparişte
          gerekiyor, sonraki siparişlerde sistem "bu kullanıcı zaten teyit edilmiş" bilgisine
          DB üzerinden bakabilir, tekrar personel onayı istemez.

          Bunun mimariye pratik yansıması Claude tarafından önerildi ve kullanıcı tarafından
          AYNEN ONAYLANDI — bu artık #62'nin mimari tasarımının bir PARÇASI olarak kayıtlı:
          - Kullanıcı kaydında bir **doğrulama durumu alanı** gerekiyor (örn.
            `phoneVerifiedAt` veya `manualConfirmationStatus: "pending" | "confirmed"`,
            kesin alan adı/tablo #62 mimari tasarımında netleştirilecek).
          - İlk sipariş → `order_history`'ye `pending` durumuyla düşer, Personel Sipariş
            Paneli'nde bekleyen onay olarak görünür. Personel onaylayınca hem o siparişin
            durumu HEM kullanıcının kaydı `confirmed` olur.
          - Sonraki siparişlerde panel bu alana bakar: `confirmed` ise sipariş direkt
            "aktif/hazırlanacak" gösterilir, ayrı onay kuyruğuna düşmez.

          Bu turda kod/şema HENÜZ ÜRETİLMEDİ — sadece mimari karar netleşti, #62'nin
          tasarım kapsamına eklendi. Kullanıcı checkpoint istedi, kod aşamasına geçilmeden
          SESSION_INDEX bu turda güncellendi.
```

Blokaj/Sıradaki için hâlâ bekleyen:
          Neon DB şifresi (`npg_8baAZqWogI1u`) süreç içinde 3 kez ekran görüntüsünde açığa
          çıktı — Reset password önerisi kullanıcıya 2 kez yapıldı, HENÜZ ONAYLANMADI.
          `app/kayit-ol/page.tsx` alt başlığı ("Bilgilerini bırak, seni arayalım.") Claude
          tarafından CONTENT_GUIDE.md görülmeden uydurulmuştu — kullanıcı karar bekliyor
          (sil / CONTENT_GUIDE.md'ye göre yeniden yaz). `INTEGRATIONS.md` §0 ve gerçek
          merkezi WhatsApp numarası (#58 için) hâlâ gelmedi. **[YENİ, Session 11]:** Gel
          Al'ın ilk-sipariş-sonrası tekrar onay gerekip gerekmediği (#64) teyit bekliyor.

Blokaj:   🟡 Twilio TR SMS kısıtı (#32) + Netgsm esnaf odası engeli (#56, 9000 TL) — İKİSİ DE
          PARKLI (silinmedi, öncelik değil).
Sıradaki: (00) [YENİ, KRİTİK, GENİŞLEDİ — Session 11] #62 — Personel Sipariş Paneli mimari
          tasarımı: personel auth yöntemi, real-time güncelleme teknolojisi (WebSocket/SSE/
          polling), Gel Al'ın manuel onay kuyruğu UI'ı, yeni DB şeması genişletmesi
          (`order_history` zaten var, Gel Al onay durumu alanı eksik olabilir — teyit gerek).
          (00b) [YENİ, Session 11] #64 — Gel Al'da onay adımının sadece ilk siparişte mi
          yoksa her seferinde mi gerektiği netleştirilmeli.
          (0) #57'yi TAM kapatmak için kalan tek açık uç:
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
          Not: [Session 11] Gel Al akışı artık sadece `wa.me` yönlendirmesi değil, İLK
          siparişte Personel Sipariş Paneli üzerinden manuel onay da içeriyor — #58 ve #62
          artık iç içe geçti, ayrı ayrı kapatılamayabilir (mimari tasarımda ele alınmalı).
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
| 🆕 | **[Session 10]** `drizzle.config.ts`'e kalıcı `dotenv` yüklemesi eklendi (`config({ path: ".env.local" })`, `defineConfig` importundan önce) — önceki migration'larda `.env.local`'in okunmaması sorununu kalıcı çözer | ✅ Canlıda doğrulandı — `order_history` migration'ı bu düzeltmeyle BAŞARILI oldu |
| 🆕 | **[Session 10, VARSAYIM — teyit bekliyor]** `order_history` tablosu (#62'nin sepetten bağımsız DB şeması ihtiyacı için) oluşturuldu: `customer_phone`, `channel`, `items`, `total_price`, `ordered_at` | 🟡 Şema Neon'a migrate edildi VE Drizzle Studio ile görsel doğrulandı. Personel auth + real-time teknoloji kararı henüz yok — #62 hâlâ açık |
| 🆕 | **[Session 11]** Genel giriş akışı: girişsiz kullanıcı menüde gezinebilir, ürün SEÇİNCE giriş sayfasına yönlendirilir; giriş sayfası her zaman giriş/kayıt seçeneği sunar | ✅ Karar netleşti, henüz KODLANMADI |
| 🆕 | **[Session 11]** Kayıt akışında bilgi+KVKK sonrası, giriş sağlanmadan ÖNCE kanal seçimi (Masaya Servis/Gel Al/Online) ZORUNLU adım olarak eklendi | ✅ Karar netleşti, henüz KODLANMADI |
| 🆕 | **[Session 11]** Masaya Sipariş kanalı: kullanıcı kişisel bilgi vermez, **"Masaya Servis"** genel etiketiyle guest girişi yapar (istisna, genel giriş/kayıt kuralını BOZMAZ) | ✅ Karar netleşti, henüz KODLANMADI |
| 🆕 | **[Session 11]** Gel Al kanalı: kullanıcı hesabıyla giriş yapıp sepeti doldurur, ama İLK siparişte Personel Sipariş Paneli'nden personel manuel telefon/WhatsApp teyidi+onayı olmadan sipariş TAMAMLANMAZ | 🟡 Karar netleşti; "sadece ilk sipariş mi" sorusu VARSAYIM (#64, teyit bekliyor), henüz KODLANMADI |
| 🆕 | **[Session 11, KRİTİK — #62 kapsam genişlemesi]** "Kasa paneli" = Personel Sipariş Paneli (#62), TEK panel — hem Masaya Sipariş'in gerçek-zamanlı akışını HEM DE Gel Al'ın ilk-sipariş manuel onay kuyruğunu yönetecek | 🔴 Kapsam netleşti, mimari tasarım (personel auth + real-time teknoloji + onay kuyruğu UI) HENÜZ YAPILMADI |
| 🆕 | **[Session 11 devamı, #64 KAPANDI]** Gel Al onay adımı SADECE ilk siparişte gerekir — ilk teyitte kullanıcı DB'ye yazılır, kullanıcı kaydında doğrulama durumu alanı (`pending`/`confirmed` benzeri) tutulur, sonraki siparişlerde panel bu alana bakıp tekrar onay istemez | ✅ Karar netleşti ve #62 mimari tasarımına eklendi, henüz KODLANMADI/ŞEMA ÜRETİLMEDİ |

*(Tam gerekçe/tarih dökümü için: `session_arşiv.md`.)*

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
| 58 | 🟡 | Gel-al WhatsApp yönlendirme (`wa.me` linki) henüz kodlanmadı — `INTEGRATIONS.md` §0 + gerçek numara bekliyor. `WhatsAppOrderButton.tsx` zaten repoda var (disabled iskelet), sıfırdan yazılmayacak. **[Session 11]:** Kapsam #62 ile iç içe geçti — Gel Al'ın İLK siparişi artık sadece `wa.me` yönlendirmesi değil, Personel Sipariş Paneli'nden manuel onay da gerektiriyor. | `lib/integrations/whatsapp.ts` (henüz yok), `components/order/WhatsAppOrderButton.tsx` |
| 59 | 🟡 | [YENİ, Session 8] Kayıt sonrası kullanıcı adı/oturum durumu hiçbir yerde görünmüyor — Header hesap ikonu giriş-yapılmamış görünümünde kalıyor. Bu akışta gerçek session/cookie var mı, kök neden araştırılmadı. | `components/layout/Header.tsx`, kayıt akışı auth mekanizması (araştırılacak) |
| 60 | 🟠 | [YENİ, Session 8] Neon DB şifresi (`npg_8baAZqWogI1u`) sorun giderme sürecinde 3 kez ekran görüntüsünde açığa çıktı — Reset password önerisi 2 kez yapıldı, HENÜZ ONAYLANMADI/YAPILMADI. | Neon console, `.env.local` |
| 61 | 🟢 | [YENİ, Session 8] `app/kayit-ol/page.tsx` alt başlığı ("Bilgilerini bırak, seni arayalım.") Claude tarafından CONTENT_GUIDE.md görülmeden uydurulmuştu — kullanıcı karar bekliyor (sil / yeniden yaz). | `app/kayit-ol/page.tsx`, `CONTENT_GUIDE.md` |
| 62 | 🔴 | Personel Sipariş Paneli — **[Session 11, KAPSAM GENİŞLEDİ]** Artık SADECE "Masaya Sipariş"in gerçek-zamanlı akışı değil, "kasa paneli" ile AYNI ŞEY olduğu teyit edildi ve Gel Al'ın İLK siparişteki manuel telefon/WhatsApp teyit+onay kuyruğunu da yönetecek. **[Session 11 devamı]:** #64 kapanışıyla mimariye yeni bir alt-karar eklendi — kullanıcı kaydında doğrulama durumu alanı (`pending`/`confirmed`), ilk onaydan sonra sonraki siparişler otomatik "aktif" sayılacak. DB şeması alt-parçası (`order_history`) canlıda var. Personel auth yöntemi, real-time güncelleme teknolojisi (WebSocket/SSE/polling) VE doğrulama durumu alanının kesin şeması HÂLÂ YAPILMADI — #62 KAPANMADI. | `order_history` (Neon, migrate edildi), personel auth sistemi (henüz yok), real-time katman (henüz yok), doğrulama durumu alanı (henüz yok) |
| 63 | 🟠 | [YENİ, Session 10] `npm install` çıktısında 12 güvenlik açığı (3 kritik) uyarısı — `npm audit fix --force` bilinçli olarak KOŞULMADI (kırıcı değişiklik riski, migration'ın ortasındaydı). Ayrı, sakin bir zamanda ele alınmalı. | `package.json`, `npm audit` çıktısı |
| 65 | 🟡 | [YENİ, Session 11/12] Guest gate middleware'i (`resolveGuestGateRedirect`) Masaya Sipariş kanalının guest-girişi istisnasını KAPSAMIYOR — Session 11'de kararlaştırılan "Masaya Sipariş = 'Masaya Servis' etiketiyle bilgi vermeden guest girişi" kuralı, şu an `/menu/customize/*` altındaki HERKESİ (kanal ayrımı yapmadan) girişe yönlendiriyor. Kod yorumunda "kullanıcı onayı: B olmalı" notu var — bu seçimin tam gerekçesi/alternatifleri (A neydi?) bu turda görülmeyen bir alt-turda konuşulmuş, netleştirilmesi istenirse kullanıcıdan teyit alınmalı. Bilinçli borç olarak kodda işaretli. | `lib/auth/guest-gate.ts`, `middleware.ts` |
| 66 | 🟢 | [YENİ, Session 11/12] İmza kase "Sepete Ekle" butonu (customize'a hiç girmeden direkt ekleme) client-side action olduğu için guest gate middleware'i tarafından YAKALANMIYOR — component-seviyesi ayrı bir guard gerekiyor. **AÇIK KARAR (kullanıcıdan teyit bekliyor):** bu, 1b'nin ayrı bir alt-görevi olarak SIRADAKİ GÖREVLER'e eklensin mi, yoksa bilinçli açık mı bırakılsın? | `components/customizer/AddToCartButton.tsx` (muhtemelen, #50 ile kesişiyor) |

> **KAPANDI (bu turda):** #64 — Gel Al onay adımının sadece ilk siparişte gerektiği kullanıcı
> tarafından netleştirildi (ilk teyitte kullanıcı DB'ye yazılır, doğrulama durumu alanı
> tutulur). Karar #62'nin mimari tasarım kapsamına taşındı, ayrı açık sorun olarak kapandı.
>
> **KAPANDI (önceki turlar):** #4, #7, #15, #16, #20, #22/Karar #11, #35, #43, #44, #49 —
> detaylar önceki SESSION_INDEX sürümlerinde ve `session_arşiv.md`'de.
>
> Detaylı gerekçe/dosya alıntıları `session_arşiv.md`'de (Session 0'dan Session 8'e tam).

---

## SESSION ÖZET (tümü — 0'dan 11'e)

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
| 9 | 2026-08-07 | Kullanıcı canlı kayıt akışını "Masaya Sipariş" kanalıyla test etti — çalışıyor doğrulandı. Fiziksel akış netleşti: tek genel QR → `/kayit-ol` → `/menu` (masa-bazlı QR YOK, önceki turdaki "masa no eksik" endişesi geri çekildi). **Büyük keşif:** "Masaya Sipariş" tamamlanınca #58 (WhatsApp) değil, ayrı bir personel Sipariş Paneli (parola korumalı, gerçek-zamanlı, sepetten bağımsız) gerektiği netleşti — #62 olarak açıldı, mimari tasarımı henüz yapılmadı. Ayrıca bu session'da kullanıcı `session_log.md` (eski isim) mekanizmasını sorguladı; CORE.md/AGENT.md'nin gerçek yazılı kuralı (400 satır eşiği, ayrı anlatı bloğu YOK) doğru şekilde bulunup uygulandı, isim/mekanizma karışıklığı giderildi — CORE.md v1.3, AGENT.md v1.4'e güncellendi. Kullanıcının tek seferlik istisna (tam dosya birleştirmesini Claude'un üretmesi) talebi, aynı sohbette onaylanan kurala dayanarak reddedildi; bunun yerine ayrı bloklar (Session 7 + Session 8) verildi, birleştirme kullanıcıya bırakıldı. | 🟡 Devam ediyor — #62 yeni sohbette |
| 10 | 2026-08-07 | ⚠️ Session_INDEX bu session'ın sonunda güncellenmemişti, sonraki sohbette geriye dönük tamamlandı — sadece sohbetin sağlanan (son) kısmı işlendi, başlangıcı görülmedi. Görülen kısım #62'nin DB şeması alt-parçası: `dotenv` kuruldu (npm audit 12/3-kritik uyarısı görüldü ama ele alınmadı → #63 yeni), `drizzle.config.ts`'e kalıcı `.env.local` yüklemesi eklendi, yeni `order_history` tablosu (`customer_phone`,`channel`,`items`,`total_price`,`ordered_at`) canlı Neon'a migrate edildi ve Drizzle Studio ile doğrulandı. #62 hâlâ KAPANMADI — personel auth + real-time teknoloji kararı yok. Konuşma sonra giriş/kayıt akışları konusuna geçti (içeriği bu turda sağlanmadı). | 🟡 Devam ediyor — #62 kısmi ilerleme, #63 yeni |
| 11 | 2026-08-07 | ⚠️ Bu güncelleme de GERİYE DÖNÜK yapıldı — Session 10'un devamı olan sohbet kapanmış ama SESSION_INDEX güncellenmemişti; kullanıcı kapanan sohbetin TAM METNİNİ bu sohbete taşıdı. İşlenen içerik: Session 10'da ertelenen giriş/kayıt/sipariş kanalı akışı netleşti. Genel kural: girişsiz kullanıcı menüde gezinebilir, ürün seçince giriş sayfasına yönlenir, giriş sayfası giriş/kayıt sunar, kayıtta bilgi+KVKK sonrası kanal seçimi (Masaya Servis/Gel Al/Online) giriş sağlanmadan ÖNCE zorunlu. Kanal bazlı netleşme: Masaya Sipariş = guest ("Masaya Servis" etiketiyle, bilgi vermeden); Gel Al = hesapla giriş + İLK siparişte personel manuel telefon/WhatsApp onayı zorunlu; Online = `/online-siparis`'e yönlendirme (değişmedi). **Kritik kapsam kararı:** "kasa paneli" ile #62 Personel Sipariş Paneli AYNI ŞEY olduğu teyit edildi — panel artık hem Masaya Sipariş gerçek-zamanlı akışını hem Gel Al'ın manuel onay kuyruğunu yönetecek; bu #58 (WhatsApp yönlendirme) ile #62'yi de iç içe geçirdi. **Aynı session'ın devamında:** #64 kapandı — Gel Al onayının sadece ilk siparişte gerektiği, ilk teyitte kullanıcının DB'ye yazılıp bir doğrulama durumu alanıyla (`pending`/`confirmed`) takip edileceği kullanıcı tarafından onaylandı; bu karar #62'nin mimari kapsamına eklendi. Bu turda kod/şema ÜRETİLMEDİ, kullanıcı checkpoint istedi ve SESSION_INDEX bu noktada güncellendi. | 🔴 Devam ediyor — #62 mimari tasarımı (auth+real-time+doğrulama alanı) hâlâ bekliyor; #64 KAPANDI |
| 12 | 2026-08-08 | ⚠️ Yine RETROAKTİF: Session 11'in devamı olan sohbet, 1b'nin guest-gate middleware'i kodlanıp checkpoint onayı BEKLENİRKEN kapandı. Kullanıcı önce kapanan sohbetin son mesajını yapıştırdı; eksik veri (kod görülmedi, "#65" belirsiz, "Sepete Ekle" kararı cevapsız) nedeniyle üretim reddedildi, netleştirme istendi. Kullanıcı ardından gerçek repo zip'ini yükledi — kod doğrudan repodan doğrulandı (tahmin edilmedi): `middleware.ts`+`guest-gate.ts`+`guest-gate.test.ts` repoda mevcut ve push edilmiş; `auth.ts` export şekli middleware ile tam uyumlu bulundu (confidence MEDIUM→HIGH). "#65" kod yorumunda zaten belgeliymiş: Masaya Sipariş'in guest istisnası middleware'e bilinçli olarak eklenmemiş. "Sepete Ekle" bypass gap'i #66 olarak açık karara bağlandı (kullanıcı teyidi bekliyor). Ağ erişimi olmadığından testler ÇALIŞTIRILAMADI, sadece kod incelemesiyle doğrulandı — bu ayrım açıkça belirtildi. | 🟡 1b kısmen tamamlandı — #65/#66 açık, kanal seçimi adımı hâlâ kodlanmadı |

*(Tam turn-by-turn detay: `session_arşiv.md`.)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel, Vercel Production'da deploy'lar Ready. Kullanıcı GitHub Codespaces (`3rw9.github.dev`) üzerinden de çalışıyor. |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 kod ile hizalı |
| Test Suite | 🟢 Header.test.tsx, customizer-summary-format.test.ts, menu-filters.test.ts, hakkimizda/page.test.tsx (2/2), send-otp.test.ts (3/3), `lib/registration/validation.test.ts` (9), `lib/auth/rate-limit.test.ts` (5), `lib/auth/rate-limit.registration.test.ts` (3), `lib/auth/guest-gate.test.ts` (8 — kod incelemesiyle doğrulandı, bu ortamda ağ yok, ÇALIŞTIRILAMADI). Genel `npm test` (tüm proje) hâlâ tekrar çalıştırılmadı. |
| Auth | 🟡 Twilio/Netgsm PARKLI (#32/#56). **[Session 8]:** Eski `/giris` (Twilio OTP) UI'ı kaldırıldı, rıza esaslı kayıt (`/kayit-ol`) birincil akış oldu. Oturum/kullanıcı adı gösterimi hâlâ netleşmedi (#59). **[Session 11]:** Genel giriş/kayıt akışı karar olarak netleşti. **[Session 11/12]:** Guest gate middleware'i (`/menu/customize/*` → `/kayit-ol` callbackUrl ile) KODLANDI, repoda push edilmiş halde doğrulandı (zip incelemesi). Kanal ayrımı (Masaya Sipariş guest istisnası, #65) ve "Sepete Ekle" bypass guard'ı (#66) hâlâ eksik — 1b TAM kapanmadı. |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Kullanıcı Kaydı (rıza esaslı) | 🟡 **[Session 8]** Backend + Frontend TAMAM, `/kayit-ol`'a BAĞLANDI, DB migration KOŞULDU, canlı uçtan uca test BAŞARILI. Kayıt sonrası oturum göstergesi eksik (#59). **[Session 11]:** Kayıt akışına "kanal seçimi zorunlu" adımı eklenmesi kararlaştırıldı, henüz KODLANMADI. |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı — kanal seçimi zorunlu, `FulfillmentGate` dokunulmadan doğrulandı |
| Veritabanı | 🟢 Neon Postgres çalışıyor. **[Session 8]:** `consentRegistrations` tablosu migration'ı BAŞARIYLA koşuldu, tablo canlıda var. **[Session 10]:** `order_history` tablosu (#62 için) migrate edildi ve doğrulandı; `drizzle.config.ts` artık `.env.local`'i kalıcı olarak doğru okuyor. ⚠️ DB şifresi 3 kez açığa çıktı, reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik, ele alınmadı (#63). |
| Personel Sipariş Paneli (#62) | 🔴 **[Session 11, KAPSAM GENİŞLEDİ]** "Kasa paneli" ile aynı panel olduğu teyit edildi — Masaya Sipariş gerçek-zamanlı akışı + Gel Al ilk-sipariş manuel onay kuyruğu, İKİSİNİ BİRDEN yönetecek. DB şeması alt-parçası (`order_history`) canlıda var. Personel auth yöntemi, real-time teknoloji (WebSocket/SSE/polling) VE onay kuyruğu tasarımı HÂLÂ YAPILMADI. |
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
| 1 | [GENİŞLEDİ, Session 11] #62 Personel Sipariş Paneli mimari tasarımı — Masaya Sipariş gerçek-zamanlı akışı + Gel Al ilk-sipariş manuel onay kuyruğu + kullanıcı doğrulama durumu alanı (#64 kararı dahil): personel auth yöntemi, real-time teknoloji, onay kuyruğu UI/veri modeli, `pending`/`confirmed` şeması | 🔴 |
| 1b | [KISMİ İLERLEME, Session 12] Genel giriş/kayıt akış kararlarını koda dök — `/menu/customize/*` guest gate middleware'i TAMAMLANDI (repoda doğrulandı). Kalan: (i) Masaya Sipariş guest istisnası middleware'e eklenmeli (#65), (ii) "Sepete Ekle" bypass için component-seviyesi guard (#66 — eklensin mi kararı bekliyor), (iii) kayıt sayfasında zorunlu kanal seçimi adımı hâlâ kodlanmadı | 🔴 |
| 2 | #57'yi TAM kapat — `/online-siparis` sayfası (marketplace linkleri: Yemeksepeti/Getir/Trendyol) | 🔴 |
| 3 | [YENİ] Kayıt sonrası oturum/kullanıcı adı gösterimini araştır ve çöz (#59) | 🟡 |
| 4 | [YENİ] Neon DB şifresini resetle, `.env.local`'i güncelle (#60, güvenlik) | 🟠 |
| 4b | [YENİ, Session 10] `npm audit fix` — 12 açık/3 kritik güvenlik açığını ayrı, sakin bir oturumda ele al (#63) | 🟠 |
| 5 | [YENİ] `app/kayit-ol/page.tsx` alt başlığı kararı — sil ya da CONTENT_GUIDE.md ile yeniden yaz (#61) | 🟢 |
| 6 | `/kvkk` sayfasını hukuk danışmanına incelettir (kullanıcı eylemi, Claude'un kapsamı dışı) | 🟡 |
| 7 | #58 Gel-al WhatsApp yönlendirme (`wa.me` linki, `WhatsAppOrderButton.tsx` iskeletini tamamla) — `INTEGRATIONS.md` §0 + gerçek numara bekliyor, artık #62 mimarisiyle birlikte tasarlanmalı | 🟡 |
| 8 | Twilio/Netgsm kararı — PARKLI, acil değil (#32/#56) | ⚪ |
| 9 | Gerçek şube adresini Şubeler sayfası/Footer.tsx/JSON-LD şemasına işle (#54 — kullanıcı aciliyet belirtti) | 🟡 |
| 10 | DESIGN_SYSTEM.md paylaşılırsa `ProfileForm.tsx` + `RegistrationForm.tsx` Tailwind sınıflarını TAM kapsamlı teyit et (#38) | 🟢 |
| 11 | CONTENT_GUIDE.md §1/§2'deki â örneklerini ve StepBase.tsx'i güncelle (#53) | 🟢 |
| 12 | AboutValues.tsx ile ValueProps.tsx senkronunu teyit et (#55) | 🟢 |
| 13 | Vektörel ikon seti üretimi (25-30 malzeme) (#52) | 🟡 |
| 14 | PHOTOGRAPHY_GUIDE.md §8 notu düzeltilmeli (#52 ile bağlantılı) | 🟢 |
| 15 | Boostfeel/QR tabanlı sadakat çözümü değerlendirilmeli (Karar #12) | 🟡 |
| 16 | `AddToCartButton.tsx` + `useCartStore.ts` tam dosya teyidi (#50/#51) | 🟢 |
| 17 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a güncelle (#10) | 🟡 |
| 18 | Alerjen gösterimini MenuCard/Customizer/SummaryPanel'de fiilen uygula | 🟡 |
| 19 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 20 | VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat | 🟢 |
| 21 | Customizer adım başlıklarını Türkçeleştir / spec ile senkronla (#28/29) | 🟢 |
| 22 | Genel `npm test` (tüm proje) çalıştırıp güncel geçen/kalan sayıyı teyit et | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v25 (v24'ten: #65/#66 eklendi, 1b kısmi tamamlandı, guest gate
middleware zip üzerinden doğrulandı, confidence HIGH'a yükseltildi). ⚠️ **400 satır eşiği
Session 11 checkpoint'inde tetiklenmişti** (bu Session 12 turunda YENİDEN tetiklenmedi):
CURRENT FOCUS'taki Session 8/9/10 anlatı blokları (3 madde, ~59 satır) `session_arşiv.md`'ye
TAŞINDI (gerekçe: hepsi kapanmış/geçmiş anlatıydı, SESSION ÖZET + KRİTİK KARARLAR/AÇIK
SORUNLAR tablolarında özleri zaten korunuyordu — bkz. dosya başındaki 400 SATIR EŞİĞİ
TAŞIMASI notu). Taşınan tam metin, bu turla BİRLİKTE ayrıca `session_arşiv.md` taşıma bloğu
olarak sunuldu; kullanıcı kendi `session_arşiv.md` dosyasının sonuna ekleyecek.
Session 11 (2026-08-07) iki turda işlendi. İlk tur GERİYE
DÖNÜK yapıldı: Session 10'un devamı olan sohbet, "giriş/kayıt akışları konusuna geçildi,
içeriği sağlanmadı" notuyla kapanmış ve SESSION_INDEX GÜNCELLENMEDEN kalmıştı. Kullanıcı o
kapanan sohbetin TAM METNİNİ bu sohbete taşıyarak güncellemeyi yaptırdı — bu nedenle DÖRDÜNCÜ
DERS olarak dosyanın başına eklendi. İşlenen içerik: genel giriş/kayıt akışı (guest gezinme →
ürün seçince giriş sayfası, giriş sayfasında her zaman giriş/kayıt seçimi, kayıtta bilgi+KVKK
sonrası kanal seçimi ZORUNLU), kanal bazlı netleşme tablosu (Masaya Sipariş=guest/"Masaya
Servis", Gel Al=hesap girişi+ilk siparişte manuel onay, Online=`/online-siparis` — değişmedi),
ve KRİTİK kapsam kararı: "kasa paneli" = Personel Sipariş Paneli (#62), TEK panel, artık hem
Masaya Sipariş gerçek-zamanlı akışını hem Gel Al'ın ilk-sipariş manuel onay kuyruğunu
yönetecek. Bu, #58 (WhatsApp yönlendirme) ile #62'yi iç içe geçirdi. Açık sorun #64 (Gel Al
onayı sadece ilk sipariş mi) bu turda AÇILDI.

**İkinci tur (aynı sohbetin devamı):** Kullanıcı #64'ü netleştirdi — ilk siparişteki manuel
teyitte kullanıcı zaten DB'ye yazıldığı için onay adımı sadece ilk siparişte gerekiyor;
Claude'un önerdiği somut mimari yansıma (kullanıcı kaydında `pending`/`confirmed` benzeri bir
doğrulama durumu alanı, ilk onaydan sonra sonraki siparişlerin otomatik "aktif" sayılması)
kullanıcı tarafından AYNEN onaylandı. #64 KAPANDI, karar #62'nin mimari tasarım kapsamına
taşındı (henüz kod/şema üretilmedi). Kullanıcı checkpoint istedi, kod aşamasına geçilmeden bu
noktada SESSION_INDEX güncellendi (AGENT.md Checkpoint protokolüne uyuldu). Diğer tüm içerik
v23'ten korundu, hiçbir madde gerekçesiz silinmedi.
Dosya artık ~380 satır — 400 eşiğinin altında, arşivleme gerekmedi.
Tam turn-by-turn gerekçe/karar dökümü için: `session_arşiv.md` (Session 11 için henüz
ayrı blok üretilmedi — 400 satır eşiği o turda tetiklenmedi).

**Session 12 (2026-08-08, RETROAKTİF):** Session 11'in devamı olan sohbet, guest-gate
middleware'i (1b) kodlanıp checkpoint onayı BEKLENİRKEN kapandı. Kullanıcı önce sadece
kapanan sohbetin son mesajını (KARAR BİLDİRİMİ) yapıştırdı; Claude bu turda "Tahmin etme"
kuralına (AGENT.md Kural #1/#2) uyarak — kod dosyaları görülmediği, "#65" referansının
kaynağı belirsiz olduğu ve "Sepete Ekle" kapsam sorusu cevapsız kaldığı için — TAM DOSYA
üretmeyi reddetti, 3 netleştirme istedi. Kullanıcı ardından GERÇEK REPO ZIP'İNİ yükledi;
bu turda hiçbir şey tahmin edilmedi, doğrudan repodan doğrulandı: `middleware.ts` +
`lib/auth/guest-gate.ts` + `lib/auth/guest-gate.test.ts` repoda MEVCUT ve push edilmiş
bulundu; `auth.ts`'in gerçek export şekli middleware'in import'uyla TAM uyumlu doğrulandı
(önceki MEDIUM confidence gerekçesi ortadan kalktı → **HIGH'a yükseltildi**). "#65" meğer
kod yorumunda zaten belgeliymiş: Masaya Sipariş kanalının guest-girişi istisnası middleware'e
BİLİNÇLİ OLARAK eklenmemiş (açık sorun olarak bu turda tabloya işlendi). "Sepete Ekle" bypass
gap'i #66 olarak yeni açık sorun/karar bekleyen madde şeklinde eklendi (backlog'a girsin mi
kullanıcı teyidi bekliyor). ⚠️ Bu ortamda ağ erişimi yoktu, `npm test` ÇALIŞTIRILAMADI —
test dosyası (8 test) SADECE kod incelemesiyle doğrulandı, bu ayrım kullanıcıya açıkça
belirtildi; "testler geçti" gibi doğrulanmamış bir iddia YAPILMADI. 1b görevi KISMEN
tamamlandı (route-seviyesi guest gate TAMAM; kanal istisnası #65 ve component-seviyesi
guard #66 hâlâ açık; kayıt akışına zorunlu kanal seçimi adımı hâlâ kodlanmadı).
Dosya artık ~380 satır — 400 eşiğinin altında, arşivleme gerekmedi.
Güncellenme: 2026-08-08.*
