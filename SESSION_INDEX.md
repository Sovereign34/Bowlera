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

---

## 🎯 CURRENT FOCUS

```
Görev (2026-08-05, Session 6):    Netgsm SMS başlık başvurusu esnaf odası (9000 TL)/marka tescili
          istediği için bloke oldu. Araştırma: SMS başlık onayı hiyerarşisi netleştirildi — vergi
          levhasında ticari ünvan varsa veya işyeri açma ruhsatında ticari ünvan yazıyorsa esnaf
          odası/marka tescili GEREKMİYOR. Kullanıcı, ruhsat aşamasında Bowlera adını kullanabileceğini
          teyit etti (Netgsm konusu bu turda kesin KAPANMADI, paralel yol açıldı).
          **Karar (kullanıcı onayı ile):** WhatsApp OTP birincil, SMS fallback ikincil kanal. Kritik
          bulgu: Twilio Verify zaten `channel: "whatsapp"` destekliyor — ayrı Meta entegrasyonu
          gerekmiyor. `verify/route.ts` DEĞİŞMEDİ (kanaldan bağımsız doğrulama).
          **Kod üretildi:** `lib/auth/send-otp.ts` (yeni, fallback zinciri), `app/api/auth/otp/send/route.ts`
          (güncellendi), `lib/auth/send-otp.test.ts` (yeni, 3 test — happy/edge/failure).
          Kalite 5/5, Güvenlik 8/8. **Test koşuldu ve ekran görüntüsüyle doğrulandı: 3/3 PASS**
          (`npx vitest run lib/auth/send-otp.test.ts` — happy path, edge case, failure path).
          Loglardaki `OTP_CHANNEL_FAILED` satırları failure-path testinin kasıtlı çift-kanal
          hatası senaryosuna ait, BSC-4 loglamasının çalıştığının kanıtı — hata değil. **Kod
          HENÜZ push edilmedi.**
          Yeni Açık Sorun #56: Twilio WhatsApp Business Sender onay durumu bilinmiyor.

Görev (2026-08-05, Session 6, devam — bu tur):    Twilio Upgrade denendi, hesap Trial modunda
          ($15.50 kredi) — WhatsApp Sender kurulumu için min. $20 gerekiyor, kullanıcı şu an
          bu tutarı ödemek istemiyor. Alternatif olarak Netgsm SMS başlığı için "vergi levhasına
          ticari ünvan işletme" yolu araştırıldı — bunun da Ticaret Sicili ilanı gerektirdiği
          (yani gerçekte ~9000 TL'ye eşdeğer olduğu) kullanıcı tarafından netleştirildi; "ücretsiz
          alternatif" iddiası bu turda GERİ ÇEKİLDİ. Google/sosyal giriş araştırıldı — Google OAuth
          kullanıcının telefon numarasını PAYLAŞMIYOR (API'de bu scope yok, doğrulanmış üçüncü
          parti kaynaklarla teyit edildi) — bu yüzden Google girişi telefon toplama ihtiyacını
          çözmüyor, elendi. Online yemek platformları (Yemeksepeti vb.) üzerinden "sosyal giriş"
          benzeri bir kimlik doğrulama da araştırıldı — BU PLATFORMLAR KİMLİK SAĞLAYICI DEĞİL,
          resmi/genel bir "___ ile giriş yap" API'leri yok, bu yol da tamamen elendi.

          **🔧 YENİ MİMARİ KARAR (kullanıcı onayı ile, bu tur):** Twilio ($20 Upgrade) ve Netgsm
          (9000 TL, Ticaret Sicili ilanı) yolları PARKLANDI — ikisi de şu an maliyetli, acil
          değil. Yerine GEÇİCİ/deneme aşamasında yeni bir mimari benimsendi:

          1. **Sipariş kanalına göre ayrım:** Online yemek platformlarından (Yemeksepeti/Trendyol/
             Getir) gelen siparişlerde kimlik doğrulama sorunu yok — platform kendi kullanıcısını
             yönetiyor. Gel-al (pickup, doğrudan site) siparişlerinde müşteri SİTEDE customizer'la
             bowl'unu oluşturur (mevcut sistem DEĞİŞMİYOR), checkout'ta kendi WhatsApp'ından
             işletme numarasına yönlendirilir (`wa.me` linki, sipariş özeti önceden dolu) —
             kullanıcı KENDİ hesabından mesaj attığı için numara doğal yoldan teyit edilmiş olur,
             ayrıca kod göndermeye gerek kalmaz.
          2. **Merkezi kullanıcı kaydı (kanal-bağımsız):** Kanal fark etmeksizin (site formu /
             WhatsApp / platform siparişi), ilk temasta telefon + adres + AÇIK RIZA (KVKK) ile
             toplanır — SMS/WhatsApp doğrulama KODU gönderilmez, rıza checkbox'ı (önceden
             işaretli DEĞİL, aktif onay) yeterli görülüyor. Opsiyonel: yaş, cinsiyet (pazarlama
             segmentasyonu). Aynı telefon numarasıyla her yeni siparişte mevcut kayıt güncellenir,
             yoksa yeni kayıt açılır (`upsertUserFromOrder()` benzeri tek fonksiyon, kanal
             bağımsız). `verifiedAt` alanı "rıza onay zamanı" olarak yeniden yorumlanacak.
          3. **Twilio Verify/OTP akışı DEVRE DIŞI bırakılacak, kod SİLİNMEYECEK** — Netgsm onayı
             ileride gelirse (ya da Twilio Upgrade'e karar verilirse) `send-otp.ts` mimarisi
             hazır katman olarak geri eklenebilir.

          ⚠️ **Not (dürüstlük kaydı):** Bu, kullanıcının "zaman geçtikçe karara varırız" dediği
          bir DENEME aşaması — kesin/nihai mimari kararı değil, ama şu an aktif geliştirme yönü
          budur. Hukuki taraf (KVKK aydınlatma metni, rıza checkbox metni) ayrı ve dikkatli
          ele alınması gereken bir iş olarak işaretlendi, bu turda hazırlanmadı.

          Yeni Açık Sorun #57: Rıza esaslı telefon+adres toplama formu (KVKK aydınlatma metni +
          checkbox + backend format doğrulama) henüz KODLANMADI. Yeni Açık Sorun #58: Gel-al
          WhatsApp yönlendirme akışı (`wa.me` linki + sipariş özeti ön-doldurma) henüz KODLANMADI —
          `lib/integrations/whatsapp.ts` (CORE.md dosya haritasında zaten planlıydı) bu iş için
          kullanılacak.

Görev (2026-08-05, Session 6, KAPANIŞ turu — MİMARİ NİHAİLEŞTİ):    #57/#58'in tam kapsamı
          netleşti, kullanıcı onayı alındı. **Kritik keşif:** `WhatsAppOrderButton.tsx` zaten
          repoda var (Session 4, Bölüm 5'te üretilip doğrulanmış) — bilinçli olarak kalıcı
          disabled bırakılmış, sebep: şube telefon numarası tanımlanmamış + `lib/integrations/
          whatsapp.ts`/`buildWhatsAppOrderLink()` henüz yazılmamış. Yani #58 sıfırdan UI değil,
          var olan iskeleti tamamlama işi.

          **NİHAİ AKIŞ (onaylandı):**
          1. Kayıt İKİ tetikleyiciden biriyle başlar: (a) kullanıcı kendi isteğiyle "Kayıt Ol",
             (b) customizer'da ürün seçimine başlarken henüz kayıtlı değilse otomatik yönlendirme.
          2. Kayıt formu ZORUNLU alanlar: ad-soyad, telefon, rıza (KVKK) checkbox. Adres
             OPSİYONEL kalır (Karar #23 ile ÇAKIŞMIYOR — kayıt zorunlu ile adres opsiyonel
             farklı şeyler; adresin amacı zamanla çoklu-şube güçlü veri tabanı oluşturmak).
             Opsiyonel: yaş, cinsiyet.
          3. Kayıt adı sitede "Merhaba, [isim]" olarak header'da gösterilir.
          4. Kayıt tamamlanınca 3 kanal seçimi sunulur: Masaya Servis / Gel-Al / Online Sipariş.
          5. Masaya Servis + Gel-Al: kullanıcı isim-gösterir halde sitede gezinir, customizer'la
             ürün seçer, sepete ekler. Sepet tamamlanınca `WhatsAppOrderButton.tsx` üzerinden
             TEK, merkezi işletme WhatsApp numarasına (normal/kişisel WhatsApp, Business API
             DEĞİL — düşük hacim, fiziksel gelen müşteri profiliyle sınırlı, risk düşük
             değerlendirildi) yönlendirilir. Bu tamamlanma anı = DB yazma tetikleyicisi.
          6. Online Sipariş: kullanıcı Yemeksepeti/Getir/Trendyol'a yönlendirilir. Platform API'leri
             (Session 5'te doğrulandı, Yemeksepeti openapi.json) müşteri verisini maskeliyor —
             OTOMATİK doğrulama teknik olarak KAPALI. Bunun yerine: kayıt sonrası aynı merkezi
             numaradan MANUEL teyit — önce WhatsApp denenir, kanal çalışmazsa SMS'e düşülür (aynı
             fallback deseni #56/send-otp.ts'teki gibi, ama OTP kodu değil, teyit mesajı).
          7. Rıza metnine eklenecek zorunlu not: "Online platform siparişleriniz otomatik
             doğrulanamadığından, kaydınızı teyit etmek için önce WhatsApp, olmazsa SMS yoluyla
             tarafınızla iletişime geçilecektir."
          8. Şube numarası: şu an TEK aktif şube (Kağıthane) olduğu için TEK merkezi numara
             yeterli — hem sipariş tamamlama hem manuel teyit aynı numaradan. Çoklu şube
             senaryosu (merkezi mi, şube-bazlı mı) İLERİYE ERTELENDİ, ayrı karar gerektirecek.

          **Marka/UX değerlendirmesi (kullanıcı istedi, yapıldı):** İlk değerlendirmede "sepet
          terki" ve "WhatsApp hacim/spam" riskleri öne sürüldü; kullanıcı haklı olarak düzeltti —
          gel-al/masaya servis müşterisi zaten FİZİKSEL olarak gelecek (online-platform anonim
          kullanıcı davranışıyla kıyaslamak yanlıştı), ve normal/kişisel WhatsApp + düşük/fiziksel-
          sınırlı hacim = Business API'nin çözmeye çalıştığı ölçek sorunu burada geçerli değil.
          Onaylanan risk: ileride hacim büyürse (başarı senaryosu) resmi WhatsApp Business API'ye
          geçiş "ne zaman" sorusu olacak, ayrı bir gelecekteki karar.

          Kod aşamasına GEÇİLİYOR — bir sonraki adım.

Önceki tur (2026-08-02, üçüncü tur):    Hakkımızda sayfası (/hakkimizda) sıfırdan
          oluşturuldu — MASTER_PLAN.md §3 sitemap girdisi karşılandı, önceki site
          denetiminde tespit edilen 404 kapandı. 6 dosya üretildi: page.tsx,
          AboutHero.tsx, AboutStory.tsx, AboutValues.tsx, AboutImagePlaceholder.tsx,
          page.test.tsx. Test sonucu kullanıcı tarafından koşuldu ve doğrulandı:
          Vitest, 2/2 test geçti (happy path + edge case).
          **Gerçek veri işlendi:** Kullanıcı gerçek şube adresini paylaştı — Çağlayan
          Park Sokak No:30, Kağıthane, İstanbul. AboutStory.tsx'e kuruluş anlatısı
          olarak işlendi (global marka VİZYONU olarak çerçevelendi, mevcut durummuş
          gibi sunulmadı). ⚠️ Bu adres HENÜZ Şubeler sayfası/Footer.tsx/JSON-LD
          şemasına işlenmedi — CONTENT_GUIDE.md §4 NAP tutarlılık kuralı gereği bu
          senkron zorunlu, yeni açık iş olarak eklendi (#54).
          **Site-geneli yazım kararı:** Kullanıcı onayıyla "kâse"→"kase" (â kaldırma)
          kararı alındı. Hero.tsx'te uygulandı (CTA: "Kaseni Oluştur", alt paragraf
          sağlıklı beslenme odaklı yeniden yazıldı — tedarikçi vurgusu kaldırıldı).
          CONTENT_GUIDE.md'deki "Kâseni Yarat" örnekleri ve StepBase.tsx HENÜZ
          güncellenmedi — karar kısmen uygulandı (#27 kısmen kapandı, #53 yeni açıldı).
          **Governance düzeltmesi:** AGENT.md/CORE.md'deki "400 satır eşiği" kuralı
          bir yanlış anlaşılma sonucu kısa süreliğine kaldırılıp aynı gün içinde
          AYNEN geri getirildi (bkz. dosya üstü not). Net kural değişikliği yok,
          sadece versiyon numaraları arttı (AGENT.md v1.5, CORE.md v1.4).

Önceki tur (2026-08-01, ikinci tur):    Pazaryeri müşteri verisi erişimi araştırıldı.
          Yemeksepeti'nin resmi openapi.json şeması incelendi — `order.Customer`
          şemasındaki TÜM kişisel alanlar (isim, telefon, ulusal kimlik, teslimat
          adresi) açıkça "Masked for identity protection" olarak işaretli, sadece
          platformun ürettiği anonim müşteri ID'si veriliyor. Bu, bilinçli bir
          platform politikası — teknik eksiklik değil. Trendyol Go/Migros Yemek
          için de aynı mantığın geçerli olduğu varsayılıyor (ayrı ayrı teyit
          edilmedi).
          **Bulunan gerçek yol:** Adisyo'nun "BOOSTFEEL Müşteri Sadakat
          Entegrasyonu" pazaryeri API'sinden veri ÇEKMİYOR — QR kod tabanlı,
          müşterinin FİZİKSEL ziyarette (gel-al) kendi isteğiyle dijital sadakat
          kartına kaydolmasına dayanıyor (Apple/Google Wallet, Adisyo/Simpra POS
          entegrasyonu üzerinden). Önerilen pratik yöntem: pazaryeri paket
          siparişlerine "QR ile üye ol, indirim kazan" kartı eklemek — platform
          ToS'unu ihlal etmeyen, müşteriyi kendi isteğiyle veri paylaşmaya davet
          eden meşru yol.
          Bu bulgu, Karar #12'deki (loyaltyPoints mekaniği henüz netleşmedi) açık
          soruyla doğrudan bağlantılı — sadakat mekaniği tasarlanırken Boostfeel
          benzeri bir QR-kayıt akışı ile `users.loyaltyPoints` alanının nasıl
          besleneceği birlikte düşünülmeli.

Önceki tur (2026-08-01, ilk tur):    VisualPreview.tsx mimarisi denetlendi — kritik bir
          mimari çelişki bulundu (#52, yeni). Kod, `/public/images/layers/` altında
          her malzeme için gerçek görsel dosyası (`base-jasmine-rice.webp` gibi)
          bekliyor, ama bu klasör TAMAMEN BOŞ — hiçbir katman görseli yok. Bu,
          PHOTOGRAPHY_GUIDE.md §8'deki "VisualPreview CSS/SVG katman mantığıyla
          çalışıyor, gerçek fotoğraf gerekmez" notuyla doğrudan çelişiyor. Şu an
          müşteri customizer'da herhangi bir malzeme seçse bile önizleme boş krem
          renkli daire olarak kalıyor.
          **Karar (kullanıcı onayı ile):** Fotoğraf katmanlama yerine markaya uygun
          (Warm Cream/Espresso Brown/Primary Olive) vektörel ikon seti kullanılacak —
          global rakip modeli: Chipotle (metin-only, görsel yok) / Cava-Sweetgreen
          (düz ikon seti). Kod tarafında DEĞİŞİKLİK GEREKMİYOR — VisualPreview.tsx
          zaten dosya yolunu id'den esnek türetiyor, sadece ikon dosyaları
          `/public/images/layers/` altına eklenecek (üretici: kullanıcı bir
          tasarımcı bulacak ya da Claude AI ile taslak üretecek — netleşmedi).
          Ayrıca: dosyanın en üstündeki "GEÇMİŞ İHLAL KAYDI" notu (v2 sıkıştırma
          olayı) bu turda tekrar teyit edildi — kullanıcıya SESSION_INDEX.md'nin
          (bu dosya) doğru/güncel kaynak olduğu, SESSION_INDEX_v2.md'nin ise
          kayıttaki ihlalin ta kendisi olduğu için kullanılmaması gerektiği
          açıkça bildirildi.

Blokaj:   🟡 Twilio TR SMS kısıtı (#32) + Netgsm esnaf odası engeli (#56, 9000 TL) — İKİSİ DE
          PARKLANDI bu tur, hemen çözülmeyecek. Yerine #57/#58 (rıza esaslı toplama + WhatsApp
          yönlendirme) aktif geliştirme öncelikleri oldu.
Sıradaki: (0) YENİ, en öncelikli — #57 rıza esaslı telefon+adres formu:
          (0a) KVKK aydınlatma metni + rıza checkbox metni yaz (hukuki dikkat gerektirir),
          (0b) telefon+adres birleşik form (mevcut ProfileForm/checkout akışına entegre),
          (0c) backend'de format doğrulama (05XX XXX XX XX) — SMS/WhatsApp kod YOK,
          (0d) `users` tablosuna opsiyonel `age`/`gender` alanları ekle (şema değişikliği,
          CORE.md §7.4 protokolü zorunlu — önce değişiklik notu),
          (0e) `verifiedAt` alanını "rıza onay zamanı" olarak yeniden yorumla, (0f) test yaz.
          (0-2) #58 Gel-al WhatsApp yönlendirme: `wa.me` linki + sipariş özeti ön-doldurma,
          `lib/integrations/whatsapp.ts` içinde.
          (0-ARŞİV) WhatsApp Sender (#56) ve Netgsm (9000 TL, #32) — PARKLANDI, ileride
          gerekirse `send-otp.ts` mimarisi katman olarak eklenmeye hazır.
          (1) Şubeler/Footer.tsx/JSON-LD'ye gerçek adresi işle (#54, öncelikli —
          "yayına vereceğiz" ifadesiyle aciliyet belirtildi),
          (2) CONTENT_GUIDE.md'deki â örneklerini ve StepBase.tsx'i güncelle (#53, yeni),
          (3) AboutValues.tsx ile ValueProps.tsx senkronunu teyit et (#55, yeni),
          (4) ARCHITECTURE.md §2.4'ü 5 adıma (+ Bitkisel Protein) güncelle (#10),
          (5) customizerCatalog + "Benim Kâsem" fiyatı — fotoğraf çekimine bağlı (#24),
          (6) Customizer adım başlıklarının Türkçeleştirilmesi/spec senkronu (#28/29),
          (7) VisualPreview.tsx çağıranlarının tam repo taraması (#34),
          (8) ProfileForm.tsx Tailwind sınıflarının DESIGN_SYSTEM.md ile teyidi (#38),
          (9) AddToCartButton.tsx — hiç görülmedi, BSC-6 (çift tıklama koruması) teyit
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
| 12 | "Kâseni Yarat" sadece "Benim Kâsem" (`build-your-own-kasem`) ürününde | ⚠️ Bağlayıcı kapsam kuralı, ayrıca test edilmedi — hâlâ geçerli varsayılıyor. **[Not, 2026-08-01]:** `loyaltyPoints` mekaniği hâlâ netleşmedi — pazaryeri müşteri verisinin erişilemez olduğu bu turda doğrulandığı için, mekanik muhtemelen QR-tabanlı fiziksel kayıt akışına (Boostfeel model) dayanmalı. |
| 13 | `FulfillmentChannel`: `"pickup"` \| `"dine-in"` (delivery yok), sepet/oturum seviyesinde tek alan | ✅ Canlıda doğrulandı VE MASTER_PLAN.md v2.2 sitemap'i artık bu isimlendirmeyle senkron |
| 14-16 | `â` karakteri kaldırıldı (menu-data.json, CartDrawer). Hero.tsx/StepBase.tsx bilinçli ertelendi (#27) | ✅ `menu-data.json` içeriği görülüp `â` yokluğu doğrulandı |
| 15 | Customizer malzeme isimleri Türkçeye çevrildi (id'ler değişmedi) | ✅ Canlıda doğrulandı |
| 18 | CartDrawer portal fix (`createPortal` → `document.body`, backdrop-blur containing-block bug'ı için) | ✅ Canlıda doğrulandı (raporlandı — `useCartStore.ts` bu sohbette bizzat görülmedi, ROADMAP.md Oturum 4'te 🟡 işaretli) |
| 19→20 | Auth: Twilio Verify + Auth.js JWT. DB: Neon Postgres (Vercel Marketplace), `users` tablosu (`phone`,`address`,`displayName`,`loyaltyPoints`,`verifiedAt`) | ✅ Kurulum tamam, build yeşil. MASTER_PLAN.md v2.2 sitemap'ine ve ROADMAP.md'ye (Oturum 4.5) işlendi. |
| 20 | AuthenticatedUser tipi `address` alanıyla genişletildi, DB'de kalıcı saklanıyor | ✅ `types/index.ts`'te doğrulandı |
| 21-22 | Auth kod (route'lar, `auth.ts`, DB katmanı) + görünür giriş UI (`/giris`) | ✅ Kod tamam, `/giris` canlı doğrulandı; OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor |
| 23 | Adres/profil modeli: adres SADECE profil/sadakat verisi, checkout'u bloklamaz, `/hesap`'ta opsiyonel toplanır | ✅ Kod üretildi VE repo varlığı (route.ts, ProfileForm.tsx, page.tsx, rate-limit.ts — 4/4) doğrulandı (#41 kapandı) |
| 🆕 | CategoryNav sekmeleri `BowlItem.category` enum'unu genişletmez — "vegan"/"sicak-tahil" sekmeleri `tags[]` üzerinden sanal filtrelenir (şema değişikliği yok) | ✅ `lib/menu-filters.ts`'te kod-içi gerekçesiyle doğrulandı (#35 kapandı) |
| 🆕 | Alerjen gösterimi: kalori/protein ile aynı zorunluluk statüsü, gizlenemez/opsiyonel yapılamaz | ✅ `DESIGN_SYSTEM.md` §7 VE `AGENT.md` v1.3 protokol karşılığı tam (#7 ve #44 kapandı) |
| 🆕 | Site-geneli "kâse"→"kase" yazım kararı (â kaldırıldı) — CTA'lar ve marka metinlerinde uygulanacak | ⚠️ Kısmen uygulandı: Hero.tsx tamam (2026-08-02). CONTENT_GUIDE.md örnekleri, StepBase.tsx henüz güncellenmedi (#53). |
| 🆕 | Gerçek şube adresi: Çağlayan Park Sokak No:30, Kağıthane, İstanbul | ⚠️ Kısmen uygulandı: AboutStory.tsx'e kuruluş anlatısı olarak işlendi (2026-08-02). Şubeler/Footer/JSON-LD'ye henüz işlenmedi (#54). |
| 🆕 | **[DENEME AŞAMASI, kesin değil]** Twilio/Netgsm yerine geçici olarak: rıza (KVKK) esaslı, doğrulamasız telefon+adres toplama (kanal-bağımsız merkezi `users` kaydı) + gel-al siparişlerinde WhatsApp'a yönlendirme (`wa.me` linki, doğal numara teyidi) | 🟡 Mimari kararlaştırıldı, kod henüz YAZILMADI (#57, #58). Kullanıcı "zaman geçtikçe karara varırız" dedi — nihai değil. |

*(Tam gerekçe/tarih dökümü için: `session_log.md`.)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor — 5 adıma (+ Bitkisel Protein alt-varyantına) hiç güncellenmedi | `ARCHITECTURE.md` §2.4, `CUSTOMIZER_SPEC.md` §3.1 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi | `lib/customizer-data.ts`, `lib/menu-data.json` |
| 27 | 🟢 | Hero.tsx KAPANDI (2026-08-02, â→a uygulandı). StepBase.tsx hâlâ â içeriyor — site-geneli karar kısmen uygulandı | `components/customizer/StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce; `CUSTOMIZER_SPEC.md` §2 senkron değil | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — hem auth hem `/hesap` akışını canlıda test edilemez kılıyor. **[Güncelleme, 2026-08-05]:** Netgsm alternatifi de esnaf odası (9000 TL)/marka tescili istiyor — ayrı bir blokaj. Paralel çözüm olarak WhatsApp OTP fallback'i KODLANDI (aynı Twilio Verify Service, `channel: "whatsapp"`) — bu kısıtı fiilen aşabilir ama canlı test edilmedi, KAPANMADI. Bkz. #56. | Twilio Console, `ROADMAP.md` Oturum 4.5, `lib/auth/send-otp.ts` |
| 34 | 🟢 | `VisualPreview.tsx`'in `className` davranışı — kısmi teyit edildi, tam repo taraması eksik | `components/customizer/VisualPreview.tsx` |
| 38 | 🟢 | `ProfileForm.tsx` Tailwind sınıfları (`bg-olive-600` vb.) DESIGN_SYSTEM.md ile teyit edilmedi | `components/account/ProfileForm.tsx` |
| 39 | 🟠 | `/hesap` akışı Twilio kısıtı yüzünden canlıda hiç fonksiyonel test edilemedi (aslında #32'nin bir sonucu) | `app/hesap/page.tsx` |
| 50 | 🆕 🟢 | `AddToCartButton.tsx` bu sohbette hiç görülmedi — BSC-6 (çift tıklama koruması) ve geçersiz adımda disabled davranışı teyit edilmedi. ROADMAP.md Oturum 3 denetimi sırasında fark edildi. | `components/customizer/AddToCartButton.tsx` |
| 51 | 🆕 🟢 | `useCartStore.ts` bu sohbette hiç görülmedi — CartDrawer portal fix'inin (Karar #18) hâlâ geçerli olduğu ve persist davranışının çalıştığı raporlanmış ama dosya üzerinden teyit edilmemiş. ROADMAP.md Oturum 4 denetimi sırasında fark edildi. | `store/useCartStore.ts` |
| 52 | 🆕 🟡 | **Mimari çelişki:** VisualPreview.tsx + `lib/customizer-visual-layers.ts`, `/public/images/layers/` altında her malzeme için gerçek görsel dosyası bekliyor — klasör tamamen boş, PHOTOGRAPHY_GUIDE.md §8'in "CSS/SVG yeterli" notuyla çelişiyor. Karar: vektörel ikon seti üretilecek (fotoğraf değil), kod değişmeyecek. PHOTOGRAPHY_GUIDE.md §8 notu da bu karara göre düzeltilmeli (ayrı bir açık iş). | `components/customizer/VisualPreview.tsx`, `lib/customizer-visual-layers.ts`, `PHOTOGRAPHY_GUIDE.md` §8 |
| 53 | 🆕 🟢 | CONTENT_GUIDE.md §1/§2'deki "Kâseni Yarat" örnekleri, site-geneli â→a kararına göre henüz güncellenmedi — sadece Hero.tsx yapıldı (#27 ile bağlantılı) | `CONTENT_GUIDE.md` §1, §2 |
| 54 | 🆕 🟡 | Gerçek şube adresi (Çağlayan Park Sokak No:30, Kağıthane, İstanbul) AboutStory.tsx'e işlendi ama Şubeler sayfası/Footer.tsx/JSON-LD şemasına henüz işlenmedi — CONTENT_GUIDE.md §4 NAP tutarlılık kuralı gereği zorunlu. Kullanıcı "yayına vereceğiz" diyerek aciliyet belirtti. | `Footer.tsx`, Şubeler sayfası (henüz yok), JSON-LD şeması |
| 55 | 🆕 🟢 | `AboutValues.tsx`'teki 3 değer listesi (MASTER_PLAN §3.1'den alındı), `components/home/ValueProps.tsx` ile senkron teyit edilmedi — o dosya bu sohbette hiç görülmedi | `components/about/AboutValues.tsx`, `components/home/ValueProps.tsx` |
| 56 | 🆕 🟢 | Twilio hesabında WhatsApp Business Sender'ın onaylı/aktif olup olmadığı bilinmiyor. **[Güncelleme, bu tur]:** PARKLANDI — Twilio Trial hesabı Upgrade için min. $20 istiyor, kullanıcı şu an ödemek istemiyor. #57/#58 mimarisi öncelikli hale geldi, bu iş beklemede. | Twilio Console → WhatsApp Senders, `lib/auth/send-otp.ts` |
| 57 | 🆕 🟡 | Rıza (KVKK) esaslı telefon+adres toplama formu henüz kodlanmadı: aydınlatma metni, rıza checkbox'ı, backend format doğrulaması, `users` şemasına opsiyonel `age`/`gender` alanı. Hukuki metin dikkatli yazılmalı. | Yeni: form bileşeni + `app/api/users/consent-register/route.ts` (henüz yok) |
| 58 | 🆕 🟡 | Gel-al siparişlerinde müşteriyi kendi WhatsApp'ından işletme numarasına yönlendirme akışı (`wa.me` linki, sipariş özeti ön-doldurma) henüz kodlanmadı. | `lib/integrations/whatsapp.ts` (CORE.md dosya haritasında planlıydı, henüz oluşturulmadı) |

