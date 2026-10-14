# BOWLERA — SESSION ARŞİV 3

> ⚠️ **DÖRT ARŞİV DOSYASI ARASINDAKİ İLİŞKİ (bu not, dosya Claude tarafından yazılmıştır —
> 2026-09-27, 37. sohbet kapanışı):**
>
> Bu dosya (`session_arşiv_3.md`), `session_arşiv_2.md`'nin YERİNE GEÇMEZ — onun
> DEVAMIDIR. Tek bir mekanizmanın (CORE.md §7.1 Adım 1: SESSION_INDEX.md 400 satır
> eşiğini geçtiğinde kapanmış içeriği taşımak) dört fiziksel dosyaya bölünmüş hâlidir.
> Bölünme nedeni içerik/kural değişikliği DEĞİL, önceki dosyanın (`session_arşiv_2.md`,
> 2201 satır / 188K) hacimce yönetilemez hale gelmesidir — CORE.md §4, tetikleyici B
> ("arşivin KENDİSİ hacimce şişerse yeni parça açılır", SESSION_INDEX'in kendi 400 satır
> eşiğinden AYRI, bağımsız bir tetikleyici).
>
> **Kronolojik sıra:**
> 1. `session_arşiv.md` → Session 0'dan Session 10'a kadar taşınan bloklar.
> 2. `session_arşiv_1.md` → Session 11'den 2026-08-10'a kadar taşınan bloklar.
> 3. `session_arşiv_2.md` → 2026-08-11'den 2026-09-01 (27. sohbet) kapanışına kadar
>    taşınan bloklar.
> 4. `session_arşiv_3.md` (BU DOSYA) → 2026-09-03'ten (23. sohbet devamı) itibaren
>    taşınan bloklar BURADAN BAŞLAR.
>
> **Değişmeyen kurallar (dört dosya için de AYNEN geçerli):**
> - Hiçbir arşiv dosyası TAM DOSYA olarak yeniden üretilmez — Claude SADECE yeni taşıma
>   bloğunu üretir, kullanıcı kendi dosyasının sonuna ekler.
> - Arşiv bloğu özetlenerek/kırpılarak verilmez — taşınan içerik SESSION_INDEX.md'deki
>   hâliyle BİREBİR (turn-by-turn) korunur.
> - Bir görev/karar/açık soru arşive taşınırken SESSION_INDEX.md'de MUTLAKA kısa bir
>   pointer + kapanış gerekçesi bırakılır.
>
> Tam turn-by-turn geçmiş gerekiyorsa: Session 0–10 için `session_arşiv.md`, Session 11'den
> 2026-08-10'a kadar `session_arşiv_1.md`, 2026-08-11'den 2026-09-01'e kadar
> `session_arşiv_2.md`, 2026-09-03'ten itibaren bu dosya (`session_arşiv_3.md`) kullanılmalı.
>
> ⚠️ **NOT — SESSION_INDEX.md üst notu güncellenmeli:** SESSION_INDEX.md'nin üst notunda
> hangi arşiv parçasının AKTİF (yeni taşıma bloklarının eklendiği) olduğu tek satırla
> belirtilir (CORE.md §4). Bu bölünmeden sonra AKTİF parça artık bu dosyadır
> (`session_arşiv_3.md`) — SESSION_INDEX.md'nin üst notu bu turda AYRICA güncellenmelidir
> (bu 3 dosyalık teslimatın kapsamı dışında bırakıldı, istenirse ayrıca üretilir).

---

## TAŞIMA — 2026-09-03 (23. sohbet devamı, 400 satır eşiği üçüncü kez aşıldı)

> Bu blok SESSION_INDEX.md'nin CURRENT FOCUS bölümünden taşındı. Taşınma gerekçesi: üç blok
> de (19. sohbet CRM keşfi, 20. sohbet SANDWICH_SPEC üretimi, 22. sohbet geriye-dönük işlenen
> sandviç UI/checkout bulgusu) aşağıdaki Açık Sorunlar'da zaten tam özetli — aktif takip için
> gerekli değil, sadece turn-by-turn anlatı taşınıyor:
> - 19. sohbet → Açık Sorunlar #92/#93/#94 + Kritik Kararlar tablosundaki ilgili 2 satır
> - 20. sohbet → Açık Sorun #95 (S1/S2/S5 hâlâ bekliyor) + SESSION_INDEX Dosya Haritası/CORE.md v1.5-1.6
> - 22. sohbet → Açık Sorunlar #99, #100, #101 (KAPANDI), #102, #103, #104

---

### 19. sohbet (2026-08-15) — Çok Şubeli/CRM Vizyon Keşfi

Kullanıcı paylaştığı bir dijital pazarlama/CRM strateji belgesini (3 markalı bir başka işletme
için yazılmış) Bowlera'nın gerçek Neon şemasıyla (5 tablo doğrulandı: `users`,
`consent_registrations`, `order_history`, `password_reset_requests`,
`registration_blocked_attempts`) karşılaştırdı. Kullanıcı vizyonu netleşti: (a) Bowlera
"herhangi an" 2./3. şubeye açılabilir — şema bunun için ŞİMDİDEN geriye dönüşsüz olmayacak
şekilde kurulmalı; (b) farklı şubelerde menü farklılığı olabilir; (c) bu CRM/veri yapısı
Bowlera'ya özel değil, ileride birçok modül/uygulamanın oturacağı TEMEL İSKELET (PUSULA OS
vizyonuyla örtüşüyor). Bulgular + önerilen yön `BOWLERA_COK_SUBELI_CRM_VIZYON.md` adlı ayrı
bir taslak belgede toplandı (ARCHITECTURE.md'nin YERİNE geçmiyor, henüz ona işlenmedi) ve
KULLANICI TALEBİYLE 3 yeni Açık Sorun (#92/#93/#94) olarak loglandı — kod ÜRETİLMEDİ, sadece
analiz + öneri. Sıradaki adım kullanıcı kararıyla netleşti: önce #91'in canlı doğrulaması
yapılacak, #92/#93/#94 SONRA ele alınacak.

---

### 20. sohbet (2026-08-23) — SANDWICH_SPEC.md v1.0/v1.1 Üretimi, Kod Yok

Kullanıcı "Sandviçini Oluştur" akışı için CUSTOMIZER_SPEC.md desenlerinin izole bir kopyasının
çıkarılmasını istedi (Seçenek A — paralel/bağımsız motor, bowl akışına dokunmaz, kullanıcı
onayladı). Subway + Jersey Mike's global sandviç zinciri UX'i web'den araştırıldı, sentezlendi:
Subway'in gerçek sırasına sadık 6 adım (Size→Bread→Protein→Cheese→Veggies→Sauce&Toast&Extras —
ilk önerilen "Bread-first" sıra kullanıcı tarafından REDDEDİLDİ, Subway'in protein/size-first
gerçeğine düzeltildi). Kullanıcının "operasyonu da düşün" uyarısı üzerine UX seçim sırası ile
fiziksel hazırlık sırasının AYRI tutulması kararlaştırıldı — yeni `getPrepOrder()` fonksiyonu
(Personel Sipariş Paneli #62 ticket render'ı için, `selections` state'ini DEĞİŞTİRMEDEN mutfak
sırasına göre yeniden düzenler: Bread→Protein+Cheese→Toast→Veggies→Sauce). Toast, şube-config'e
bağlı opsiyonel özellik olarak tasarlandı (çok şubeli mimariyle #92/#93/#94 bağlantılı, henüz
kararlaştırılmadı). `SANDWICH_SPEC.md` dosyası kullanıcıya artifact olarak verildi, CORE.md
Bölüm 3 (Tetikleyici Tablosu) + Bölüm 4 (Dosya Haritası) AYNI TURDA güncellendi (v1.5) — yeni
referans dosyası eklenince CORE.md senkron kalmalı kuralı uygulandı. Durum: SADECE yapısal
iskelet onaylandı, kod ÜRETİLMEDİ. 6 açık soru (S1: gerçek `sandwich-data.json` verisi, S2:
Veggies ücretsiz kota sayısı, S3: `extras.doubleProtein` vs `proteinPortion:'double'` çakışması,
S4: Toast sabit mi/config'e mi bağlı, S5: "Mike's Way" preset içeriği, S6: `useCartStore
.customization` union tipi genişletmesi) kod aşamasından ÖNCE netleşmeli.

**DÜZELTME (aynı sohbet devamı):** Kullanıcı adım sırasını sorguladı — "Ekmek seçimi en başta
olacak değil mi?" SANDWICH_SPEC.md v1.0'daki "Subway'e sadık Size→Bread" iddiası YANLIŞ çıktı
(gerçek Subway sırası protein-first'tür, ilk araştırmada bu netleştirilmemişti). Kullanıcı
onayıyla Bread-first'e düzeltildi: Bread→Size→Protein→Cheese→Veggies→Sauce&Toast&Extras
(SANDWICH_SPEC.md v1.1). CORE.md Dosya Haritası'ndaki versiyon referansı v1.0→v1.1'e
güncellendi (v1.6). Durum DEĞİŞMEDİ — S1-S6 hâlâ bekliyor.

---

### 22. sohbet (2026-08-23, geriye dönük işlendi) — Sandviç UI Düzeltmeleri + Checkout Blokajı Keşfi

Kullanıcı ham sohbet metnini yapıştırdı — sohbet, Claude bir `grep` çıktısı beklerken
checkpoint'siz kesilmiş. Hiçbir dosyanın push/canlı-test edildiği TEYİT EDİLMEDİ; hepsi "kod
var, doğrulama YOK" statüsüyle #99-#104'e loglandı, hiçbiri TAMAMLANDI sayılmadı.

**Kullanıcının 4 şikâyeti:** (1) menüde "Kâseni Oluştur"/"Sandviçini Oluştur" yan yana durmuyordu;
(2) hero görseli tam görünmüyordu; (3) Sepete Ekle sonrası akış BAŞA dönüyordu (sepete/checkout'a
gitmeliydi); (4) fiyatların "geçici" olduğu belli değildi.

**İddia edilen (PUSH/TEST TEYİT EDİLMEDİ):** `Hero.tsx` buton grid'e çevrildi;
`SandwichSummaryPanel.tsx`'e TEST VERİSİ rozeti eklendi; `HeroImagePlaceholder.tsx` mobil taşma
düzeltildi (`aspect-[4/3]`+`max-h-72`); `SandwichCustomizer.tsx` artık `/siparis`'e yönlendiriyor;
paylaşılan `CartDrawer.tsx` satır 84'teki "her zaman Özel Kase" bug'u "Özel Sandviç" gösterecek
şekilde düzeltildi (Bowl davranışı KORUNDUĞU iddia edildi, DOĞRULANMADI — risk MEDIUM);
`OrderSummary.tsx`'te aynı bug + "Kaldır" butonu eklendi.

**ÇÖZÜLEMEDEN KALAN, KRİTİK:** Sandviçte fiyat ne olursa olsun "Siparişi Onayla"da kırmızı
"fiyatlandırılamadı" hatası çıkıyor, sipariş TAMAMLANAMIYOR. Şüphe (doğrulanmadı):
`FulfillmentGate.tsx`/`ConfirmPickupOrderButton.tsx` sadece Bowl'un `bowlItem`/`customization`
alanlarını tanıyor, `sandwichCustomization`'ı bilmiyor. Kullanıcıdan
`grep -rn "fiyatlandırılamadı" --include="*.tsx" --include="*.ts" .` istendi, YANIT GELMEDEN
kesildi — bkz. #99 (🔴), sandviç checkout'unu tamamen bloklu.

**Sonraki sohbette önce:** (a) grep çıktısını al, kök nedeni doğrula/düzelt; (b) 7 dosya
değişikliğinin hangilerinin fiilen push/test edildiğini tek tek teyit al (ÜÇÜNCÜ DERS).
----.
# EKLENTİ — session_arşiv_2.md'nin SONUNA eklenecek
# Taşıma tarihi: 2026-09-05, 25. sohbet
# Kaynak: SESSION_INDEX.md v77 → v78, CURRENT FOCUS bloğu (23. sohbet devamı, MOTION SYSTEM
# MOBİL TACTILE DÜZELTMESİ anlatısı)
# Kapanış gerekçesi: İçerik artık Açık Sorunlar tablosunda (-5a KAPANDI, P0-2/P0-3 tamamlandı,
# tokens.ts teyidi #107 kapandı) ve Motion System raporunun P0 bölümünde zaten tam özetli —
# aktif takip için gerekli değil, sadece turn-by-turn anlatı taşınıyor.

---

> **[YENİ, 2026-09-03, 23. sohbet devamı — MOTION SYSTEM, MOBİL TACTILE DÜZELTMESİ]**
> Rapor P0-1 (CartDrawer) önceki turda TAMAMLANDI (bkz. #105). Bu turda P0-2 (MenuCard)
> başladı ve canlı doğrulamada kritik bir bulgu çıktı: **rapor (v1.0) baştan sona
> `whileHover` üzerine kurulu, ama Bowlera trafiği neredeyse tamamen dokunmatik** — kod+test
> PASS olmasına rağmen kullanıcı canlıda MenuCard efektlerinin mobilde HİÇ görünmediğini
> doğruladı (ÜÇÜNCÜ DERS'in tekrarı). Üç çözüm seçeneği sunuldu (A: `whileTap` — dokunma anı
> çok kısa; B: mobilde efekti tamamen kaldır — trafiğin çoğu hiç görmez; C: mobile özel ayrı
> tetikleyici), kullanıcı **A'yı** onayladı: `whileTap="hover"` eklendi — dokunma artık
> masaüstü hover ile AYNI hedef variant'a gidiyor. Fiziksellik için giriş/çıkış ayrıştırıldı:
> giriş (rest→hover) mevcut ease korunuyor, çıkış (hover→rest, hem mouse-leave hem
> tap-release) spring'e çevrildi. `MenuCard.tsx` + `MenuCardImage.tsx` (variant propagation
> ile CTA/image otomatik kapsanıyor) kodlandı.
> **Sertlik düzeltmesi (aynı sohbet devamı):** Kullanıcı canlıda "dokunuş çok sert, süre
> uzatılmalı" bildirdi. Release spring, elle tahmin edilen `stiffness/damping` (300/24)
> yerine `duration/bounce` (0.45s / 0.15) tabanlı tanıma çevrildi — süre/sertlik hissini
> doğrudan ayarlamayı sağlıyor.
> **Merkezileştirme (aynı sohbet devamı):** Kullanıcının paylaştığı güncel `MenuCard.tsx`,
> spring'i artık LOKAL değil `lib/motion/tokens.ts`'teki `springs.cardRelease`'ten import
> ediyor. `MenuCardImage.tsx` da aynı kaynağa geçirildi, iki dosya arasındaki LOKAL
> DUPLİKASYON kapandı. **AÇIK MADDE:** `tokens.ts` bu turda hiç görülmedi — `springs
> .cardRelease`'in orada gerçekten var olduğu ve değerinin (0.45/0.15) `MenuCard.tsx`'in son
> paylaşılan importuyla eşleştiği VARSAYILDI (Kural #2 ihlali riski — kaynak: kullanıcının
> paylaştığı dosyanın import satırı). `tokens.ts` paylaşılınca kesin teyit edilmeli.
> **Rapor güncellendi (v1.0→v1.1):** `BOWLERA_MOTION_SYSTEM_RAPORU.md`'ye yeni §1a (Dokunmatik
> Öncelik — zorunlu ön koşul) eklendi, §2/§3/§6/§7 dokunma-tetikleyici ile senkronlandı,
> `springs.cardRelease` token'ı işlendi. Dosya sonuna P1+ katmanların (AccountMenu, Header,
> Hero, Page transitions, Add to Cart, Cart badge) AYNI denetimden HENÜZ geçmediğini belirten
> not eklendi — bunlar kod olarak henüz uygulanmadı.
> **KALAN (MenuCard/#105'e ek):** (a) `tokens.ts`'in gerçek içeriği hiç görülmedi, varsayım
> teyit edilmeli; (b) MenuCard mobil-tactile kararı + `springs.cardRelease` DESIGN_SYSTEM.md
> §6.1'e HENÜZ işlenmedi; (c) CORE.md Dosya Haritası'na rapor v1.1 + değişen dosyalar
> yansımadı; (d) push + canlı doğrulama yapılmadı; (e) mevcut testler (`MenuCard.test.tsx`,
> `MenuCardImage.test.tsx`) yapısal — dokunma davranışını gerçek anlamda test etmiyor, tek
> güvenilir doğrulama telefonda canlı deneme; (f) CategoryNav (P0-3) A/B/C netleşmesine bağlı
> olarak beklemeye devam ediyor — MenuCard'daki whileTap kararının CategoryNav'a nasıl
> yansıyacağı henüz konuşulmadı.

---
# NOT: Yukarıdaki "KALAN" maddelerinin çoğu artık ÇÖZÜLDÜ (tokens.ts paylaşıldı ve #107
# kapandı, P0-2/P0-3 tamamlandı, Motion System P1/P2 de tamamlandı — bkz. SESSION_INDEX.md
# v77/v78 Açık Sorunlar tablosu). Bu blok SADECE tarihsel kayıt olarak arşivleniyor.
------
> **EKLENTİ — 2026-09-05 (26. sohbet, devam 2).** Bu blok, kullanıcı tarafından mevcut
> `session_arşiv_2.md` dosyasının SONUNA elle eklenmelidir. Aşağıdaki 13 satır, SESSION_INDEX.md
> 400 satır eşiğini beşinci kez aştığı için taşınmıştır (CORE.md §7.1 Adım 1). Hepsi taşınma
> anında zaten ✅ (tamamen kapanmış) durumdaydı — kapanış gerekçesi her satırın kendi metninde
> mevcuttur, ayrıca aşağıda tek satırlık özetleri de verilmiştir.

---

## Taşınan Açık Sorunlar (6 madde)

| # | Öncelik | Açıklama | Etkilenen Dosya(lar) |
|---|---|---|---|
| 39 | 🟢 | **[Bu turda ÇÖZÜLDÜ]** `/hesap` akışı artık rıza esaslı kayıt (OTP'siz) üzerinden canlıda test edildi ve DOĞRULANDI — Twilio kısıtı bu akışı artık engellemiyor. | — |
| 50 | ✅ | **[BU TURDA KAPANDI]** `AddToCartButton.tsx` görüldü, BSC-6 (çift ekleme race condition) doğrudan ele alındı ve seçim-kimliği bazlı kilitle çözüldü — bkz. #75. | `components/customizer/AddToCartButton.tsx` |
| 70 | ✅ | **[BU TURDA KAPANDI]** `order_history.table_number` tipi `text` olarak kararlaştırıldı (masa adları sayısal olmayabilir), index sadece `status` üzerine eklendi (`table_number` filtrelenmeyecek). Migration Neon'da koşuldu ve DOĞRULANDI. | `docs/schema-changes/20260809140000_order_history_status_tablenumber_customernotes_eklendi.md` |
| 85 | ✅ | **[BU TURDA KAPANDI]** Gel Al kod incelemesi bulgularının 5'i de ele alındı: (1) BSC-4 sessiz catch → structured log + kullanıcı mesajı; (2) reduced-motion → `motion-safe:` varyantı; (3) bayat yorumlar temizlendi; (4) `recordFailedContactAttempt` atomik SQL UPDATE'e çevrildi (confirm/reject kısmı bilinçli MVP-dışı bırakıldı, bkz. #87); (5) 3 test dosyası yazıldı, Codespaces'te 15/15 PASS doğrulandı, GitHub'a push edildi. | `components/personel/GelAlPanel.tsx`, `GelAlOrderCard.tsx`, `lib/personel/gel-al-queries.ts` + 3 test dosyası |
| 96 | ✅ | **[BU TURDA KAPANDI]** Sandviç bileşen testleri (`SandwichCustomizer` + 6 adım bileşeni) yazıldı ve Codespaces'te doğrulandı: 7/7 dosya, 27/27 test PASS (2026-08-23 18:28). Yol boyunca 2 sorun çıktı, ikisi de çözüldü: `act()` eksikliği ve unutulan `StepSauceToastExtras.test.tsx` pushu. | `components/sandwich/*.test.tsx` |
| 101 | ✅ | **[BU TURDA KAPANDI, 2026-09-03, 23. sohbet]** 22. sohbetteki "Özel Kase" fallback bug'u (`item.bowlItem?.name ?? "Özel Kase"` sandviçlerde hep "Özel Kase" yazdırıyordu) `CartDrawer.tsx`'in bu turdaki motion yükseltmesiyle YENİDEN yazıldı VE test edildi — `CartDrawer.test.tsx`'teki "bowlItem null + sandwichCustomization dolu → Özel Sandviç; ikisi de null → Özel Kase" testi Codespaces'te PASS (8/8, 2026-09-03 06:16, ekran görüntüsü). Bowl davranışı da (`bowlItem?.name` önceliği) happy-path testinde doğrulandı. **KALAN:** push + canlı/production doğrulaması — bkz. #105. | `components/cart/CartDrawer.tsx` |

## Taşınan Sıradaki Görevler (7 madde)

| Sıra | Görev | Öncelik |
|---|---|---|
| -5a | **[TAMAMLANDI, 24. sohbet, 2026-09-04 ✅]** `lib/motion/tokens.ts` satır 61 `springs.cardRelease` — kullanıcının yüklediği güncel dosyada değer zaten `{duration:0.45, bounce:0.15}` olarak doğruydu (kod değişikliği GEREKMEDİ, önceki turda zaten düzeltilip push edilmiş ama SESSION_INDEX'e işlenmemişti). Kullanıcı "push edildi ve canlıda" diye doğruladı. | ✅ |
| -11 | **[KAPANDI, 25. sohbet, 2026-09-05 ✅]** CartBadge'de 2 gerçek bug bulundu ve düzeltildi (canlı testte kullanıcı bulguları üzerine): (1) `count===0` iken bileşen hiç mount olmuyordu, ilk ürün eklemede (0→1) `useRef` başlangıcı yanlış eşitlenip pulse hiç tetiklenmiyordu; (2) düzeltme sırasında `controls.start({scale:[...]})` opacity'i hiç 1'e ayarlamadığı için rozet tamamen görünmez kaldı. İkisi de düzeltildi, kullanıcı "bu sorun tamam" dedi. Ayrıca süre/bounce/scale kullanıcı testiyle güçlendirildi (0.4s/1.3→0.6s/1.5, bounce:0.35). | ✅ |
| -12 | **[TAMAMLANDI, 25. sohbet, 2026-09-05 ✅]** Motion System rapor P2 — Customizer Spatial step transition. `app/menu/customize/[id]/page.tsx` (kase) VE `components/sandwich/SandwichCustomizer.tsx` (sandviç) — ikisine de `AnimatePresence(mode="wait")`+opacity/x eklendi, yön (ileri/geri) `currentStep`'in önceki render değeriyle hesaplanıyor, #90'ın hassas height/scroll layout'una DOKUNULMADI. Sandviç akışında kayma mesafesi kullanıcı testiyle 24px→40px'e çıkarıldı (kart sarmalayıcısı olmadığı için daha az belirgindi). **YAN BULGU (düzeltildi):** sandviç akışında "Geri" butonu HİÇ YOKTU (sadece StepDots'tan tıklanabiliyordu) — `SandwichCustomizer.tsx`'e paylaşılan tek bir "Geri" butonu eklendi (previousStep(), 1. adımda gizli). | ✅ |
| -13 | **[TAMAMLANDI, 25. sohbet, 2026-09-05 ✅]** Motion System rapor P2 — VisualPreview Layer entrance. Kod ZATEN vardı (`VisualPreview.tsx`, opacity+scale, reduced-motion korumalı) — sadece hardcoded `0.25`/`"easeOut"` yerine merkezi `durations.visualPreviewLayer`+`easings.easeOut` token'larına bağlandı. Görsel değişiklik YOK (davranış birebir aynı), kullanıcıya bu netleştirildi. | ✅ |
| -1 | **[TAMAMLANDI, bu turda ✅]** #84 — isim gösterme sorunu kullanıcı tarafından canlıda ("bari" görünür) doğrulandı. Kök neden SQL sorgusuyla izole edilmedi, kullanıcı deneyimi seviyesinde kapandı. | ✅ |
| 0 | **[TAMAMLANDI, bu turda ✅]** #83 — "Sıfırla" → üretilen geçici kodla (460244) giriş canlıda BAŞARILI test edildi. | ✅ |
| 0b | **[TAMAMLANDI, bu turda ✅]** #82 — Neon'a elle dokunmadan, orijinal kayıt şifresiyle çıkış→giriş döngüsü canlıda BAŞARILI test edildi. | ✅ |

---

*Kapanış gerekçesi (tümü için ortak): yukarıdaki 13 satırın hepsi taşınma anında ✅ durumundaydı;
kapanış bilgisi SESSION_INDEX.md'nin Kritik Kararlar tablosunda ve/veya bu bloğun kendisinde
tam olarak korunmaktadır. Aktif takip için SESSION_INDEX.md'de tutulmaları gerekmiyor.*
------
> Bu blok, SESSION_INDEX.md'nin 2026-09-07 (Admin Panel CRUD/cache-bug turu) güncellemesinde
> 400 satır eşiği yeniden aşıldığı için taşındı. Kendi elinizle `session_arşiv_2.md`'nin
> SONUNA ekleyin. Kapanış gerekçesi: bu blok artık Kritik Kararlar tablosunda (ImageKit,
> menu_items migration, admin rolü, tags/allergens listeleri) ve Açık Sorunlar #108-#113'te
> tam özetli — aktif takip için gerekli değil, sadece turn-by-turn planlama anlatısı arşive
> taşınıyor.

## 26. sohbet (2026-09-05) — Admin Panel planlaması tam anlatısı

**Kararlaştırılanlar:**
- Erişim: tek admin hesabı. MVP kapsamı: tam kapsam tek seferde (görsel+menü/fiyat/kalori CRUD).
- Görsel depolama: **ImageKit** (Cloudinary'ye karşı karşılaştırıldı — sınırsız dönüşüm +
  daha geniş ücretsiz bant genişliği gerekçesiyle tercih edildi).
- Menünün gerçek konumu doğrulandı (#93 KAPANDI): `lib/menu-data.json` (imza kaseler+
  içecekler), `lib/sandwich-data.json` (sandviçler, TEST VERİSİ, #95), `lib/customizer-
  data.ts` (build-your-own malzeme kataloğu). Bu turda SADECE `menu-data.json` ele alındı.
- Alan listesi netleşti: `name/category/price/image` zorunlu; `calories/protein` ZORUNLU
  (asla gizlenemez — ARCHITECTURE.md §3/DESIGN_SYSTEM.md §7.0); `allergens` (5 sabit değer:
  gluten/dairy/nuts/soy/shellfish — kod+canlı davranışla teyitli, DESIGN_SYSTEM.md'nin 7'lik
  listesi GÜNCEL DEĞİL, bkz. Açık Sorun #108); `tags`/diyet-kalori etiketi (5 sabit değer,
  gerçek veriden çıkarıldı: yüksek protein/glutensiz/vegan/sıcak-tahıl/düşük kalori — canlı
  filtre ekranının "Keto" seçeneği hiç kullanılmadığı için DAHİL EDİLMEDİ, bkz. Açık Sorun
  #109); `carbs`/`fat` opsiyonel.
- `build-your-own-kasem` kaydı (test verisi) `menu_items` tablosuna DAHİL EDİLMEDİ —
  `grep -rn "build-your-own-kasem"` ile DOĞRULANDI: sadece `Hero.tsx`'te bir CTA linki
  (`/menu/customize/build-your-own-kasem`), hiçbir menü listeleme bileşeninde ürün olarak
  render edilmiyor.
- `menu_items.id` bilinçli olarak `uuid` DEĞİL `text` — mevcut string id'ler
  (`sig-teriyaki-tavuk` vb.) korundu, dış referans kırılması riske edilmedi.
- Admin yetkisi `users.role`'e YENİ bir `"admin"` değeri olarak eklendi — mevcut `"staff"`
  rolünden BİLİNÇLİ OLARAK AYRI (gerekçe: staff ileride birden fazla kişiye açılabilir,
  admin "tek admin hesabı" kararı gereği ayrı kalmalı — bu karar 27. sohbette kısmen
  revize edildi, bkz. Kritik Kararlar/#112).

**Yapılıp Neon'da doğrulanan:**
- `menu_items` tablosu migration'ı (`001_menu_items.sql`) koşuldu — 13 kolon, tipler
  `information_schema.columns` sorgusuyla DOĞRULANDI (id:text, calories/protein:integer
  NOT NULL, carbs/fat:integer nullable, tags/allergens:ARRAY NOT NULL — hepsi beklendiği gibi).
- Seed (`002_seed_menu_items.sql`, 8 gerçek ürün) koşuldu — `SELECT COUNT(*)` **8** döndü,
  DOĞRULANDI.

**Bu turda kullanıcıya TESLİM EDİLDİ (27. sohbette repoya uygulanıp doğrulandı — bkz. #112):**
- `lib/db/schema.ts`, `middleware.ts`, `auth.ts`, `types/next-auth.d.ts` — 4 dosya, `"admin"`
  rolü için TAM DOSYA olarak, üçlü senkron üretildi.
  ----
  > ─────────────────────────────────────────────────────────────────────────
> **EKLENTİ — 2026-09-08, 29. sohbet kapanışı, SESSION_INDEX.md 400 satır eşiği**
> **yeniden aşıldığı için taşındı.** Kendi elinizle mevcut `session_arşiv_2.md`
> dosyanızın SONUNA aşağıdaki 4 bloğu (DÖRDÜNCÜ–YEDİNCİ DERS) ekleyin.
> ─────────────────────────────────────────────────────────────────────────

> ⚠️ DÖRDÜNCÜ DERS (2026-08-07, Session 11): Session 10'un kapanış notunda "konuşma
> giriş/kayıt akışlarına geçti, içeriği sağlanmadı, bir sonraki güncellemede eklenecek"
> denmişti — ama o sohbet kapandığında SESSION_INDEX GÜNCELLENMEDEN kaldı. Kullanıcı,
> kapanan sohbetin tam metnini yeni bir sohbete taşıyarak bu güncellemeyi GERİYE DÖNÜK
> yaptırdı. Kural teyit edildi: "bir sonraki güncellemede eklenecek" notu bırakmak,
> güncellemenin GERÇEKTEN yapılacağının garantisi değildir. Mümkünse görev, sohbet
> kapanmadan ÖNCE işlenmeli; bu mümkün değilse not AÇIK SORUN olarak da ayrıca loglanmalı.

> ⚠️ BEŞİNCİ DERS (2026-08-08, DÖRDÜNCÜ DERS'in TEKRARI): `types/index.ts`/`auth.ts`/
> `middleware.ts` kodu üretilip [KARAR BİLDİRİMİ] ile sunulmuştu (confidence MEDIUM, 2 açık
> varsayım: 403-vs-redirect kararı + `next-auth.d.ts` görülmedi) — ama kullanıcı onayı
> gelmeden ve SESSION_INDEX güncellenmeden sohbet kesildi. Kullanıcı üretilen 3 dosyayı +
> AGENT.md/CORE.md/SESSION_INDEX.md'yi yeni sohbete taşıyarak güncellemeyi GERİYE DÖNÜK
> yaptırdı — DÖRDÜNCÜ DERS'teki mekanizmanın birebir tekrarı. Ek bulgu: dosyalar arası
> senkron kontrolünde `types/index.ts`'in kendi iç yorumu ("auth.ts HENÜZ bu alanı set
> etmiyor") GÜNCEL DEĞİL — auth.ts fiilen zaten `role`'ü JWT/session callback'lerine
> set ediyor. Bu, "üç dosya senkron" iddiasının TAM doğru olmadığını gösteriyor (kod
> senkron, ama açıklayıcı yorum bloklarından biri geride kalmış). Kural pekiştirildi:
> KARAR BİLDİRİMİ + kod üretimi sonrası kullanıcı onayı/checkpoint gelmeden sohbet kapanma
> riski varsa, en azından AÇIK SORUN olarak loglanmalı.

> ⚠️ ALTINCI DERS (2026-08-09, DÖRDÜNCÜ/BEŞİNCİ DERS'in ÜÇÜNCÜ TEKRARI): #75 üzerinde
> derin bir çözüm turu yapıldı (3 iterasyon: `useRef`→`useState` görsel geri bildirim,
> süre-bazlı kilit→seçim-kimliği kilidi, tekil `lockedKey`→`Set<string> addedKeys` — testin
> yakaladığı gerçek bir tasarım hatası düzeltildi) — ama sohbet, testlerin YENİDEN
> koşturulduğu/geçtiği, `npm run build`'in yerel doğrulandığı VE commit+push'un fiilen
> yapıldığı teyit edilmeden kesildi. Kullanıcı yine tam sohbet metnini yeni bir sohbete
> taşıyarak güncellemeyi GERİYE DÖNÜK yaptırdı. Kural aynı: bu üç ders artık tek seferlik
> istisna değil, TEKRARLAYAN bir kalıp — checkpoint sorusu her büyük görev ADIMINDAN sonra
> (sadece görev TAMAMEN bitince değil) daha sık sorulmalı.

> ⚠️ YEDİNCİ DERS (2026-08-09, DÖRDÜNCÜ/BEŞİNCİ/ALTINCI DERS'in DÖRDÜNCÜ TEKRARI): #79'un
> masaüstü ayağı (`SummaryPanel.tsx`) + iki test dosyası düzeltildi, `npm run build` yerelde
> temiz koştu, kullanıcı 3 dosyayı GitHub'a manuel kaydettiğini onayladı. Ajan SESSION_INDEX.md'yi
> TAM DOSYA olarak üretmeye başlamıştı (400 satır eşiği geçildiği için önce 2 eski CURRENT
> FOCUS bloğunun `session_arşiv_1.md`'ye taşınacağını bildirmişti) — ama bu işlem
> TAMAMLANMADAN sohbet kesildi. Kullanıcı yine tam sohbet metnini yeni bir sohbete taşıyarak
> güncellemeyi GERİ DÖNÜK yaptırdı. Kural aynı, artık dördüncü kez doğrulandı: checkpoint/
> dosya-üretimi "başladım" demek "bitti" demek değildir.

> **Kapanış gerekçesi (bu taşımanın kendisi için):** Bu 4 ders bloğu SESSION_INDEX.md'nin
> güncel çalışma alanı için artık gerekli değil — ders içerikleri zaten AGENT.md'nin genel
> "checkpoint sık sorulmalı" ilkesine kalıcı olarak işlenmiş durumda, burada sadece
> turn-by-turn tarihsel kanıt olarak tutuluyorlardı. Aktif takip gerektiren hiçbir açık
> madde içermiyorlar.

---------
<!-- session_arşiv_2_EKLENTI_2026-09-24.md -->
<!-- SADECE YENİ EKLEME: kullanıcı bu bloğu kendi elinle mevcut session_arşiv_2.md dosyasının sonuna ekler. -->
<!-- Kaynak: SESSION_INDEX.md, 2026-09-24 (30. sohbet kapanışı), 400 satır eşiği aşıldığı için taşındı (CORE.md §7.1 Adım 1). -->

---

## TAŞIMA BLOĞU — 2026-09-24 (30. sohbet kapanışı, 400 satır eşiği)

### 1. Eski üst-not (header) blokları

**Kapanış gerekçesi:** Bunlar SESSION_INDEX.md'nin başındaki uyarı yığınında biriken, artık tamamlanmış geçmiş taşıma kayıtları ve iki ders bloğuydu (İKİNCİ DERS, ÜÇÜNCÜ DERS). Ders içerikleri AGENT.md VERSİYON GEÇMİŞİ'nde (Session 4 — 400 satır eşiği kuralının kendisi; 23. sohbet — ÜÇÜNCÜ DERS'in "dokunmatik öncelik" tekrarı) kalıcı ilke olarak zaten işli, aktif takip gerektirmiyordu.

> ⚠️ **TAŞIMA NOTU (2026-09-08, 29. sohbet kapanışı):** SESSION_INDEX.md yeniden 400 satır
> eşiğini aştı. DÖRDÜNCÜ, BEŞİNCİ, ALTINCI ve YEDİNCİ DERS blokları (4 blok, ~42 satır — hepsi
> "checkpoint sık sorulmalı, sohbet aniden kesilebilir" temasının tekrarı, en eskisi
> 2026-08-07 tarihli) TAM metinleriyle `session_arşiv_2.md`'ye taşındı — kullanıcıya ayrı bir
> eklenti dosyası (`session_arsiv_2_EKLENTI_2026-09-08.md`) olarak verildi, kendi elinizle
> mevcut `session_arşiv_2.md`'nizin sonuna eklemeniz gerekiyor. Kapanış gerekçesi o dosyada
> mevcut — ders içerikleri AGENT.md'nin genel ilkesine zaten kalıcı işlendiği için aktif
> takip gerektirmiyorlardı. ⚠️ **DÜRÜST NOT:** bu tek taşıma (42 satır) yeni eklenen içeriği
> (kategori sistemi + #116 dersi, ~55 satır) dengelemedi — dosya bu güncellemeyle de 400
> satırın ÜZERİNDE kalıyor. Bir sonraki sohbette İKİNCİ bir taşıma turu (aday: en eski
> KAPANDI ✅ satırlarının [#85/#93/#96/#101/#112/#113 gibi] tam anlatısı, SESSION ÖZET
> tablosundaki 0-9 arası satırlar) ele alınmalı.
> ⚠️ **YENİ TAŞIMA UYARISI (bu güncelleme, 2026-09-05, 26. sohbet):** Bu dosya bu güncellemeyle
> 407 satırdan ~480+ satıra çıktı — 400 satır eşiği (CORE.md §7.1 Adım 1) yeniden aşıldı.
> Bu turda AJAN dosyanın SADECE 93-315. satırları arasını (eski turlarda) görebildi, TAM
> içeriği bu turda ilk kez uçtan uca okundu — ama hacim/taşıma işlemi (hangi bloğun
> `session_arşiv_2.md`'ye gideceği) BU TURDA YAPILMADI, çünkü arşiv dosyasının güncel hâli
> görülmedi (Kural #2 — arşive ekleme yapmadan önce dosyanın mevcut sonunu görmek gerekir).
> **Bir sonraki sohbette ele alınmalı:** en eski/en çok özetlenmiş bloklar (SESSION ÖZET
> tablosundaki 0-10, ve/veya en eski KAPANDI notları) taşınmalı.
> ⚠️ GEÇMİŞ İHLAL KAYDI (ders çıkarıldı, hâlâ geçerli):
> 2026-07-20'de üretilen bir "v2 sıkıştırılmış" SESSION_INDEX dosyası, kapanış notu
> olmadan 7 açık sorunu (#4,7,15,16,20,22,34) ve 2 kararı (#11,#12) tablolardan düşürmüştü.
> Bu, aynı gün içindeki bir sonraki sohbette fark edilip geri eklenmiş, ve BU sohbette
> tek tek dosyayla teyit edilerek gerçek sonuçlarına kavuşturulmuştur. Kural teyit edildi:
> tamamlanmış görev silinirken MUTLAKA kapanış gerekçesi session_arşiv.md'ye yazılmalı;
> aksi halde "tamamlandı" iddiası doğrulanamaz hale geliyor.

> ⚠️ **TAŞIMA NOTU (2026-08-23, 21. sohbet):** SESSION_INDEX.md 441 satıra ulaşınca (400 satır
> eşiği aşıldı), 7 kapanmış/güncelliğini yitirmiş blok (18. sohbet #91 detayı, 17. sohbet #90
> detayı, + 5 "KAPANDI (BU TURDA)" anlatı bloğu: #82/83/84, #74, #79/75/80, #50, #76/77) TAM
> metinleriyle `session_arşiv_2.md`'ye taşındı — kullanıcıya ayrı bir eklenti dosyası
> (`session_arsiv_2_EKLENTI_2026-08-23.md`) olarak verildi, kendi elinizle mevcut
> `session_arşiv_2.md`'nizin sonuna eklemeniz gerekiyor. Kapanış gerekçesi o dosyada mevcut.

> ⚠️ **TAŞIMA NOTU (2026-08-23, 22. sohbet):** SESSION_INDEX.md yeniden 400 satır eşiğini
> aşınca, SEKİZİNCİ DERS (21. sohbet) tam anlatı bloğu TAM metniyle `session_arşiv_2.md`'ye
> taşındı — kullanıcıya ayrı bir eklenti dosyası (`session_arsiv_2_EKLENTI_2026-08-23-devam2.md`)
> olarak verildi, kendi elinizle mevcut `session_arşiv_2.md`'nizin sonuna eklemeniz gerekiyor.
> Kapanış gerekçesi o dosyada ve Arşiv Taşıma Kaydı tablosunda mevcut.

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

> ⚠️ **TAŞIMA NOTU (2026-08-10, 13. sohbet devamı):** SESSION_INDEX.md 463 satıra ulaşınca
> (400 satır eşiği aşıldı, CORE.md §7.1 Adım 1), 4 kapanmış/güncelliğini yitirmiş CURRENT
> FOCUS bloğu (SOHBET KAYBI uyarısı, iki adet #62 Gel Al ara-durum bloğu, #82/#83/#84 kapanış
> bloğu) TAM metinleriyle `session_arşiv_1.md`'ye taşındı — kullanıcıya ayrı bir eklenti
> dosyası (`session_arsiv_1_EKLENTI_2026-08-10.md`) olarak verildi, kendi elinizle mevcut
> `session_arşiv_1.md`'nizin sonuna eklemeniz gerekiyor. Her taşınan madde için kapanış
> gerekçesi o dosyada mevcut.


### 2. CURRENT FOCUS — 28. sohbet (2026-09-07) tam anlatısı

**Kapanış gerekçesi:** İçerik Açık Sorunlar #114 (kapandı, kök neden REVİZE EDİLDİ) ve #116'da (DOKUZUNCU DERS) zaten tam özetli; turn-by-turn anlatı aktif takip için gerekli değil.

> **[ÖNCEKİ — 2026-09-07, 28. sohbet]** Admin panelde ilk gerçek kullanıcı testi yapıldı —
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


### 3. CURRENT FOCUS — 27. sohbet (2026-09-06) tam anlatısı

**Kapanış gerekçesi:** İçerik Açık Sorunlar #112/#113 (ikisi de kapandı) ve GENEL DURUM'daki "Auth"/"Admin Panel" satırlarında zaten tam özetli.

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


### 4. SESSION ÖZET tablosu — Session 0-9 satırları

**Kapanış gerekçesi:** Bu 10 session'ın tamamı ✅ Tamamlandı veya 🟡/🔴 durumuyla sonraki session'lara devretmiş biçimde kapanmıştı; ilerleyişleri Açık Sorunlar tablosunda ve GENEL DURUM özetinde ayrıca izleniyor, tarihsel kayıt olarak burada saklanıyor.

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


### 5. Açık Sorunlar tablosu — KAPANDI ✅ satırlarının tam anlatısı (#85/#93/#96/#101/#112/#113)

**Kapanış gerekçesi (hepsi):** Bu 6 madde de ✅ KAPANDI durumunda; sonuçları Kritik Kararlar tablosunda ve/veya GENEL DURUM özetinde hâlâ özet olarak duruyor. Aşağıda tam anlatı korunuyor.

| # | Öncelik | Açıklama | Etkilenen Dosya(lar) |
|---|---|---|---|
| 85 | ✅ | **[BU TURDA KAPANDI]** Gel Al kod incelemesi bulgularının 5'i de ele alındı: (1) BSC-4 sessiz catch → structured log + kullanıcı mesajı; (2) reduced-motion → `motion-safe:` varyantı; (3) bayat yorumlar temizlendi; (4) `recordFailedContactAttempt` atomik SQL UPDATE'e çevrildi (confirm/reject kısmı bilinçli MVP-dışı bırakıldı, bkz. #87); (5) 3 test dosyası yazıldı, Codespaces'te 15/15 PASS doğrulandı, GitHub'a push edildi. | `components/personel/GelAlPanel.tsx`, `GelAlOrderCard.tsx`, `lib/personel/gel-al-queries.ts` + 3 test dosyası |
| 93 | ✅ | **[BU TURDA (26. sohbet) KAPANDI]** Menü verisinin gerçek konumu doğrulandı: `lib/menu-data.json` (imza kaseler+içecekler), `lib/sandwich-data.json` (sandviçler, TEST VERİSİ, #95), `lib/customizer-data.ts` (build-your-own malzeme kataloğu). `menu-data.json`'daki 8 gerçek ürün `menu_items` DB tablosuna taşındı, migration+seed Neon'da doğrulandı. Şube-bazlı menü önerisi (branch_menu_items eşleme tablosu) HÂLÂ ONAYLANMADI, ayrı bir karar — bu turun kapsamı SADECE tek-şube admin panel ön koşuluydu. | `lib/menu-data.json`, `lib/db/schema.ts` |
| 96 | ✅ | **[BU TURDA KAPANDI]** Sandviç bileşen testleri (`SandwichCustomizer` + 6 adım bileşeni) yazıldı ve Codespaces'te doğrulandı: 7/7 dosya, 27/27 test PASS (2026-08-23 18:28). Yol boyunca 2 sorun çıktı, ikisi de çözüldü: `act()` eksikliği ve unutulan `StepSauceToastExtras.test.tsx` pushu. | `components/sandwich/*.test.tsx` |
| 101 | ✅ | **[BU TURDA KAPANDI, 2026-09-03, 23. sohbet]** 22. sohbetteki "Özel Kase" fallback bug'u (`item.bowlItem?.name ?? "Özel Kase"` sandviçlerde hep "Özel Kase" yazdırıyordu) `CartDrawer.tsx`'in bu turdaki motion yükseltmesiyle YENİDEN yazıldı VE test edildi — `CartDrawer.test.tsx`'teki "bowlItem null + sandwichCustomization dolu → Özel Sandviç; ikisi de null → Özel Kase" testi Codespaces'te PASS (8/8, 2026-09-03 06:16, ekran görüntüsü). Bowl davranışı da (`bowlItem?.name` önceliği) happy-path testinde doğrulandı. **KALAN:** push + canlı/production doğrulaması — bkz. #105. | `components/cart/CartDrawer.tsx` |
| 112 | ✅ | **[BU TURDA (27. sohbet) KAPANDI]** 4 dosya (`schema.ts`/`auth.ts`/`middleware.ts`/`types/next-auth.d.ts`) repoya uygulandı, `npx tsc --noEmit` + `npm run build` temiz, push edildi. Neon'da `+905431615778` numarası `role='admin'` yapıldı VE canlıda doğrulandı (`SELECT` ile teyit edildi). **YENİ KARAR (kullanıcı isteğiyle):** bu hesabın hem `/personel` hem `/admin`'e erişmesi istendiği için `middleware.ts`'teki `/personel` guard'ı `role !== 'staff' && role !== 'admin'` olarak GENİŞLETİLDİ (admin artık staff'ın süperkümesi, ama `/admin` guard'ı hâlâ SADECE `role==='admin'` — tek admin kararı bozulmadı). Canlıda hem `/personel` hem `/admin` (o an 404 — sayfa yoktu ama 403 YOKTU) doğrulandı. | `middleware.ts` |
| 113 | ✅ | **[BU TURDA (27. sohbet) KAPANDI]** Admin panelinin ilk CRUD'u yazıldı ve DEPLOY EDİLDİ: `lib/imagekit.ts`, `lib/admin/menu-item-constants.ts`, `app/api/admin/upload-image/route.ts`, `app/api/admin/menu-items/route.ts` (GET+POST), `app/api/admin/menu-items/[id]/route.ts` (GET+PATCH+DELETE), `components/admin/MenuItemForm.tsx`, `app/admin/page.tsx` (liste), `app/admin/menu-items/new/page.tsx`, `app/admin/menu-items/[id]/page.tsx`. ImageKit hesabı açıldı (Public Key/Private Key/URL Endpoint alındı, `.env.local`+Vercel env'e eklendi), `imagekit` npm paketi kuruldu. Yol boyunca 3 build hatası çıktı, hepsi çözüldü: (1) `imagekit` paketi package.json'a hiç eklenmemişti — `npm install imagekit --save`; (2) `MENU_ITEM_TAGS.includes()` TS literal-tipi hatası — `as readonly string[]` cast'iyle çözüldü; (3) `app/admin/page.tsx`'in kendisi ilk pushta unutulmuştu (sadece alt sayfalar gitmişti) — ayrıca eklenip push edildi. **CANLIDA DOĞRULANDI:** `/admin` artık 8 gerçek ürünü doğru isim/fiyat/kategoriyle listeliyor. | `app/admin/*`, `app/api/admin/*`, `lib/imagekit.ts`, `components/admin/MenuItemForm.tsx` |


### 6. Sürüm geçmişi — v75 ila v79 (tam metin)

**Kapanış gerekçesi:** Bu 5 sürüm notu 2026-09-04→2026-09-05 arası Motion System P1/P2 çalışmasını anlatıyor; sonuçları Açık Sorunlar #105/#107 ve GENEL DURUM'da zaten özetli. v80 artık dosyanın en eski sürüm kaydı olarak kalıyor.

*BOWLERA SESSION_INDEX.md — v79 (v78'den: **[25. sohbet devamı, 2026-09-05]** MOTION SYSTEM
RAPORU KAPANDI. P3 (Instagram controlled marquee) reponuzda hiçbir karşılığı olmadığı için
(grep sonucu boş — `Instagram` metnini içeren tek bir `.tsx` yok) kapsam dışı bırakıldı;
özellik ileride inşa edilirse ayrıca ele alınmalı, önkoşulu yok. Raporun P0/P1/P2 bölümündeki
9 kalemin TAMAMI mevcut kod tabanında işlendi. Kalan teknik borçlar hâlâ açık: -6 (AccountMenu
debug değeri `duration:1` production'da kaldı, kalıcı değere dönülmedi — kullanıcı kararıyla
ertelendi), -9/-10 (Page transitions/AddToCart canlı doğrulama hâlâ bildirilmedi).)*

*BOWLERA SESSION_INDEX.md — v78 (v77'den: **[25. sohbet devamı, 2026-09-05]** 400 satır eşiği
dördüncü kez aşıldı — 23. sohbet devamının (MOTION SYSTEM Mobil Tactile Düzeltmesi, ~36 satır)
tam anlatı bloğu `session_arşiv_2.md`'ye taşındı, kullanıcıya ayrı eklenti dosyası olarak
verildi. İçerik zaten #107 (KAPANDI) ve Açık Sorunlar/Motion System P0 özetinde tam
korunuyor, kayıp yok.)*

*BOWLERA SESSION_INDEX.md — v77 (v76'dan: **[25. sohbet, 2026-09-05]** P2 TAMAMEN KAPANDI:
-11 CartBadge'de 2 gerçek bug bulunup düzeltildi (0→1 mount köründü + opacity hiç
ayarlanmıyordu), -12 Customizer spatial transition hem kase hem sandviç akışına eklendi
(yan bulgu: sandviçte "Geri" butonu hiç yoktu, eklendi), -13 VisualPreview token'a bağlandı
(görsel değişiklik yok, davranış aynı). Motion System raporu artık SADECE P3 (Instagram
marquee) ve teknik borçlar (AccountMenu debug değeri, -9/-10 canlı doğrulama) hariç
tamamlandı. Genel gözlem bu oturumdan: kullanıcı testleri defalarca "gerçek dosyanın
kaydedilip kaydedilmediğini doğrula" adımını atlayınca zaman kaybına yol açtı (AccountMenu,
CartBadge) — bu artık standart ilk adım olarak yerleşti.)*

*BOWLERA SESSION_INDEX.md — v76 (v75'ten: **[24. sohbet devamı, 2026-09-04]** P1'in geri
kalanı işlendi: -6 (AccountMenu) kök nedeni çözüldü (kayıt/doğrulama sorunuymuş, kod baştan
doğruydu) ama production'da debug değeri kaldı (teknik borç, kullanıcı kararıyla ertelendi).
-7 Header Scroll kullanıcı kararıyla atlandı. -8 Hero orchestration TAMAMLANDI, `layout.tsx`
incelenip global MotionConfig'in GERÇEKTEN olmadığı doğrulandı. -9 Page transitions
(`app/template.tsx`, sadece giriş animasyonu) ve -10 AddToCart token-bağlama teslim edildi
ama canlı doğrulama bekliyor. P1 kod tarafı kapandı, kalan iş canlı doğrulamalar.)*

*BOWLERA SESSION_INDEX.md — v75 (v74'ten: **[24. sohbet, 2026-09-04]** -5a KAPANDI ✅ (kod
zaten doğruydu, sadece doğrulama gerekiyordu). Motion System P1 başladı: AccountMenu.tsx'e
AnimatePresence+spring dropdown eklendi, tokens.ts'e `springs.dropdown` VARSAYIM'ı eklendi,
kod push edildi — ama canlıda animasyon GÖRÜNMÜYOR, kök neden bulunamadı, debug sürüyor
(bkz. Açık Sorun -6). Yan bulgular: `.gitignore` eksikliği (-6a), bir file-existence
iddiasının yanlış çıkması (-6b, ders notu). Bir önceki sürüm notu aşağıda korunmuştur.)*
===
# EKLENTİ — session_arşiv_2.md sonuna eklenecek (2026-09-25, 30. sohbet kapanışı)

> Bu blok SESSION_INDEX.md'nin 400 satır eşiğini aşması nedeniyle taşındı. İçerik Kritik
> Kararlar tablosunda ve Açık Sorunlar #114/#115/#116'da hâlâ özetli olduğu için aktif takip
> gerektirmiyor — bu SADECE turn-by-turn tam anlatının arşiv kaydıdır.

---

## [TAŞINAN BLOK 1] Eski CURRENT FOCUS — 29. sohbet (2026-09-08)

**[GÜNCEL — 2026-09-08, 29. sohbet, KAPANDI]** Kategori sistemi UÇTAN UCA kodlandı VE
canlıda doğrulandı; #114'ün KÖK NEDENİ önceki turda sanılandan daha derinmiş, o da bulunup
düzeltildi. Üç ayrı iş:

1. **Kategori sistemi (YENİ #115, KAPANDI).** `categories` tablosu (id=ASCII slug/name/
   sortOrder) eklendi, `menu_items.category` buna FK (RESTRICT) ile bağlandı. Admin'e
   `/admin/categories` ekranı (liste+ekle+sil) eklendi, `MenuItemForm.tsx`'teki serbest
   metin `category` alanı sabit bir `<select>`'e çevrildi, her iki `menu-items` API
   route'u (POST+PATCH) FK ihlalini (23503) kullanıcı dostu mesaja çeviriyor. 7 başlangıç
   kategorisi (İmza Ürünler/Bowl/Dürüm/Salata Bowl/Sandviç/Tatlı/İçecek) kullanıcı kararıyla
   belirlendi. **CANLIDA DOĞRULANDI** — `/admin/categories` 7 kategoriyi doğru listeliyor.
2. **Migration uygulandı.** 8 test ürünü `DELETE FROM menu_items` ile temizlendi (kullanıcı
   onayı: gerçek ürün yoktu), `categories` 7 satırla seed edildi, FK constraint eklendi —
   hepsi Neon konsolunda ekran görüntüsüyle doğrulandı.
3. **#114'ün KÖK NEDENİ REVİZE EDİLDİ — YENİ DERS (bkz. #116).** Migration sonrası admin
   listesi hâlâ eski 8 ürünü gösterdi; `export const dynamic = 'force-dynamic'` (önceki
   turun düzeltmesi) DOĞRUYDU ama TEK BAŞINA YETERSİZ çıktı. Gerçek kök neden: Neon'un
   `neon-http` sürücüsü sorguları arka planda `fetch()` ile yapıyor, Next.js bu iç
   `fetch()` çağrılarını sayfa-seviyesi `force-dynamic`'ten TAMAMEN AYRI bir katmanda
   (Data Cache) önbelleğe alıyordu. `lib/db/client.ts`'teki `neon()` çağrısına
   `fetchOptions: { cache: 'no-store' }` eklenerek KÖKTEN çözüldü — bu merkezi dosyada
   olduğu için TÜM admin sayfalarını otomatik kapsıyor. **CANLIDA DOĞRULANDI** (ekran
   görüntüsü: "Henüz ürün yok." — DB'nin gerçek boş durumunu artık doğru yansıtıyor).

**KALAN (sıradaki oturumun işi):** (a) gerçek ürünleri admin panelden yeni kategorilerle
girmek; (b) `app/api/admin/menu-items/[id]/page.tsx`'in dolu geldiği + gerçek ImageKit
yüklemesinin uçtan uca çalıştığı hâlâ canlıda TEST EDİLMEDİ; (c) public `/menu`'nün
`menu_items`/`categories` DB'sine bağlanması (Seçenek B — ISR + on-demand `revalidatePath`,
bu sohbette kararlaştırıldı) HENÜZ KODLANMADI, `/menu` hâlâ statik `menu-data.json`
okuyor — bu bir hata DEĞİL, ayrı bir görev (bkz. Sıradaki Görevler A9).

*(Not: A9'un fiili sonucu 30. sohbette CURRENT FOCUS'a farklı çıktı — Seçenek B canlı build'de
kırıldı, Karar A'ya dönüldü. Bkz. güncel SESSION_INDEX.md CURRENT FOCUS + Açık Sorun #117/#118.)*

---

## [TAŞINAN BLOK 2] SESSION ÖZET tablosu — Session 10, 11, 12, 12 (devamı), 12 (devamı, 2026-08-09)

| Session | Tarih | Ana içerik | Durum |
|---|---|---|---|
| 10 | 2026-08-07 | ⚠️ Geriye dönük tamamlandı. `order_history` tablosu migrate edildi. #63 (npm audit) yeni. | 🟡 Devam ediyor |
| 11 | 2026-08-07 | ⚠️ Geriye dönük tamamlandı. Genel giriş/kayıt akışı netleşti (kanal bazlı tablo), #62 kapsamı genişledi ("kasa paneli" = Personel Sipariş Paneli), #64 kapandı (doğrulama durumu alanı kararı). | 🔴 Devam ediyor — #62 mimarisi bekliyor |
| 12 | 2026-08-08 | ⚠️ Retroaktif: guest-gate middleware'i zip ile doğrulandı (confidence HIGH), #65/#66 açıldı. ARCHITECTURE.md v1.7'ye güncellendi (Masaya Sipariş ayrı `/masaya-siparis/*` yüzeyine taşındı), #65 KAPANDI, #67/#68/#69 açıldı+kapandı, 400 satır eşiği tetiklendi. Masa numarası kararı: TUTULACAK, ARCHITECTURE.md v1.11'e işlendi (`CartState.tableId`, path segment route, `order_history.table_number` şema notu), #69 kapsamı genişletildi (#70 yeni açıldı). Canlı build kırığı bulunup düzeltildi (`channel-options.ts`), #71 yeni açıldı. | 🟡 §2.7b kod üretimine hazır; #70/#71 netleşmeli |
| 12 (devamı) | 2026-08-08 | 1d KAPANDI (Vercel build yeşil, kullanıcı doğruladı). #62'nin 3 mimari sorusu (personel auth, real-time, onay kuyruğu UI) kullanıcı onayıyla kapandı, ARCHITECTURE.md v1.12'ye işlendi. `users.role` için CORE.md §7.4 şema notu üretildi. `lib/db/schema.ts` diff'i + migration SQL'i üretildi, sunuldu. **Kullanıcı migration'ı Neon'da koşturdu ve Tables görünümünde `role` sütununu doğruladı.** `users.role` DB tarafı TAM kapandı — kod tarafı (`types/index.ts`/`auth.ts`/`middleware.ts`) bir sonraki tur. | 🟢 DB tamam; kod tarafı bekliyor |
| 12 (devamı, 2026-08-09) | 2026-08-09 | #70 kapandı (`order_history` şema genişletmesi: status/table_number/customer_notes, migration koşuldu+doğrulandı). `middleware.ts`'teki `/api/personel/*` guard açığı kapatıldı. #62'nin Masaya sekmesi 10 dosyayla uçtan uca kodlandı VE canlıda test siparişiyle doğrulandı (PATCH→durum makinesi→DB→polling→UI zinciri). Yol boyunca `users.role` düzeltmesi (staff'a manuel `UPDATE`) ve JWT-cache nedeniyle yeniden giriş gerekliliği yaşandı — #74 (çıkış butonu eksikliği) bu yüzden önceliği yükseltilerek tekrar gündeme geldi. | 🟢 Masaya TAMAM; Gel Al + #74 + ARCHITECTURE.md güncellemesi bekliyor |

---

*Bu eklentinin `session_arşiv_2.md`'nin sonuna eklenmesiyle taşıma tamamlanmış olur.*

------
> ⚠️ Bu dosya `session_arşiv_2.md`'nin SONUNA elle eklenmesi gereken bir EKLENTİdir — TAM dosya
> değildir, sadece bu taşımada çıkarılan iki blok. Kapanış gerekçeleri SESSION_INDEX.md'nin
> Arşiv Taşıma Kaydı tablosunda (2026-09-25, 31. sohbet satırı) özetlidir.

---

## [TAŞINDI — 2026-09-25, 31. sohbet kapanışı] BLOK 1: 30. sohbet CURRENT FOCUS tam anlatısı (A9)

**[2026-09-25, 30. sohbet, KAPANDI]** A9 (public `/menu` → DB bağlantısı) UÇTAN UCA
TAMAMLANDI, kullanıcı onayıyla ("Her şey tamam") kapatıldı. Üç ayrı iş:

1. **Kategori sekmeleri dinamikleştirildi (YENİ #117, KAPANDI).** `lib/menu-filters.ts`'teki
   sabit `CategoryTabId` union'ı (`'tumu'|'imza'|'sicak-tahil'|'vegan'|'icecek'`) KALDIRILDI —
   sekmeler artık `categories` DB tablosundan `buildCategoryTabs()` ile üretiliyor. "vegan"/
   "sicak-tahil" sanal sekmeleri (gerçek bir DB kategorisi DEĞİLDİ) `DIET_FILTERS`'a taşındı.
   `CategoryNav.tsx` artık `categories` prop'unu kabul ediyor, `MenuPageClient.tsx` bunu
   geçiriyor. Gerçek 7 kategori id'si (`bowl`/`durum`/`icecek`/`imza-urunler`/`salata-bowl`/
   `sandwic`/`tatli`) kullanıcının Neon ekran görüntüsüyle DOĞRULANDI.

2. **Cache mimarisi — ONUNCU DERS (YENİ #118, kalıcı ilke).** Önce Karar B (`unstable_cache`
   ile ISR denemesi) kodlandı, CANLI BUILD'DE KIRILDI: `DYNAMIC_SERVER_USAGE` hatası
   (`no-store fetch .../menu`, prerender hatası). Kök neden: `unstable_cache` içindeki bir
   fetch'in AÇIK `cache:'no-store'` ayarını MASKELEMİYOR — bu sarmalayıcı esas olarak fetch
   KULLANMAYAN fonksiyonlar için tasarlanmış. `neon()` sürücüsü (#116 gereği) no-store fetch
   yapmaya devam ettiği için `/menu` gerçek ISR/statik üretime bu mimariyle UYGUN DEĞİL.
   **KARAR A'ya (her istekte taze DB sorgusu, `force-dynamic`) kullanıcı onayıyla GERİ
   DÖNÜLDÜ.** 3 mutasyon route'u (`POST`/`PATCH`/`DELETE`) `revalidatePath('/menu')`
   kullanıyor — no-store nedeniyle fiilen no-op ama zararsız, gelecek-kanıtı.

3. **Teknik borç açıldı (YENİ #119).** `lib/db/queries/menu.ts` (Karar B'nin unstable_cache
   sarmalayıcısı) artık HİÇBİR yerden import edilmiyor — kullanıcı tarafından repodan
   SİLİNMELİ.

**AÇIK KALAN RİSK:** `CategoryTabButton.tsx` hâlâ hiç görülmedi, uyumluluk varsayımla kabul
edildi — detay Açık Sorun #120'de.

**KALAN:** (a) gerçek ürünleri admin panelden 7 kategoriyle girmek (A10); (b) düzenleme
formu + gerçek ImageKit yüklemesi uçtan uca canlıda TEST EDİLMEDİ (A11).

*Kapanış gerekçesi: içerik SESSION_INDEX.md'nin Kritik Kararlar tablosunda ve Açık Sorunlar
#117/#118/#119/#120 satırlarında, ayrıca GENEL DURUM'daki "Public Menü"/"Admin Panel"
satırlarında zaten tam özetli — aktif takip için turn-by-turn anlatının SESSION_INDEX.md'de
kalması gerekli değildi. A10/A11 kalan görevleri SIRADAKİ GÖREVLER tablosunda hâlâ açık,
kaybolmadı.*

---

## [TAŞINDI — 2026-09-25, 31. sohbet kapanışı] BLOK 2: v80/v81 sürüm-geçmişi notları

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
tabloya dahil edilmemesi kararı `grep` ile KODDA DOĞRULANDI.)*

*Kapanış gerekçesi: her iki not da (#108/#109/#112/#113) SESSION_INDEX.md'nin Açık
Sorunlar/Kritik Kararlar tablosunda ve GENEL DURUM'da hâlâ özetli — turn-by-turn sürüm
notunun kendisinin aktif dosyada kalması gerekli değildi. #109 bu arada (31. sohbette)
KAPANDI, #108/#112/#113'ün güncel durumu SESSION_INDEX.md'nin ilgili satırlarında görülebilir.*
---
# session_arşiv_2.md EKLENTİSİ — 2026-09-26 (32. sohbet kapanışı)

> Bu blok, SESSION_INDEX.md 400 satır eşiğini aştığı için 32. sohbet kapanışında taşındı.
> Kendi elinizle mevcut `session_arşiv_2.md` dosyanızın SONUNA ekleyin.
> İçerik Kritik Kararlar tablosunda (#109 satırı) ve Açık Sorunlar #109/A6/A7'de ve GENEL
> DURUM'da zaten tam özetlidir — bu blok sadece turn-by-turn anlatı ayrıntısıdır, aktif takip
> için gerekli değildir.

---

**[GÜNCEL — 2026-09-25, 31. sohbet, KAPANDI]** Açık Sorun #109 KAPANDI (A6 tamamlandı).
**Karar 1:** Keto filtre panelinden kaldırıldı — admin sabitlerinde hiç yoktu, gerçek veride
hiç kullanılmıyordu, kalıcı kritere dayanmadan her zaman 0 sonuç veren bir seçenek olarak
durması güven-verme ilkesine aykırıydı. **Karar 2:** "sıcak-tahıl" de kaldırıldı, `DIET_FILTERS`
artık `MENU_ITEM_TAGS`'tan TÜRETİLİYOR (allergen'lerle aynı desen) — yapısal senkron sağlandı.
Etiket görünüm senkronu: yeni `MENU_ITEM_TAG_LABELS` haritası admin formu + `MenuCardBadges.tsx`
tarafından okunuyor, eski/silinmiş id için `?? tag` fallback'i var (crash yok). 4 dosya:
`menu-item-constants.ts`, `menu-filters.ts`, `MenuItemForm.tsx`, `MenuCardBadges.tsx`.
**⚠️ A7 (#108, DESIGN_SYSTEM.md alerjen listesi 7→5 senkronu) bu turda KAPATILMADI** — kullanıcı
A6 ile birlikte kapatılmasını istedi ama bu turun değişiklikleri sadece diyet tag'lerini
kapsıyor, alerjen dokümanına hiç dokunulmadı; gerekçesiz madde düşürülmesin diye açık bırakıldı
(Self-Correction, bkz. Açık Görevler A7).
**⚠️ Dosya hacmi notu:** bu güncelleme dosyayı 425 satıra çıkarmıştı, 400 satır eşiği aşıldı.
30. sohbetin (A9) tam anlatı bloğu arşive taşındı (bkz. üst not + Arşiv Taşıma Kaydı) —
dosya artık eşiğin ALTINDA. Taşıma bloğu kullanıcıya AYRI bir dosya olarak verildi, kendi
elinizle `session_arşiv_2.md`'nin sonuna eklemeniz gerekiyor.
--------
## [TAŞINAN BLOK — 32. sohbet CURRENT FOCUS tam anlatısı, taşıma tarihi: 2026-09-26 (33. sohbet kapanışı)]

> **[GÜNCEL — 2026-09-26, 32. sohbet]** **ON BİRİNCİ DERS (#121, kalıcı ilke) + DB şema senkron
> hatası bulundu/düzeltildi.** Önceki turda (25 dosyalık sandviç→DB bağlama refactoru) `lib/db/schema.ts`'e
> eklenen `ingredients.isMikesWayDefault` ve `sandwich_sizes.priceMultiplier` (priceModifier'ın
> yerine) kodda/GitHub'da vardı, ama gerçek Neon veritabanı tablosuna HİÇ İŞLENMEMİŞTİ —
> `docs/schema-changes/` klasöründe de bu değişikliğin dosyası yoktu (CORE §7.4 notu metin olarak
> yazıldı ama dosyaya hiç düşmedi). Sonuç: `db.select().from(ingredients)` yapan 3 admin sayfası
> (liste/yeni/düzenle) "column does not exist" ile çöküyordu. **Kalıcı ilke:** `schema.ts`
> değiştirip GitHub'a push etmek, gerçek DB'nin senkron olduğu anlamına GELMEZ — `db:push`/ALTER
> AYRICA koşulmalı, aksi halde şemadaki TÜM kolonları SELECT eden her sayfa production'da aynı
> şekilde çöker. Kullanıcının Codespaces limiti dolu olduğu için terminal/CLI kullanılamadı —
> teşhis Neon SQL Editor'e yapıştırılan `information_schema.columns` sorgusuyla doğrulandı
> (kolonlar gerçekten yoktu, `sandwich_sizes` 0 satır — veri kaybı riski yoktu), düzeltme de aynı
> yerden 2 ALTER TABLE ile koşuldu: `ingredients.is_mikes_way_default boolean NOT NULL DEFAULT
> false` eklendi; `sandwich_sizes.price_modifier` DROP edilip `price_multiplier numeric(4,2)
> NOT NULL DEFAULT 1` eklendi. **Kullanıcı doğruladı: admin/ingredients çökmesi gitti.** **KALAN
> (bkz. Açık Sorun #122):** kod tarafı (pricing motoru, store, 6 step bileşeni, admin
> sandwich-sizes formu) bu turda HİÇ görülmedi/test edilmedi; `docs/schema-changes/` notu hâlâ
> dosya olarak yok (kullanıcıya soruldu, henüz yanıt gelmedi); iki tablo da gerçek beden/malzeme
> verisi içermiyor.

> Kapanış gerekçesi: içerik Kritik Kararlar tablosunda ve Açık Sorunlar #121/#122'de zaten tam
> özetli — aktif takip için gerekli değil, sadece turn-by-turn anlatı taşındı.
------
# EKLENTİ — session_arşiv_2.md'nin sonuna eklenecek
> Kaynak: SESSION_INDEX.md, 34. sohbet kapanışı (2026-09-26), Self-Correction sonrası taşıma.
> Taşınan blok: A13 teyit checkpoint'inin tam anlatısı.
> Kapanış gerekçesi: içerik SIRADAKİ GÖREVLER (A13) ve GENEL DURUM (Sandviç Akışı satırı)
> tablolarında zaten tam özetli — aktif takip için gerekli değil, sadece turn-by-turn anlatı
> taşınıyor. Bu blok normalde 33. sohbet kapanışında taşınması gerekirken (dosya o turda da
> 400 satır eşiğinin üzerindeydi, 416 satır), CORE.md §7.1 Adım 1'e aykırı biçimde 34. sohbete
> kadar taşınmadan bırakılmıştı; bu eklenti o gecikmiş taşımayı tamamlıyor.

---

**[2026-09-26, A13 teyit checkpoint'i]** Kullanıcı sandviç customize akışının 2 canlı
ekran görüntüsünü paylaştı ve A13'ü AÇIKÇA kapattı: Ekmek adımında Glutensiz Somun (+13 TL,
25 kcal)/Tam Buğday Somun (+12 TL, 150 kcal), Peynir adımında Cheddar (+58 TL, 25 kcal,
görseliyle) — gerçek ürün adı/fiyat/kalori/görsel DOĞRULANDI (bkz. SIRADAKİ GÖREVLER A13,
GENEL DURUM Sandviç Akışı satırı). **33. sohbetin tam anlatısı** (#124 — client bundle'a `db`
sızması → DATABASE_URL çökmesi; #125 — 4 adımda eksik ürün görseli; ON İKİNCİ DERS: `db`
import eden dosyadaki HERHANGİ export client component'e sızma riski taşır) daha önce arşive
taşınmıştı — özeti Kritik Kararlar #124/#125'te ve GENEL DURUM'da hâlâ tam mevcut.

------
# EKLENTİ — session_arşiv_2.md'nin sonuna eklenecek
> Kaynak: SESSION_INDEX.md, 34. sohbet kapanışı Self-Correction'ının 2. taşıma turu (2026-09-26).
> Taşınan: sürüm-geçmişi footer'ındaki v82-v87 girdileri (28.-33. sohbet).
> Kapanış gerekçesi: içeriği Açık Sorunlar #114/#115/#116/#117/#118/#119/#120/#121/#122/#123/
> #124/#125/#126'da ve Kritik Kararlar tablosunda ("33. sohbet" satırı) zaten tam özetli — aktif
> takip için gerekli değil, sadece sürüm-değişikliği anlatısı taşınıyor.

---

*BOWLERA SESSION_INDEX.md — v87 (v86'dan: **[33. sohbet, 2026-09-26]** #124 KAPANDI —
customize sayfası ilk mount'ta "DATABASE_URL eksik" hatasıyla çöküyordu, kök neden:
`lib/sandwich-catalog.ts` (db import eden) içindeki `SANDWICH_BRANCH_CONFIG` sabitini 2 client
component doğrudan import ediyor, webpack `db`'yi tarayıcı bundle'ına sızdırıyordu — sabit
`lib/sandwich-constants.ts`'e (db import etmeyen) taşınarak çözüldü. #125 KAPANDI — Ekmek/
Protein/Peynir/Sebzeler adımlarında DB'de dolu olan `item.image` hiç gösterilmiyordu, Sos
adımıyla aynı `<img>` deseni 4 bileşene eklendi. Kullanıcı canlıda 6 adımın tamamını ekran
görüntüsüyle DOĞRULADI. ON İKİNCİ DERS (kalıcı ilke) eklendi: db import eden bir dosyadaki HER
export, o dosyayı client bundle'ına sızdırma riski taşır — "saf sabit, zararsız" varsayımı
yeterli değil, gerçek bir derleme-zamanı güvenlik ağı (`server-only` paketi) YOKTU (#126, yeni
açık sorun, npm paket onayı bekliyor). GERİYE DÖNÜK KAYIT: #123 (isCatalogReady guard'ı, 32.
sohbette kodlanmış ama SESSION_INDEX'e hiç işlenmemiş) bu turda fark edilip kapalı olarak
kaydedildi. A13 durumu düşürüldü (🔴→🟡) — ekran görüntülerinde gerçek veri var GİBİ görünüyor
ama kullanıcı açıkça teyit etmedi. Dosya zaten 400 satır eşiğinin üzerindeydi (416 satır); bu
turun eklediği içerikle AYNI TURDA taşıma da yapıldı: 32. sohbetin (#121/#122) tam anlatı bloğu
`session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-26-devam2.md`).)*

*BOWLERA SESSION_INDEX.md — v86 (v85'ten: **[32. sohbet, 2026-09-26]** ON BİRİNCİ DERS + DB
şema senkron hatası bulundu/düzeltildi (#121, YENİ). Önceki turda schema.ts'e eklenen
`ingredients.isMikesWayDefault`/`sandwich_sizes.priceMultiplier` GitHub'a push edilmişti ama
gerçek Neon DB'sine hiç işlenmemişti — admin `ingredients` sayfaları (liste/yeni/düzenle) bu
yüzden çöküyordu. Kullanıcının Codespaces limiti dolu olduğu için CLI kullanılamadı; teşhis +
düzeltme Neon SQL Editor'den 2 ALTER TABLE ile yapıldı, kullanıcı çökmenin gittiğini doğruladı.
**KAPANMADI (#122, YENİ):** kod tarafı (pricing motoru/store/6 step/Mike's Way preseti) hiç
canlı test edilmedi, iki tablo da gerçek veri içermiyor, `docs/schema-changes/` notu hâlâ dosya
olarak yok. A12/A13/A14 SIRADAKİ GÖREVLER'e eklendi. Bu güncelleme dosyayı 400 satır eşiğinin
üzerine çıkardığı için AYNI TURDA taşıma da yapıldı: 31. sohbetin (A6/#109) tam anlatı bloğu
`session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-26.md`).)*

*BOWLERA SESSION_INDEX.md — v85 (v84'ten: **[31. sohbet, 2026-09-25]** Açık Sorun #109 KAPANDI,
A6 tamamlandı — Keto filtre panelinden kaldırıldı, "sıcak-tahıl" kaldırıldı, `DIET_FILTERS`
artık `MENU_ITEM_TAGS`'tan türetiliyor (yapısal senkron), `MENU_ITEM_TAG_LABELS` etiket görünüm
haritası eklendi (4 dosya: `menu-item-constants.ts`/`menu-filters.ts`/`MenuItemForm.tsx`/
`MenuCardBadges.tsx`). **A7 (#108) BİLİNÇLİ OLARAK KAPATILMADI** — kullanıcının isteğine rağmen
bu turun kapsamı dışında kaldığı için Self-Correction ile açık bırakıldı, gerekçe CURRENT
FOCUS'ta. Bu güncelleme dosyayı 400 satır eşiğinin üzerine (425) çıkardığı için AYNI TURDA
taşıma da yapıldı: 30. sohbetin (A9) tam anlatı bloğu `session_arşiv_2.md`'ye taşındı (eklenti:
`session_arsiv_2_EKLENTI_2026-09-25-devam2.md`), dosya eşiğin altına indi.)*

*BOWLERA SESSION_INDEX.md — v84 (v83'ten: **[30. sohbet, 2026-09-25]** A9 KAPANDI — detay
CURRENT FOCUS'ta. Özet: kategori sekmeleri dinamikleşti (#117), Karar B build'de kırıldı,
ONUNCU DERS olarak kalıcı ilkeye işlendi (#118), Karar A'ya dönüldü. #119/#120 açık kaldı.
Eski CURRENT FOCUS + Session 10-12 anlatıları 400 satır eşiği için arşive taşındı (eklenti:
`session_arsiv_2_EKLENTI_2026-09-25.md`).)*

*BOWLERA SESSION_INDEX.md — v83 (v82'den: **[29. sohbet, 2026-09-08]** KATEGORİ SİSTEMİ +
GERÇEK KÖK NEDEN BULUNDU. #115 KAPANDI: `categories` tablosu (FK ile `menu_items.category`'ye
bağlı, RESTRICT) + admin CRUD ekranı + form/API validasyonu uçtan uca kodlanıp deploy edildi,
7 kategori seed edildi, 8 test ürünü kullanıcı onayıyla temizlendi — hepsi CANLIDA DOĞRULANDI.
#114 KAPANDI ama kök neden REVİZE EDİLDİ: 28. sohbetteki `force-dynamic` fix'i doğruydu ama
TEK BAŞINA YETERSİZDİ — asıl sorun Neon `neon-http` sürücüsünün iç `fetch()` çağrılarının
Next.js Data Cache'inde önbelleğe alınmasıydı, `lib/db/client.ts`'e `fetchOptions:
{cache:'no-store'}` eklenerek KÖKTEN çözüldü (YENİ #116, kalıcı ilke olarak loglandı — bkz.
DOKUZUNCU DERS). Bu turda 4 eski "checkpoint" ders bloğu (DÖRDÜNCÜ-YEDİNCİ) 400 satır eşiği
yeniden aşıldığı için arşive taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-08.md`).)*

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

---

## Ayrıca taşınan Açık Sorunlar satırları (kısaltıldı, tam metin)

**#50 [BU TURDA KAPANDI]** `AddToCartButton.tsx` görüldü, BSC-6 (çift ekleme race condition)
doğrudan ele alındı ve seçim-kimliği bazlı kilitle çözüldü — bkz. #75.
(`components/customizer/AddToCartButton.tsx`)

**#124/#125 [KAPANDI, 33. sohbet]** Customize sayfası ilk mount'ta "DATABASE_URL eksik"
hatasıyla çöküyordu — `lib/sandwich-catalog.ts` (`db` import eden, server-only) içindeki
`SANDWICH_BRANCH_CONFIG` sabitini 2 client component doğrudan import ediyordu, webpack `db`'yi
de tarayıcı bundle'ına dahil ediyordu. Sabit `lib/sandwich-constants.ts`'e (db import etmeyen)
taşınarak çözüldü — kullanıcı canlıda tüm 6 adımı ekran görüntüsüyle test etti, çökme gitti.
Ayrıca Ekmek/Protein/Peynir/Sebzeler adımlarında DB'de zaten dolu olan `ingredients.image` hiç
render edilmiyordu — 5 adım bileşeninden sadece Sos adımı `<img>` basıyordu. Aynı desen 4
bileşene eklendi ("Peynirsiz" sentetik seçeneği BSC-5 gereği görselsiz bırakıldı, "Boy" adımı
şema gereği zaten görselsiz — kasıtlı). Kullanıcı canlıda doğruladı.
(`lib/sandwich-catalog.ts`, `lib/sandwich-constants.ts`, `store/useSandwichStore.ts`,
`components/sandwich/StepBread.tsx`, `StepProtein.tsx`, `StepCheese.tsx`, `StepVeggies.tsx`,
`StepSauceToastExtras.tsx`)
-----
## EKLENTİ — 2026-09-26, 35. sohbet kapanışı (devam6)

> Bu blok `session_arşiv_2.md`'nin SONUNA eklenir. SESSION_INDEX.md 400 satır eşiğini
> aştığı için CORE.md §7.1 Adım 1 gereği taşınan içerik.

---

### 1. Eski TAŞIMA NOTU zinciri (2026-09-24 / 2026-09-25) — pointer'a indirildi

**Kapanış gerekçesi:** Bu notlar zaten kendi taşıma turlarında arşive tam metinle işlenmişti
(`session_arsiv_2_EKLENTI_2026-09-24.md`, `..._2026-09-25.md`, `..._2026-09-25-devam2.md`).
SESSION_INDEX.md üzerinde kalan metin sadece tekrar eden bir pointer'dı, aktif takip için
gerekli değildi.

- **[TAŞIMA NOTU, 2026-09-24, 30. sohbet kapanışı]** SESSION_INDEX.md 499 satıra ulaşınca 5 eski
  üst-not bloğu (21./22. sohbet TAŞIMA NOTU'ları, İKİNCİ/ÜÇÜNCÜ DERS, 13. sohbet devamı TAŞIMA
  NOTU'su), 2 eski CURRENT FOCUS anlatısı (27./28. sohbet), SESSION ÖZET Session 0-9 satırları,
  6 KAPANDI ✅ açık-sorun satırının tam anlatısı (#85/#93/#96/#101/#112/#113) ve en eski 5
  sürüm-geçmişi notu (v75-v79) `session_arsiv_2_EKLENTI_2026-09-24.md` olarak arşive taşındı.
- **[TAŞIMA NOTU, 2026-09-25, 30. sohbet kapanışı]** 400 satır eşiği yeniden aşıldığı için eski
  CURRENT FOCUS (29. sohbet) + Session 10-12 anlatıları arşive taşındı
  (`session_arsiv_2_EKLENTI_2026-09-25.md`).
- **[TAŞIMA NOTU, 2026-09-25, 31. sohbet kapanışı]** 400 satır eşiği üçüncü kez aynı gün aşıldığı
  için eski CURRENT FOCUS (30. sohbet, A9 tam anlatısı) arşive taşındı
  (`session_arsiv_2_EKLENTI_2026-09-25-devam2.md`).
- **Geçmiş ihlal kaydı (2026-07-20):** Gerekçesiz satır silme ihlali — "400 satır eşiği" kuralının
  doğduğu olay. Kalıcı ders kaydı AGENT.md VERSİYON GEÇMİŞİ'nde (Session 4) duruyor, etkilenmedi.
- **[DÖRDÜNCÜ-YEDİNCİ DERS, 2026-09-08]** "Checkpoint sık sorulmalı, sohbet aniden kesilebilir"
  temalı 4 ders bloğu (2026-08-07→08-09) zaten daha önce arşive taşınmıştı.

---

### 2. 34. sohbetin CURRENT FOCUS tam anlatısı — Bowl DB bağlama (#127/#128)

**Kapanış gerekçesi:** 35. sohbette bu konu üzerine yeni gelişme oldu (yeni build hatası bulundu
ve düzeltildi, #129) — eski anlatı artık CURRENT FOCUS'ta güncel değil, ama Açık Sorunlar
(#127 ✅, #128 hâlâ 🔴) ve Kritik Kararlar tablosunda tam özetli olduğu için aktif takip
gerektirmiyor.

> **[GÜNCEL — 2026-09-26, 34. sohbet — Bowl akışı DB'ye bağlandı, BLOKAJ bulundu]** Sandviç
> akışında kullanılan desen (`ingredients` tablosu + server component catalog fetch +
> `setCatalog()`) Bowl ("Kâseni Yarat") tarafına da uygulandı — #127 KAPANDI. Kapsam genişledi:
> `app/menu/customize/[id]/page.tsx` server component'e çevrilince client mantığı
> (Zustand/framer-motion/Sepete Ekle) yeni bir dosyaya (`components/customizer/BowlCustomizer.tsx`)
> taşındı — bu, ilk onaylanan dosya planında YOKTU, Self-Correction ile şeffafça bildirildi ve
> kullanıcı onayı sonrası eklendi (SandwichCustomizer.tsx ile birebir aynı mimari). Ölü kod
> `lib/customizer-data.ts` SİLİNDİ — yeni zorunlu `isAlwaysPaid` alanını karşılamadığı için
> build'i kırıyordu (kimse import etmiyordu, temiz silme). Kullanıcı `npm run build`'i yeşile
> aldı, GitHub'a push etti.
> **BLOKAJ (YENİ, #128, 🔴):** Ana sayfadaki (`Hero.tsx`) "Kaseni Oluştur"/"Sandviçini Oluştur"
> butonları sabit `build-your-own-kasem`/`build-your-own-sandwich` id'lerine gidiyor — bu id'ler
> `menu_items` tablosuna HİÇ GİRİLMEMİŞTİ (bu durum aslında #126/26. sohbette ZATEN NOT
> EDİLMİŞTİ — "build-your-own-kasem DAHİL EDİLMEDİ, grep ile doğrulandı" — ama o zaman kod tarafı
> henüz DB'ye bağlı olmadığı için sorun fiilen tetiklenmiyordu). Bowl DB'ye bağlanınca ilk kez
> gerçek 404 olarak ortaya çıktı. Ayrıca admin `menu-items` POST route'u id'yi HER ZAMAN
> `slugify(isim)+"-"+rastgele5harf` ile ürettiği için (`app/api/admin/menu-items/route.ts`), admin
> panelinden bu sabit id'ler ELLE GİRİLEMEZ — kalıcı çözüm ya Hero.tsx'in linkini kullanıcının
> oluşturduğu GERÇEK id'ye göre güncellemek (hızlı) ya da admin formuna manuel id alanı eklemek
> (ayrı karar/tur, Kural #5). **KALAN, sohbet burada kesildi:** kullanıcı admin'den "Kendi Kasem"
> ürününü oluşturuyor, gerçek üretilen id henüz paylaşılmadı — paylaşılınca Hero.tsx güncellenip
> test edilmeli. Sandviç tarafı için de AYNI sorun muhtemelen geçerli (`build-your-own-sandwich`
> id'sinin `menu_items`'da var olup olmadığı bu turda TEYİT EDİLMEDİ).

---

### 3. SELF-CORRECTION notu (2026-09-26, 34. sohbetin kapanışı düzeltildi, 2 turda)

**Kapanış gerekçesi:** Bu düzeltme fiilen uygulandı ve dosyanın o zamanki hâline işlendi
(465 satıra indi). Artık sadece tarihi bir kayıt; sonraki turlarda (35. sohbet) yeni taşımalar
zaten üstüne bindiği için ayrıca aktif takip gerektirmiyor.

> ⚠️ **SELF-CORRECTION (2026-09-26, 34. sohbetin kapanışı düzeltildi, 2 turda):** Önceki turda bu
> dosya 400 satır eşiğinin üzerinde ("HENÜZ YAPILMADI" notuyla) TESLİM EDİLMİŞTİ — CORE.md §7.1
> Adım 1 Madde 3'ün ("taşıma AYNI TURDA yapılır, biri verilip diğeri sonraya bırakılamaz") açık
> bir ihlaliydi; "BLOKAJ önceliği" bu adımı atlamak için geçerli bir gerekçe değildir. Bu turda 2
> taşıma yapıldı: (1) 33. sohbetin artık-eski A13 checkpoint anlatısı `session_arşiv_2.md`'ye
> taşındı (eklenti: `..._EKLENTI_2026-09-26-devam4.md`) — SIRADAKİ GÖREVLER A13/GENEL DURUM'da
> zaten özetli; (2) sürüm-geçmişi footer'ındaki v82-v87 (28.-33. sohbet, #114-#126) + Açık
> Sorunlar'daki 3 zaten-Kritik-Kararlar'da-özetli satır (#50, #124, #125) da taşındı/kısaltıldı
> (eklenti: `..._EKLENTI_2026-09-26-devam5.md`). Dosya 528→465 satıra indi.

---

### 4. Sürüm-geçmişi tam metinleri — v88, v89, v90

**Kapanış gerekçesi:** Her biri sonraki sürümde ("v89'dan", "v90'dan", "v91'den") özetlenip
üstüne yeni sürüm eklendiği için artık en güncel sürüm değil; içerikleri Açık Sorunlar
(#99, #107-#127) ve Kritik Kararlar/GENEL DURUM tablolarında zaten tam özetli.

*BOWLERA SESSION_INDEX.md — v88 (v87'den: **[bu turda, 2026-09-26]** A13 KAPANDI — kullanıcı
2 canlı ekran görüntüsüyle sandviç customize akışında gerçek beden/malzeme/fiyat verisini AÇIKÇA
teyit etti ("A13 kapandı"): Ekmek adımında Glutensiz Somun (+13 TL/25 kcal) ve Tam Buğday Somun
(+12 TL/150 kcal), Peynir adımında Cheddar (+58 TL/25 kcal, görseliyle). SIRADAKİ GÖREVLER ve
GENEL DURUM Sandviç Akışı satırı güncellendi.)*

*BOWLERA SESSION_INDEX.md — v89 (v88'den: **[bu turda, 2026-09-26]** #99 KAPANDI —
sandviç checkout blokajı artık yok, kullanıcı 3 canlı ekran görüntüsüyle doğruladı: sepet
("Özel Sandviç" 156₺) → Gel Al/Nakit → "Siparişi Onayla" hatasız tamamlandı (156₺/174 kcal) →
sipariş personel paneline (Gel Al sekmesi, Onay Bekleyen) doğru malzeme detaylarıyla düştü.
Kök neden kesin belirlenmedi — muhtemelen 33. sohbetteki #124/#125 düzeltmelerinin yan etkisi.)*

*BOWLERA SESSION_INDEX.md — v90 (v89'dan: **[34. sohbet, 2026-09-26]** #127 KAPANDI — Bowl
("Kâseni Yarat") akışı sandviçteki AYNI desenle DB'ye bağlandı (14 dosya: `lib/bowl-catalog.ts`
yeni, `types/index.ts`/`lib/customizer-pricing.ts`/`store/useCustomizerStore.ts` değişti, 8
customizer bileşeni store'dan okuyacak şekilde güncellendi, `app/api/orders/gel-al/route.ts`
BSC-3 için `buildBowlCatalog()` çağırıyor). Onaylı plana 1 ekleme yapıldı ve Self-Correction ile
bildirildi: `components/customizer/BowlCustomizer.tsx` (yeni). Ölü kod `lib/customizer-data.ts`
build'i kırdığı için SİLİNDİ. Kullanıcı `npm run build`'i yeşile aldı, push etti. **YENİ BLOKAJ
(#128, 🔴):** `Hero.tsx`'teki "Kaseni Oluştur" CTA'sı `menu_items`'da hiç var olmayan sabit bir
id'ye (`build-your-own-kasem`) gidiyor.)*

---

*(Bu eklentiyi mevcut `session_arşiv_2.md` dosyanızın en sonuna, kendi elinizle ekleyin —
AGENT.md Kural gereği arşiv dosyası burada tam olarak yeniden üretilmez.)*
------
## EKLENTİ — 2026-09-26 (35. sohbet devamı, devam7)
> `session_arşiv_2.md`'nin SONUNA eklenecek blok. Bu dosyanın kendisi arşivin yerine geçmez,
> sadece SESSION_INDEX.md'den bu turda çıkarılan pointer/versiyon metinlerinin TAM halini taşır.

### 1) Konsolide edilen 9 tekil TAŞINDI pointer'ı (SESSION_INDEX.md CURRENT FOCUS'tan çıkarıldı)

> **[TAŞINDI — 2026-09-26, bu turda (35. sohbet)]** 34. sohbetin (#127 Bowl DB bağlama) tam
> CURRENT FOCUS anlatısı `session_arşiv_2.md`'ye taşındı (eklenti:
> `session_arsiv_2_EKLENTI_2026-09-26-devam6.md`) — içerik Açık Sorunlar #127/#128 ve GENEL
> DURUM'da zaten tam özetli, aktif takip için gerekli değil.
>
> **[TAŞINDI — 2026-09-26, bu turda]** A13 teyit checkpoint'inin tam anlatısı (kullanıcının 2
> canlı ekran görüntüsüyle Ekmek/Peynir adımlarındaki gerçek fiyat/kalori/görseli doğrulaması)
> `session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-26-devam4.md`) —
> içerik SIRADAKİ GÖREVLER A13 ve GENEL DURUM Sandviç Akışı satırında zaten tam özetli. **KALAN
> (değişmedi):** `docs/schema-changes/` notu hâlâ dosya olarak yok (#121); `server-only` paketi
> kurulumu kullanıcı onayı bekliyor (A15/#126); sandviç sipariş verme ucu (Sepete Ekle→checkout)
> hâlâ hiç canlı test edilmedi.
>
> **[TAŞINDI — 2026-09-26, 33. sohbet kapanışı]** 32. sohbetin (ON BİRİNCİ DERS #121 + DB şema
> senkron hatası #121/#122 tam anlatısı) tam anlatı bloğu `session_arşiv_2.md`'ye taşındı
> (eklenti: `session_arsiv_2_EKLENTI_2026-09-26-devam2.md`) — içerik Kritik Kararlar/#121/#122
> ve GENEL DURUM'da zaten tam özetli, aktif takip için gerekli değil. Dosya zaten 400 satır
> eşiğinin üzerindeydi (416 satır), bu turun eklediği içerikle taşıma AYNI TURDA yapıldı.
>
> **[TAŞINDI — 2026-09-26, 32. sohbet kapanışı]** 31. sohbetin (A6/#109 tam anlatısı: Keto/
> "sıcak-tahıl" filtre kaldırma kararları, `DIET_FILTERS` türetme refactoru, A7'nin bilinçli açık
> bırakılma gerekçesi) tam anlatı bloğu `session_arşiv_2.md`'ye taşındı (eklenti:
> `session_arsiv_2_EKLENTI_2026-09-26.md`) — içerik Kritik Kararlar/#109/A6/A7 ve GENEL DURUM'da
> zaten tam özetli, aktif takip için gerekli değil.
>
> **[TAŞINDI — 2026-09-25, 31. sohbet kapanışı]** 30. sohbetin (A9 tam anlatısı: kategori sekmeleri
> #117, cache mimarisi ONUNCU DERS #118, teknik borç #119, açık risk #120) tam anlatı bloğu
> `session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-25-devam2.md`) —
> içerik Kritik Kararlar/#117/#118/#119/#120 ve GENEL DURUM'daki "Public Menü"/"Admin Panel"
> satırlarında zaten tam özetli, aktif takip için gerekli değil. **KALAN görevler A10/A11 olarak
> SIRADAKİ GÖREVLER'de hâlâ açık duruyor, kaybolmadı.**
>
> **[TAŞINDI — 2026-09-25]** 29. sohbetin (kategori sistemi #115 + #114 kök neden revizyonu #116)
> tam anlatı bloğu `session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-25.md`)
> — içerik Kritik Kararlar/#115/#116/GENEL DURUM'da zaten tam özetli, aktif takip için gerekli değil.
>
> **[TAŞINDI — 2026-09-24]** 28. sohbet (ilk gerçek admin kullanıcı testi, cache bug keşfi) ve
> 27. sohbet (Admin Panel canlıya alınışı) tam anlatı blokları `session_arşiv_2.md`'ye
> taşındı — içerik #110-#114 ve GENEL DURUM'da zaten tam özetli, aktif takip için gerekli değil.
>
> **[TAŞINDI — 2026-09-07, 400 satır eşiği beşinci kez aşıldı]** 26. sohbetin (Admin Panel
> planlaması) tam anlatı bloğu `session_arşiv_2.md`'ye taşındı (eklenti:
> `session_arsiv_2_EKLENTI_2026-09-07.md`). Kapanış gerekçesi: içerik Kritik Kararlar
> tablosunda ve Açık Sorunlar #108-#113'te zaten tam özetli — aktif takip için gerekli değil.

### 2) v92'nin tam versiyon-geçmişi paragrafı (SESSION_INDEX.md footer'ından çıkarıldı)

*BOWLERA SESSION_INDEX.md — v92 (v91'den: **[35. sohbet devamı, 2026-09-26 — SELF-CORRECTION]**
v91'in kapanış paragrafı kendi içinde çelişkiliydi: CURRENT FOCUS ve GENEL DURUM/Bowl Akışı
satırı #128/A16'yı KAPANDI olarak işlerken, bu footer paragrafı hâlâ "#128/A16 HÂLÂ AÇIK" diye
yazıyordu — footer, CURRENT FOCUS'a kapanış notu eklenirken senkronize edilmemişti. Bu turda
SADECE bu footer metni düzeltildi, başka hiçbir tabloya/karara dokunulmadı. Gerçek/güncel durum
(v91'in geri kalanıyla aynı): #127 (Bowl DB-bağlama) + #129 (`EXTRA_OPTIONS`'ın `image` alanı
eksikliğinden doğan build hatası — düzeltme SADECE `types/index.ts`, `image?: string` opsiyonel
yapıldı, diğer 6 dosyaya dokunulmadı) + #128 (Hero.tsx "Kaseni Oluştur" `href`'i gerçek
`fekafel-bowl-hb0fc` id'sine güncellendi) — ÜÇÜ DE KAPANDI. Kullanıcı `#129` sonrası akışı GERÇEK
ürün id'siyle doğrudan test etti, çalıştığını onayladı; Hero.tsx değişikliği ise henüz push/
build/canlı doğrulanmadı (A16, 🟠, kapanmış görev ama canlı teyidi bekliyor). Yeni A17 (🟢):
`image` opsiyonel olduğu için render tarafındaki `undefined` davranışı doğrulanmalı. Yeni A18
(🟡): sandviç tarafındaki `build-your-own-sandwich` id'sinin `menu_items`'da var olup olmadığı
hâlâ teyitsiz — varsa aynı 404 riski orada da mevcut.)*
## EKLENTİ — 2026-09-26 (35. sohbet devamı, devam8)
> `session_arşiv_2.md`'nin SONUNA eklenecek blok (devam7'den SONRA). Bu dosya arşivin yerine
> geçmez, SESSION_INDEX.md'nin footer'ından bu turda kısaltılan v94 versiyon paragrafının TAM
> halini taşır.

### v94'ün tam versiyon-geçmişi paragrafı (SESSION_INDEX.md footer'ından çıkarıldı)

*BOWLERA SESSION_INDEX.md — v94 (v93'ten: **[35. sohbet devamı, 2026-09-26]** A12 KAPANDI —
kullanıcı admin `ingredients` sayfalarını (liste/yeni/düzenle, Mike's Way checkbox'ının sadece
sandwich+veggies/sauce'ta göründüğü) canlıda test etti, sorun bildirmedi (#122 KAPANDI). Kapanış
kullanıcının kısa sözlü onayına dayanıyor — A13'teki gibi ekran görüntüsü paylaşılmadı, bu SIRADAKİ
GÖREVLER A12 satırına ve Kritik Kararlar'daki ilgili satıra not olarak işlendi. Başka hiçbir
tabloya/karara dokunulmadı.)*
----
# EKLENTİ — 2026-09-27 (36. sohbet açılışı, SESSION_INDEX.md 400 satır eşiği aşımı nedeniyle taşındı)

> Bu blok, SESSION_INDEX.md'nin 35. sohbet (2./3. kez devamları) CURRENT FOCUS anlatısının TAM
> metnidir (CORE.md §7.1 Adım 1 gereği özetlenmeden taşındı). Kapanış gerekçesi: içeriğin tamamı
> Açık Sorunlar (#128 KAPANDI, #129 KAPANDI, #131 kısmen KAPANDI, #91 KAPANDI, A12 KAPANDI),
> Kritik Kararlar tablosu ve GENEL DURUM'da hâlâ tam özetli — aktif takip için bu turn-by-turn
> anlatının SESSION_INDEX.md'de durmasına gerek yoktu, sadece pointer bırakıldı.

> **[GÜNCEL — 2026-09-26, 35. sohbet devamı (2. kez)]** Kullanıcı canlı ekran görüntüleriyle
> (menüdeki ürünlerde sepete ekleme yok, ürün detay sayfası açılıp sos/içecek/ekstra satışı
> istendi) yeni bir özellik talep etti: Bowl/Dürüm/Salata Bowl kategorisindeki HAZIR ürünlere,
> Kâseni Oluştur/Sandviçini Oluştur customizer akışlarına HİÇ dokunmadan, opsiyonel çoklu
> sos (signature flavor havuzu)/içecek/tatlı seçimli tam ekran "Sepete Ekle" akışı eklendi.
> **[KARAR BİLDİRİMİ onaylandı, 5 dosya üretildi]:** `types/index.ts` (`CartItem`'a izole
> `quickAddSelection` alanı — `customization`/`sandwichCustomization` ile AYNI izolasyon
> deseni), `app/menu/page.tsx` (`buildBowlCatalog()` ile signature flavor'lar server-side
> çekiliyor), `components/menu/MenuPageClient.tsx` (kategori adı eşleştirme + `QuickAddSheet`
> state'i + `useCartStore` bağlantısı), `components/menu/MenuCard.tsx` (yeni "Sepete Ekle"
> butonu, "Özelleştir" ile KARŞILIKLI DIŞLAYICI), yeni `components/menu/QuickAddSheet.tsx`.
> **[SELF-CORRECTION, bu turda]:** Kategori eşleştirmesi için gerçek `categories.id` slug
> değerleri sohbette hiç teyit edilmemişti (Kural #1 gereği tahmin edilmedi) — SESSION_INDEX.md
> bu dosyanın KENDİSİNDE, #115 kaydında ("7 kategori: İmza Ürünler/Bowl/Dürüm/Salata Bowl/
> Sandviç/Tatlı/İçecek seed edildi") zaten yazılıydı, bu turda fark edildi. Bu yüzden eşleştirme
> id DEĞİL, `categories.name` (DB'de gösterilen Türkçe ad) üzerinden yapıldı — hem #115'teki
> gerçek seed verisiyle birebir örtüşüyor hem de slug hiç bilinmeden çalışıyor. **KALAN:**
> kullanıcı 5 dosyayı repoya uygulayıp build/push/canlı doğrulamalı; ayrıca CartDrawer/checkout/
> personel paneli bu yeni `quickAddSelection` alanını HENÜZ okumuyor (fiyat/kalori toplamı
> doğru yansır, sadece "hangi sos/içecek/tatlı" ayrı satır olarak GÖRÜNMÜYOR) — bkz. A19/#131.
>
> **[GÜNCEL — 2026-09-26, 35. sohbet devamı]** #2/#57 PARKLANDI: kullanıcı `/online-siparis`
> sayfasının sanal POS (ödeme ağ geçidi) entegrasyonu olmadan tamamlanamayacağını belirtti —
> dış bağımlılık (banka/ödeme kuruluşu sözleşmesi/API anahtarı gerekiyor), bu turda kod
> üretilmedi. Hangi sanal POS sağlayıcısının kullanılacağı kararı hâlâ kullanıcıdan bekleniyor.
>
> **[GÜNCEL — 2026-09-26, 35. sohbet devamı]** #91 KAPANDI: kullanıcı canlıda hem role-revocation
> 403'ü hem rate-limit'i test etti — 5'ten fazla yanlış şifre denemesinde sistem girişi bir süre
> bekletiyor (geçici cooldown). Kısa sözlü onay, ekran görüntüsü yok.
>
> **[GÜNCEL — 2026-09-26, 35. sohbet devamı]** A12 KAPANDI: kullanıcı admin `ingredients`
> sayfalarını (liste/yeni/düzenle + Mike's Way checkbox mantığı) canlıda test etti, sorun
> bildirmedi (#122 KAPANDI). **Not:** kısa sözlü onay — A13'teki gibi ekran görüntüsü/adım adım
> detay yok, kapanış buna dayanıyor.
>
> **[GÜNCEL — 2026-09-26, 35. sohbet — build hatası düzeltildi, Bowl akışı canlıda ÇALIŞIYOR,
> #128/A16 HÂLÂ AÇIK]** #127'nin (34. sohbet) push'undan sonra YENİ bir build hatası çıktı:
> `EXTRA_OPTIONS` sabiti (avokado/sos/çıtırlık — DB'den değil, kod içinde sabit) `image` alanı
> taşımıyordu, ama #127'de eklenen katalog tipi bu alanı artık HERKES için zorunlu kılıyordu.
> Düzeltme: SADECE `types/index.ts` değişti — `image` alanı `carbs`/`fat` ile aynı desende
> **opsiyonel** yapıldı (`image?: string`), böylece hem DB'den gelen malzemeler hem kod-içi sabit
> ekstra'lar aynı tipe uyuyor. Diğer 6 dosyaya (`bowl-catalog.ts` + 5 `Step*.tsx`) DOKUNULMADI —
> önceki turda onaylanan/üretilen halleri geçerliliğini koruyor. #129 olarak KAPANDI (bkz. Açık
> Sorunlar). Kullanıcı bunu pushladı ve customize sayfasına **GERÇEK ürün id'siyle DOĞRUDAN
> giderek** (Hero.tsx CTA'sı ÜZERİNDEN DEĞİL) test etti — "Kaseni Oluştur" akışı çalışıyor onayı
> geldi.
> **#128/A16 KAPANDI (aynı turda):** Kullanıcı admin'den `fekafel-bowl-hb0fc` id'li ("Felafel
> bowl"/"Kendi kasem") gerçek ürünü buldu, `Hero.tsx` paylaşıldı, "Kaseni Oluştur" `href`'i bu
> gerçek id'ye güncellendi (dosyanın kendi niyet yorumuna da işlendi). **Not (#130, 🟢, kozmetik):**
> ürünün DB'deki `name`'i "Felafel bowl" — customizer başlığında bu isim görünecek, "Kendi kasem"
> beklentisiyle uyuşmuyor, admin panelden rename edilebilir. **Hâlâ TEYİT EDİLMEDİ:** Sandviç
> tarafındaki `build-your-own-sandwich` id'sinin `menu_items`'da var olup olmadığı — `Hero.tsx`'e
> bu turda BİLEREK dokunulmadı (Kural #5, tek dosya/tek değişiklik onayı sadece Kaseni Oluştur
> içindi).
>
> **[SELF-CORRECTION — 2026-09-26, bu turda (35. sohbet devamı)]** Dosyanın en altındaki versiyon
> notu (v91 footer) bu CURRENT FOCUS'taki #128/A16 kapanışıyla çelişiyordu — footer hâlâ "HÂLÂ
> AÇIK" yazıyordu. SADECE bu footer metni düzeltildi (v92), başka bir tablo/karar değişmedi.
>
> ⚠️ **TAŞIMA NOTU (2026-09-26, bu turda — 35. sohbet devamı, KONSOLİDE):** 26-34. sohbet
> kapanışlarındaki tekil TAŞINDI pointer'larının (26/27/28/29/30/31/32/33/34. sohbet + A13
> checkpoint'i — Admin Panel planlaması, kategori sistemi #115/#116, A9 #117-120, A6/A7 #109,
> #121/#122 DB şema senkronu, A13 sandviç fiyat/kalori doğrulaması, #127 Bowl DB bağlama) TAM
> metni zaten kendi eklenti dosyalarında (`session_arsiv_2_EKLENTI_2026-09-07.md`,
> `-2026-09-25.md`, `-2026-09-25-devam2.md`, `-2026-09-26.md`, `-2026-09-26-devam2.md`,
> `-2026-09-26-devam4.md`, `-2026-09-26-devam6.md`) arşivde duruyordu — buradaki tekil pointer'lar
> bu turda TEK bir konsolide pointer'a indirildi (yeni eklenti: `session_arsiv_2_EKLENTI_2026-09-26-devam7.md`,
> aşağıdaki bloğun kendisi). Hiçbiri aktif takip için gerekli değildi; hepsi Açık Sorunlar/Kritik
> Kararlar/GENEL DURUM'da ve SIRADAKİ GÖREVLER'de (A9/A10/A11/A13 dahil) hâlâ tam özetli — içerik
> kaybı yok, sadece pointer metni sıkıştırıldı (§7.1 Adım 1.5).
-----
## [36. sohbet, 2026-09-27] CURRENT FOCUS — tam anlatı (37. sohbette SESSION_INDEX.md'den taşındı)

> **[GÜNCEL — 2026-09-27, 36. sohbet]** Kullanıcının bildirdiği 2 sorun çözüldü: **Sorun 1**
> (İçecek/Tatlı kategorilerinde "Sepete Ekle" yoktu) — kullanıcı kararıyla kapsam genişletildi:
> `MenuPageClient.tsx`'te kategoriler BUNDLE (Bowl/Dürüm/Salata Bowl/**+Sandviç**, gerçek
> `signatureFlavors`/`drinkItems`/`dessertItems` ile `QuickAddSheet` açılır) ve STANDALONE
> (İçecek/Tatlı, AYNI `QuickAddSheet` boş dizilerle açılır — yeni bileşen YAZILMADI, mevcut şart
> zaten destekliyordu) olarak ikiye ayrıldı. **Sorun 2** ("Sipariş Onayla" → "fiyatlandırılamadı"
> hatası) — kod incelemesiyle KESİN kök neden bulundu: `app/api/orders/gel-al/route.ts`'teki
> `priceItem()` hazır ürün fiyatını hâlâ statik `lib/menu-data.json`'dan okuyordu, ama `/menu`
> artık DB `menu_items`'tan besleniyordu (#117) — sadece DB'de var olan ürünler (ör. "Kendi
> kasem") bu yüzden fiyatlandırılamıyordu. AYRICA `quickAddSelection` alanı bu fonksiyonda hiç
> tanınmıyordu. **Düzeltme (4 dosya, KARAR BİLDİRİMİ onaylı):** yeni `lib/menu-items-catalog.ts`
> (`bowl-catalog.ts`/`sandwich-catalog.ts` ile AYNI desende DB'den `menu_items` Map'i çeker),
> `route.ts` (fiyatlandırma DB'ye taşındı + `quickAddSelection` için sunucu-taraflı yeniden
> hesaplama dalı — BSC-3 — + `selectionSummary`'e ayrı satır, #131(a) KAPANDI),
> `ConfirmPickupOrderButton.tsx` (incelerken bulunan AYRI bir eksik: sepet payload'ı
> `quickAddSelection`'ı sunucuya hiç göndermiyordu — route düzeltmesi bu olmadan işe yaramazdı,
> aynı turda kapatıldı). **Build hatası ve düzeltmesi:** ilk deploy'da
> `Module '"@/types"' has no exported member 'QuickAddSelection'` hatası çıktı — `types/index.ts`
> dosyasının kendisinde bu tip ZATEN doğru export edilmiş haldeydi (dosya bu turda tekrar
> paylaşılıp doğrulandı), yani dosyanın İÇERİĞİ hatalı değildi. **Kesin sebep TEYİT EDİLMEDİ**
> (Kural #1) — en olası açıklama, bu dosyanın ilk push'ta gerçek repoya gitmemiş olması; kullanıcı
> tekrar push edip **deploy'u yeşile aldı**, ayrıca bir kök neden araştırması YAPILMADI. Bkz.
> #132/#133.

**Kapanış gerekçesi (37. sohbet):** Bu anlatının teşhis ettiği #131(a) düzeltmesi (`needsBowlCatalog`
kontrolü) 37. sohbette kullanıcının paylaştığı repo zip'i üzerinden KOD SEVİYESİNDE teyit edildi —
zaten yaşıyordu. İçerik Açık Sorunlar #131/#132/#133 satırlarında ve GENEL DURUM → Checkout
satırında hâlâ tam özetli, aktif takip için bu tam anlatı gerekli değil.

## TAŞIMA BLOĞU — 2026-09-27 (400 satır eşiği beşinci kez aşıldı, bu turda)

> Bu blok `SESSION_INDEX.md`'nin CURRENT FOCUS bölümünden, 400 satır eşiği aşıldığı için
> taşındı (CORE.md §7.1 Adım 1). Kullanıcı bu dosyayı kendi eliyle `session_arşiv_3.md`'nin
> SONUNA ekleyecek. Kapanış gerekçesi: içerik Açık Sorunlar #134 (KAPANDI), #135 (P0-1/P0-4
> KAPANDI) ve GENEL DURUM → Checkout/Veritabanı satırlarında zaten tam özetli — aktif takip
> için gerekli değil, içerik kaybı yok. Taşınan 4 paragraf: 38. sohbet (#135/#134 çifte kapanış),
> "bu turda devamı" (#136 seçenek a + #135/1 kodlama), "bu turda" (repo zip reconciliation),
> 37. sohbet (Quick-Add "ilk sos ücretsiz" özelliği #134).

> **[GÜNCEL — 38. sohbet]** İki madde kapandı. **#135 P0-1 (verificationStatus) TAM KAPANDI:**
> kullanıcı Codespaces kullanamadığı için (mobilde, dosyaları manuel push etti, deploy yeşil)
> `npm test` yerine doğrudan canlıda test etti — onaysız hesapla "Siparişi Onayla" denendiğinde
> "Hesabınız henüz onaylanmadı, lütfen şubeyle iletişime geçin" mesajıyla 403 engellendi (ekran
> görüntüsü); aynı hesap personel panelinden onaylandıktan sonra tekrar denendi, sipariş
> başarıyla tamamlandı (ekran görüntüsü). Her iki yön de doğrulandı. `route.test.ts` hâlâ hiç
> koşulmadı — test borcu olarak açık kaldı, kapanışı bloklamıyor. **#134 (Quick-Add ilk sos
> ücretsiz) KAPANDI:** kullanıcı push/build/canlı doğrulamayı kısa sözlü onayladı ("#134
> onaylandı kapat") — ekran görüntüsü paylaşılmadı, A12 tipi bir kapanış. A21 buna göre ✅
> işaretlendi. **Kapı hâlâ AÇIK:** #135 P0 madde 3 (admin ikinci yetki, `requireAdminSession()`
> yok) ve 4 (DB CHECK/enum constraint yok) hiç kodlanmadı — "admin ikinci yetki"nin tam kapsamı
> (hangi işlem için ikinci onay isteniyor) kullanıcıdan netleştirme bekliyor. #136 (numara
> çakışması) da hâlâ karar bekliyor.
>
> **[GÜNCEL — bu turda, devamı]** Kullanıcı "sen karar ver, devam et" dedi. Claude #136 için
> seçenek (a)'yı seçti (PayTR callback yorumlarındaki çakışan numaralara dokunulmadı) ve öncelik
> sırasına göre (1→2→3→4→5) sıradaki tam-açık P0 maddesi olan **#135/1'i (verificationStatus)
> kodladı**: `route.ts`'e DB'den taze okunan `verificationStatus==="confirmed"` kontrolü eklendi
> (403 fail-closed, JWT'ye güvenilmedi — personel onayı session'a anında yansımayabilir).
> `route.test.ts` (bu route'un İLK test dosyası, 5 senaryo: session yok/telefon yok/kullanıcı
> yok/pending/confirmed) yazıldı. **ÇALIŞTIRILMADI** (bu ortamda `node_modules` yok) — kullanıcı
> kendi ortamında `npm test` koşup teyit etmeli, ayrıca canlıda/Codespaces'te onaysız hesapla
> gerçek bir sipariş denemesiyle 403'ün GÖZLE doğrulanması gerekiyor. **Kapı hâlâ AÇIK:** P0
> madde 3 (admin ikinci yetki) ve 4 (DB constraint) kod yazılmamış — bkz. A22.
>
> **[GÜNCEL — bu turda]** Kullanıcı "#135 (canlıya çıkış listesi) üzerinde çalışıyorduk ama
> sanırım session'a kaydetmedik" dedi. Repo zip'i indirilip kod satır satır incelendi (sadece
> analiz — hiç kod YAZILMADI bu turda). Sonuç: #135 kaydı GERÇEKTEN stale'miş — madde 5/5b zaten
> kodlanmış, madde 7 (PayTR) ayrı bir oturumda büyük ölçüde çözülmüş ama numarası çakışıyor (yeni
> #136). #135 satırı ve SIRADAKİ GÖREVLER (yeni A22) buna göre güncellendi — bkz. aşağıdaki #135/#136
> satırları ve A22. **Kapı hâlâ AÇIK:** P0 madde 1/3/4 kod yazılmamış durumda, production'a
> çıkılmamalı.
>
> **[GÜNCEL — 2026-09-27, 37. sohbet]** Kullanıcı repoyu (zip) paylaştı — 36. sohbette teşhis
> edilen `needsBowlCatalog` düzeltmesinin (quickAddSelection.signatureFlavorIds kontrolü) fiilen
> repoda YAŞADIĞI kod üzerinden TEYİT EDİLDİ (#131(a) kapanışı doğrulandı, ayrı kanıt gerekmedi).
> Bunun üstüne YENİ bir özellik istendi ve kodlandı: **Quick-Add sos seçiminde ilk (seçim
> SIRASINA göre) sos ücretsiz, sonrakiler tam fiyatına.** Kullanıcı 3 soruyla kapsamı netleştirdi:
> (1) kapsam Quick-Add + Customizer Signature Flavor adımı — ama Customizer TEK seçimli kaldığı
> için kural orada davranışı DEĞİŞTİRMİYOR (zaten seçilen tek sos vardı), fiilen SADECE Quick-Add'i
> etkiliyor; (2) "ilk" = kullanıcının TIKLADIĞI sıra (dizideki index 0); (3) tüm Quick-Add
> ürünlerinde geçerli. Kod incelemesiyle `signatureFlavorIds`'in zaten sıralı bir dizi olduğu
> (`toggle()` seçilince sona ekliyor/kaldırılınca filtreliyor) görüldü — **şema değişikliği
> GEREKMEDİ**. 2 dosya güncellendi: `app/api/orders/gel-al/route.ts` (`priceQuickAddSelection`
> → `priceFlavorSelection`/`priceMenuItemSelection`'a bölündü, Kural #5 — ilk sos ücretsiz mantığı
> SADECE `priceFlavorSelection`'da), `components/menu/QuickAddSheet.tsx` (canlı fiyat/kalori
> hesaplaması `computeQuickAddTotals`'a taşındı + AYRICA bir bug düzeltildi: eski kod
> `signatureFlavors.filter()` kullanıyordu — bu, "ilk seçilen"i KATALOG sırasına göre yanlış
> belirlerdi, `selectedFlavorIds.map()`'e çevrildi; "Ücretsiz" rozeti + açıklayıcı metin eklendi).
> Kalori hiçbir zaman ücretsiz sayılmadı (CORE.md §9). **KALAN:** kullanıcı bu 2 dosyayı henüz
> push/build/canlı doğrulamadı; `priceFlavorSelection`/`computeQuickAddTotals` için test seti
> YOK (kullanıcıya soruldu, henüz yanıt yok) — bkz. yeni #134/A21.
>
> ⚠️ **TAŞIMA NOTU (2026-09-27, bu turda — 36. sohbet):** 35. sohbetin (2./3. kez devamları)
> CURRENT FOCUS anlatısı (QuickAddSheet KARAR BİLDİRİMİ detayı, #2/#57 park, #91/A12 kapanışları,
> #127/#129/#128/A16 build-hatası-ve-düzeltme anlatısı, footer self-correction, konsolide taşıma
> notu) TAM metniyle `session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-27.md`,
> ayrı dosya olarak üretildi, kullanıcı kendi eliyle arşiv dosyasının sonuna ekleyecek). ⚠️
> **DÜZELTME (bu turda, arşiv bölünmesi sonrası):** İçerik tarih olarak 2026-09-03 sonrasına
> ait olduğu için artık `session_arşiv_3.md`'nin sonuna eklenmeli, `session_arşiv_2.md`'nin
> değil — eklenti dosyasının adı değişmedi. Kapanış gerekçesi: hepsi Açık Sorunlar #128/#129/#131
> (KAPANDI/kısmen kapandı), Kritik Kararlar ve GENEL DURUM'da hâlâ tam özetli — aktif takip
> için gerekli değil, içerik kaybı yok.

## TAŞIMA BLOĞU — 2026-09-27 (400 satır eşiği altıncı kez aşıldı, bu turda — versiyon geçmişi sıkıştırması)

> Bu blok `SESSION_INDEX.md`'nin footer'ındaki VERSİYON GEÇMİŞİ'nden taşındı (CORE.md §7.1
> Adım 1). Kullanıcı bu dosyayı kendi eliyle `session_arşiv_3.md`'nin SONUNA ekleyecek.
> Taşınan 3 versiyon paragrafı: v101 (#136 seçenek a + #135/1 kodlama), v100 (repo zip
> reconciliation, #135/#136 kaydı güncellendi), v99 (37. sohbet — Quick-Add "ilk sos ücretsiz"
> #134 özelliği). Kapanış gerekçesi: üçü de Açık Sorunlar #134/#135/#136 satırlarında ve
> GENEL DURUM'da zaten tam özetli — aktif takip için gerekli değil, içerik kaybı yok. Bu,
> SESSION_INDEX.md'deki mevcut "v95 TAŞINDI/KISALTILDI" pointer'ının devamı niteliğinde
> (aynı desen, bir sonraki 3 versiyonu kapsıyor).

*BOWLERA SESSION_INDEX.md — v101 (v100'den: **[bu turda]** Kullanıcı "sen karar ver, devam et"
dedi. #136 için seçenek (a) seçildi (kod yorumları değişmedi). Öncelik sırasına göre #135/1
(verificationStatus) KODLANDI: `app/api/orders/gel-al/route.ts`'e DB-taze `verificationStatus
==="confirmed"` kontrolü (403 fail-closed) eklendi, dosya başı niyet yorumu güncellendi.
`route.test.ts` (bu route'un İLK testi, 5 senaryo) yazıldı ama ÇALIŞTIRILMADI (node_modules yoktu).
#135 satırındaki madde (1) ve A22 buna göre güncellendi. P0 madde 3/4 hâlâ açık. Başka hiçbir
tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v100 (v99'dan: **[bu turda, repo zip'i üzerinden #135 reconciliation]**
Kullanıcı "#135'i çözüyorduk ama session'a kaydetmedik" dedi — repo kodu satır satır incelenip
GERÇEK durum teyit edildi. #135 kaydı GÜNCELLENDİ (önceki "KOD YOK" kaydı STALE çıktı): madde 5/5b
zaten `route.ts`'e kodlanmış (`#135/5`/`#135/5b` kod imzalarıyla teyitli); madde 7 (PayTR callback
güvenliği) BÜYÜK ÖLÇÜDE ayrı, kaydedilmemiş bir oturumda çözülmüş ama `#110`/`#115`/`#116`
numaralarıyla anılıyor — bu numaralar SESSION_INDEX'te ZATEN başka konulara atanmıştı, **YENİ #136
(numara çakışması) açıldı**, kullanıcı kararı bekliyor. Madde 6 (`Hero.test.tsx`) kod karşılaştırmasıyla
KESİN KIRIK bulundu (test eski href `build-your-own-kasem` bekliyor, kod #128'den beri
`fekafel-bowl-hb0fc` kullanıyor) — kök neden teyitli. Madde 1/3/4 hâlâ hiç kodlanmamış, teyitli.
Madde 8 sadece Masaya akışında merkezi, Gel Al'da değil. Madde 9/10 hiç başlamamış. **YENİ A22**
eklendi (gate hâlâ açık, 3 P0 maddesi bekliyor). Başka hiçbir tabloya/karara dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v99 (v98'den: **[37. sohbet, 2026-09-27]** Kullanıcı repo zip'i
paylaştı — 36. sohbetin `needsBowlCatalog` düzeltmesi kod üzerinden TEYİT EDİLDİ (#131(a) hâlâ
yaşıyor). Yeni özellik: Quick-Add sos seçiminde ilk (seçim sırasına göre) sos ücretsiz, sonrakiler
tam fiyat (#134) — kullanıcı 3 soruyla kapsamı/"ilk"in tanımını/geçerli ürünleri netleştirdi.
`signatureFlavorIds`'in zaten sıralı dizi olduğu görülüp **şema değişikliği GEREKMEDİĞİ** teyit
edildi. 2 dosya güncellendi: `route.ts` (`priceQuickAddSelection` → `priceFlavorSelection`/
`priceMenuItemSelection`'a bölündü, Kural #5), `QuickAddSheet.tsx` (`computeQuickAddTotals`'a
bölündü + ayrı bir bug düzeltildi: istemci "ilk seçilen"i katalog sırasına göre yanlış
belirliyordu, seçim sırasına çevrildi). Kalite 5/5, Güvenlik 8/8. A19 değişmedi, **A21 eklendi**
(push/build/canlı doğrulama + test seti kararı bekliyor). **400 satır eşiği aşılmadan önce**
36. sohbetin CURRENT FOCUS anlatısı `session_arşiv_3.md`'ye taşındı (eklenti:
`session_arsiv_2_EKLENTI_2026-09-27-devam2.md`, ayrı dosya olarak verildi — kullanıcı arşivin
sonuna kendi eklemeli). Başka hiçbir tabloya/karara dokunulmadı.)*

## TAŞIMA BLOĞU — 2026-09-27 (400 satır eşiği, bu turda — SIRADAKİ GÖREVLER kapanmış satırları)

> Bu blok `SESSION_INDEX.md`'nin SIRADAKİ GÖREVLER tablosundan taşındı (CORE.md §7.1 Adım 1).
> Kullanıcı bu dosyayı kendi eliyle `session_arşiv_3.md`'nin SONUNA ekleyecek. Taşınan 20 satırın
> HEPSİ ✅ (KAPANDI/TAMAMLANDI) durumundaydı: A21, A12, A13, A9, A6, 91, 99, 23, 24, 25, 27, 28, 29,
> 30, 31, -13, -3, -1, 0, 0b. Açık/bekleyen (🟠🟡🟢🔴⚪) hiçbir satır taşınmadı. Kapanış gerekçesi:
> hepsi Açık Sorunlar/Kritik Kararlar/GENEL DURUM'da zaten özetli, içerik kaybı yok.

| Sıra | Görev | Öncelik |
|---|---|---|
| A21 | **[KAPANDI, 38. sohbet ✅]** Quick-Add "ilk sos ücretsiz" özelliği (#134) — `route.ts` + `QuickAddSheet.tsx` kodlandı, kullanıcı push/build/canlı doğrulamayı onayladı ("#134 onaylandı kapat"). **Not:** kapanış kısa sözlü onaya dayanıyor, ekran görüntüsü paylaşılmadı. Test seti (`priceFlavorSelection`/`computeQuickAddTotals`) hâlâ yazılmadı — ayrı, düşük öncelikli borç. | ✅ |
| A12 | **[KAPANDI, bu turda ✅]** Admin `ingredients` sayfaları (liste/yeni/düzenle) canlıda test edildi, kullanıcı sorun bildirmedi (#122 KAPANDI). **Not:** kapanış kullanıcının kısa sözlü onayına dayanıyor, ekran görüntüsü/detay paylaşılmadı — A13'teki gibi görsel kanıt yok. | ✅ |
| A13 | **[KAPANDI, bu turda ✅]** `sandwich_sizes` + sandviç `ingredients` tablolarına gerçek beden/malzeme/fiyat verisi girildi — kullanıcı 2 canlı ekran görüntüsüyle AÇIKÇA teyit etti ("A13 kapandı"): Ekmek adımında Glutensiz Somun (+13 TL/25 kcal)/Tam Buğday Somun (+12 TL/150 kcal), Peynir adımında Cheddar (+58 TL/25 kcal, görseliyle). | ✅ |
| A9 | **[TAMAMLANDI, 30. sohbet ✅]** Public `/menu` sayfası `menu_items`/`categories` DB'sine bağlandı — Karar A (her istekte taze sorgu, `force-dynamic` + `revalidatePath`), kategori sekmeleri dinamik. Kullanıcı onayıyla canlı build doğrulandı. | ✅ |
| A6 | **[TAMAMLANDI, 31. sohbet ✅]** `/menu` canlı filtre ekranındaki Keto/sıcak-tahıl tag uyuşmazlığı — Keto kaldırıldı, `DIET_FILTERS` admin sabitlerinden türetilir hale getirildi, tag label senkronu eklendi (#109 KAPANDI). | ✅ |
| 91 | **[KAPANDI, bu turda ✅]** Güvenlik denetimi (#91) — canlıda GÖZLE doğrulandı: role-revocation 403 + rate-limit (5'ten fazla yanlış şifrede geçici bekletme) ikisi de çalışıyor | ✅ |
| 99 | **[KAPANDI, bu turda ✅]** #99 Sandviç checkout blokajı — canlıda 3 ekran görüntüsüyle doğrulandı, artık bloklu değil (kök neden kesin bilinmiyor, muhtemelen #124/#125 yan etkisi) | ✅ |
| 23 | [TAMAMLANDI] `types/index.ts` görüldü, #68 (RegistrationChannel/FulfillmentChannel tip etkisi) netleşti ve kodlandı | ✅ |
| 24 | [TAMAMLANDI] Vercel build yeşil doğrulandı (1d) | ✅ |
| 25 | [TAMAMLANDI] #62'nin 3 mimari sorusu kapandı — ARCHITECTURE.md v1.12 | ✅ |
| 27 | [TAMAMLANDI, önceki tur] `users.role` migration'ı Neon'da koşuldu, `role text` sütunu Tables görünümünde doğrulandı | ✅ |
| 28 | [TAMAMLANDI, önceki tur] #70 kapandı — `order_history.table_number`/`status`/`customer_notes` migration'ı Neon'da koşuldu ve doğrulandı | ✅ |
| 29 | [TAMAMLANDI, önceki tur] #62 Masaya sekmesi (10 dosya) uçtan uca kodlandı, build+deploy yeşil, canlıda gerçek test siparişiyle doğrulandı | ✅ |
| 30 | [TAMAMLANDI, önceki tur] #89 IP delili + engellenen deneme logu — 4 dosya kodlandı, migration Neon'da koşuldu+6 sorguyla doğrulandı, test 6/6 PASS (Codespaces), Vercel deploy yeşil | ✅ |
| 31 | [TAMAMLANDI, 26. sohbet] `menu_items` tablosu migration+seed Neon'da koşuldu ve doğrulandı (13 kolon, 8 satır) | ✅ |
| -13 | **[TAMAMLANDI, 25. sohbet, 2026-09-05 ✅]** Motion System rapor P2 — VisualPreview Layer entrance. Kod ZATEN vardı, sadece hardcoded değerler yerine merkezi `durations.visualPreviewLayer`+`easings.easeOut` token'larına bağlandı. Görsel değişiklik YOK. | ✅ |
| -3 | **[KAPANDI, bu turda ✅]** #91 — Güvenlik denetimi SEC-01/SEC-02 kod+test+build+tsc TAMAM, canlıda (a) role-revocation 403, (b) rate-limit (5'ten fazla yanlış şifrede geçici bekletme) ikisi de doğrulandı. | ✅ |
| -1 | **[TAMAMLANDI ✅]** #84 — isim gösterme sorunu kullanıcı tarafından canlıda doğrulandı. | ✅ |
| 0 | **[TAMAMLANDI ✅]** #83 — "Sıfırla" → üretilen geçici kodla giriş canlıda BAŞARILI test edildi. | ✅ |
| 0b | **[TAMAMLANDI ✅]** #82 — orijinal kayıt şifresiyle çıkış→giriş döngüsü canlıda BAŞARILI test edildi. | ✅ |

## TAŞIMA BLOĞU — 2026-09-27 (400 satır eşiği, bu turda — CURRENT FOCUS + versiyon geçmişi)

> `SESSION_INDEX.md`'den taşındı (CORE.md §7.1 Adım 1). Kullanıcı bu dosyayı `session_arşiv_3.md`'nin
> SONUNA kendi eliyle ekleyecek. İçerik: (1) CURRENT FOCUS'tan 2 kapanmış paragraf (#138 ödeme
> sağlayıcısı netleştirmesi; #135 madde 4 DB constraint kapanışı), (2) v102-v105 versiyon paragrafları.
> Hepsi Açık Sorunlar #135/#136/#138, A22 ve GENEL DURUM'da zaten özetli — içerik kaybı yok.

> **[GÜNCEL — bu turda]** Kullanıcı önemli bir netleştirme yaptı: **PayTR kesin değil** —
> Iyzico gibi başka bir sağlayıcı da değerlendiriliyor, karar henüz verilmedi. Bu, `#135`
> madde 2 (refund race condition) ve madde 7'yi (PayTR callback güvenliği) doğrudan etkiliyor:
> madde 7 TAMAMEN PayTR'a özel (webhook imza formatı/API sözleşmesi sağlayıcıya göre değişir),
> madde 2'nin DB `WHERE` koruma kısmı sağlayıcıdan BAĞIMSIZ (genel iyi pratik, kalıcı) ama
> "PayTR'a çift istek gitmeme" (gerçek idempotency-key) kısmı sağlayıcıya özel. **Karar:**
> sağlayıcı netleşmeden madde 2/7'nin sağlayıcıya-özel kısımlarına daha fazla efor
> harcanmayacak (atılabilir iş riski) — **YENİ #137** açıldı, madde 2/7 "sağlayıcı bekliyor"
> etiketiyle bekletiliyor. Ayrıca kullanıcı, ChatGPT'nin ayrı/dış bir değerlendirmesini
> (10 maddelik kendi numaralandırmasıyla, 8,4→8,5 puan) paylaştı — bu SESSION_INDEX'e dışarıdan
> gelen, teyitsiz bir kaynak olarak not edildi, kendi `#135` P0/P1/P2 sıramızla birebir
> eşleşmiyor. `#135` madde 4 (DB CHECK constraint) kullanıcı tarafından ayrıca sözlü teyit
> edildi (zaten önceki turda kapanmıştı, ek işlem gerekmedi).

> **[GÜNCEL — bu turda]** #135 P0 madde 4 (DB CHECK/enum constraint yok) **TAM KAPANDI.**
> Kullanıcı `20260927_users_role_verification_status_check_eklendi.md` şema notundaki
> migration'ı Neon SQL Editor'de koştu ve iki sorgu çıktısını paylaştı: (1) ön-adım
> `SELECT DISTINCT role FROM users` → sadece `admin`/`customer` (constraint kapsamında,
> `staff` yok ama sorun değil); (2) migration sonrası `pg_constraint` doğrulaması →
> `chk_users_role` (`role IN ('customer','staff','admin')`) ve
> `chk_users_verification_status` (`verification_status IN ('pending','confirmed')`)
> ikisi de tanımlarıyla döndü. İkinci `ALTER TABLE`'ın hatasız geçmesi, `verification_status`
> sütununda da constraint dışı bir değer olmadığını dolaylı olarak kanıtladığı için ayrıca
> `SELECT DISTINCT verification_status` çıktısı istenmedi. Kod tarafı (`lib/db/schema.ts`
> yorumları) zaten önceki turda güncellenmişti — bu turda SADECE SQL migration'ı fiilen
> koşuldu ve doğrulandı. **Kapı artık SADECE #135 P0 madde 3'e (admin ikinci yetki,
> `requireAdminSession()` yok) bağlı** — kapsamı (hangi işlem için ikinci onay isteniyor)
> hâlâ kullanıcıdan netleştirme bekliyor. #136 (numara çakışması) da hâlâ karar bekliyor.


*BOWLERA SESSION_INDEX.md — v105 (v104'ten: **[bu turda]** Kullanıcı önemli bir netleştirme
yaptı: PayTR KESİN DEĞİL — Iyzico gibi başka bir sağlayıcı da değerlendiriliyor, karar henüz
verilmedi. **YENİ #138** açıldı (`#137` bilinçli olarak ATLANDI — `#136`'nın (b) seçeneği
ileride `#137+` ile yeniden numaralandırma öneriyor, çakışma önlendi). `#135` madde 2 (refund
race condition) ve madde 7 (PayTR callback güvenliği) `#138`'e çapraz referanslandı — DB `WHERE`
koruması (madde 2, sağlayıcıdan bağımsız kısım) kalıcı kabul edildi, ama PayTR'a özel idempotency-
key (madde 2) ve TÜM madde 7 sağlayıcı netleşene kadar beklemede işaretlendi. SIRADAKİ GÖREVLER
satır 2 (#57, online ödeme) ile çapraz referans eklendi. Kullanıcı ayrıca ChatGPT'den gelen dış/
teyitsiz bir değerlendirmeyi (10 maddelik kendi numaralandırması, 8,4→8,5 puan) paylaştı — bu
CURRENT FOCUS'a not düşüldü, kendi `#135` sıramızı DEĞİŞTİRMEDİ. `#135` madde 4 kullanıcı
tarafından ayrıca sözlü teyit edildi (zaten kapalıydı, ek işlem gerekmedi). Başka hiçbir tabloya
dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v104 (v103'ten: **[bu turda]** Dosya 400 satır eşiğini beşinci kez
aştı (479 satır). CORE.md §7.1 Adım 1 gereği CURRENT FOCUS'taki 4 kapanmış paragraf (38. sohbet
#135/#134 çifte kapanış, "bu turda devamı" #136+#135/1, "bu turda" repo zip reconciliation, 37.
sohbet Quick-Add ilk-sos-ücretsiz) TAM metniyle `session_arşiv_3.md`'ye taşındı (eklenti:
`session_arsiv_2_EKLENTI_2026-09-27-devam3.md`, ayrı dosya olarak üretildi, kullanıcı kendi
eliyle arşiv dosyasının sonuna ekleyecek). Yerine tek bir TAŞIMA NOTU pointer'ı bırakıldı. Arşiv
Taşıma Kaydı tablosuna yeni satır eklendi. Kapanış gerekçesi: hepsi Açık Sorunlar #134/#135 ve
GENEL DURUM'da zaten tam özetli, içerik kaybı yok. **Not:** taşımadan sonra dosya hâlâ ~415-424
satır civarında — 400 eşiğinin tam altına inmek için ayrı, daha büyük bir sıkıştırma turu (örn.
kapanmış SIRADAKİ GÖREVLER maddelerinin taşınması) gerekebilir, kullanıcı isterse bir sonraki
turda yapılabilir. Başka hiçbir tabloya/karara dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v103 (v102'den: **[bu turda]** Kullanıcı checkpoint onayı verdi
("evet, kurallara göre güncelle"). #135 P0 madde 4 (DB CHECK/enum constraint yok) **TAM
KAPANDI**: Neon SQL Editor'de `chk_users_role`+`chk_users_verification_status` migration'ı
koşuldu, ön-adım (`SELECT DISTINCT role`) ve doğrulama (`pg_constraint`) sorgu çıktıları
kullanıcı tarafından paylaşıldı, ikisi de teyitli. #135 satırı, A22, CURRENT FOCUS ve GENEL
DURUM/Veritabanı satırı buna göre güncellendi. **Kapı artık SADECE madde 3'e (admin ikinci
yetki) bağlı** — kapsamı hâlâ netleşmedi. Başka hiçbir tabloya/karara dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v102 (v101'den: **[38. sohbet]** Kullanıcı canlıda iki testi bizzat
koştu ve sonuçlarını ekran görüntüsüyle paylaştı (Codespaces/`npm test` yerine — mobilde
çalışıyor, dosyaları manuel push etti, deploy yeşil). Sonuç 1: onaysız hesapla sipariş denemesi
→ 403 + "Hesabınız henüz onaylanmadı" mesajı doğrulandı. Sonuç 2: aynı hesap onaylandıktan sonra
sipariş başarıyla tamamlandı. Bu ikisi ile **#135 P0-1 TAM KAPANDI**, A22 buna göre güncellendi
(`route.test.ts` hâlâ koşulmadı, borç olarak kaydedildi). Ayrıca kullanıcı **#134'ü onaylayıp
kapattı** ("#134 onaylandı kapat") — #134 satırı, A21, GENEL DURUM/Checkout ve GENEL DURUM/Hızlı
Sepete Ekle satırları buna göre ✅ işaretlendi (kısa sözlü onay, ekran görüntüsü yok — A12 tipi
kapanış). Başka hiçbir tabloya/karara dokunulmadı. P0 madde 3/4 ve #136 hâlâ açık.)*
-------------
# TAŞIMA BLOĞU — 2026-09-30 (9. taşıma) — `session_arşiv_3.md`'nin SONUNA EKLE

> Bu dosya SADECE YENİ EKLEMEDİR (CORE.md §7.1 Adım 1.4): `session_arşiv_3.md` yeniden üretilmedi, bu metin dosyanın sonuna elle eklenir.
> Taşınan içerik TAM ve DEĞİŞTİRİLMEMİŞ metindir; her madde için kapanış gerekçesi aşağıdadır. Kaynak: SESSION_INDEX.md v117 kopyası (406 satır).

## 1) Eski CURRENT FOCUS paragrafları (önceki oturumlar)

**Kapanış gerekçeleri:**
- #63 paragrafı: #63 KAPANDI; kalan iş Açık Sorunlar #141-#144 ve SIRADAKİ 4b'de.
- Menü mobil filtre + görsel paragrafı: #139 KAPANDI (bu arşive taşındı); #140 açık satırı duruyor, Kâseni Oluştur ebat talebi A25'te.
- #135 P0 madde 3 paragrafı: #135 satırı P0 kapanışlarını taşıyor. Buradaki 'Step-up onay ayrı, opsiyonel iş olarak parklandı' kararı kaybolmasın diye SIRADAKİ GÖREVLER'e yeni A26 satırı olarak alındı.
- #135 madde 6 paragrafı: #135 satırı (madde 6, Hero.test.tsx kod düzeltildi/koşulmadı) taşıyor.
- #135 madde 10 / #60 paragrafları (devamı 2 ve 3): #135 satırı madde 10'u, #60 satırı (bu arşivde) ve A11 kapanışı özetliyor. Kaynak dosyada 'devamı 2' cümlesi 'bakıyor,' ile yarım kalmıştı; olduğu gibi taşındı.

**Taşınan TAM metin:**

> **[GÜNCELLENDİ — bu turda, #63 KAPANDI]** Next 15.5.26 + React 19 yükseltmesi `main`'e alındı ve canlıda doğrulandı (Production `31e1701`). Dependabot PR #2 kapatıldı. Kalan iş: #141 (Vitest `vite` eksik, onay bekliyor), #142 (next-auth yama bekleniyor), #143 (drizzle, kod arandı, düşük risk), #144 (`legacy-peer-deps`, PostCSS/nanoid, dal koruması).

> **[GÜNCEL — bu turda, menü mobil filtre + görsel]** #139 KAPANDI (mobil filtre bağlantısı + QuickAddSheet görsel düzeltmesi, canlıda 3 madde doğrulandı — detay Açık Sorunlar #139'da). **[BU TURDA, devamı]** Sandviç adımlarında malzeme görseli büyütüldü + lazy-load eklendi (#140), canlı doğrulama bekliyor; Kâseni Oluştur akışında aynısı istendi ama dosyalar henüz paylaşılmadı.

> **[GÜNCEL — bu turda]** #135 P0 madde 3 **TAM KAPANDI.** Kullanıcı önerimi (sadece route-level guard, step-up onay YOK)
> kabul etti. `lib/auth/require-admin.ts` + `/api/admin/*` altındaki 17 handler'a guard eklendi, kullanıcı push edip canlıda
> doğruladı: admin paneli çalışıyor, girişsiz istek 401. **P0 kod maddeleri artık kapalı;** kalan kapı: madde 2 sağlayıcı kısmı
> (#138), P1 madde 6 (`Hero.test.tsx`) ve 8. Step-up onay (kritik işlemde şifre yeniden girişi) ayrı, opsiyonel iş olarak parklandı.
>
> **[GÜNCEL — bu turda, devamı]** #135 madde 6 (`Hero.test.tsx`) KOD DÜZELTİLDİ, KOŞULMADI: sorun `href` + buton etiketi
> ("Kâseni Yarat"→"Kaseni Oluştur") + eksik "Sandviçini Oluştur" CTA'sıydı. Vitest koşulamadı (Codespaces yok) — test borcu.
>
> **[GÜNCEL — bu turda, devamı 2]** #135 madde 10 KISMEN KODLANDI: `upload-image` artık gerçek dosya imzasına (magic bytes) bakıyor,
> **[GÜNCEL — bu turda, devamı 3]** #60 KAPANDI (Neon şifre reset, Vercel otomatik rotasyon, redeploy, `/menu` OK). #135 madde 10 CANLIDA DOĞRULANDI: SVG yükleme reddedildi ("Sadece JPEG, PNG, WebP veya GIF..."), mevcut görsel değişmedi; normal JPG yükleme çalıştı. A11 KAPANDI. Açık: Ayran kalori/protein geçici (A10), vitest hâlâ koşulmadı. SVG reddediliyor (stored-XSS). Push/canlı yükleme testi + vitest bekliyor. Audit log/action log/rate-limit yapılmadı (şema gerektirir).

## 2) Eski TAŞIMA NOTU / TAŞINDI pointer paragrafları (CURRENT FOCUS içindeydi)

**Kapanış gerekçesi (hepsi için):** Bu paragraflar başka arşiv eklentilerine işaret eden işaretçilerdi; her birinin karşılığı 'Arşiv Taşıma Kaydı' tablosunda satır olarak duruyor (2026-08-23, 2026-08-23 22. sohbet 2. taşıma, 2026-09-03, 2026-09-05, 2026-09-27 sekizinci taşıma, 2026-09-27 beşinci eşik aşımı). Bilgi kaybı yok, tekrar kaldırıldı.

**Taşınan TAM metin:**

> ⚠️ **TAŞIMA NOTU (2026-09-27, bu turda):** #138 (ödeme sağlayıcısı belirsiz) ve #135 madde 4 (DB CHECK
> constraint kapanışı) CURRENT FOCUS paragraflarının TAM metni `session_arşiv_3.md`'ye taşınacak eklentide:
> `session_arsiv_2_EKLENTI_2026-09-27-devam6.md`. Özet: PayTR kesin değil (#138), madde 2/7'nin sağlayıcıya-özel
> kısmı bekliyor; madde 4 Neon'da doğrulandı. Detay Açık Sorunlar #135/#138'de.

> ⚠️ **TAŞIMA NOTU (2026-09-27, bu turda — 400 satır eşiği beşinci kez aşıldı):** 38. sohbet
> (#135 P0-1/#134 çifte kapanış), "bu turda devamı" (#136 seçenek a + #135/1 kodlama), "bu turda"
> (repo zip reconciliation) ve 37. sohbet (Quick-Add "ilk sos ücretsiz" #134) paragraflarının
> TAM metni `session_arşiv_3.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-27-devam3.md`,
> ayrı dosya olarak üretildi, kullanıcı kendi eliyle arşiv dosyasının sonuna ekleyecek). Kapanış
> gerekçesi: hepsi Açık Sorunlar #134 (KAPANDI), #135 (P0-1/P0-4 KAPANDI) ve GENEL DURUM →
> Checkout/Veritabanı satırlarında zaten tam özetli — aktif takip için gerekli değil, içerik
> kaybı yok.

> **[TAŞINDI — 2026-08-23, 400 satır eşiği]** 18. sohbet (#91 SEC-01/SEC-02 detay anlatısı) ve
> 17. sohbet (#90 detay anlatısı) blokları `session_arşiv_2.md`'ye taşındı (bkz. Arşiv Taşıma
> Kaydı altında). Kapanış gerekçesi: her iki blok da Açık Sorunlar #91/#90 satırlarında zaten
> tam özetli — aktif takip için gerekli değil, sadece turn-by-turn anlatı taşındı.
>
> **[TAŞINDI — 2026-09-03, 400 satır eşiği üçüncü kez aşıldı]** 19. sohbet (CRM/çok-şubeli
> vizyon keşfi), 20. sohbet (SANDWICH_SPEC.md v1.0/v1.1 üretimi) ve 22. sohbet (sandviç UI
> düzeltmeleri + checkout blokajı keşfi, geriye dönük işlendi) blokları `session_arşiv_3.md`'ye
> taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-03.md`, ⚠️ bu turda arşiv bölünmesiyle
> hedef dosya `session_arşiv_3.md`'ye düzeltildi, dosya adı değişmedi). Kapanış gerekçesi: üçü de Açık
> Sorunlar #92/#93/#94 (19. sohbet), #95 (20. sohbet, S1/S2/S5 hâlâ bekliyor), #99-#104 (22.
> sohbet) ve Kritik Kararlar tablosunda zaten tam özetli — aktif takip için gerekli değil,
> sadece turn-by-turn anlatı taşındı.
> **[TAŞINDI — 2026-08-23, 400 satır eşiği ikinci kez aşıldı]** SEKİZİNCİ DERS (21. sohbet)
> bloğu (build hatası düzeltmesi, `sandwich-data.json` TEST VERİSİ üretimi, `Hero.tsx` CTA
> değişikliği, 6 adım bileşeni + eksik `page.tsx` kodlanması, 7 test dosyası/27 test PASS)
> `session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-08-23-devam2.md`).
> Kapanış gerekçesi: içerik Açık Sorunlar #95/#96/#97/#98'de zaten tam özetli — aktif takip
> için gerekli değil, sadece turn-by-turn anlatı taşındı.

> **[TAŞINDI — 2026-09-05, 400 satır eşiği dördüncü kez aşıldı]** 23. sohbet devamı (MOTION
> SYSTEM Mobil Tactile Düzeltmesi — MenuCard whileTap kararı, sertlik düzeltmesi,
> merkezileştirme anlatısı) `session_arşiv_3.md`'ye taşındı (eklenti: ⚠️ hedef bu turda düzeltildi,
> `session_arsiv_2_EKLENTI_2026-09-05.md`). Kapanış gerekçesi: içerik artık #107 (KAPANDI) ve
> Motion System P0 bölümünde zaten tam özetli — aktif takip için gerekli değil.

## 3) Kapanmış Açık Sorun satırları

**Kapanış gerekçeleri:**
- **#39:** Rıza esaslı /hesap akışı canlıda doğrulandı, Twilio kısıtı artık engel değil; GENEL DURUM → Kullanıcı Profili/Adres satırında özetli.
- **#60:** Neon şifre sıfırlama + Vercel yeniden dağıtım + /menu canlıda doğrulandı; SIRADAKİ GÖREVLER 4 numaralı eski satır bu turda ✅ olarak işaretlendi.
- **#63:** Next 15.5 yükseltmesi canlıda doğrulandı, kalan uyarılar #141-#144'e ayrıldı; o satırlarda ve SIRADAKİ 4b'de özetli.
- **#70:** order_history.table_number tipi kararlaştırıldı, migration Neon'da doğrulandı; Kritik Kararlar'daki masa numarası satırında özetli.
- **#91:** SEC-01 (rol iptali) ve SEC-02 (login rate-limit) kod+test+canlı doğrulandı; GENEL DURUM → Auth satırında özetli.
- **#99:** Sandviç checkout blokajı canlıda 3 ekran görüntüsüyle kalktı; GENEL DURUM → Checkout satırında özetli (kök nedenin hâlâ kesin bilinmediği orada yazılı).
- **#107:** tokens.ts yapı çelişkisi çözüldü; kalan Motion System işi #105 satırında.
- **#109:** Keto/sıcak-tahıl kararı uygulandı, DIET_FILTERS türetildi; GENEL DURUM → Public Menü satırında özetli. Kayıtlı RİSK (DB'de eski etiket kalırsa ham id görünür) bu arşivde de duruyor.
- **#114:** Admin listesi önbellek sorunu kökten çözüldü (neon-http no-store); kalıcı ilke #116 satırında (açık) duruyor.
- **#115:** Kategori sistemi uçtan uca canlıda doğrulandı; GENEL DURUM → Veritabanı ve Admin Panel satırlarında özetli. #131'in kategori eşleştirmesi bu satırdaki isimlere dayanıyor.
- **#117:** A9: public /menu DB'ye bağlandı; GENEL DURUM → Public Menü satırında özetli.
- **#123:** isCatalogReady guard'ı geriye dönük kaydedilmişti ve kodda yaşıyor; GENEL DURUM → Sandviç Akışı satırında özetli.
- **#124/125:** db bundle sızması ve eksik görseller canlıda doğrulandı; Kritik Kararlar'daki 33. sohbet satırında özetli.
- **#127:** Bowl akışı DB'ye bağlandı, build yeşil; GENEL DURUM → Bowl Akışı satırında özetli.
- **#128:** Hero CTA gerçek ürün id'sine bağlandı, canlıda doğrulandı (A16); Bowl Akışı satırında özetli. Kök neden notu (admin id'yi manuel girmeye izin vermiyor) bu arşivde duruyor.
- **#129:** image opsiyonel yapıldı, build yeşil; Kritik Kararlar'daki 35. sohbet satırında özetli. 'Tüketici bileşenler undefined görseli nasıl karşılıyor' işi A17'de açık.
- **#134:** Quick-Add ilk sos ücretsiz kuralı canlıda onaylandı; GENEL DURUM → Checkout satırında özetli (test borcu notu orada).
- **#139:** Mobil filtre + QuickAddSheet görseli canlıda onaylandı; Public Menü satırında özetli. ⚠️ Bu satırın sonundaki AÇIK not (MenuCard'da Süper Gıda/Kids Meals rozet çakışması) SIRADAKİ GÖREVLER'e yeni A31 satırı olarak taşındı.

**Taşınan TAM satırlar (sütunlar: # / Öncelik / Açıklama / Etkilenen Dosya(lar)):**

| # | Öncelik | Açıklama | Etkilenen Dosya(lar) |
|---|---|---|---|
| 39 | 🟢 | **[Bu turda ÇÖZÜLDÜ]** `/hesap` akışı artık rıza esaslı kayıt (OTP'siz) üzerinden canlıda test edildi ve DOĞRULANDI — Twilio kısıtı bu akışı artık engellemiyor. | — |
| 60 | ✅ | **[KAPANDI, bu turda]** Neon `neondb_owner` şifresi sıfırlandı; Neon–Vercel entegrasyonu `DATABASE_URL`'yi Production+Preview'da otomatik güncelledi ("System rotated"), Redeploy yapıldı (`DZVGVJU4d` Ready), `/menu` hatasız açılıyor. Eski şifre geçersiz. Yerel `.env.local` yok (sadece mobil çalışılıyor). | Neon console, Vercel env |
| 63 | ✅ | **[KAPANDI, bu turda — Next 15.5 yükseltmesi CANLIDA]** `chore/next-15` dalı PR #3 ile `main`'e squash-merge edildi (Production `31e1701` Ready, kullanıcı canlıda `/menu`+giriş+`/admin`'i doğruladı). Next 15.5.26 + React 19 + yeni `package-lock.json` (GitHub Actions `regenerate-lock` ile üretildi, CI build'i için sahte `IMAGEKIT_*`/`TWILIO_*` env verildi — workflow dosyaları sonradan silindi). Dependabot PR #2 (Next 16'ya sıçrama) KAPATILDI, merge edilmedi. Uyarılar 48→25'e düştü, Next.js uyarıları kapandı. **Kalan uyarılar ve borçlar: #141-#144.** | `package.json`, `package-lock.json`, `.npmrc`, 14 route/page dosyası (async params) |
| 70 | ✅ | **[BU TURDA KAPANDI]** `order_history.table_number` tipi `text` olarak kararlaştırıldı (masa adları sayısal olmayabilir), index sadece `status` üzerine eklendi (`table_number` filtrelenmeyecek). Migration Neon'da koşuldu ve DOĞRULANDI. | `docs/schema-changes/20260809140000_order_history_status_tablenumber_customernotes_eklendi.md` |
| 91 | ✅ | **[KAPANDI, bu turda]** Güvenlik denetimi SEC-01 (rol revocation) + SEC-02 (login rate-limit) — kod+test (33/33 PASS)+build+tsc TAMAM, kullanıcı CANLIDA test etti: (a) role-revocation 403 doğrulandı; (b) rate-limit doğrulandı — kullanıcının gözlemi: 5'ten fazla yanlış şifre denemesinde sistem bir süre girişi bekletiyor (geçici kilit/cooldown). **Not:** kapanış kullanıcının kısa sözlü onayına dayanıyor, ekran görüntüsü paylaşılmadı; 5 dosyanın (`middleware.ts`/`auth.ts`/`lib/auth/rate-limit.ts` + testler) fiilen push/deploy edildiği canlı testin başarılı olmasından ÖRTÜK olarak çıkarsanıyor, ayrıca teyit istenmedi. | `middleware.ts`, `auth.ts`, `lib/auth/rate-limit.ts` |
| 99 | ✅ | **[KAPANDI, bu turda — 3 canlı ekran görüntüsüyle doğrulandı]** Sandviç checkout BLOKAJI artık YOK: sepette "Özel Sandviç" (156₺) görünüyor, Gel Al + Nakit seçilip "Siparişi Onayla" tıklandığında "fiyatlandırılamadı" hatası ÇIKMIYOR (156₺/174 kcal doğru gösterildi), sipariş personel paneline (Gel Al sekmesi, "Onay Bekleyen") doğru detaylarla (Ekmek/Boy/Protein/Peynir/Sebzeler/Sos) düştü. **Kök neden hâlâ kesin belirlenmedi** — önceki şüphe (`FulfillmentGate.tsx`/`ConfirmPickupOrderButton.tsx`'in `sandwichCustomization`'ı tanımaması) bu turda AYRICA doğrulanmadı, muhtemelen #124/#125 düzeltmelerinin (33. sohbet) yan etkisiyle kendiliğinden düzelmiş olabilir — bu KESİN değil, sadece bir olasılık. | `components/checkout/FulfillmentGate.tsx` veya `ConfirmPickupOrderButton.tsx` (kesin dosya hâlâ DOĞRULANMADI) |
| 107 | ✅ | **[KAPANDI]** `tokens.ts` paylaşıldı, yapı çelişkisi çözüldü — gerçek kod düz `durations/easings/springs` export'ları kullanıyor. | `lib/motion/tokens.ts` |
| 109 | ✅ | **[BU TURDA (31. sohbet) KAPANDI]** Karar 1: **Keto** filtre panelinden tamamen KALDIRILDI — admin'in kendi `MENU_ITEM_TAGS` sabitinde hiç yoktu, gerçek veride hiç kullanılmıyordu, kalıcı bir kritere (karb/yağ eşiği) dayanmadan sadece her zaman 0 sonuç veren bir seçenek olarak durması YASAK LİSTE'deki "context eksikken güven verme" ilkesine aykırıydı — gerçek kriter belirlenip ürünlere işlenince geri eklenebilir. Karar 2: **"sıcak-tahıl"** de kaldırıldı; `DIET_FILTERS` artık elle yazılan liste değil, `MENU_ITEM_TAGS`'tan TÜRETİLİYOR (allergen'lerle aynı desen) — böylece ikisi kendiliğinden senkron kalıyor, tekrar ayrışma riski yapısal olarak kapandı. Ayrıca etiket görünüm senkronu uygulandı: yeni `MENU_ITEM_TAG_LABELS` haritası (`menu-item-constants.ts`) admin formu VE `MenuCardBadges.tsx` tarafından okunuyor; `MenuCardBadges.tsx`'e eski/silinmiş id için `?? tag` fallback'i eklendi (crash yok, ham id gösterir). **RİSK (kapanmadı, kayıt altında):** DB'de hâlâ `sıcak-tahıl` etiketli bir ürün varsa kartında bu ham id görünmeye devam eder — DB'den elle temizlenmesi gerekir (DB şu an boş olduğu için şu an fiili risk yok, bkz. #115). | `lib/menu-item-constants.ts`, `lib/menu-filters.ts`, `components/admin/MenuItemForm.tsx`, `components/menu/MenuCardBadges.tsx` |
| 114 | ✅ | **[BU TURDA (29. sohbet) KAPANDI — kök neden REVİZE EDİLDİ]** Admin panelde yeni ürün oluşturuldu ("Fogy"), DB'ye yazıldığı doğrulanmıştı ama listede görünmüyordu. `export const dynamic = 'force-dynamic'` (28. sohbet fix'i) DOĞRUYDU ama TEK BAŞINA YETERSİZ çıktı — asıl kök neden `neon-http` sürücüsünün iç `fetch()` çağrılarının Next.js Data Cache'inde önbelleğe alınmasıydı (bkz. #116). `lib/db/client.ts`'e `fetchOptions:{cache:'no-store'}` eklenerek KÖKTEN çözüldü, canlıda doğrulandı. | `lib/db/client.ts`, `app/admin/page.tsx` |
| 115 | ✅ | **[BU TURDA (29. sohbet) KAPANDI]** Kategori sistemi uçtan uca kodlandı: `categories` tablosu (`id`=ASCII slug PK, `name`, `sortOrder`) + `menu_items.category`'ye FK (RESTRICT — bağlı ürün varken silme DB seviyesinde engellenir, cascade YOK, kullanıcı kararı). Admin'e `/admin/categories` (liste+ekle+sil) eklendi, `MenuItemForm.tsx`'teki serbest metin `category` alanı `<select>`'e çevrildi, `POST`/`PATCH` menu-items route'ları FK ihlalini (23503) 400 ile kullanıcı dostu mesaja çeviriyor. 7 kategori (İmza Ürünler/Bowl/Dürüm/Salata Bowl/Sandviç/Tatlı/İçecek) seed edildi. 8 test ürünü kullanıcı onayıyla `DELETE FROM menu_items` ile temizlendi. **CANLIDA DOĞRULANDI. [35. sohbet devamı (2. kez) notu]:** Bu satırdaki 7 kategori adı, yeni QuickAddSheet özelliğinin (bkz. #131) kategori eşleştirmesinin DAYANDIĞI TEK kaynak oldu — gerçek `id` (slug) değerleri hâlâ görülmedi, sadece bu satırdaki `name` değerleri kullanıldı. | `lib/db/schema.ts`, `types/index.ts`, `components/admin/MenuItemForm.tsx`, `components/admin/CategoryForm.tsx`, `components/admin/DeleteCategoryButton.tsx`, `app/admin/categories/*`, `app/api/admin/categories/*`, `app/api/admin/menu-items/*` |
| 117 | ✅ | **[BU TURDA (30. sohbet) KAPANDI]** A9 — public `/menu` artık `menu_items`/`categories` DB'sine bağlı. Kategori sekmeleri sabit union yerine `categories` tablosundan `buildCategoryTabs()` ile dinamik üretiliyor; "vegan"/"sicak-tahil" sanal sekmeleri `DIET_FILTERS`'a taşındı. Kullanıcı onayıyla ("Her şey tamam") canlı build doğrulandı. | `app/menu/page.tsx`, `components/menu/{MenuPageClient,CategoryNav}.tsx`, `lib/menu-filters.ts`, `app/api/admin/menu-items/{route.ts,[id]/route.ts}` |
| 123 | ✅ | **[GERİYE DÖNÜK KAYIT, 33. sohbet — 32. sohbette yapılmış ama hiç loglanmamış]** `app/sandwich/customize/[id]/page.tsx`'e `isCatalogReady()` guard'ı eklenmişti (boş/kısmi katalog varsa `SandwichCustomizer`'a hiç geçilmiyor) — kod `lib/sandwich-catalog.ts` header yorumunda "#123 düzeltmesi" olarak anılıyordu ama SESSION_INDEX.md'ye hiç işlenmemişti (governance/fiili kod arasında senkron kopukluğu, AGENT.md v1.5'teki arşiv-parçalama dersiyle AYNI TÜR ihlal). Bu turda dosya okunurken fark edildi, gerekçesiz kaybolmasın diye buraya geriye dönük kaydedildi. | `app/sandwich/customize/[id]/page.tsx`, `lib/sandwich-catalog.ts` |
| 124/125 | ✅ | **[KAPANDI, 33. sohbet — özet, tam anlatı Kritik Kararlar tablosunda]** `db` bundle sızması (#124) ve eksik ürün görselleri (#125) — bkz. Kritik Kararlar "33. sohbet" satırı. | `lib/sandwich-catalog.ts`, `lib/sandwich-constants.ts`, `components/sandwich/Step*.tsx` |
| 127 | ✅ | **[YENİ, 34. sohbet — KAPANDI, kullanıcı build'i yeşile aldı]** Bowl ("Kâseni Yarat") akışı sandviçteki AYNI desenle DB'ye bağlandı: yeni `lib/bowl-catalog.ts` (`buildBowlCatalog`/`isCatalogReady`), `types/index.ts`'e `CustomizerGardenCatalogItem`+`isAlwaysPaid` (Garden'daki "her zaman ücretli" tespiti artık `item.id==="avocado"` hardcode DEĞİL, DB-yönetimli bayrak — `lib/customizer-pricing.ts` + `StepGarden.tsx` ikisi de güncellendi), `store/useCustomizerStore.ts`'e `catalog` state+`setCatalog()` (statik `customizerCatalog` importu kalktı), 5 `Step*.tsx`+`VisualPreview.tsx`+`MobileSummaryDrawer.tsx` store'dan okuyacak şekilde değişti, `app/api/orders/gel-al/route.ts` BSC-3 gereği `buildBowlCatalog()` çağırıyor. **Onaylı plana 1 ekleme:** `app/menu/customize/[id]/page.tsx` server component'e çevrilince client mantığı yeni `components/customizer/BowlCustomizer.tsx`'e taşındı (plan dışıydı, Self-Correction ile bildirildi, SandwichCustomizer.tsx ile aynı mimari). **Yan düzeltme:** ölü kod `lib/customizer-data.ts` build'i kırdığı için SİLİNDİ (hiçbir gerçek kod import etmiyordu, grep ile doğrulandı). Kullanıcı onayları: Extras DB'ye taşınmadı (Soru #1), malzeme kartı görseli bu turda eklenmedi (Soru #2, kapsam dışı), admin veri girişini kullanıcı elle yapacak (Soru #3, seed script yok). | `lib/bowl-catalog.ts`, `types/index.ts`, `lib/customizer-pricing.ts`, `store/useCustomizerStore.ts`, `components/customizer/BowlCustomizer.tsx` (yeni), `app/menu/customize/[id]/page.tsx`, `components/customizer/Step{Base,Main,Garden,SignatureFlavor,Finish}.tsx`, `VisualPreview.tsx`, `MobileSummaryDrawer.tsx`, `app/api/orders/gel-al/route.ts` |
| 128 | ✅ | **[KAPANDI, 35. sohbet]** `Hero.tsx`'teki "Kaseni Oluştur" CTA'sı sabit `build-your-own-kasem` id'sine gidiyordu (`menu_items`'a hiç girilmemişti, ilk kez 34. sohbette Bowl DB'ye bağlanınca gerçek 404 olarak ortaya çıkmıştı). Kullanıcı admin'den gerçek `fekafel-bowl-hb0fc` id'li ürünü oluşturdu, `Hero.tsx` paylaşıldı, `href` bu gerçek id'ye güncellendi (niyet yorumuna da işlendi). Kök neden (admin POST route'unun id'yi her zaman otomatik üretmesi, manuel id girilemiyor olması) DEĞİŞMEDİ — ileride yeni bir "build-your-own-*" ürünü gerekirse aynı adım tekrarlanmalı. **Sandviç tarafı (`build-your-own-sandwich`) bu turda BİLEREK dokunulmadı, hâlâ TEYİT EDİLMEDİ.** | `components/home/Hero.tsx` |
| 129 | ✅ | **[YENİ, 35. sohbet — KAPANDI]** #127'nin (34. sohbet) eklediği Bowl katalog tipi, `image` alanını TÜM öğeler için zorunlu kılıyordu — ama `EXTRA_OPTIONS` sabiti (avokado/sos/çıtırlık, DB'den değil kod içinde sabit, `lib/customizer-pricing.ts` veya ilgili sabit dosyası) hiç `image` taşımıyor, bu yüzden build kırıldı. Düzeltme: `types/index.ts`'te `image` alanı `carbs`/`fat` ile aynı desende **opsiyonel** yapıldı (`image?: string`) — SADECE bu dosya değişti, `bowl-catalog.ts` + 5 `Step*.tsx` dosyasına dokunulmadı. Kullanıcı pushladı, customize sayfasını gerçek ürün id'siyle doğrudan test etti, akış çalıştı. **Not (izlenmeli, KOD TARAFI BU TURDA TEYİT EDİLMEDİ):** `image` artık opsiyonel olduğu için, `item.image`'ı doğrudan `<img src>` gibi kullanan tüketici bileşenler (`VisualPreview.tsx`, `Step*.tsx`, `MenuCardImage.tsx` benzerleri) `undefined` durumunu görsel olarak nasıl karşılıyor, bu turda GÖRÜLMEDİ/DOĞRULANMADI — sadece derleme (tip) seviyesinde çözüldü. | `types/index.ts` |
| 134 | ✅ | **[KAPANDI, 38. sohbet — kullanıcı onayladı]** Quick-Add sos seçiminde "ilk seçilen ücretsiz, sonrakiler tam fiyat" kuralı — kullanıcı 3 soruyla netleştirdi: kapsam Quick-Add (Customizer tek seçimli kaldığı için orada davranış değişmiyor), "ilk" = seçim SIRASI (dizideki index 0, deselect edilirse kalan ilk eleman ücretsiz sayılır), tüm Quick-Add ürünlerinde geçerli. Kod incelemesiyle `signatureFlavorIds`'in zaten sıralı dizi olduğu görüldü — **şema değişikliği GEREKMEDİ**. `route.ts`'te `priceFlavorSelection` (yeni, Kural #5 böldü) + `QuickAddSheet.tsx`'te `computeQuickAddTotals` (yeni) ile hem sunucu hem istemci senkron. **Yan düzeltme:** istemci eskiden `signatureFlavors.filter()` kullanıyordu (katalog sırası) — "ilk seçilen"i YANLIŞ belirlerdi, `selectedFlavorIds.map()`'e çevrildi. Kalori hiçbir promosyonla düşülmez (CORE.md §9). **KAPANIŞ:** kullanıcı push/build/canlı doğrulamayı onayladı ("#134 onaylandı kapat"). **Not:** kapanış kullanıcının kısa sözlü onayına dayanıyor, ekran görüntüsü paylaşılmadı — A12'deki gibi görsel kanıt yok. `priceFlavorSelection`/`computeQuickAddTotals` için ayrı bir test seti hâlâ yazılmadı (test borcu, kapanışı geçersiz kılmaz). | `app/api/orders/gel-al/route.ts`, `components/menu/QuickAddSheet.tsx` |
| 139 | ✅ | **[KAPANDI, bu turda — kullanıcı canlıda 3 maddeyi onayladı]** Mobil filtre bağlantısı + QuickAddSheet görsel düzeltmesi. Deploy `5bdc5a9` yeşil (Vercel ekran görüntüsü + canlı `/menu` görüntüsü: Filtrele butonu görünüyor, kart görseli tam). Kullanıcı doğrulaması: (1) alerjen kutusu işaretleniyor → `FilterCheckboxGroup` id çakışması OLMADI, (2) "N ürünü göster" butonu/rozet/çip çalışıyor, (3) QuickAddSheet görseli tam görünüyor. #73 (`bg-olive-primary`) bu bileşenlerde sorun çıkarmadı (kullanıcı görsel olarak olumlu bildirdi, ayrı kanıt yok). **AÇIK, ayrı iş:** `MenuCard`'da "Süper Gıda" rozetinin arkasında "Kids Meals" yazısı üst üste biniyor — `MenuCard.tsx` GÖRÜLMEDİ, nedeni bilinmiyor. | `components/menu/{MenuPageClient,MobileFilters,FilterTriggerButton,FilterSheet,QuickAddSheet}.tsx` |
--------
# session_arşiv_3 EKLENTİ — 2026-09-30 (devam2)
> Kullanıcı kararıyla KAPATILAN 5 SIRADAKİ GÖREVLER satırı. Kapatma = önceliksiz/kapsam dışı; kod yazılmadı, canlıda doğrulanmadı.
> Bağlı açık sorunlar (#141, #145, #147, #148, #149) ve A23 açık kalır. `session_arşiv_3.md`'nin sonuna eklenecek.

| Sıra | Görev | Öncelik |
|---|---|---|
| A27 | **[YENİ, bu turda]** Sıfırlama sonrası zorunlu şifre değişimi (`must_change_password` kolonu = migration + `auth.ts` + arayüz; ayrı tur, KARAR BİLDİRİMİ gerekir). Admin şifresini unutursa panelden sıfırlanamaz: Neon SQL Editor'den elle (bcrypt hash gerekir, pgcrypto `crypt`) — DENENMEDİ, kabul edilebilir bulundu (tek admin). | 🟡 |
| A28 | **[YENİ, bu turda]** `middleware.ts` + `next.config.ts` dosyaları gelince: personel guard'ında taze rol (#147), güvenlik başlıkları + `error.tsx`/`not-found.tsx` (#148). Sonra kırık testler (#141). | 🟡 |
| A29 | **[YENİ, bu turda]** Yeni şifre route/hook/form + resolve + `validation.test.ts` (8→6) için testler; `gel-al/route.test.ts` örnek alınacak (kullanıcı dosyayı atacak). Vitest koşulamıyor (Codespaces yok) — test borcu. | 🟡 |
| A30 | **[YENİ, bu turda]** Uzun SESSION_INDEX kopyasını (v118?) ayrı adla/zip'le yükle → fark çıkar → düşen içeriği taşıma bloğuna ekle (#149). | 🟠 |
| A10 | **[GÜNCELLENDİ, bu turda]** Admin panelde ürünler girilmeye başladı: Ayran, Burrito, Cheesecake, Kendi kasem, Salata bowl, Soda, Su, Vegan sandviç (görselli). **KALAN:** kalan gerçek ürünlerin fotoğraf çekimi/girişi; Ayran kalori/protein değeri geçici (1 kcal/2g) — paket besin tablosundan gerçek değerle düzeltilmeli (kalori zorunluluğu, DESIGN_SYSTEM). | 🟠 |
-----
# session_arsiv_3_EKLENTI_2026-10-01.md

> Bu dosya `session_arşiv_3.md`'nin SONUNA kullanıcı tarafından eklenecek (10. taşıma, 2026-10-01).
> Kapanan satırların TAM metni; içerik kaybı yok. Kapanış gerekçeleri SESSION_INDEX v121 → CURRENT FOCUS (2).

## KAPANMIŞ SATIRLAR (TAM METİN)

| 119 | 🟢 | **[YENİ, 30. sohbet — teknik borç]** `lib/db/queries/menu.ts` (Karar B'nin `unstable_cache` sarmalayıcısı, bkz. #118) artık HİÇBİR dosyadan import edilmiyor — ölü kod. Kullanıcı tarafından repodan SİLİNMELİ. | `lib/db/queries/menu.ts` |

| 122 | 🔴 | **[YENİ, 32. sohbet]** DB şema senkron hatası düzeltildi ve kullanıcı admin/ingredients çökmesinin gittiğini DOĞRULADI, ama **kullanıcı henüz uçtan uca denemedi** (kendi ifadesi). Bu turda SADECE `lib/db/schema.ts`, admin `ingredients` sayfaları (liste/yeni/`[id]`), `IngredientForm.tsx` ve `ingredients` API route'u statik olarak incelendi — önceki turda "25 dosya" olarak push edildiği bildirilen sandviç-DB bağlama refactorunun geri kalanı (`lib/sandwich-catalog.ts`, `lib/sandwich-pricing.ts`, `store/useSandwichStore.ts`, 6 `Step*.tsx`, `SandwichSummaryPanel.tsx`, `SandwichCustomizer.tsx`, `app/sandwich/customize/[id]/page.tsx`, `app/api/orders/gel-al/route.ts`, `SandwichSizeForm.tsx`) bu sohbette HİÇ GÖRÜLMEDİ. Ayrıca `sandwich_sizes` (0 satır) ve muhtemelen `ingredients` (sandviç malzemeleri) tabloları gerçek beden/malzeme verisi içermiyor — Mike's Way preseti/fiyat hesaplama gerçek veri girilmeden ANLAMLI test edilemez. | `lib/sandwich-catalog.ts`, `lib/sandwich-pricing.ts`, `store/useSandwichStore.ts`, `components/sandwich/*`, `app/api/orders/gel-al/route.ts` |

| 147 | 🟡 | **[YENİ, bu turda]** `requireStaffSession` (`lib/personel/api-guards.ts`) rolü JWT oturumundan okuyor, `requireAdminSession` gibi DB'den TAZE okumuyor. `auth.ts` notuna göre `middleware.ts` `/personel` ve `/api/personel` için taze DB rol kontrolü yapıyor (SEC-01, #91 canlıda doğrulanmıştı) — yani route guard ikinci katman olabilir; `middleware.ts` (matcher kapsamı) bu turda GÖRÜLMEDİ. Bu turda önce 'açık var' alarmı verildi, sonra geri çekildi; kesin karar `middleware.ts` görülünce. Yapılırsa dönüş şekli (oturum ya da null) korunarak yalnız guard içine DB okuması eklenmeli. | `lib/personel/api-guards.ts`, `middleware.ts` (görülmedi) |

| A15 | **[YENİ, 33. sohbet]** `server-only` npm paketini kurup `lib/db/client.ts`'e eklemek isteniyor mu? (#126 — kullanıcı onayı bekliyor, bu sınıf hatayı derleme zamanında yakalamak için) | 🟢 |

| A9.1 | **[YENİ, 30. sohbet — temizlik]** Kullanılmayan `lib/db/queries/menu.ts` dosyasını repodan sil (#119) | 🟢 |

-----
# session_arsiv_3_EKLENTI_2026-10-01-b.md

> Bu dosya `session_arşiv_3.md`'nin SONUNA kullanıcı tarafından eklenecek (11. taşıma, 2026-10-01).
> SESSION_INDEX v121 → v122 geçişinde çıkarılan/özetlenen satırların TAM metni; içerik kaybı yok.

## ESKİ SATIRLAR / PARAGRAFLAR (TAM METİN)

| E2 | **[YENİ]** Ödeme ekranı onay satırına tıklanıp okunabilen "Ön Bilgilendirme Formu" + Satış Sözleşmesi linkleri (Ön Bilgilendirme sayfası YOK, taslak + hukuk incelemesi) | 🟠 |

> **[GÜNCEL — bu turda, 2026-10-01 devamı: E1 hazırlığı + açık borç temizliği]** (1) **E1:** beş dosya okundu (kod değişmedi). Bulgular: Ön Bilgilendirme Formu YOK; sözleşme/iade metinleri JSX'e gömülü (e-postada kullanılamaz); satıcı bilgisi yalnız "Bowlera (şahıs şirketi)"+VKN+adres. Kullanıcı verdi: e-posta `bowleraa34@gmail.com`; telefon YOK (yeni numara alınacak); ticari unvan BOŞ (#156). `lib/legal/seller.ts` ÜRETİLDİ (adım 1, kimse import etmiyor). Adım 2 (metinleri `lib/legal/`a taşıma + `TERMS_VERSION` artışı) kullanıcı onayı BEKLİYOR.

> (2) **Borç temizliği (kullanıcı "sen karar ver" dedi):** #119 KAPANDI (GitHub ekran görüntüsünde `lib/db/queries/` altında `menu.ts` yok). #147 KAPANDI (`middleware.ts` görüldü: `/personel` ve `/api/personel` matcher'da, rol her istekte taze DB'den okunuyor, route guard 2. katman). #122 KAPANDI (ajan önerisi, kullanıcı itiraz etmedi; gerekçe: canlı doğrulamada `users` 12 / `order_history` 15 kolon koddaki şemayla birebir eşleşti). #126: kullanıcı "evet" dedi, `client.ts` üretildi. #148: `next.config.mjs` güvenlik başlıkları üretildi (CSP bilinçli yok, #155).

> (3) Kullanıcı: "Push yaptım, bozulma yok, deploy yeşil" — hangi dosyaların (`client.ts`+paket, `next.config.mjs`, `seller.ts`) gittiği ve ImageKit/PayTR iFrame kontrolü AÇIKÇA teyit EDİLMEDİ (#126/#148 satırları). Dersler: (a) `server-only` Next dışında (Vitest, `tsx` scriptleri) hata fırlatır; (b) yapılandırma dosyası `next.config.mjs`'tir, `.ts` değil; (c) tek turda iki ayrı dosya push edilirse bozulmanın kaynağı ayırt edilemez — ayrı push önerildi; (d) aynı adlı SESSION_INDEX.md yüklenmesi #149'daki kayıp riskini taşır — çıktı `SESSION_INDEX_v121.md` adıyla verildi, repoda `SESSION_INDEX.md` olarak değiştirilmeli.

| 151 | 🔴 | **[YENİ, 2026-10-01]** E-posta sözleşme metnini TAŞIMIYOR (sadece özet + `/satis-sozlesmesi` ve `/iptal-ve-iade` linkleri + `TERMS_VERSION`). **Ön Bilgilendirme Formu sayfası/metni HİÇ YOK**; `ConfirmPickupOrderButton.tsx` onay satırında "Ön Bilgilendirme Formu" adı geçmiyor (sadece İptal/İade Koşulları + Satış Sözleşmesi). Satıcı bilgisinin (unvan/adres/vergi no) sitede nerede yazdığı bilinmiyor. Mesafeli satışta kalıcı veri saklayıcısıyla (e-posta) gönderim beklentisi → hukuk incelemesi gerekir. | `lib/email/order-email-content.ts`, `components/order/ConfirmPickupOrderButton.tsx`, `app/satis-sozlesmesi/page.tsx`, `app/iptal-ve-iade/page.tsx` |

| E1 | **[GÜNCELLENDİ, 2026-10-01]** E-postayı Yemeksepeti biçimine geçir (tam metinli, siparişe özel). Girdiler GELDİ ve okundu (`ConfirmPickupOrderButton`, `iptal-ve-iade/page`, `satis-sozlesmesi/page`, `terms-version.ts`, `order-email-content.ts`). ADIM 1 yapıldı: `lib/legal/seller.ts` üretildi (repoya konduğu TEYİTSİZ). **Sıradaki:** ADIM 2 — iki sayfanın metnini BİREBİR `lib/legal/` veri dosyasına taşı, sayfaları ondan render ettir, satıcı satırını `seller.ts`'ten oku, `TERMS_VERSION`'ı `2026-10-01-v1` yap (kullanıcı onayı BEKLİYOR). Sonra: ADIM 3 Ön Bilgilendirme Formu şablonu (taslak, hukuki metin UYDURULMAZ), ADIM 4 onay satırına link, ADIM 5 e-posta içeriği (#151/#152, #156 bloklayıcı) | 🔴 |

# session_arşiv_3.md — EKLENTİ 2026-10-10 (12. taşıma)
> Bu bloğu `session_arşiv_3.md` dosyasının SONUNA kullanıcı elle ekler. Dosyanın kendisi yeniden üretilmez.

## TAŞIMA BLOĞU — 2026-10-10 (12. taşıma, SESSION_INDEX 400 satır eşiği)
**Taşınan:** SESSION_INDEX.md sonundaki 15 eski sürüm notu (v121, v120, v119, v117, v116, v115, v114, v113, v112, v111, v110, v109, v108, v107, v106), aşağıda BİREBİR, TAM metinle.
**Kapanış gerekçesi:** Hepsi tamamlanmış turların sürüm-geçmişi özetidir; içerikleri Açık Sorunlar, Kritik Kararlar ve GENEL DURUM'da zaten özetlidir (örn. #63, #60, #135, A16/A18/A19, `users.email`, şifre değiştirme, E1 girdileri). Aktif takip için gerekli değil. v125 ve v127 ile yeni v128 index'te kaldı. Hiçbir Açık Sorun/Karar satırı bu taşımada düşürülmedi.

---

*BOWLERA SESSION_INDEX.md — v121 (v120'den, 113.486 bayt/376 satırlık kopya üzerinden: **[bu turda, 2026-10-01 devamı]** E1 girdileri okundu, `lib/legal/seller.ts` üretildi (adım 1); #119/#122/#147/A15/A9.1 KAPANDI ve eklentiye taşındı; #126 ve #148 güncellendi (`next.config.ts` kayıt hatası düzeltildi → `next.config.mjs`); yeni açık sorunlar #155 (CSP yok), #156 (telefon+ticari unvan eksik); yeni görevler E7, E8; E1 güncellendi. Kullanıcı "push yaptım, deploy yeşil" dedi, dosya bazında teyit YOK. TEST_MATRIX.md/DEPENDENCIES.md paylaşılmadı, GÜNCELLENMEDİ.)*

*BOWLERA SESSION_INDEX.md — v120 (v119'dan: **[bu turda, 2026-10-01]** `users.email` (NOT NULL) + DB sıfırlama + zorunlu e-posta (kayıt/`/hesap`), Gmail SMTP sipariş e-postası canlıda çalıştı (spam'e düştü), personel paneli 403 kök nedeni (JWT'de eski rol) bulundu. Yeni Kritik Kararlar #150-#153, yeni açık sorunlar #150-#154 (ikisi AYNI numara aralığını kullanır: bu dosyada Karar ve Sorun tabloları bağımsız sayılmaya devam ediyor, 141/142'de de aynı çakışma vardı), yeni Sıradaki Görevler E1-E6, CURRENT FOCUS ve GENEL DURUM güncellendi. TEST_MATRIX.md/DEPENDENCIES.md bu turda paylaşılmadı, GÜNCELLENMEDİ. Arşive taşıma YAPILMADI (dosya 400 satırın altında).)*

*BOWLERA SESSION_INDEX.md — v119 (v117 kopyası üzerinden; v118 KAYIP/işlenemedi, bkz. #149. **[bu turda]** Şifre değiştirme eklendi, minimum şifre 8→6 (kullanıcı kararı), personel şifre sıfırlaması yalnız müşteri hesaplarına kısıtlandı (canlıda doğrulandı), `params` build hatası düzeltildi. Yeni açık sorunlar #145-#149, Kritik Kararlar +2, SIRADAKİ A26-A31. 12 eski CURRENT FOCUS paragrafı + 18 kapanmış Açık Sorun satırı `session_arsiv_3_EKLENTI_2026-09-30.md`'ye taşındı; #141'e v118'den kısmi not, SIRADAKİ 4 (#60) ve -5 (#99) stale satırları işaretlendi. Dosya 406→357 satır.)*

*BOWLERA SESSION_INDEX.md — v117 (v116'dan: **[bu turda]** #63 KAPANDI (Next 15.5 yükseltmesi canlıda, PR #3, Dependabot PR #2 kapatıldı, uyarılar 48→25). Yeni açık sorunlar #141 (Vitest `vite` eksik), #142 (next-auth yama bekliyor), #143 (drizzle, düşük risk), #144 (teknik borç). Sıradaki Görevler 4b güncellendi. CURRENT FOCUS'a not eklendi. Başka tabloya dokunulmadı. ⚠️ Dosya hâlâ 400 satır eşiğinin ÜSTÜNDE — taşıma bu turda YAPILMADI, ayrı karar.)*
*BOWLERA SESSION_INDEX.md — v116 (v115'ten: **[bu turda]** #63 güncellendi: Dependabot açıldı, 48 uyarı analiz edildi, PR #2 (Next 14→16 sıçraması, build başarısız) merge EDİLMEYECEK, gerçek risk düşük (AVIF kapalı, Linux), Next 15.5.x yükseltmesi ayrı dalda planlanacak. Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v115 (v114'ten: **[bu turda]** A19 KAPANDI (sandviç uçtan uca canlıda doğrulandı, toplam kullanıcı tarafından teyit edildi). A24 açıldı (kozmetik: ürün adı tutarsızlığı, "Boy: 30" birimi, Tatlı denenmedi). Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v114 (v113'ten: **[bu turda]** A19 güncellendi: Ayran ile Sepete Ekle→checkout→personel paneli→Teslim Edildi canlıda çalıştı. Tatlı/Sandviç ayrı denenmedi. Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v113 (v112'den: **[bu turda]** A23 güncellendi: sandviç ekmek ve Ayran değerleri kullanıcı tarafından geçici/test verisi olarak teyit edildi. Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v112 (v111'den: **[bu turda]** A16 ve A18 canlıda doğrulanıp KAPANDI (bowl + sandviç CTA'ları 404 vermiyor). A23 açıldı (Glutensiz Somun 25 kcal / ortak görsel şüphesi). Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v111 (v110'dan: **[bu turda]** #60 KAPANDI (Neon şifre reset + Vercel redeploy + /menu doğrulandı). #135 madde 10 canlıda doğrulandı (SVG reddi + JPG yükleme). A11 KAPANDI, A10 güncellendi (8 ürün girildi, Ayran kalori geçici). CURRENT FOCUS güncellendi. Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v110 (v109'dan: **[bu turda]** #135 madde 10 (P2) KISMEN işlendi: `lib/admin/image-signature.ts` + test + `upload-image/route.ts` magic-byte doğrulaması kodlandı, SVG reddediliyor (AVIF/HEIC/SVG yan etkisi kayıtlı). Push/canlı test ve vitest HENÜZ YOK. Audit log/action log/rate-limit açık. #135 satırı, Sıra, A22, CURRENT FOCUS güncellendi. Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v109 (v108'den: **[bu turda]** #135 madde 6 işlendi: `Hero.test.tsx` düzeltildi (etiket+href+eksik CTA, ilk teşhis eksikti), vitest KOŞULMADI. #135 satırı, Sıra/Kapı, A22, CURRENT FOCUS güncellendi. Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v108 (v107'den: **[bu turda]** Kullanıcı talimatıyla dosya 400 eşiğinin altına indirildi (431→~370 satır): CURRENT FOCUS'tan 2 kapanmış paragraf + v102-v105 `...-devam6.md` eklentisine taşındı. Açık satırlara dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v107 (v106'dan: **[bu turda]** #135 P0 madde 3 TAM KAPANDI — `requireAdminSession()` + 17 admin handler, canlıda doğrulandı (admin çalışıyor, girişsiz 401; 401 middleware ile aynı metin olduğundan guard'ın kendi dalları için test borcu var). #135 satırı, Sıra/Kapı, A22, CURRENT FOCUS güncellendi. Başka tabloya dokunulmadı.)*

*BOWLERA SESSION_INDEX.md — v106 (v105'ten: **[bu turda]** Kullanıcı "hafızanı tazele, taşıma bloğunu ayır, hacmi düşür" dedi. v99-v101 versiyon paragrafları (`...-devam4.md`) ve SIRADAKİ GÖREVLER'den 20 kapanmış ✅ satır (`...-devam5.md`) ayrı eklentilere taşındı, yerlerine pointer bırakıldı. Açık/bekleyen hiçbir satıra dokunulmadı. Dosya 467→~425 satıra indi; 400 altına inmek için kalan tek yol eski 1e-31 listesindeki AÇIK satırların budanması — bu, dosyanın kendi notuna göre kullanıcı kararı gerektiriyor.)*

--- (taşıma bloğu sonu) ---
## TAŞIMA BLOĞU — 2026-10-14 (13. taşıma, SESSION_INDEX 400 satır eşiği)

> Bu blok `session_arşiv_3.md`'nin SONUNA kullanıcı tarafından eklenir (CORE.md §7.1 Adım 1.4 — arşiv dosyası asla tam yeniden üretilmez).
> Kaynak: SESSION_INDEX.md v137 altbilgisindeki 7 sürüm-notu paragrafı (v125–v132; içlerinde zincirli v122–v124 notları). TAM metin, değiştirilmeden.

### Kapanış gerekçesi (taşınan HER madde için)
Hepsi kapanmış turların SÜRÜM-GEÇMİŞİ notlarıdır; hiçbiri aktif takip gerektiren bir satır değildir. Notlarda geçen açık maddelerin hepsi aktif dosyada yaşamaya devam ediyor:
- `TEST_OK` (TB-24) doğrulaması / 404 kök nedeni (v129–v131): CURRENT FOCUS (0)(3)(5) ve (7)'de takipte — `TEST_OK`'in tabloyu KANITLAMADIĞI dersi (5)'te işlendi; 404 kök nedeni CURRENT FOCUS (7)'de hâlâ 'kanıtlanmadı' olarak AÇIK.
- Genel koşudaki kırık testler (v128, TB-CRM-04): Açık Sorun #161 / `TEKNIK_BORC_CRM.md` TB-CRM-04 + yeni Açık Sorun #167.
- #126, #141, #148 (v122–v125 notları): kendi Açık Sorun satırlarında (`| 126 |`, `| 141 |`, `| 148 |`) duruyor.
- #157–#160 (v122 notu): kendi Açık Sorun satırlarında duruyor.
- CRM-1/2/3a/3b/3c turlarının sonuçları (v123–v132): CURRENT FOCUS (1)–(9), Açık Sorun #161 ve SIRADAKİ GÖREVLER → CRM-0 satırında özetli.
- 'TEST_MATRIX/ROADMAP/KVKK checklist güncellenmedi' uyarıları (v129–v132): Açık Sorun #168 (doküman senkron borcu) ve CURRENT FOCUS (10)'da devralındı.

### TAM METİN (SESSION_INDEX.md v137 altbilgisinden, kaynak sırasıyla)

*BOWLERA SESSION_INDEX.md — v132 (v131'den: **[bu turda, 2026-10-12, devam]** CRM-3c 3c-1 şema (`TEST_OK`) + 3c-2 kod/test (tsc temiz, `lib/crm` 21 dosya/238 test PASS, deploy yeşil) işlendi; yeni paragraf EKLENMEDİ, mevcut [GÜNCEL] paragrafın (4) maddesi güncellendi; #161 ve CRM-0 satırları güncellendi. Arşive taşıma YAPILMADI. Hiçbir Açık Sorun/Karar satırı düşürülmedi. ⚠️ AÇIK: notlar canlıda uçtan uca denenmedi (arayüz yok); TEST_MATRIX/ROADMAP/KVKK checklist güncellenmedi.)*

*BOWLERA SESSION_INDEX.md — v131 (v130'dan: **[bu turda, 2026-10-12]** hesap planı bittiği için kapanışı yapılamayan CRM-3b işlendi (kullanıcı beyanı + zip'te kod teyidi): CURRENT FOCUS'a yeni [GÜNCEL] paragraf, önceki [ÖNCEKİ TUR]'a indi; #161 ve CRM-0 satırları güncellendi. Arşive taşıma YAPILMADI (satır sayısı eşiğin altında). Hiçbir Açık Sorun/Karar satırı düşürülmedi. TEST_MATRIX/ROADMAP/KVKK checklist verilmediği için güncellenmedi. Kullanıcı: testler geçti, dosyalar onaylandı. ⚠️ AÇIK: canlı doğrulama ayrıntısı görülmedi; 404 kök nedeni kanıtlanmadı; `TEST_OK` (TB-24) doğrulaması hâlâ görülmedi.)*

*BOWLERA SESSION_INDEX.md — v130 (v129'dan: **[bu turda, 2026-10-11 gece]** CRM-3a canlı doğrulama ve TB-CRM-11 kapanışı işlendi; CURRENT FOCUS'a yeni [GÜNCEL] paragraf, önceki [ÖNCEKİ TUR]'a indi; #161 ve CRM-0 satırları güncellendi. Arşive taşıma YAPILMADI (satır sayısı eşiğin altında). Hiçbir Açık Sorun/Karar satırı düşürülmedi. ⚠️ AÇIK: 404 kök nedeni kanıtlanmadı; `TEST_OK` (TB-24) doğrulaması hâlâ görülmedi.)*

*BOWLERA SESSION_INDEX.md — v129 (v128'den: **[bu turda, 2026-10-11 akşam]** CRM kararları (TB-07 (a)(b), TB-13, TB-14, TB-24) ve TB-09/10/24 uygulaması işlendi; CURRENT FOCUS'a yeni [GÜNCEL] paragraf eklendi, önceki (KVKK/çerez kapanışı) [ÖNCEKİ TUR]'a indi, #161 satırı ve CRM-0 görev satırı güncellendi. Arşive taşıma YAPILMADI (satır sayısı eşiğin altında). Hiçbir Açık Sorun/Karar satırı düşürülmedi. TEST_MATRIX.md paylaşılmadığı için güncellenmedi. ⚠️ AÇIK: `TEST_OK` doğrulaması görülmedi.)*

*BOWLERA SESSION_INDEX.md — v128 (v127'den, kullanıcının yüklediği 400 satırlık kopya üzerinden: **[bu turda, 2026-10-10 akşam]** TB-CRM-26 çerez bandı (kendi bileşen, 11 dosya, 46 test, deploy yeşil, bayrak KAPALI) işlendi; CURRENT FOCUS'a yeni [GÜNCEL] paragraf eklendi, CRM-0 görev satırı güncellendi. 12. taşıma: v106–v121 sürüm notları (15 paragraf) TAM metinle `session_arsiv_3_EKLENTI_2026-10-10.md`'ye taşındı (kayıt tablosunda satır + TAŞINDI notu). Hiçbir Açık Sorun/Karar satırı düşürülmedi. TEST_MATRIX.md paylaşılmadığı için güncellenmedi. Genel koşudaki 3 kırık test (görünen kaynak Header.test.tsx, diğerleri görülmedi) TB-CRM-04'e eklendi, nedeni DOĞRULANMADI.)*

*BOWLERA SESSION_INDEX.md — v127 (v126'dan: **[bu turda, 2026-10-10 öğleden sonra, devam]** CRM-2 Adım C2a + C2b (kayıt + sipariş akışı attribution, ÇEREZ + İLK TEMAS kararı, bayrak KAPALI, 41/41 PASS, tsc temiz, deploy yeşil) işlendi; CURRENT FOCUS'a yeni paragraf eklendi (eski GÜNCEL → ÖNCEKİ TUR), #161 ve CRM-0 görev satırı güncellendi, dosya tam 400 satır (eşik AŞILMADI), hiçbir satır silinmedi/taşınmadı, arşive dokunulmadı. v126 notu: (v125'ten: **[bu turda, 2026-10-10 öğleden sonra]** CRM-2 Adım A (şema, canlıda `TEST_OK`) + Adım B (backfill 3+28) + Adım C1 (olay yazımı kodu, 22/22 PASS, bayrak KAPALI) işlendi; CURRENT FOCUS'a yeni paragraf eklendi (eski GÜNCEL → ÖNCEKİ TUR), #161 ve CRM-0 görev satırı güncellendi, hiçbir satır silinmedi/taşınmadı, arşive dokunulmadı. v125 notu: (v124'ten: **[bu turda, 2026-10-10]** CRM-1 Adım 1 (şema, Neon `TEST_OK`) + Adım 2 (kod, 11/11 PASS, deploy yeşil, bayrak KAPALI) işlendi; TB-05 karar ✅, TB-06 ✅; CURRENT FOCUS'a yeni paragraf eklendi (eski GÜNCEL → ÖNCEKİ TUR), #161 satırı ve CRM-0 görev satırı güncellendi, hiçbir satır silinmedi/taşınmadı, arşive dokunulmadı. v124 notu: (v123'ten: **[bu turda, 2026-10-10]** TB-CRM-06 Adım 1+2 canlıda doğrulandı (`branches` + `branch_id`, kayıt ve Gel Al siparişi şube yazıyor); TB-CRM-04 düzeltildi (paket yeşil değil: 24 dosya/42 test kırık, tsc temiz). #161 satırı güncellendi, satır eklenmedi/silinmedi. v123: **[2026-10-09]** CRM hazırlık oturumu — #161 eklendi (CRM teknik borç paketi, 23 madde, tam liste `TEKNIK_BORC_CRM.md`), CRM-0 görev satırı eklendi, #92 şube önerisi kullanıcı tarafından ONAYLANDI (satır güncellendi). Hiçbir satır silinmedi/taşınmadı; arşive dokunulmadı. #141 kapanışı için `npm test` tarihi/test sayısı BEKLENİYOR.)))*

*BOWLERA SESSION_INDEX.md — v125 (v124'ten, 400 satırlık kopya üzerinden, checkpoint 2026-10-10 — canlı doğrulama A ✅, hesap değişikliği; önceki v124: checkpoint 15:48: CRM-2 Adım D route testleri işlendi — `read-attribution-safe` kararı + consent ve gel-al route testleri, 59/59 PASS, manuel push beyanı; TEST_MATRIX.md paylaşılmadı, GÜNCELLENMEDİ; hiçbir arşiv parçasına dokunulmadı. Önceki v122 notu: v121'den, 384 satırlık kopya üzerinden: **[bu turda, 2026-10-01 sonu]** E1 adım 2–4 üretildi ve CANLIDA doğrulandı (ekran görüntüleri); adım 5 (tam metinli e-posta) üretildi, teyit BEKLİYOR; yeni açık sorunlar #157 (ana sayfada geliştirici notu), #158 (bileşen boyutu), #159 (`kvkk/page.tsx` seller.ts'e bağlı değil), #160 (hukuk incelemesi); #151 🔴→🟠, #154 güncellendi; E2 KAPANDI; E1 güncellendi. #126/#148 push teyidi hâlâ yanıtsız. TEST_MATRIX.md/DEPENDENCIES.md paylaşılmadı, GÜNCELLENMEDİ.)*
# session_arşiv_3 EKLENTİ — 2026-10-15 (14. taşıma)
> SESSION_INDEX.md CURRENT FOCUS'tan taşınan 8 eski tur paragrafı (2026-10-10 → 2026-10-12: CRM-0/1/2, çerez bandı, KVKK kapanışı, CRM-3a/3b, TB-09/10/24). TAM metin, değişiklik yok. `session_arşiv_3.md`'nin SONUNA eklenir.
> Kapanış gerekçesi: hepsi kapanmış turlar; sonuçları #161, TEKNIK_BORC_CRM.md (TB-CRM-05…26, 33…56), Kritik Kararlar ve GENEL DURUM'da özetli.

> > **[ÖNCEKİ TUR — 2026-10-12: CRM-3b ✅ kapandı — personele şube kapsamlı + maskeli müşteri sekmesi]** (0) **Bağlam:** önceki oturumun kapanışı hesap planı bittiği için yapılamamıştı; bu tur yüklenen zip (`Bowlera_site-main`, 2026-10-12) + kullanıcı beyanı ("3b-3 kapandı") üzerinden dokümanları hizaladı. Canlı doğrulama ayrıntısı PAYLAŞILMADI (testler sonradan kullanıcıca geçti). (1) **Kapanan:** TB-CRM-19 3b = 3b-1 şema (`staff_branches`, birleşik PK) + 3b-2 yetki/sorgu/API (`crm-staff-guard`, `staff-customer-access`, `staff-customer-queries`, `phone-mask`, `staff-http`, `/api/personel/customers` + `[id]`) + 3b-3 arayüz (`MusterilerPanel.tsx`, `staff-panel-helpers.ts`, personel paneline "musteriler" sekmesi) — hepsi repoda görüldü. TB-CRM-07 (b) uygulandı; K-09/K-10 ✅ sayıldı. (2) **Davranış (kodda yazılı):** personel yalnız atandığı şubede sipariş vermiş VEYA kayıt olmuş müşteriyi görür; admin hepsini; şubesiz personel 403 (fail-closed); rol taze DB'den; liste 20/sayfa, arama ≥3 karakter; tam telefon/e-posta/adres/harcama/kaynak/olay personele GİTMEZ, telefon `+90 5•• ••• •• 78`; kapsam dışı id = 404 (var olduğu sızmaz) ama okuma denemesi audit'e yazılır; audit yazılamazsa veri yok; polling YOK. (3) **Açık/dürüst notlar:** ✅ 3b testleri kullanıcıca çalıştırıldı, hepsi geçti (sayı paylaşılmadı; statik sayım: 6 yeni test dosyasında 47 `it`; `lib/crm` 19 test dosyası) ve dosyalar onaylandı · ⚠️ personel API'sinde hız sınırı YOK → yeni **TB-CRM-51** (asistan önerisi, onay bekliyor) · ⚠️ `CRM_KVKK_CHECKLIST.md` bu turda verilmedi → K-09/K-10 ✅ işlenmeli (v1.2) · ⚠️ `staff_branches` doluluğu (tüm personel Bowlerapark'a atandı mı) teyit edilmedi → TEKNIK_BORC Açık soru #16 · ⚠️ 404 kök nedeni (3a) hâlâ kanıtlanmadı; `[CRM_ACCESS_DENIED]` logu `console.error` seviyesinde kalıyor; telefon arama normalizasyonu yapılmadı · TEST_MATRIX/ROADMAP verilmedi → güncellenmedi. (4) **[GÜNCEL, aynı gün sonra] CRM-3c:** 3c-1 şema ✅ (`customer_notes` append-only, Neon `TEST_OK`) + 3c-2 kod ✅ (not yazma/okuma API: personel kendi şubesine yazar, YALNIZ admin okur; audit fail-closed; `tsc` temiz, `lib/crm` 21 dosya/238 test PASS, deploy yeşil — kullanıcı çıktısı). TS adı `crmCustomerNotes` (sipariş notu `order_history.customerNotes` ile karışmasın). (5) **[GÜNCEL, 2026-10-12 08:45] 3c-3 ✅ CANLIDA doğrulandı:** admin 360'ta Notlar bölümü (`app/admin/musteriler/[id]/notes-section.tsx`, `note-form.tsx`, `actions.ts`; `lib/crm/customer-note-view.ts`, `customer-note-submit.ts` + 2 test dosyası). Yeni 2 test dosyası 17 test PASS (kullanıcı ekranı, Codespaces); deploy yeşil. Canlı: Notlar bölümü açılıyor, 500 sayaç + özel veri uyarısı görünüyor, 'İyi bir müşteri' notu eklendi, yazan adı+saatle listelendi. Audit canlıda doğrulandı: `customer_note_add_requested` `{role,surface,length:15}` ve `customer_notes_viewed` `{role,surface}` — not metni audit'te YOK. 🔴→✅ **Olay:** ilk denemede müşteri sayfası `NeonDbError: relation "customer_notes" does not exist` (log ekran görüntüsü, ad kırpık) ile ÇÖKTÜ; Neon'da `to_regclass` ikisi de null, adında 'note' geçen tablo yoktu → 3c-1'deki 'TEST_OK' tabloyu KANITLAMAMIŞTI. Olası sebep (KANITLANMADI): SQL 1 (migration) ile SQL 2 (RAISE EXCEPTION ile biten doğrulama) aynı çalıştırmada koşulup tümü geri alındı. SQL'ler AYRI çalıştırılınca tablo kuruldu. Ders: şema 'canlıda' sayılmadan önce ayrı sorguyla `to_regclass` ile tablo varlığı doğrulanır. Önlem: `notes-section.tsx` okuma hatasını yakalar (log'a yalnız hata kodu, sayfa çökmez). ⚠️ **AÇIK:** (a) **[✅ KAPANDI, bkz. (6)]** audit `surface` etiketi YANLIŞ: admin sayfasından yapılan okuma/yazma `"personel"` yazıyor (append-only, eski satırlar düzeltilemez; düzeltme önerildi, kullanıcı onayı BEKLİYOR); (b) **[✅ KAPANDI, bkz. (6)]** personel not yazma kutusu YOK (yazma kodu hazır, arayüz yok) — kullanıcı: not özelliği personel kutusu olmadan yarım değer üretir; (c) **[kısmen kapandı, bkz. (6)]** tam `lib/crm` koşusu ve `tsc` çıktısı bu turda GÖRÜLMEDİ (yalnız 2 yeni dosyanın sonucu görüldü); (d) KVKK: alerji gibi sağlık notu riski + silinemezlik — `CRM_KVKK_CHECKLIST` K-28 (🔵) eklenmesi önerildi, onay BEKLİYOR; (e) sunucu tarafı idempotency yok (yalnız istemci kilidi); (f) TEST_MATRIX/ROADMAP/KVKK checklist verilmedi → güncellenmedi. **(Eski sıradaki, (6) ile güncellendi):** audit etiketi düzeltmesi kararı → personel not kutusu → 3d. (6) **[GÜNCEL, 2026-10-12 09:50] Audit `surface` düzeltmesi + personel not kutusu ✅ CANLIDA:** (i) **KÖK NEDEN:** `lib/crm/customer-note-access.ts`'te `surface: "personel"` iki yerde SABİT yazılıydı (`addCustomerNote`, `loadCustomerNotes`); admin sayfası aynı fonksiyonları çağırdığı için admin işlemleri `personel` yazıyordu. Eski test bu hatalı davranışı doğru diye sabitliyordu (admin okumasında `surface: "personel"` bekliyordu). **DÜZELTME (kullanıcı onayı):** `type CrmSurface = "admin" | "personel"`; iki fonksiyona ZORUNLU `surface` parametresi (varsayılan YOK → unutulursa `tsc` hatası); çağıran SUNUCUDA sabit verir: `app/admin/musteriler/[id]/actions.ts` → "admin" (istemciden ALINMAZ), `notes-section.tsx` → "admin", `app/api/personel/customers/[id]/notes/route.ts` → "personel". Değişen: `customer-note-access.ts`, `customer-note-submit.ts`, `actions.ts`, `notes-section.tsx`, `notes/route.ts` + testler `customer-note-access.test.ts` (etiket assert'leri + 2 yeni test: etiket role'den değil çağırandan gelir) ve `customer-note-submit.test.ts`. **Canlı kanıt (Neon, kullanıcı çıktısı):** 06:33 admin işlemleri `{"role":"admin","surface":"admin"}`; 06:46/06:47 personel panelinden yazılan notlar `{"role":"admin","length":4,"surface":"personel"}`; 05:44 satırı (düzeltme ÖNCESİ) `personel` KALDI — append-only, DÜZELTİLEMEZ. (ii) **PERSONEL NOT KUTUSU:** `components/personel/MusterilerPanel.tsx` müşteri özet kartında not kutusu (admin ile AYNI `NoteForm`: sayaç, özel veri uyarısı, çift tık kilidi; `key={detailId}` ile müşteri değişince sıfırlanır); YENİ `lib/crm/staff-note-client.ts` (`submitStaffNote`: POST `/api/personel/customers/[id]/notes`, HTTP durumu → genel mesaj, sunucu gövdesi okunmaz, ağ hatası NoteForm'a bırakılır) + `staff-note-client.test.ts` (13 test). Personel notu OKUYAMAZ; kartta "yalnız yönetici görebilir" yazar. Canlıda: kutu görünür, "Not eklendi. Notu yalnız yönetici görebilir.", not admin 360'ta listelendi, telefon maskeli. (iii) **Doğrulama:** `npx vitest run lib/crm` **24 dosya / 271 test PASS** (kullanıcı ekran görüntüsü, 09:44); deploy yeşil (kullanıcı beyanı). `npx tsc --noEmit` 09:32 koşusunda (surface düzeltmesi sonrası, personel kutusu ÖNCESİ) çıktı boştu = hatasız; kutu sonrası AYRI `tsc` çıktısı GÖRÜLMEDİ (deploy yeşil dolaylı kanıt; `next.config` hata-yoksayma ayarı kontrol EDİLMEDİ). (iv) **[✅ KISMEN KAPANDI, bkz. (7)]** ⚠️ **AÇIK (eski):** personel kutusu **STAFF ROLÜYLE canlıda DENENMEDİ** — tüm canlı testler admin hesabıyla; personelin yalnız kendi şubesindeki müşteriye yazması ve şubesiz personelin reddi yalnız kodda/testte, canlı kanıt YOK (`role:"staff"` audit satırı henüz yok) → **TB-CRM-53**; `NoteForm` admin klasöründen import ediliyor → **TB-CRM-52**; form renkleri gri/siyah, personel paneli Bowlera token'ları değil (admin'de de aynı); K-28 (sağlık notu riski/silinemezlik) onay BEKLİYOR; K-09/K-10 ✅ ve checklist v1.2 hâlâ işlenmedi; sunucu tarafı idempotency yok; TEST_MATRIX/ROADMAP/KVKK checklist verilmedi → güncellenmedi. **Sıradaki:** TB-CRM-53 staff rolüyle canlı not denemesi → 3d (etiketler, yeni tablo); küçükler: K-28 kararı, TB-CRM-51 kararı, TB-CRM-52 NoteForm taşıma, 404 kök nedeni, arama normalizasyonu; canlı öncesi TB-CRM-33…42 ve paralelde TB-01/02/03. (7) **[GÜNCEL, 2026-10-12 öğleden sonra] TB-CRM-53 staff rolüyle CANLIDA denendi:** Neon'da `staff_branches` 0 satır, roller 1 admin + 6 customer (personel hesabı YOKTU; kullanıcı: tüm hesaplar test). Test personeli Emine (`a3dc1884…`) SQL ile `staff` yapıldı, Bowlerapark'a (`8159bba4…`) atandı. 🔴→✅ **Olay:** `UPDATE … WHERE email=…` aynı e-postalı İKİ hesabı birden `staff` yaptı (Azrail `6c3e16e9…` + Emine); Azrail `id` ile `customer`'a geri alındı. Ders: rol/atama `id` ile, önce `SELECT` ile eşleşen satır sayısı; sütun adı şemadan teyit (`users.name` YOK, `display_name` var; `crm_audit_log`: id, actor, action, entity, entity_id, metadata, created_at; `staff_branches`: user_id, branch_id, created_at). **Canlı kanıt:** Müşteriler sekmesi listeleniyor, telefon `+90 5•• ••• •• 78` maskeli, 14 karakterlik not eklendi, "Not eklendi. Notu yalnız yönetici görebilir."; audit (Neon, kullanıcı çıktısı) `customer_list_viewed` 10:03:14, `customer_viewed` 10:03:25, `customer_note_add_requested` 10:04:44 — hepsi `role:"staff", surface:"personel"`, actor Emine, not metni YOK (`length:14`). Atama silinince (13:11, 13:22 ekranları) liste gelmedi, "yetkin yok ya da şube ataması yapılmamış" mesajı çıktı; atama geri yazılınca (`atama_sayisi: 1`, 13:24) liste döndü. ⚠️ **AÇIK:** başka şubedeki müşteri → 404 denenemedi (tek şube var); şubesiz denemenin audit/log kaydı ve HTTP kodu görülmedi; notun admin 360'ta görünmesi bu turda bakılmadı; atama 13:08 INSERT'inden sonra 13:22'de 0 görüldü (neden kayıtsız), son durum 1. **Yeni borçlar:** TB-CRM-54 (admin panelinden personel rol + şube ataması — kullanıcı talebi) ve TB-CRM-55 (aynı e-postayla iki hesap; `users.email` kısıtı DOĞRULANMADI). TEKNIK_BORC_CRM.md v2.7. **Sıradaki:** TB-CRM-54 mü yoksa TB-CRM-34 (`CRON_SECRET`) mi — kullanıcı kararı bekliyor; sonra K-28/TB-CRM-51 kararları → 3d. (8) **[GÜNCEL, 2026-10-12 akşam] CRM-3d etiketler: 3d-2a (arka uç) + 3d-2b (admin 360 Etiketler arayüzü) KOD ÜRETİLDİ, deploy YEŞİL (kullanıcı beyanı).** 3d, 3c'deki gibi "tek problem tek çözüm" kuralıyla iki KARAR BİLDİRİMİ'ne bölündü; kullanıcı iki bildirimden sonra dosyaların üretildiğini ve deploy'un yeşil olduğunu bildirdi. **3d-2a (arka uç, arayüz yok):** `schema.ts` `crmTags` + `customerTags`; `audit.ts` iki yeni eylem (`customer_tag_add_requested`, `customer_tag_remove_requested`); `customer-tag-params.ts` (uuid), `customer-tag-queries.ts` (listele/ekle/sil; yetki ve audit YAPMAZ), `customer-tag-access.ts` (tek kapı, `customer-note-access.ts` kalıbı) + testleri. **Kararlar (asistan önerisi):** A yetki: etiketi YALNIZ admin ekler/kaldırır/görür, personel hiçbir şey göremez · B audit sırası taze rol → doğrulama → audit → işlem, audit yazılamazsa işlem yok, metadata `{role,surface,tagId}`, etiket ADI yazılmaz · C etiket listesinin ayrı audit'i yok (360'taki `customer_viewed` kapsar) · D arşivli etiket yeni müşteriye atanamaz, mevcut atamada görünür · E kaldırma = atama satırı silinir, zaten kaldırılmışı tekrar kaldırmak hata vermez. **3d-2b (arayüz):** `customer-tag-view.ts` (saf yardımcılar), `customer-tag-submit.ts` (`customer-note-submit` kalıbı), `app/admin/musteriler/[id]/tag-actions.ts` (`surface` sunucuda SABİT `"admin"`), `tags-section.tsx` (okuma hatası bölümü düşürür, sayfa açık kalır), `tag-controls.tsx` (istemci, çift tık kilidi), 2 test dosyası (view, submit); `page.tsx`'e Notlar'ın üstüne `<TagsSection />`, başlıktaki "Etiketler sonra eklenir" notu güncellendi. Arayüz kararları: açılır liste yalnız atanmamış AKTİF etiketler + "Ekle"; "Kaldır" onaysız (geri alınabilir, ikisi de audit'li); arşivdeki etiket "(arşivde)" notuyla görünür ve kaldırılabilir; iyimser güncelleme yok (sunucu sayfayı tazeler); seçenek kalmazsa "Atanabilecek başka etiket yok"; personel panelinde etiket kodu YOK. ⚠️ **KVKK işareti (K-25, uygunluk onayı = insan):** audit satırları silinemez; `tagId` bir müşterinin hangi etiketi ne zaman aldığını sonsuza dek tutar, saklama süresi (K-24) hukuki karar → TB-CRM-19 satırı ve KVKK checklist K-24'e işlendi. ⚠️ **AÇIK / GÖRÜLMEDİ (dürüst not):** (a) kullanıcının A–E ve `tagId` dahil/hariç için AÇIK yazılı onayı görülmedi — iki bildirimle dosyaların üretilmesi örtük onay sayıldı, `tagId` DAHİL varsayıldı → TEYİT (Açık soru #19); (b) `crm_tags`/`customer_tags` tablolarının Neon'da KURULDUĞU ayrıca görülmedi — 3c dersi: deploy yeşil ≠ tablo var; `to_regclass` ile AYRI sorguda doğrulanmalı (Açık soru #20), şema notu/SQL bu turda görülmedi; (c) `tsc` ve `npx vitest run lib/crm` çıktısı/test sayısı GÖRÜLMEDİ; (d) canlı kabul testi (ekle → kaldır → tekrar ekle + `crm_audit_log` satırları `{role:"admin",surface:"admin",tagId}`) YAPILMADI; `INSERT … ON CONFLICT … RETURNING`'in Neon HTTP sürücüsünde ilk gerçek çalışması orada olacak; (e) üretilen dosyaların içeriği bu turda GÖRÜLMEDİ, liste karar bildirimlerinden alındı; (f) kritik boşluk: karar bildirimlerinde etiket OLUŞTURMA/ARŞİVLEME yolu geçmiyor — `crm_tags` boşsa ekranda hep "Atanabilecek başka etiket yok" çıkar → TB-CRM-56; (g) K-28, TB-CRM-51, TB-CRM-54/55 kararları hâlâ bekliyor; TEST_MATRIX/ROADMAP verilmedi → güncellenmedi. **Sıradaki:** Neon'da tablo teyidi → canlı kabul testi → TB-CRM-56 kararı; sonra TB-CRM-54 / TB-CRM-34 / K-28 / TB-CRM-51. (9) **[2026-10-13 — CRM-3d ✅ KAPANDI + etiketle müşteri filtresi ✅ canlı]** (8)'in AÇIK (a)(b)(d) maddeleri kapandı (silinmedi): (b) tablolar Neon'da VAR (`information_schema`); (d) canlı kabul testi yapıldı. Kanıt (2026-10-13): Neon `information_schema` ile `crm_tags` + `customer_tags` VAR; kolonlar ve kısıtlar görüldü (`customer_tags` PK `(customer_id, tag_id)`, `tag_id` FK'si CASCADE'siz, `customer_id` FK'si `ON DELETE CASCADE`, `crm_tags.name` CHECK 1–30 + trim, UNIQUE indeks `uq_crm_tags_name_lower` = `lower(name)`); ekleme canlıda ✅ (3 etiket, `customer_tags` + 3 `customer_tag_add_requested` satırı, audit satırı etiket satırından ~0,3 sn ÖNCE → fail-closed teyit); kaldırma canlıda ✅ (arayüz "Etiket yok." + `customer_tags` 0 satır + 3 `customer_tag_remove_requested`, `tagId`'ler eşleşiyor, `role:admin`, `surface:admin`); müşteri listesi etiket filtresi canlıda ✅ (Kurumsal seçilince tek müşteri; `customer_list_viewed` metadata `{page,hasQuery,hasTag:true}`). **Kararlar (kullanıcı):** TB-CRM-56 için geçici yol **B** (etiketler SQL ile oluşturulur: VIP, Sadık müşteri, Kurumsal, Yeni müşteri; "Şikayetçi" müşteriyi yargılayan ad olduğu için önerilmedi) — arayüzden oluşturma (A) ve oluşturmanın audit'i AÇIK BORÇ; etiket filtresi YALNIZ admin listesinde (personele etiket gösterilmez); `customer_list_viewed` audit'ine `hasTag` bayrağı (etiket id/adı YAZILMAZ) onaylandı. **Kod (repoya konacak 4 dosya, canlıda çalışıyor):** `lib/crm/customer-params.ts` (`?tag=` uuid doğrulaması, bozuk değer yok sayılır), `lib/crm/customer-queries.ts` (arama + etiket filtresi, `EXISTS` alt sorgusu), `lib/crm/admin-customer-access.ts` (`loadCustomerList` etiket seçeneklerini de döner, audit `hasTag`), `app/admin/musteriler/page.tsx` (etiket seçim kutusu; ilk sürümde "Ara" butonu telefonda ekran dışına taşıyordu → seçim kutusu ayrı satıra alındı). **Test (2026-10-13, Codespaces):** `npx vitest run lib/crm` → 28 dosya / 321 test PASS (ilk koşuda `customer-params.test.ts` 2 test + `admin-customer-access.test.ts` dosyası kırıktı: `parseListParams` artık `tagId` döndürüyor; `customer-tag-queries` mock'u yoktu → `server-only` import hatası; ikisi de test dosyası düzeltmesiyle kapandı, canlı kod değişmedi); `npx tsc --noEmit` hata çıktısı vermeden bitti (test dosyaları düzeltilmeden ÖNCE koşuldu, sonrası yeniden koşulmadı). ⚠️ GÖRÜLMEDİ: trigger sorgusu çıktısı (boş beklenir); yinelenen etiketi ARAYÜZDEN ikinci kez ekleme denemesi (kullanıcı kararıyla atlandı — DB tarafı PK + UNIQUE ile korumalı); `lower()` Türkçe İ/ı davranışı doğrulanmadı. Kalan: TB-CRM-56 (A yolu + audit), Açık soru #19 (`tagId` audit'te kalsın mı — yanıtsız), TB-CRM-34, TB-CRM-53 kalanı, TB-CRM-54, K-28, TB-CRM-51/55. (10) **[2026-10-14 — Şube bazlı "Tükendi": Faz 1 ✅ canlıda + Adım 5a ✅ canlıda]** (a) **Bağlam:** Faz 1 önceki sohbetlerde yapıldı ama bu dosyaya HİÇ işlenmemişti (v137 bunu bilmiyordu); bu tur kullanıcının 'YENİ SOHBET PAKETİ' beyanı + yüklenen repo zip'indeki kod varlığıyla işlendi. (b) **Faz 1 (kullanıcı beyanı; zip'te dosyaların varlığı görüldü, personel route/panel içeriği OKUNMADI):** 🗄️ `branch_item_availability` (PK `branch_id`+`menu_item_id`, `unavailable_until`, `marked_by`; `lib/db/schema.ts` yorumuna göre Neon'da `to_regclass` ile doğrulanmış), `lib/availability/*` (sunucu kontrolü `branch-item-availability.ts`, personel tarafı `staff-availability-*`), `app/api/orders/gel-al/route.ts` 409 `ITEM_UNAVAILABLE` + `unavailableItemIds`, `app/api/personel/availability/route.ts` + personel panelinde 'Ürünler' sekmesi (`hooks/usePersonelAvailability.ts`). Canlı kabul ✅ (kullanıcı beyanı + 07:06 ekran görüntüsü): Şinitzel/Burrito tükendi işaretlendi → Gel Al onayında 409 'Şu ürün(ler) bu şubede şu an tükendi: Burrito'. İşaret ertesi gün 00:00'da (İstanbul, UTC+3 sabit) kendiliğinden kalkar. Sunucu kontrolü FAIL-OPEN (DB/şube hatasında sipariş alınır, structured log — bilinçli, kullanıcı önerisi). (c) **Kök neden 🔴→✅:** test personeli Emine (`a3dc1884…`) `staff_branches`'te satırsızdı → 403 'yetkin yok ya da şube ataması yapılmamış'; Neon'da SQL ile Bowlerapark'a (`8159bba4…`) atandı, doğrulandı. (d) **Adım 5a ✅ CANLIDA (deploy yeşil, 07:06 ekran görüntüsü: Burrito gri, 'Tükendi' butonu, 120 kcal/30g protein/450₺ okunuyor):** `app/menu/page.tsx` varsayılan şubeyi `getDefaultBranchId()` ile (gel-al'la AYNI kaynak) okur, yeni `lib/availability/menu-unavailable-ids.ts` FAIL-OPEN sarmalayıcıyla tükendi id'lerini bulur; `MenuPageClient.tsx` `unavailableItemIds` → kartlara `isUnavailable`; `MenuCard.tsx` + yeni `MenuCardSoldOut.tsx`; 3 yeni test dosyası. Kararlar (kullanıcı 'Evet'): K1 kart gri, 'Sepete Ekle' yerine devre dışı 'Tükendi', görsel-tık kapalı; K2 QuickAddSheet'te içecek/tatlı gizlenmez, gri + seçilemez (5b); K3 5a/5b bölme. Tasarım: YENİ RENK YOK (DESIGN_SYSTEM §2) — görselde `grayscale opacity-60`; kalori/alerjen gizlenmez (§7.0); `whileHover`+`whileTap` BİRLİKTE kapalı (§6.3); customizer ('Özelleştir') kartı tükendi sayılmaz (sunucu kilidi onu kapsamıyor → Faz 3). Test (kullanıcı ekranı 07:09–07:10): 3 yeni dosya 20/20 PASS; `tsc --noEmit` çıktısız (hatasız). (e) **Buton rengi (kullanıcı kararı 'Evet', 2026-10-14):** nötr gri → yeşil (`bg-olive-primary/10 text-olive-primary`, mevcut Primary Olive opaklığı = yeni renk değil); `MenuCardSoldOut.tsx` güncel hali ÜRETİLDİ, push/canlı görüntü BEKLİYOR; risk: yeşil 'aktif' çağrıştırabilir (dosya başında not, geri dönüş tek satır). (f) ⚠️ **AÇIK / GÖRÜLMEDİ (dürüst not):** Madde 1 — admin panel ataması gerçekten DB'ye yazıyor mu (#165; zip'te `lib/crm/staff-admin-*.ts` VAR ama OKUNMADI, TB-CRM-54 kodu index'e işlenmeden yazılmış olabilir); 5b (#166); Faz 1 route testi `vi.clearAllMocks()` düzeltmesi sonrası 81/81 teyidi GELMEDİ + 3 dosya/7 test kırık (CategoryNav/FilterPanel, 5a'da dokunulmayan dosyalar, nedeni DOĞRULANMADI) (#167); TEST_MATRIX/ROADMAP/DEPENDENCIES/DESIGN_SYSTEM/ARCHITECTURE verilmedi/işlenmedi (#168). Kullanıcı bu işlerden sonra YENİ bir görev bildirecek (henüz belirtilmedi). (11) **[2026-10-14, bu turda, checkpoint — TB-CRM-51 ✅ + `rate-limit-memory.ts` kök neden + TB-CRM-56 ✅ (A yolu canlı)]** (a) **TB-CRM-51 (personel müşteri API hız sınırı):** kod bu turda yüklenen dosyalardan OKUNDU ve doğrulandı: `rate-limit.ts` `staffCustomers` kovası dakikada 30 istek (anahtar = `users.id`); `staff-customer-access.ts` sırası guard → hız sınırı → audit → okuma (yetkisiz istek sayaç tüketmez, reddedilen istek audit satırı yazmaz); sayaç deposu hata verirse fail-closed 429 (60 sn); `staff-http.ts` 429'u `Retry-After` (saniye, yukarı yuvarlanır, en az 1) + `no-store` ile döner; `app/api/personel/customers/[id]/route.ts` (yüklendi) sonucu `staffResultToResponse`'tan geçiriyor → liste ve detay AYNI kovayı kullanıyor. Kullanıcı: deploy yeşil. ⚠️ Canlıda gerçek 429 DENENMEDİ. (b) **Kök neden (`lib/auth/rate-limit.test.ts` 57:60 'pencere dolunca sayaç sıfırlanır' kırığı, TB-51'den bağımsız):** `rate-limit-memory.ts` `createMemoryStore(now = Date.now)` varsayılan parametresi store oluşurken GERÇEK `Date.now` fonksiyonunu yakalıyor → `vi.useFakeTimers()`/`setSystemTime` etkisiz. Düzeltme (kullanıcı 'Evet'): `now = () => Date.now()` (tek satır + başlığa not); tam dosya verildi, kullanıcı push/deploy etti (deploy yeşil). ⚠️ `rate-limit.test.ts`'in düzeltme SONRASI yeşil koşusu GÖRÜLMEDİ. (c) **Tam vitest koşusu (kullanıcı ekranı):** 1 test kırık + 'FAIL' listesi kısmen görüldü: `app/menu/page.test.tsx` (`server-only` çözülemiyor — `lib/db/client.ts`), `components/menu/FilterPanel.test.tsx` (`../FilterPanel` bulunamıyor), `components/personel/gel-al-queries.test.ts` (`./gel-al-queries` bulunamıyor), `StepProtein.test.tsx`, `lib/sandwich-catalog.test.ts`, `lib/auth/otp-store.test.ts` (nedenleri görülmedi); log satırları (`OTP_CHANNEL_FAILED`, `db.execute is not a function`) hata-yolu testlerinin çıktısı olabilir. Tam FAIL listesi (`grep "^ ?FAIL"`) ve `git status` çıktısı GELMEDİ → #167. (d) **TB-CRM-56 ✅ KAPANDI (A yolu, kullanıcı: 'canlı kontrol tamam, sorun yok'):** Neon'da doğrulandı: `crm_audit_log` üzerinde YALNIZ `crm_audit_log_pkey` var, `action` CHECK'i YOK. Adım 1 arka uç: yeni `lib/crm/customer-tag-admin-access.ts` (yalnız admin; sıra girdi doğrulama → taze rol → AUDIT → yazma; oluşturmada etiket id'si uygulamada `randomUUID()` ile ÖNCEDEN üretilir, audit `entityId` aynı id), `customer-tag-params.ts` (+`parseTagName`, `TAG_NAME_MAX`=30, kod noktası sayımı, kontrol karakteri reddi), `customer-tag-queries.ts` (+`listAllTags`, `insertTag` ON CONFLICT DO NOTHING → 'duplicate', `setTagArchived` changed/unchanged/not_found), `audit.ts` (+`crm_tag_create_requested`, `crm_tag_archive_set_requested`; metadata yalnız {role, surface, archived?} — etiket ADI YOK). Adım 2 arayüz: `app/admin/musteriler/etiketler/{page.tsx, tag-admin-controls.tsx, tag-admin-actions.ts}` (`surface` sunucuda sabit "admin"), `lib/crm/customer-tag-admin-{view,submit}.ts` (başarıda `revalidatePath`), `app/admin/musteriler/page.tsx`'e 'Etiketleri yönet' bağlantısı. Testler: `customer-tag-admin-access` 15 + `customer-tag-name` 7 + `customer-tag-admin-view` 9 + `customer-tag-admin-submit` 7 → kullanıcı ekranı 31/31 PASS (Adım 2 koşusu), `tsc --noEmit` çıktısız. Canlı: ekran açıldı, 'Etiket oluşturuldu.' görüldü, 7 aktif etiket listeli. ⚠️ AÇIK: audit satırlarının (3 satır: create/archive/unarchive; metadata'da ad YOK) Neon çıktısı GÖRÜLMEDİ; yinelenen-ad hata mesajı ve arşivle/geri al canlı adımları kullanıcı 'sorun yok' dedi ama çıktı paylaşılmadı; `customer-tag-submit.ts` (müşteri etiketi submit'i) GÖRÜLMEDİ — yeni submit kendi kalıbıyla (`revalidatePath`) yazıldı (#169). (e) **Karar (kullanıcı sorusu 'etiketleri nasıl silerim'):** etiket SİLİNEMEZ, yalnız arşivlenir (iz `crm_audit_log`'da etiket kimliğiyle durur, geri alınabilir); gerçekten silme gerekirse ayrı TB (yalnız hiçbir müşteride yoksa + audit'li) — şimdilik açılmadı (#169). (f) **Karar (kullanıcı, 2026-10-14): CRM-3 KAPANDI sayılır; 'başka şube müşterisi → 404' kontrolü ERTELENDİ** (kabul edilen açık risk: kodda yazılı ama canlıda/testle DENENMEDİ, #170(f)); **sıradaki CRM-4 (TB-CRM-20, segmentler).** Diğer: TB-CRM-34 (`CRON_SECRET`, kullanıcı tarafı); #166 (5b), #167 (test borçları), #168 (doküman senkronu). TEST_MATRIX/ROADMAP/DEPENDENCIES/DESIGN_SYSTEM/ARCHITECTURE verilmedi → GÜNCELLENMEDİ.
> > **[ÖNCEKİ TUR — 2026-10-11 (gece): CRM-3a canlı — admin müşteri listesi + 360]** (1) **Kararlar (kullanıcı):** CRM-3 dört adıma bölündü: 3a admin liste+360 salt okunur (yeni tablo YOK), 3b `staff_branches` + personele maskeli görünüm, 3c notlar, 3d etiketler. Müşteri verisi okumada **audit FAIL-CLOSED**; URL'de telefon değil `users.id` (uuid). TB-CRM-11 ✅ (`CRM_KVKK_CHECKLIST.md` v1.0 onaylı, v1.1: K-07/K-11/K-12 ✅). (2) **Kod (canlı, `lib/crm` 13 dosya / 150 test PASS):** `lib/crm/admin-customer-access.ts` (admin kontrolü + audit-önce-oku, tek kapı), `customer-queries.ts` (liste: `v_customer_stats` ⋈ `users`, 50/sayfa; 360: profil+istatistik+güncel rıza+kaynak+olay; `payload` okunmaz), `audit.ts`, `customer-params.ts`, `customer-format.ts` (Neon ham zaman damgası normalizasyonu), `app/admin/musteriler/page.tsx` + `[id]/page.tsx` (`force-dynamic`). (3) **Canlı doğrulama:** liste + 360 açıldı; `/admin/musteriler/abc` → 404; arama çalışıyor; `crm_audit_log`: `customer_list_viewed {page,hasQuery}` ve `customer_viewed {}`, `actor`/`entity_id` uuid, telefon/ad YOK. (4) **Açık/dürüst notlar:** ⚠️ `/admin/musteriler` ilk deploy'da 404 verdi, sonra açıldı — **kök neden KANITLANMADI** (eski deploy'da rota yok mu, guard `notFound()` mı; `[CRM_ACCESS_DENIED]` logu eklendi, Build Logs/log araması yapılmadı). Arama metni URL'de (`?q=`). `05…` araması `+90`'ın `0`'ıyla tesadüfen eşleşir. `users.phone` biçimi `+90xxxxxxxxxx` (teyit edildi). Ekran görüntülerinde gerçek müşteri verisi göründü (telefon/e-posta) — paylaşırken karalama önerildi. (5) **Sıradaki:** CRM-3b (`staff_branches` şeması + şema notu + personel maskeli görünüm, K-09/K-10); küçük: 404 kök nedeni, telefon arama normalizasyonu, `CRM_ACCESS_DENIED` seviyesi.
> > **[ÖNCEKİ TUR — 2026-10-11 (akşam): CRM kararları + TB-CRM-09/10/24 uygulaması]** (1) **Kararlar (kullanıcı):** TB-CRM-07 (a) müşteri sipariş öncesi şubeyi KENDİSİ seçer (tek şubede ekran yok, `getDefaultBranchId`), (b) personel `staff_branches(user_id, branch_id)` ile atandığı şubeleri görür (admin hepsini), (c) şube bazlı menü/fiyat ERTELENDİ. TB-CRM-24 `completed_at` nullable, backfill YOK, **DB trigger yazar** (asistan önerisi, kullanıcı onayı). TB-CRM-14 eşikleri: haftalık 1 ileti, sessiz saat 21:00–09:00 (mevzuat aralığı DOĞRULANMADI), holdout %10, atıf 7 gün; değerler `config.ts`'e HENÜZ girmedi. TB-CRM-13 = Vercel Cron. **Kırık testler (TB-CRM-04) CRM önkoşulu DEĞİL** (kullanıcı); CRM kapısı yalnız `lib/crm`. (2) **TB-CRM-09/10 paketi (kod, canlı, deploy yeşil):** `lib/crm/config.ts` (+`isSendingEnabled`, `getSendingMode`, `getTestPhones`), YENİ `lib/crm/sending-gate.ts` (`evaluateSendingGate`: kill switch / geçersiz telefon / test listesi / hata → ENGELLİ; her çağrıda env yeniden okunur; DB'ye gitmez, telefonu loglamaz), `sending-gate.test.ts` (21) + `sending-gate.error.test.ts` (2). Codespaces `npx vitest run lib/crm`: **8 dosya / 88 test PASS**, `tsc --noEmit` temiz. Dokümanlar (başka repoda, kullanıcı beyanı): `docs/schema-changes/_SABLON.md` (GERİ ALMA zorunlu, drift sorguları, `DO`/`TEST_OK` kalıbı), `CONFIG_SCHEMA.md` v1.5 (CRM_* + `CRON_SECRET`). (3) 🗄️ **TB-CRM-24 şema (canlı):** `docs/schema-changes/20261011170000_crm_order_completed_at.md` + `_migration.sql` + `_dogrulama.sql`; `order_history.completed_at`, fonksiyon `crm_stamp_order_completed_at`, trigger `trg_order_history_completed_at` (`BEFORE INSERT OR UPDATE OF status`; dolu değeri ezmez, aynı status'le UPDATE'te damgalamaz), `v_customer_stats`/`v_customer_branch_stats` `COALESCE(completed_at, ordered_at)` (öncesinde `reloptions` NULL teyit edildi). `schema.ts` `completedAt` repoda. Canlı: kolon `timestamptz | YES`, view'larda `completed_at` + trigger `t,t,t`; gerçek siparişlerde damga göründü (10 Ekim 12:59'da verilen sipariş `completed_at` = 11 Ekim 15:10). ⚠️ `TEST_OK` doğrulama bloğu çalıştırıldığı GÖRÜLMEDİ → ezmeme + aynı-status korumaları canlıda doğrulanmadı. (4) **Dersler/uyarılar:** (a) Yüklenen `CONFIG_SCHEMA.md` v1.3'tü, önceki "v1.4" repoda yoktu; Gmail SMTP env adları dosyada YOK (kod görülmediği için uydurulmadı). (b) `sending-gate` RIZA kapısı DEĞİL — `canSendMarketing` CRM-5. (c) `CRM_TEST_PHONES` biçimi `users.phone` ile birebir olmalı, canlı biçim DOĞRULANMADI; Vercel Production'a `CRM_SENDING_ENABLED=false`/`CRM_SENDING_MODE=test` girildi mi BİLİNMİYOR (varsayılan zaten KAPALI/test). (d) Route'lar (`app/api/personel/orders/[id]/route.ts` yalnız Masaya; Gel Al `completed` geçişi ayrı) trigger sayesinde DEĞİŞMEDİ. (e) `TEKNIK_BORC_CRM.md` v2.0'da tutarsız satırlar düzeltildi (TB-08/26 güncel durum, TB-16 simgesi, kayıp TB-27…32 numara notu). (5) **Sıradaki:** `TEST_OK` teyidi; TB-CRM-11 (KVKK kontrol listesi) veya CRM-3 (TB-07 kararlarıyla `staff_branches` + müşteri paneli); canlı öncesi TB-CRM-33…42.
> > **[ÖNCEKİ TUR — 2026-10-11 (gündüz): KVKK/çerez kapanışı — çerezli yol CANLIDA; kalanlar TB-CRM-33…50]** (1) **Kararlar (kullanıcı):** hukukçu YOK, kalan riskler yazılı kabul (`KVKK_KARAR_KAPANIS.md`). "Çerez olmadan CRM'in anlamı kalmaz" → edinim çerezi AÇIK yol. D1 = A (tek bant, açık metin, telefonla ilişkilendirme bantta yazılı; ayrı onay kutusu yok), D2 = 90 gün, D3 = A (onay sürümü satırda), D4 = B (geri çekme eski kaydı silmez; e-postayla silme başvurusu). Veri sorumlusu = Bari Akyıldız (şahıs işletmesi); vergi levhasında ticari unvan YOK → `seller.ts` `tradeName` = "Bari Akyıldız (Bowlera)". VERBİS: muaf sayıldı (ikincil kaynak, TB-CRM-36). Yurt dışı: Vercel ABD (iad1, Hobby planda), Neon Frankfurt → aydınlatmada açık yazıldı, standart sözleşme e-postası taslağı hazır (TB-CRM-35), kalan risk kabul. (2) **Kod (canlı, deploy yeşil, `tsc` temiz):** `lib/legal/seller.ts`, `terms-version.ts` (`2026-10-11-v1`), `app/kvkk/page.tsx` (§1,2,5,6,8,9: veri sorumlusu, sunucu günlüğü, aktarım, e-postayla başvuru, çerez), `app/cerez-politikasi/page.tsx` (YENİ), bant v2 (`cookie-consent-text.ts` `COOKIE_CONSENT_VERSION=2026-10-11-v2`, `CookieConsentBanner.tsx` bağlantılı), `read-attribution.ts` (`attributionConsentVersion`), `consent-registration.ts`, registration route (artık `readAttributionSafely`), `schema.ts` (+4 kolon), `app/api/cron/purge-attribution/route.ts` + `vercel.json` (günlük 03:17 UTC; `CRON_SECRET` Vercel'de, yetkisiz çağrı 401). (3) 🗄️ **Şema:** `docs/schema-changes/20261011120000_crm_attribution_retention.{md,sql}` + `_dogrulama.sql` — her iki tabloda `attribution_consent_version`, `attribution_recorded_at`; trigger `crm_stamp_attribution_recorded_at`; `attribution_summary` (anonim özet: hafta/kaynak/sayı/gerçek satış/ciro); fonksiyon `crm_purge_attribution(int, bool)`; Neon doğrulaması `TEST_OK` ✅. (4) **Test/canlı:** banner 12/12, `lib/crm` 65/65 (6 dosya), cron route 8/8 (+2 trim testi eklendi, ÇALIŞTIRILMADI), `tsc` temiz. Canlı: dry-run curl ✅ (0/0), **Kabul → kaynak + sürüm `2026-10-11-v2` + recorded_at yazıldı ✅, Reddet → hepsi NULL ✅**. Bayrak `CRM_ATTRIBUTION_ENABLED=true` Production'da AÇIK (config.ts: `=== "true"`). (5) **Güvenlik:** üç ayrı `CRON_SECRET` değeri ekran görüntülerinde göründü → TB-CRM-34 (yenile). (6) **Açık / sıradaki:** TB-CRM-33…50 (`TEKNIK_BORC_CRM.md` EK bölümü). Canlıdan ÖNCE: 33 Pro plan, 34 secret yenile, 35 e-postaları gönder, 36 VERBİS, 42 telefon. Yüksek: 37 altbilgi bağlantısı, 38 geri çekme testi + test hesapları, 39 sipariş akışı doğrulaması, 41 VKN kararı.
> > **[ÖNCEKİ TUR — 2026-10-10 (akşam): TB-CRM-26 çerez bandı — kod + test + deploy]** (1) **Karar (kullanıcı: "Senin önerin geçerlidir"):** yol A = KENDİ BİLEŞEN (yeni paket/harici script YOK). Hazır çerez aracı (CMP) reddedildi: şu an tek pazarlama çerezi var, CSP (#155) ve PayTR iFrame uyum işi çıkarır, yeni paket Kural #5 onayı ister. Kullanıcı `layout.tsx`, `AttributionCapture.tsx`, `attribution.ts` dosyalarını gönderdi. (2) **Kod (11 dosya):** YENİ `lib/crm/cookie-consent-text.ts` (⚠️ TASLAK bant metni + `COOKIE_CONSENT_VERSION=2026-10-10-taslak-v1`; çerez adı ve gün sayısı `attribution.ts`'ten türer), `lib/crm/cookie-consent.ts` (karar saklama: localStorage `bowlera_cookie_consent`, granted/denied/unknown; bozuk/eski sürüm/erişilemeyen depolama → unknown, hata fırlatmaz), `lib/crm/attribution-cookie.ts` (çerez yaz/sil/var metinleri; silme yazmayla AYNI öznitelikleri taşır), `components/layout/useCookieConsent.ts` (useSyncExternalStore, sunucuda "loading", depolama yazılamazsa bellek yedeği, `resetCookieConsent()` = onayı geri çekme), `components/layout/CookieConsentBanner.tsx` (Kabul/Reddet EŞİT düğmeler, bayrak kapalıyken görünmez, GEÇİCİ nötr sınıflar); DEĞİŞEN `components/layout/AttributionCapture.tsx` (çerez YALNIZ "granted" ile yazılır; denied/unknown'da varsa SİLİNİR; ilk temas çerezi ezilmez; onay öncesi UTM/yönlendiren yalnız useRef'te tutulur, depolamaya yazılmaz) ve `app/layout.tsx` (`attributionEnabled` yerel sabiti + Footer'dan sonra `<CookieConsentBanner enabled=… />`); 4 test dosyası (cookie-consent 15, attribution-cookie 9, CookieConsentBanner 10, AttributionCapture 12 = 46 test). (3) **Doğrulama:** Codespaces `npx vitest run` bu 4 dosya → 46/46 PASS (kullanıcı ekran görüntüsü, 17:33); deploy yeşil (kullanıcı beyanı, 17:35). Asistan ortamında vitest/jsdom kurulamadı (npm erişimi yok): aynı test dosyaları gerçek Chromium + React 19 + asistanın mini koşucusuyla 46/46 PASS; onay kapısı bilerek bozulunca testler PATLADI (mutasyon doğrulaması). `tsc` asistan ortamında yalnız React için geçici tip stub'ıyla temiz — kullanıcının `tsc --noEmit` çıktısı GELMEDİ. (4) **Genel koşu `npx vitest run lib/crm components/layout`:** 13 dosya (2 kırık / 11 geçti), 118 test (3 kırık / 115 geçti), 1 unhandled error. Kaynak: `components/layout/Header.test.tsx` ("Çıkış Yap'a tıklayınca signOut callbackUrl=\"/\"…"), yığın izinde `…enu.tsx:89` (Header'ın menü bileşeni olduğu TAHMİN). Asistanın dosyaları bu yolda DEĞİL, ama ESKİ kırık olduğu KANITLANMADI: `grep` bağ kontrolü ve kırık dosya adlarının dökümü kullanıcıdan GELMEDİ → TB-CRM-04'e işlendi. (5) **Açık/bekleyen:** Footer'a "Çerez tercihleri" bağlantısı (`Footer.tsx` GÖNDERİLMEDİ; olmadan onay geri çekilemez → bayrak açılmadan ÖNCE ŞART); bant renkleri `DESIGN_SYSTEM.md` token'larıyla değişmeli (okunmadı); hukuk onaylı bant metni + çerez politikasına `bowlera_attr` (TB-CRM-03); çerez onayı sunucuda KANITLANMIYOR (yalnız tarayıcıda) → hukuk sorusu; mobilde bantın sepet çekmecesi/sticky özet panelle z-index çakışması GÖZLE kontrol EDİLMEDİ; canlıda bandın görünmediği (bayrak kapalı) kullanıcıdan teyit EDİLMEDİ; bilinen sınırlar: onaydan önceki UTM tam sayfa yenilemede kaybolur, bayrak açıkken karar yokken mevcut `bowlera_attr` çerezi silinir; `CONFIG_SCHEMA.md` ve `TEST_MATRIX.md` paylaşılmadı (güncellenmedi). Kalan canlı doğrulama C: bayrak açıkken önce bant → Kabul → UTM'li kayıt/sipariş → `bowlera_attr` ve DB kolonları.
> > **[ÖNCEKİ TUR — 2026-10-10 (öğleden sonra, devam): CRM-2 Adım C2a + C2b — kayıt ve sipariş akışı attribution]** (1) **Kararlar:** UTM/attribution saklama biçimi = **ÇEREZ** (kullanıcı, sessionStorage önerisine rağmen). Çerez bandı sorusuna açık yanıt GELMEDİ; `app/layout.tsx`'te bant bileşeni YOK → "bant yok" VARSAYILDI (bayrak bu yüzden kapalı, açmadan önce hukuk + çerez bandı/politikası şart). Asistan varsayımları (ONAY BEKLİYOR): ilk temas (çerez varsa üzerine yazılmaz), çerez adı `bowlera_attr`, ömür 30 gün (GEÇİCİ — TB-CRM-14 atıf penceresi), yalnız UTM veya DIŞ yönlendiren site sinyalinde yazılır (doğrudan ziyaret yazılmaz → NULL), `acquisition_source` = `utm_source` ?? yönlendiren host. (2) **C2a kod (9 dosya, push + deploy yeşil — kullanıcı beyanı):** YENİ `lib/crm/attribution.ts` (saf: sanitize, UTM/referrer, çerez serialize/parse; sınırlar 64/100 = DB CHECK), `lib/crm/read-attribution.ts` (sunucu, bayrak kapısı), `components/layout/AttributionCapture.tsx` (istemci, çerezi yazar), 2 test dosyası; DEĞİŞEN `lib/crm/config.ts` (`isAttributionEnabled`, env `CRM_ATTRIBUTION_ENABLED`, varsayılan KAPALI), `app/layout.tsx` (bileşen eklendi), `consent/route.ts` (`readAttribution(request.headers)` → upsert 4. argüman), `lib/db/queries/consent-registration.ts` (attribution `values`'a yazılır, `onConflictDoUpdate.set`'e BİLİNÇLİ KONMADI = ilk temas korunur). `validation.ts`, `useRegistrationForm.ts`, `ConfirmPickupOrderButton.tsx`, `kayit-ol/page.tsx` DEĞİŞMEDİ (çerez sunucuya kendiliğinden gelir). (2b) **C2b (sipariş akışı — kullanıcı kararı: İLK TEMAS, kayıt akışıyla AYNI çerez):** `app/api/orders/gel-al/route.ts` (INSERT'e `...readAttribution(req.headers)`, 3 satır) + `lib/db/schema.ts` (yalnız yorum: sipariş kaynağı = ilk temas); `ConfirmPickupOrderButton.tsx` DEĞİŞMEDİ; push + deploy yeşil, `tsc --noEmit` temiz (kullanıcı, 14:38); `gel-al` için route testi YOK (bilinen boşluk). (3) **Doğrulama:** Codespaces `npx vitest run lib/crm` → 4 dosya / 41 test PASS (11 olay + 15 attribution + 11 rıza + 4 read-attribution); deploy yeşil. `tsc --noEmit` çıktısı paylaşılmadı. Canlıda davranış DEĞİŞMEDİ (bayrak KAPALI). Asistan ortamında route/DB/bileşen derlenemedi (npm ağı yok) — yalnız saf mantık Node ile test edildi. (4) **Açık/bekleyen:** Adım D (uygulama seviyesi test + bayrak açma öncesi uçtan uca doğrulama); `CONFIG_SCHEMA.md`'ye `CRM_ATTRIBUTION_ENABLED` (üretilmedi); çerez politikasına `bowlera_attr` (hukuk, TB-03); çerez bandı eklenince yakalama onaya bağlanmalı; `consent/route.ts` için upsert argümanlarını kontrol eden test varsa güncellenmeli (varlığı DOĞRULANMADI); bilinen sınır: aynı telefonda önceki yarım kayıt varsa kaynak sonradan doldurulmaz; `customer_registered` olay payload'ına attribution EKLENMEDİ; TB-CRM-25 (bayrak öncesi backfill tekrarı); TEST_MATRIX.md paylaşılmadı (güncellenmedi); şema notunun repoda `docs/schema-changes/` altında olduğu hâlâ TEYİT EDİLMEDİ. (5) **[Aynı gün, devam — Adım D parça 1: KULLANICI KARARI + test]** **Karar (kullanıcı "Önerin kabul"):** kaynak (attribution) okuma hatası kaydı/siparişi ASLA düşürmemeli (kaynak İKİNCİL veri) → YENİ `lib/crm/read-attribution-safe.ts` (`readAttributionSafely`: `readAttribution`'ı sarar, hata olursa `console.error` + `null`); `consent/route.ts` (import + satır 162) ve `gel-al/route.ts` (import + satır 535 spread) yalnız bu 2'şer satırla değişti. `read-attribution.ts`'in GERÇEK hâli teyit edildi: bayrak kapalı → `null`, açık → sanitize edilmiş çerez (çerez yoksa dört alanı null nesne), throw etmiyor (sarmalayıcı ikinci güvence). **Test:** YENİ `app/api/registration/consent/route.attribution.test.ts` (6 test: attribution upsert'in 4. argümanı; şifre/e-posta rıza verisine girmez; bayrak kapalı→200; 409/429'da okunmaz; throw→200 ve hesap açılır). Codespaces `npx vitest run lib/crm app/api/registration/consent` → **5 dosya / 47 test PASS** (kullanıcı ekran görüntüsü, 15:06). **Doğrulanmayanlar:** `lib/crm/read-attribution-safe.test.ts` (3 test) teslim edildi ama koşuda GÖRÜNMÜYOR → repoya eklenmedi; `tsc --noEmit` ve deploy çıktısı paylaşılmadı. Bayraklar KAPALI, canlı davranış DEĞİŞMEDİ. **[Güncelleme, aynı gün 15:48]** YENİ `app/api/orders/gel-al/route.attribution.test.ts` (6 test: kaynak INSERT'e yazılır; bayrak kapalı→kolonlar yazılmaz; okuma hatası siparişi DÜŞÜRMEZ; istemci body'sindeki sahte kaynak yok sayılır; idempotency tekrarında ve onaysız hesapta (403) kaynak okunmaz). Codespaces `npx vitest run app/api/orders/gel-al lib/crm app/api/registration/consent` → **8 dosya / 59 test PASS** (kullanıcı ekran görüntüsü; eski `gel-al/route.test.ts` 5/5 ve `online-disabled.test.ts` 2/2 dahil → #135 "route.test.ts hiç koşulmadı" test borcu KAPANDI). `gel-al` yaması (`readAttributionSafely`) repoda YERİNDE (throw→201 testi geçti). Kullanıcı MANUEL PUSH yaptı (beyan); deploy sonucu ve `tsc` çıktısı paylaşılmadı. `read-attribution.test.ts` bu koşuda 3 test gösterdi (önceki koşuda 4) — fark AÇIKLANMADI, TEYİT EDİLMEDİ. `read-attribution-safe.test.ts` hâlâ koşuda görünmüyor (repoya eklenmemiş). **Kalan Adım D:** yalnız bayrak açma öncesi canlı uçtan uca doğrulama listesi. **[Güncelleme, aynı gün — canlı doğrulama A ✅ (bayrak KAPALI)]** Kullanıcı: deploy yeşil, sipariş akışı çalışıyor; `order_history` son siparişlerinde (12:56 ve 12:59 UTC, test koşusundan sonra) `acquisition_source`/`utm_*` dört kolon NULL — beklenen davranış (kesin push saati bilinmiyor → "büyük olasılıkla yeni kodla"). **B (bayrak şartları) BEKLİYOR:** hukuk onayı (TB-CRM-03, sorumlu belirsiz), çerez bandı/politikası (TB-CRM-26 — **yol kararı kullanıcıdan BEKLENİYOR: hazır araç mı, kendi bileşen mi**), `CONFIG_SCHEMA.md`'ye `CRM_ATTRIBUTION_ENABLED` kaydı (dosya yüklenmedi, üretilmedi). **C (bayrak AÇIKKEN deneme)** yapılmadı: yalnız `CRM_ATTRIBUTION_ENABLED` açılır (diğer CRM bayrakları KAPALI — append-only tablolar), mümkünse Preview; sıra: `?utm_source=test&utm_medium=adim_d&utm_campaign=ekim` ile gizli sekme → yeni hesapla kayıt → `consent_registrations` ve `order_history` dört kolon dolu mu → ikinci UTM ile sipariş (ilk temas korunmalı) → UTM'siz doğrudan ziyaret (NULL). Geri alma: bayrağı kapat + redeploy; test satırları elle temizlenir. **Kullanıcı bu noktada checkpoint aldı ve BAŞKA HESAPTA devam edecek** (yeni sohbet paketi verildi).
> > **[ÖNCEKİ TUR — 2026-10-10 (öğleden sonra): CRM-2 Adım A + B + C1]** (1) **Tasarım ONAYLANDI (kullanıcı):** metrikler `order_history` VIEW'larından; `customer_events` append-only (`customer_registered`, `order_placed`; `order_completed` YOK — tamamlanma zamanı yok, TB-CRM-24); attribution = iki tabloda 4 nullable kolon, `channel` kullanılmaz; `customer_registered` zamanı = `users.created_at`. ⚠️ `Bowlera_CRM_Teknik_Uygulama_Plani.md` HİÇ yüklenmedi (iki kez istendi) — olay tipleri/payload plandan değil asistan önerisi. (2) **Adım A (şema) CANLIDA DOĞRULANDI:** `docs/schema-changes/20261010160000_crm2_customer_events_views_attribution.md`; `crm2_migration.sql` Neon'da koşuldu; doğrulama Bölüm 1 → `9|8|2|2|0`, Bölüm 2 → `TEST_OK` (append-only UPDATE/DELETE/TRUNCATE, `source_key` tekrarı, `event_type` CHECK, 9 durum kombinasyonu TB-05, siparişsiz müşteri 0), Bölüm 3 → `count=0`; `schema.ts` push + deploy yeşil. ⚠️ Onaylı TB-05 koşuluna EK KORUMA eklendi (`payment_status NOT IN ('iade_edildi','tutarsizlik')`) — bildirildi, açık itiraz yok, AYRI onay bekliyor. (3) **Adım B (backfill) TAMAM:** 3 `customer_registered` + 28 `order_placed` (`source_key` = `customer_registered:<users.id>` / `order_placed:<order_history.id>`); ikinci koşuda çoğalmadı (3/3/28/28). Satırlar append-only → geri alınamaz. 28 siparişin bir kısmı test/personel hesabından olabilir; `v_customer_stats` yalnız `role='customer'`. (4) **Adım C1 (kod) TAMAM:** `lib/crm/config.ts` (`CRM_CUSTOMER_EVENTS_ENABLED`, varsayılan KAPALI), `lib/crm/record-customer-event.ts` + test (`recordOrderPlacedEvent` → `gel-al/route.ts`, `recordCustomerRegisteredEvent` → `consent/route.ts`; ikisi `after()` içinde, throw etmez, log'a telefon yazmaz, bayrak kapalıyken DB'ye gitmez); `lib/crm` 22/22 PASS (11 olay + 11 rıza), deploy yeşil, canlıda davranış DEĞİŞMEDİ. (5) **Dersler:** (a) iki `route.ts` aynı anda yüklenince ilki ezildi (consent route kayboldu) — her zaman farklı ad (`consent-route.ts`, `gel-al-route.ts`). (b) Neon SQL Editor'de mobilde dosyadan kopyalama zor → SQL'i sohbette AYRI blok ver. (c) View mantığı atomik `DO` bloğu + `RAISE EXCEPTION 'TEST_OK'` ile canlıda test edildi (append-only tabloya test satırı kalmaz). (6) **Açık/bekleyen:** Adım C2 attribution yakalama — KULLANICI KARARI BEKLİYOR: UTM `sessionStorage` (önerilen) mi çerez mi; dosyalar bekleniyor: `useRegistrationForm.ts`, `app/kayit-ol/page.tsx`, `ConfirmPickupOrderButton.tsx`, `validation.ts`; Adım D; bayrak açma TB-CRM-03 (hukuk)'a bağlı; bayrak açılmadan ÖNCE backfill tekrar koşulmalı (TB-CRM-25); `CONFIG_SCHEMA.md`'ye `CRM_CUSTOMER_EVENTS_ENABLED` işlenmeli (üretilmedi); şema notunun repoda `docs/schema-changes/` altına konduğu TEYİT EDİLMEDİ; TEST_MATRIX.md paylaşılmadı; E1 Adım 5 teyidi ve spam (E3) hâlâ açık.
> > **[ÖNCEKİ TUR — 2026-10-10: CRM-0 kapanışı + CRM-1]** (1) **Kararlar:** TB-CRM-06 Adım 3 → `branch_id` nullable KALIR; TB-CRM-05 → gerçek satış = `status IN ('completed','served') AND (nakit OR payment_status='odendi')`, `confirmed` SAYILMAZ. (2) **CRM-1 Adım 1 (şema):** `marketing_consents` (append-only ledger: UPDATE/DELETE/TRUNCATE trigger'la engelli, channel/action/source CHECK), `crm_audit_log`, `iys_sync_queue`; not `docs/schema-changes/20261010150000_crm1_marketing_consents_audit_iys_queue.md`; Neon'da koşuldu, `crm1_dogrulama.sql` → `TEST_OK`, `count(*)=0`; `schema.ts` push edildi. (3) **CRM-1 Adım 2 (kod):** `lib/crm/config.ts` (bayrak, varsayılan KAPALI), `consent-text.ts` (⚠️ TASLAK metin+`policy_version`, hukuk onayı YOK), `record-marketing-consents.ts` (+test, 11/11 PASS), `consent/route.ts` hesap açıldıktan sonra tek çağrı (hata kaydı düşürmez), form/hook/page bayrağa bağlı kutular. `validation.ts`'e dokunulmadı. Push+deploy yeşil, `tsc` temiz, canlı form çalışıyor, kutular görünmüyor. (4) **Dersler/uyarılar:** (a) Neon HTTP sürücüsü transaction DESTEKLEMEZ → rıza→kuyruk→denetim sıralı yazılır; rıza satırı kaynak. (b) `lib/db/client.ts` `server-only` import ediyor → testlerde `vi.mock("@/lib/db/client")` şart. (c) Append-only tabloya test satırı yazılırsa silinemez — doğrulama `DO $$ … RAISE EXCEPTION` ile atomik geri alınır. (5) **Açık/bekleyen:** TB-CRM-03 hukuk sorumlusu atanmadı (bayrağı açmanın ön şartı); IP saklama süresi + silme talebi↔append-only çakışması (CRM-7'de kontrollü erase yolu) TASARLANMADI; E1 Adım 5 (tam metinli sipariş e-postası) push/test teyidi hâlâ YANITSIZ; TEST_MATRIX.md bu turda paylaşılmadı (güncellenmedi); `CONFIG_SCHEMA.md` v1.4 üretildi (kullanıcı repoya taşıyacak).