> **KAPANDI (önceki turlar):** #4, #7, #15, #16, #20, #22/Karar #11, #35, #43, #44, #49 —
> detaylar önceki SESSION_INDEX sürümlerinde ve bu sohbetin geçmişinde.
>
> **KAPANDI (bu sohbet, bu tur — 2026-08-02):**
> - **Hakkımızda sayfası (404 kapandı):** `/hakkimizda` 6 dosyayla oluşturuldu, test
>   edildi (Vitest, 2/2 geçti — kullanıcı tarafından koşulup teyit edildi). Gerçek
>   şube adresi içeriğe işlendi.
> - **Hero.tsx â→a (site-geneli kararın ilk uygulaması):** CTA "Kaseni Oluştur", alt
>   paragraf sağlıklı beslenme odaklı yeniden yazıldı.
> - **AGENT.md/CORE.md dosya karışıklığı:** AGENT.md yanlışlıkla PUSULA projesinin
>   dosyasıyla yeniden yüklenmişti, fark edilip doğru (Bowlera web sitesi) sürüm
>   tekrar istenip teyit edildi.
> - **"400 satır eşiği" kuralı — kaldırılıp geri getirildi:** Kullanıcı önce kuralı
>   kaldırmayı istedi (CORE.md §7.1, AGENT.md 3 referans), sonra aynı gün bunun
>   yanlış anlaşılma olduğunu belirtti — kural AYNEN eski hâline döndürüldü
>   (AGENT.md v1.4→v1.5, CORE.md v1.3→v1.4). Net kural değişikliği yok.
>
> Detaylı gerekçe/dosya alıntıları bu sohbetin geçmişinde; bir sonraki turda `session_log.md`'ye
> taşınmalı (henüz taşınmadı, bu tur da dahil).

---

## SESSION ÖZET (tümü — 0'dan 6'ya)

| Session | Tarih | Ana içerik | Durum |
|---|---|---|---|
| 0 | — | Ajan altyapısı (14 dosya) | ✅ Tamamlandı |
| 1 | 2026-07-1x | Next.js+Tailwind kurulum, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| 2 | 2026-07-18 | Menü sayfası, filtreleme, MenuCard, statik veri, CategoryNav+FilterPanel, customizer 4→5 adım kararı | ✅ Tamamlandı |
| 3 | 2026-07-18 | Zustand store + pricing + customizer data, masaüstü UI bileşenleri (kesintiye uğradı) | ✅ Büyük ölçüde tamam, bu sohbette dosya-dosya teyit edildi |
| 4 (devam) | 2026-07-18 → 07-22 (11 bölüm) | Sepet/kanal seçimi, Türkçeleştirme, â düzeltmesi, CartDrawer bugfix, auth mimarisi+kod+DB+UI, adres/profil (#23), test triyajı, menü animasyonu, ARCHITECTURE.md v1.3→v1.4, rate-limit üretimi, repo tutarsızlığı keşfi (#42 kapandı), v2 sıkıştırma turunda düşen maddelerin geri bulunması, DESIGN_SYSTEM.md §7 (#7 kapandı), Karar #11/#22 Bitkisel Protein uçtan uca (canlıda doğrulandı), MobileSummaryDrawer format konsolidasyonu (#43), AGENT.md v1.3 alerjen self-check (#44), CUSTOMIZER_SPEC.md §3.5 (#49), **MASTER_PLAN.md v2.2 + ROADMAP.md v1.3 tutarlılık denetimi ve güncellemesi** (Auth/Hesap sitemap'e ve Oturum 4.5'e işlendi, #50/#51 yeni fark edildi) | 🟡 Devam ediyor — Twilio (#32) TEK gerçek darboğaz |
| 5 | 2026-08-01 → 08-02 (3 tur) | (1) 2026-08-01: Netgsm sözleşmesi onaylandı, VisualPreview.tsx mimari denetimi (#52 açıldı, vektörel ikon kararı). (2) 2026-08-01: Pazaryeri müşteri verisi erişimi araştırıldı, Boostfeel/QR-tabanlı sadakat modeli bulundu (Karar #12 ile ilişkilendirildi). (3) 2026-08-02: Hakkımızda sayfası oluşturuldu (gerçek adresle, test edildi), Hero.tsx â→a uygulandı, AGENT.md/CORE.md "400 satır eşiği" kuralı kaldırılıp aynı gün geri getirildi (yanlış anlaşılma), AGENT.md dosya karışıklığı (PUSULA/Bowlera) çözüldü. | 🟡 Devam ediyor — #32 çözüme yaklaşıyor, #53/#54/#55 yeni açıldı |
| 6 | 2026-08-05 (uzun, çok turlu) | Netgsm'in de esnaf odası/marka tescili istediği keşfedildi. WhatsApp OTP birincil + SMS fallback kodlandı, test edildi (3/3 PASS, doğrulandı), push edildi. Twilio Upgrade denendi ($20 gerekiyor, kullanıcı ödemek istemedi) — Netgsm'in "vergi levhası" alternatifinin de Ticaret Sicili ilanı (~9000 TL) gerektirdiği netleşti. Google OAuth telefon paylaşmadığı, online yemek platformlarının kimlik sağlayıcı olmadığı araştırıldı, ikisi de elendi. **Büyük mimari karar:** Twilio/Netgsm PARKLANDI, yerine rıza (KVKK) esaslı doğrulamasız telefon+adres toplama + gel-al siparişlerde WhatsApp yönlendirme kararlaştırıldı (DENEME aşaması, #57/#58 yeni açıldı, henüz kodlanmadı). | 🟡 Devam ediyor — #57/#58 kodlanacak, #32/#56 parklandı |

*(Tam turn-by-turn detay: `session_log.md`.)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel, Vercel Production'da deploy'lar Ready |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 artık kod ile hizalı (Auth/Hesap, kanal isimlendirmesi, Oturum 3/4 durumları) |
| Test Suite | 🟢 `Header.test.tsx`, `customizer-summary-format.test.ts`, `menu-filters.test.ts`, `app/hakkimizda/page.test.tsx` (2/2), `lib/auth/send-otp.test.ts` (yeni, 3/3 PASS — kullanıcı tarafından koşuldu ve ekran görüntüsüyle doğrulandı, 2026-08-05) doğrulandı. Genel `npm test` bu aralıkta tekrar çalıştırılmadı. |
| Auth | 🟡 Kod tamam (`/giris` canlı doğrulandı, MASTER_PLAN/ROADMAP'te resmi) AMA mimari yönü DEĞİŞİYOR — Twilio/Netgsm PARKLANDI (#32/#56), yerine rıza esaslı doğrulamasız toplama + WhatsApp yönlendirme geliştiriliyor (#57/#58, DENEME aşaması, henüz kodlanmadı) |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı — kanal seçimi zorunlu |
| Veritabanı | 🟢 Neon Postgres çalışıyor |
| ARCHITECTURE.md | 🟢 v1.4 güncel ve repoda doğrulandı. §2.4 (5 adım + Bitkisel Protein, #10) bilinçli/teyitli kapsam dışı durum |
| Menü Filtreleme | 🟢 `lib/menu-filters.ts` — kod+test ile doğrulandı |
| Customizer Özet Formatlama | ✅ `lib/customizer-summary-format.ts` — kod+test ile doğrulandı VE `MobileSummaryDrawer.tsx` konsolide edildi |
| Alerjen Gösterim Sistemi | ✅ `DESIGN_SYSTEM.md` §7 VE `AGENT.md` v1.3 protokol karşılığı tam. 🟡 UI implementasyonu henüz yazılmadı. |
| Bitkisel Protein (Main alt-varyant) | ✅ Kod + spec + canlı doğrulama tam. MASTER_PLAN'a bilinçli taşınmadı (spec referansı). |
| Sepet (`useCartStore.ts`, `AddToCartButton.tsx`) | 🟡 Bu sohbette hiç görülmedi — CartDrawer bugfix'i raporlandı ama teyit edilmedi (#50, #51 yeni) |
| Customizer Görsel Önizleme (VisualPreview) | 🔴 Kod çalışıyor ama görsel katmanların hepsi eksik (`/public/images/layers/` boş) — şu an boş daire gösteriyor. Vektörel ikon seti üretimi bekleniyor (#52, yeni) |
| Hakkımızda Sayfası (`/hakkimizda`) | 🟢 Kod tamam, test geçti (2/2). Gerçek adres var; kuruluş yılı/kurucu notu yok (içerik kısmen taslak). Şubeler/Footer/JSON-LD adres senkronu bekleniyor (#54) |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | #57 Rıza esaslı telefon+adres formu (KVKK metni + form + validasyon) — yeni öncelikli yön | 🔴 |
| 1b | #58 Gel-al WhatsApp yönlendirme akışı (`wa.me` linki) | 🟡 |
| 1c | Twilio/Netgsm kararı — PARKLANDI, acil değil (#32/#56) | ⚪ |
| 2 | Gerçek şube adresini Şubeler sayfası/Footer.tsx/JSON-LD şemasına işle (#54, yeni — kullanıcı "yayına vereceğiz" ifadesiyle aciliyet belirtti) | 🟡 |
| 3 | CONTENT_GUIDE.md §1/§2'deki â örneklerini ve StepBase.tsx'i güncelle (#53, yeni) | 🟢 |
| 4 | AboutValues.tsx ile ValueProps.tsx senkronunu teyit et (#55, yeni) | 🟢 |
| 5 | Vektörel ikon seti üretimi (25-30 malzeme, marka paletiyle uyumlu) — kullanıcı üretici bulacak/Claude taslak üretecek, netleşmedi (#52) | 🟡 |
| 6 | PHOTOGRAPHY_GUIDE.md §8 notu düzeltilmeli — "CSS/SVG yeterli" ifadesi kodla çelişiyor (#52 ile bağlantılı) | 🟢 |
| 7 | **Pazaryeri müşteri verisi erişilemez (araştırma tamamlandı):** Boostfeel (ya da benzeri QR tabanlı sadakat çözümü) değerlendirilmeli — Karar #12'deki loyaltyPoints mekaniği bu bulguyla birlikte netleştirilmeli | 🟡 |
| 8 | `AddToCartButton.tsx` + `useCartStore.ts` paylaşılırsa BSC-6 ve persist davranışını teyit et (#50/#51) | 🟢 |
| 9 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a (Bitkisel Protein dahil) güncelle (#10) | 🟡 |
| 10 | DESIGN_SYSTEM.md §7'ye göre alerjen gösterimini MenuCard/Customizer/SummaryPanel'de fiilen uygula | 🟡 |
| 11 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 12 | VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat | 🟢 |
| 13 | ProfileForm Tailwind sınıflarını DESIGN_SYSTEM.md ile teyit et (#38) | 🟢 |
| 14 | Customizer adım başlıklarını Türkçeleştir / spec ile senkronla (#28/29) | 🟢 |
| 15 | Genel `npm test` çalıştırıp güncel geçen/kalan sayıyı teyit et | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v17. ⚠️ Dosya 390 satır — 400 satır eşiğine ÇOK YAKIN. Arşiv
`session_log.md`'ye taşıma bir sonraki oturumda ZORUNLU hale gelecek (Session 4/5/6 detayları
henüz taşınmadı). Bu turda taşınmadı çünkü kullanıcı onayı önce mimari kapanışa odaklandı.
v16'dan değişenler (2026-08-05, Session 6, KAPANIŞ turu): #57/#58 mimarisi TAMAMEN
netleşti ve onaylandı. Kritik keşif: `WhatsAppOrderButton.tsx` zaten repoda var (Session 4,
bilinçli disabled bırakılmış iskelet) — #58 sıfırdan UI değil, iskelet tamamlama işi. Nihai
akış: zorunlu kayıt (ad+telefon+rıza, adres opsiyonel) → 3 kanal seçimi (Masaya Servis/Gel-Al/
Online Sipariş) → fiziksel kanallar WhatsApp'a yönlenir (tek merkezi normal WhatsApp numarası,
Business API DEĞİL) → online platform siparişleri otomatik doğrulanamadığı için kayıt sonrası
manuel WhatsApp→SMS teyidiyle kesinleştirilir. Marka/UX riskleri (sepet terki, WhatsApp hacim)
değerlendirildi, kullanıcı gerekçeyle düzeltti (fiziksel müşteri profili + düşük hacim yüzünden
risk düşük) — kabul edildi. Kod aşamasına geçiliyor.
v15'ten değişenler (2026-08-05, Session 6, bu tur — BÜYÜK MİMARİ KARAR): Kod push edildi.
Twilio Upgrade denendi, Trial hesabı min. $20 istiyor — kullanıcı ödemedi, PARKLANDI.
Netgsm'in "vergi levhası" yolunun da Ticaret Sicili ilanı (~9000 TL) gerektirdiği netleşti —
"ücretsiz alternatif" iddiası GERİ ÇEKİLDİ. Google OAuth ve online yemek platformu "sosyal
girişi" araştırıldı, ikisi de telefon toplama ihtiyacını çözmediği için ELENDİ. Sonuç:
Twilio (#56) ve Netgsm (#32) PARKLANDI — yerine DENEME aşamasında yeni mimari kararlaştırıldı:
(1) rıza (KVKK) esaslı, SMS/WhatsApp kodu OLMADAN telefon+adres toplama, kanal-bağımsız
merkezi `users` kaydı (opsiyonel yaş/cinsiyet), (2) gel-al siparişlerde müşteriyi kendi
WhatsApp'ından işletme numarasına yönlendirme (`wa.me` linki, doğal numara teyidi). Kullanıcı
açıkça "nihai karar değil, zamanla netleşecek" dedi — bu not korunmalı. Yeni açık sorunlar:
#57 (rıza formu, henüz kodlanmadı), #58 (WhatsApp yönlendirme akışı, henüz kodlanmadı).
Öncelik sıralaması buna göre değişti — Twilio/Netgsm artık en düşük öncelik, #57/#58 en üstte.
v14'ten değişenler (2026-08-05, Session 6): `lib/auth/send-otp.test.ts` kullanıcı
tarafından koşuldu ve ekran görüntüsüyle DOĞRULANDI — 3/3 PASS (happy path, edge case,
failure path). Loglardaki `OTP_CHANNEL_FAILED` girdileri failure-path testinin kasıtlı
senaryosu, hata değil — BSC-4 loglaması çalışıyor. Sıradaki liste ve GENEL DURUM tablosu
buna göre güncellendi. Kalan tek adım: kod push + Twilio Console'da WhatsApp Sender
onay kontrolü (#56). Ayrıca dosya-içi tutarsızlık düzeltildi: "SESSION ÖZET (son 5)"
başlığı 7 satır (Session 0-6) içeriyordu, başlık içerikle uyumlu hale getirildi.
v13'ten değişenler (2026-08-05, Session 6): Netgsm SMS başlık başvurusu esnaf odası (9000 TL)/
marka tescili istediği için bloke oldu (⚠️ Session 5'teki "Netgsm sözleşmesi onaylandı" notuyla
çelişiyor, netleştirilmeli). WhatsApp OTP birincil + SMS fallback kararı alındı (Twilio Verify
`channel` parametresiyle tek entegrasyon, ayrı Meta entegrasyonu gerekmiyor). `lib/auth/send-otp.ts`
(yeni), `app/api/auth/otp/send/route.ts` (güncellendi), `lib/auth/send-otp.test.ts` (yeni, 3 test)
üretildi — Kalite 5/5, Güvenlik 8/8. `verify/route.ts` DEĞİŞMEDİ. Yeni açık sorun: #56 (Twilio
WhatsApp Sender onay durumu bilinmiyor).
#32 KAPANMADI ama WhatsApp fallback'le fiilen aşılabilir hâle geldi — canlı doğrulama bekliyor.
Kalan açık sorunlar: #10, #24, #27 (kısmen), #28/29, #32, #34, #38, #39, #50, #51, #52,
#53, #54, #55, #56.
Güncellenme: 2026-08-05.*
