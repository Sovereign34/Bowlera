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
> ⚠️ BEŞİNCİ DERS (2026-08-08, DÖRDÜNCÜ DERS'in TEKRARI): `types/index.ts`/`auth.ts`/
> `middleware.ts` kodu üretilip [KARAR BİLDİRİMİ] ile sunulmuştu (confidence MEDIUM, 2 açık
> varsayım: 403-vs-redirect kararı + `next-auth.d.ts` görülmedi) — ama kullanıcı onayı
> gelmeden ve SESSION_INDEX güncellenmeden sohbet kesildi. Kullanıcı üretilen 3 dosyayı +
> AGENT.md/CORE.md/SESSION_INDEX.md'yi yeni sohbete taşıyarak güncellemeyi GERİYE DÖNÜK
> yaptırdı — DÖRDÜNCÜ DERS'teki mekanizmanın birebir tekrarı. Ek bulgu: dosyalar arası
> senkron kontrolünde `types/index.ts`'in kendi iç yorumu ("auth.ts HENÜZ bu alanı set
> etmiyor") GÜNCEL DEĞİL — auth.ts fiilen zaten `role`'ü JWT/session callback'lerine
> set ediyor. Bu, "üç dosya senkron" iddiasının TAM doğru olmadığını gösteriyor (kod
> senkron, ama açıklayıcı yorum bloklarından biri geride kalmış — bkz. Açık Sorun #72).
> Kural pekiştirildi: KARAR BİLDİRİMİ + kod üretimi sonrası kullanıcı onayı/checkpoint
> gelmeden sohbet kapanma riski varsa, en azından AÇIK SORUN olarak loglanmalı — bu turda
> yapılıyor.
> ⚠️ ALTINCI DERS (2026-08-09, DÖRDÜNCÜ/BEŞİNCİ DERS'in ÜÇÜNCÜ TEKRARI): #75 üzerinde
> derin bir çözüm turu yapıldı (3 iterasyon: `useRef`→`useState` görsel geri bildirim,
> süre-bazlı kilit→seçim-kimliği kilidi, tekil `lockedKey`→`Set<string> addedKeys` — testin
> yakaladığı gerçek bir tasarım hatası düzeltildi) — ama sohbet, testlerin YENİDEN
> koşturulduğu/geçtiği, `npm run build`'in yerel doğrulandığı VE commit+push'un fiilen
> yapıldığı teyit edilmeden kesildi. Kullanıcı yine tam sohbet metnini yeni bir sohbete
> taşıyarak güncellemeyi GERİYE DÖNÜK yaptırdı. Kural aynı: bu üç ders artık tek seferlik
> istisna değil, TEKRARLAYAN bir kalıp — checkpoint sorusu (Bölüm 7.2) her büyük görev
> ADIMINDAN sonra (sadece görev TAMAMEN bitince değil) daha sık sorulmalı; mümkünse ara
> KARAR BİLDİRİMİ'nden hemen sonra SESSION_INDEX'e "beklemede" statüsüyle taslak satır
> düşülmeli, sohbetin kesilme anını beklemeden.
> ⚠️ YEDİNCİ DERS (2026-08-09, DÖRDÜNCÜ/BEŞİNCİ/ALTINCI DERS'in DÖRDÜNCÜ TEKRARI): #79'un
> masaüstü ayağı (`SummaryPanel.tsx`) + iki test dosyası (`SummaryPanel.test.tsx`,
> `MobileSummaryDrawer.test.tsx`) düzeltildi, `npm run build` yerelde temiz koştu, kullanıcı
> 3 dosyayı GitHub'a manuel kaydettiğini onayladı. Ajan SESSION_INDEX.md'yi TAM DOSYA olarak
> üretmeye başlamıştı (400 satır eşiği geçildiği için önce 2 eski CURRENT FOCUS bloğunun
> `session_arşiv_1.md`'ye taşınacağını bildirmişti) — ama bu işlem TAMAMLANMADAN sohbet
> kesildi. Kullanıcı yine tam sohbet metnini yeni bir sohbete taşıyarak güncellemeyi GERİYE
> DÖNÜK yaptırdı. Kural aynı, artık dördüncü kez doğrulandı: checkpoint/dosya-üretimi
> "başladım" demek "bitti" demek değildir — bir TAM DOSYA üretimi yarım kalmışsa, session
> kapanmadan ÖNCE tamamlanmalı ya da en azından hangi adımda kaldığı AÇIK SORUN olarak
> ayrıca loglanmalı, sadece niyet belirtmek yeterli değil.

---

## 🎯 CURRENT FOCUS

> **[YENİ SOHBET (devamı, 10.), 2026-08-09 — #74 TAM KAPANDI ✅]**
> **(1) Kod:** Çıkış (sign-out) mantığı `Header.tsx`'ten ayrıştırılıp `AccountMenu.tsx`'e
> taşındı — hesap ikonuna tıklanınca "Hesabım"/"Çıkış Yap" menüsü açılıyor, next-auth'un
> hazır `signOut({ callbackUrl: "/" })` fonksiyonu kullanıldı, yeni backend gerekmedi.
> **(2) Test sürecinde bulunan gerçek bug:** `AccountMenu.test.tsx` (7 test, happy+edge+
> failure) yazılırken failure testi bir açık ortaya çıkardı — `signOut()` çağrısı promise
> reject olduğunda yakalanmıyordu (unhandled rejection), oysa dosyanın kendi yorumu "sessiz
> başarısızlık" davranışını öngörüyordu. `.catch(() => {})` eklenerek koddaki gerçek
> davranış, yorumdaki niyetle hizalandı.
> **(3) Test altyapısı düzeltmesi:** İlk koşuda mock'un varsayılan dönüş değeri
> tanımsızdı (`signOutMock` her çağrıda `undefined` dönüyordu), `.catch()` eklenince
> `undefined.catch()` senkron `TypeError` fırlattı — `beforeEach`'e
> `signOutMock.mockResolvedValue(undefined)` eklenerek çözüldü.
> **(4) CANLI + TEST DOĞRULAMA TAM:** `npx vitest run AccountMenu` → 7/7 PASS, 0 error
> (üç iterasyonluk teşhis: önce component'te unhandled rejection, sonra "hangi test"
> yanlış atfı, sonunda mock'un varsayılan resolved value eksikliği bulundu ve düzeltildi).
> Third Lesson'ın gerektirdiği hem kod+build hem test koşusu kontrol noktaları geçildi.

> **[YENİ SOHBET (devamı, 9.), 2026-08-09 — #62 MASAYA SEKMESİ UÇTAN UCA TAMAMLANDI VE
> CANLIDA DOĞRULANDI ✅ — #70 KAPANDI]**
> **(1) Şema genişletmesi (#62+#70 birleşik karar):** `order_history`'ye `status`
> (`text NOT NULL DEFAULT 'pending'`), `table_number` (`text`, nullable — masa adları
> sayısal olmayabilir), `customer_notes` (`text`, nullable) eklendi. Şema notu:
> `docs/schema-changes/20260809140000_order_history_status_tablenumber_customernotes_eklendi.md`.
> Migration (`ALTER TABLE` + `status` üzerine `CREATE INDEX`) Neon'da koşuldu, Tables
> görünümünde DOĞRULANDI (ekran görüntüsü). #70'in iki açık sorusu kapandı: tip=`text`,
> index sadece `status`'ta (`table_number` filtrelenmeyecek, sadece görüntülenecek).
> **(2) `types/index.ts`:** `DineInOrderStatus`/`PickupOrderStatus`/`OrderStatus`,
> `OrderItemSummary`, `OrderHistoryEntry` tipleri eklendi — panelin okuma modeli.
> **(3) KRİTİK güvenlik düzeltmesi:** Panel API route'ları (`/api/personel/orders/*`)
> planlanırken fark edildi — `middleware.ts`'in matcher'ı SADECE `/personel/:path*`
> kapsıyordu, `/api/personel/*` guard'sızdı (yetki sızıntısı riski, personel olmayan
> biri API'yi doğrudan çağırabilirdi). Kullanıcı onayıyla bu turda düzeltildi: matcher'a
> `/api/personel/:path*` eklendi, guard mantığı API rotalarında JSON 401/403, sayfalarda
> eski davranış (redirect/403 metin) döner. Aynı dosya zaten değiştiği için içindeki
> eski "TASARIM KARARI (teyit bekliyor)" yorumu da senkronize edildi (SESSION_INDEX'e göre
> bu karar zaten kapanmıştı, sadece yorum geride kalmıştı — ayrı görev açılmadı).
> **(4) Kod üretildi (10 dosya):** `lib/personel/order-status.ts` (durum makinesi —
> sunucu tarafında SADECE bir sonraki duruma geçişe izin verir, geri gitme/atlama
> reddedilir), `lib/personel/api-guards.ts` (`requireStaffSession()` — middleware'e ek
> defense-in-depth), `lib/personel/queries.ts` (DB sorguları route handler'lardan ayrık),
> `app/api/personel/orders/route.ts` (GET — aktif dine-in kuyruğu), `app/api/personel/orders/[id]/route.ts`
> (PATCH — durum ilerletme, sunucu tarafı validasyonlu), `hooks/usePersonelOrders.ts`
> (5sn polling — ARCHITECTURE.md §2.9a "real-time=polling" kararı), `components/personel/OrderCard.tsx`
> + `MasayaPanel.tsx` (DESIGN_SYSTEM.md paleti — Cream arka plan, Primary Olive CTA
> arbitrary value `bg-[#53502A]`, bkz. #73), `app/personel/page.tsx`.
> **(5) Edge case'ler ele alındı:** boş kuyruk ("Aktif sipariş yok"), `tableNumber: null`
> güvenli gösterim ("—"), network hatası UI'ı çökertmiyor (sessiz retry + banner),
> geri/atlama-durum geçişi UI'dan mümkün değil (sadece sıradaki durum butonu gösteriliyor).
> Bilinçli ERTELENEN: eşzamanlı iki personelin aynı siparişi güncellemesi (optimistic lock
> yok, son yazan kazanır), polling'in sekme arka plandayken duraklatılmaması (Page
> Visibility API) — İKİSİ DE Açık Sorunlar'a not düşüldü (#81, aşağıda).
> **(6) CANLI DOĞRULAMA TAM — Üçüncü Ders'in gerektirdiği ikinci kontrol noktası geçildi:**
> `npm run build` yerelde ve Codespaces'te temiz koştu (route tablosunda `/personel` +
> `/api/personel/orders(/[id])` hatasız listelendi), git push yapıldı, Vercel deploy
> YEŞİL. Canlıda gerçek bir engelle karşılaşıldı ve ÇÖZÜLDÜ: kullanıcının `users.role`'ü
> hâlâ `customer`'dı (staff olarak hiç set edilmemişti) — Neon'da elle `UPDATE` ile
> `staff`'a çevrildi, ardından **JWT/session eski rolü taşımaya devam ettiği için** (aynı
> kalıp: #59'daki `SessionProvider` cache sorunu) kullanıcı çıkış yapıp yeniden giriş yaptı
> (çıkış butonu olmadığı fark edildi — bkz. #74 güncellemesi altta — `/api/auth/signout`'a
> doğrudan gidilerek aşıldı). Yeniden girişten SONRA `/personel` 403 vermeden açıldı.
> Neon'da elle 1 test siparişi (`dine-in`, masa "Bahçe 3", not "Az baharatlı olsun")
> eklendi — panelde doğru kart olarak göründü (masa no, saat, ürün, not, "Bekliyor"
> rozeti). "Hazırlanmaya Başla" butonuna tıklandı — durum "Hazırlanıyor"a geçti, buton
> etiketi "Hazır Olarak İşaretle"ye döndü, polling listeyi otomatik tazeledi. **PATCH →
> durum makinesi validasyonu → DB güncelleme → polling tazelemesi → UI güncellemesi**
> zincirinin TAMAMI canlıda kanıtlandı.
> **#62 KAPSAM NOTU:** SADECE Masaya sekmesi bu turda kapandı (§2.9a kararı — "önce Masaya,
> Gel Al ayrı tur"). Gel Al onay kuyruğu HENÜZ YAZILMADI, #62 bu nedenle TAM kapanmadı —
> Masaya kısmı ✅, Gel Al kısmı için #62 açık kalıyor (aşağıda SIRADAKİ GÖREVLER'de).

> **[YENİ SOHBET (devamı, 8.), 2026-08-09 — #79'un iki test dosyası + masaüstü ayağı
> düzeltildi, BUILD TEMİZ, GitHub'a MANUEL KAYDEDİLDİ — CANLI DOĞRULAMA HÂLÂ BEKLİYOR]**
> **(1) `MobileSummaryDrawer.test.tsx` teşhisi:** Hata, önceki turda üretilen koddan değil,
> ESKİ bir test mock'undan kaynaklanıyordu — `setupStore()` #75 döneminden (henüz
> `isReadyToAddToCart` yokken) kalmıştı. Çözüm: mock'a gerçek store'daki mantığın aynısı
> (`base`+`main`+`signatureFlavor` kontrolü) eklendi. Kod hatası değildi, sadece test dosyası
> güncellendi.
> **(2) `SummaryPanel.tsx` (masaüstü) doğrulandı:** #79'un AYNISI burada da vardı — buton
> `isStepValid(5)`'e göre aktifleşiyordu, Finish adımı opsiyonel olduğu için `selections` boş
> olsa bile her zaman `true` dönüyordu. Çözüm: `isStepValid` yerine `isReadyToAddToCart()`
> kullanılacak şekilde güncellendi (SADECE 2 satır) — store'da hiçbir değişiklik gerekmedi,
> metod zaten mevcuttu.
> **(3) `SummaryPanel.test.tsx` güncellendi:** `mockStore()`'daki `overrides.isValid` zaten
> genel amaçlı bir "buton aktif mi" bayrağıydı, `isReadyToAddToCart`'a aynen bağlanınca mevcut
> 4 test DEĞİŞMEDEN geçti. 1 test adı (`isStepValid(5)` referansı) güncellendi, #79'un
> masaüstü regresyon senaryosu için 1 yeni test eklendi.
> **Değişen dosyalar (bu turda):** `SummaryPanel.tsx`, `SummaryPanel.test.tsx`,
> `MobileSummaryDrawer.test.tsx`. (Not: `MobileSummaryDrawer.tsx` ve `useCustomizerStore.ts`
> bu turdan ÖNCEKİ turda zaten GitHub'a kaydedilmişti.)
> **Doğrulama:** `npm run build` yerelde koşuldu, route tablosu hatasız üretildi (temiz
> çıktı) — build BAŞARILI kabul edildi. Kullanıcı git push kullanmadan yukarıdaki 3 dosyayı
> GitHub'a MANUEL kaydettiğini onayladı.
> ⚠️ **KISMEN KAPANDI — Üçüncü Ders gereği:** #79 tam "KAPANDI" değil. **MOBİL taraf
> CANLIDA DOĞRULANDI** (kullanıcı: "Sepete Ekle sorunu çözüldü" — mobilde test edildi,
> boş seçimle artık öğe eklenmiyor). **MASAÜSTÜ (`SummaryPanel.tsx`) HÂLÂ DOĞRULANMADI** —
> aynı fix'in orada da çalıştığı ayrıca GÖRSEL olarak teyit edilmeli. #75 de aynı gerekçeyle
> KISMEN açık: mobil senaryo (bu turda test edilen boş-seçim/₺0 belirtisi) düzeldi, ama
> #75'in kendi orijinal belirtisi (çift tık → duplicate ekleme) bu turda AYRICA test
> edilmedi — o da doğrulanmadan #75 tam kapanamaz.
> ⚠️ Bu turun kendisi de YARIM KALDI — bkz. YEDİNCİ DERS (yukarı).
> **[ÇÖZÜLDÜ — 2026-08-09, mobil canlı doğrulama]** Kullanıcı önceki turda paylaştığı
> ekran görüntüsündeki (Base/Main/Flavor boş, "Sepete Ekle" görsel olarak aktif stildeydi)
> butona fiilen tıkladı ve "Sepete Ekle sorunu çözüldü" olarak onayladı — boş seçimle artık
> sepete öğe eklenmiyor. Görsel stil sorusu (buton gradient'inin disabled durumunu
> göstermemesi) önemsiz kaldı — davranış doğru, sadece kozmetik bir ayrım olabilir, ayrı
> bir görev olarak açılmadı (öncelik yok, kullanıcı rahatsız olmadı). **KALAN:** masaüstü
> (`SummaryPanel.tsx`) aynı senaryoyla canlıda test edilmeli.

> ⚠️ **Arşiv taşıması — 2026-08-09:** 6 kapanmış CURRENT FOCUS bloğu (#62 kod kapanışı,
> BEŞİNCİ DERS, `users.role` migration, şema notu üretimi, masa numarası kararı,
> channel-options.ts build kırığı) `session_arşiv.md`'ye taşındı — CORE.md §7.1 Adım 1
> (400 satır eşiği). Taşıma bloğu ayrı artifact olarak sunuldu, kullanıcı kendi
> `session_arşiv.md`'sinin sonuna ekleyecek.

> ⚠️ **Arşiv taşıması — 2026-08-09 (devamı):** 2 kapanmış CURRENT FOCUS bloğu ("5 yeni
> bug/UX tespiti — #74-78 açılışı" ve "#76+#77 kod+test tamam, deploy yeşil, canlı doğrulama
> bekliyor") + eski "KAPANDI (önceki tur)" anlatı bloğu (#59, #72, `users.role` migration,
> 1d) `session_arşiv_1.md`'ye taşındı — CORE.md §7.1 Adım 1 (400 satır eşiği). Kapanış
> gerekçesi: hepsinin içeriği SESSION_INDEX'te kalıcı olarak başka yerde temsil ediliyor —
> #74-78 açılışı Açık Sorunlar tablosunda satır olarak duruyor, #76/#77'nin canlı doğrulaması
> "KAPANDI (YENİ SOHBET, bu turda ✅)" notuyla, #59/#72/users.role/1d ise Kritik Kararlar
> tablosu ve GENEL DURUM satırlarıyla zaten kapanmış görünüyor; turn-by-turn anlatı artık
> aktif takip gerektirmiyor. Taşıma bloğu ayrı olarak sunuldu, kullanıcı kendi
> `session_arşiv_1.md`'sinin sonuna ekleyecek.

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
| 🗄️✅ | **[BU TURDA — #62 MASAYA SEKMESİ UÇTAN UCA TAMAMLANDI + CANLI DOĞRULANDI]** `order_history` şeması genişletildi (`status`/`table_number`/`customer_notes`, migration koşuldu+doğrulandı, #70 KAPANDI). `middleware.ts` matcher'ına `/api/personel/:path*` eklendi (ÖNCEDEN korumasız olan API guard açığı kapatıldı). 10 dosya (durum makinesi, API route'ları, polling hook'u, `MasayaPanel`/`OrderCard`, sayfa) kodlandı. Canlıda gerçek bir test siparişiyle PATCH→durum makinesi→DB→polling→UI zinciri UÇTAN UCA doğrulandı (ekran görüntüleriyle). | ✅ Masaya kısmı TAMAM, canlı doğrulandı. Gel Al onay kuyruğu ayrı tur (#62 bu yüzden tam kapanmadı). |

*(Tam gerekçe/tarih dökümü için: `session_arşiv.md` [Session 0-10], `session_arşiv_1.md` [Session 11+].)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor | `ARCHITECTURE.md` §2.4 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi | `lib/customizer-data.ts` |
| 27 | 🟢 | Hero.tsx KAPANDI. StepBase.tsx hâlâ â içeriyor | `components/customizer/StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — PARKLI (`users` tablosunun hâlâ 0 satır olmasının kök nedeni) | `lib/auth/send-otp.ts` |
| 34 | 🟢 | `VisualPreview.tsx`'in `className` davranışı — tam repo taraması eksik | `components/customizer/VisualPreview.tsx` |
| 38 | 🟠 | **[Bu turda kısmen çözüldü]** `ProfileForm.tsx`'teki `bg-olive-600` KIRIKTI (tanımsız sınıf) — `bg-olive-primary`'ye çevrildi, O DA derlenmedi (bkz. #73). Kalıcı çözüm: `bg-[#53502A]` (arbitrary value). `RegistrationForm.tsx`'in Tailwind sınıfları hâlâ TAM teyit edilmedi — #73 bulgusuna göre AYNI riski taşıyabilir. | `components/registration/RegistrationForm.tsx` |
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
| 62 | 🟡 | Personel Sipariş Paneli — **Masaya sekmesi BU TURDA TAMAMLANDI + canlı doğrulandı** (UI, API route'ları, polling, durum makinesi — hepsi çalışıyor). **KALAN:** Gel Al ilk-sipariş manuel onay kuyruğu (§2.9a'da "ayrı tur" olarak bilinçli ertelenmişti) HENÜZ YAZILMADI. | ARCHITECTURE.md §2.9a |
| 63 | 🟠 | `npm install`: 12 açık/3 kritik güvenlik açığı — `npm audit fix --force` bilinçli KOŞULMADI | `package.json` |
| 66 | 🟢 | İmza kase "Sepete Ekle" butonu (customize'a girmeden direkt ekleme) guest gate middleware'i tarafından YAKALANMIYOR — component-seviyesi guard gerekiyor. **[Session 12 devamı, kapsam teyidi]:** bu, `/menu/customize/*` (Gel Al) bağlamına özgüdür — Masaya artık ayrı `/masaya-siparis/*` yüzeyinde olduğu ve zaten auth gerektirmediği için bu sorunla kesişmiyor. AÇIK KARAR (kullanıcıdan teyit bekliyor): 1b'nin ayrı alt-görevi mi, bilinçli açık mı? | `components/customizer/AddToCartButton.tsx` |
| 70 | ✅ | **[BU TURDA KAPANDI]** `order_history.table_number` tipi `text` olarak kararlaştırıldı (masa adları sayısal olmayabilir), index sadece `status` üzerine eklendi (`table_number` filtrelenmeyecek). Migration Neon'da koşuldu ve DOĞRULANDI. | `docs/schema-changes/20260809140000_order_history_status_tablenumber_customernotes_eklendi.md` |
| 71 | 🟠 | DEPENDENCIES.md, `RegistrationChannel`'ın tüketicisi olarak `channel-options.ts`'i (ve muhtemelen görülmemiş başka dosyaları) listelemiyor — #68 kapanırken bu dosya atlandığı için canlı build kırılmıştı (düzeltildi, 1d KAPANDI). DEPENDENCIES.md bu sohbette paylaşıldı ama v1.1 (Session 3) — genel olarak ESKİ, `RegistrationChannel` tüketicileri dahil yeni alan/tablo/store değişiklikleri (tableId, order_history, users.role, vb.) hiç yansımamış. Ayrı bir turda kapsamlı güncellenmeli. | `DEPENDENCIES.md` |
| 73 | 🟠 | `tailwind.config.ts`'teki `extend.colors` custom token'ları (`olive-primary` doğrulandı, muhtemelen `olive-deep`/`bronze`/`espresso` de) `bg-*` sınıfı olarak KULLANILDIĞINDA derlenmiyor — `bg-red-500` (standart) çalışıyor, `bg-olive-primary` (custom) çalışmıyor, `bg-[#53502A]` (arbitrary) çalışıyor. Kök neden BULUNAMADI. **[Bu turda ek kanıt]:** `AddToCartButton.tsx`'te de AYNI kırık pattern görüldü (#50'de "hiç görülmedi" idi), aynı `bg-[#53502A]` workaround'ıyla düzeltildi — üçüncü dosyada doğrulanan tekrar, sistematik tarama gerekliliğini pekiştiriyor. `text-olive-primary`'nin çalışıp çalışmadığı hâlâ TEYİT EDİLMEDİ. | `tailwind.config.ts`, tüm `bg-{custom-token}` kullanan dosyalar |
| 81 | 🟢 | **[YENİ, bu turda — bilinçli erteleme]** Masaya Paneli'nde (1) iki personelin aynı siparişi eşzamanlı güncellemesine karşı optimistic lock yok (son yazan kazanır), (2) `usePersonelOrders` polling'i sekme arka plandayken duraklamıyor (Page Visibility API kullanılmadı). İkisi de MVP kapsamı dışı bırakıldı, kullanım yoğunlaşırsa ele alınmalı. | `hooks/usePersonelOrders.ts`, `app/api/personel/orders/[id]/route.ts` |
| 80 | 🟢 | **[YENİ — kullanıcı kararıyla, 2026-08-09]** #79/#75 kapatıldı (mobil canlıda doğrulandı: "Sepete Ekle sorunu çözüldü"). Masaüstü (`SummaryPanel.tsx`) fix'i AYRICA canlıda doğrulanmadı — kod+test tarafı aynı (`isReadyToAddToCart()`), risk düşük görülüyor ama not olarak açık bırakılıyor. #75'in orijinal çift-tık/duplicate senaryosu da bu turda ayrıca test edilmedi. | `components/customizer/SummaryPanel.tsx` |
| 78 | 🟢 | **[Kaynak bileşen bu turda teyit edildi — UX çözümü hâlâ AÇIK]** Customizer'da collapsed sticky özet panel (fiyat/kalori satırı + ▲ ikonu) seçim anında "Sepete Ekle" butonunu ve Base/Main/Flavor özetini GİZLİYOR — panel manuel genişletilmeden görünmüyor. Kaynak bileşenin `MobileSummaryDrawer.tsx` olduğu bu turda doğrulandı (bkz. #75) — SADECE o dosyadaki build-kırığı prop eksikliği düzeltildi, panel-görünürlüğü UX çözümüne bilinçli olarak DOKUNULMADI (Kural #5, ayrı karar). CORE.md §8 mimari varsayımı "Özet panel her zaman görünür... asla gizlenmez" ile çelişiyor. Çözüm yönü henüz kararlaştırılmadı (varsayılan yarı-açık / mikro-metin / otomatik ilk-açılış seçenekleri konuşuldu). | `components/customizer/MobileSummaryDrawer.tsx` |

> **KAPANDI (BU TURDA ✅):** #74 — `AccountMenu.tsx`'e çıkış (sign-out) butonu eklendi,
> `AccountMenu.test.tsx` (7/7 PASS, 0 error) yazıldı, test süreci `signOut()`'un yakalanmamış
> reject durumunu ortaya çıkardı ve `.catch(() => {})` ile düzeltildi. Kod+build+canlı
> doğrulama+test kapsamı hepsi tamamlandı.
>
> **KAPANDI (kullanıcı kararıyla, bu turda):** #79 + #75 — mobil canlıda doğrulandı
> ("Sepete Ekle sorunu çözüldü"), kullanıcı kararıyla kapatıldı. **Not olarak açık
> bırakıldı — bkz. #80:** masaüstü (`SummaryPanel.tsx`) aynı fix AYRICA canlıda
> doğrulanmadı; #75'in orijinal çift-tık/duplicate senaryosu da bu turda test edilmedi.
> Gerekçesiz düşürülmedi — CORE.md §7.1 Adım 1 uyarınca #80 açık sorun olarak devam ediyor.
>
> **KAPANDI (BU TURDA):** #50 — `AddToCartButton.tsx` artık görüldü, BSC-6 doğrudan ele
> alındı (bkz. #75). Not: #75'in KENDİSİ henüz kapanmadı (test/build/push/canlı doğrulama
> bekliyor) — sadece #50'nin "dosya hiç görülmedi" durumu sona erdi.
>
> **KAPANDI (YENİ SOHBET, bu turda ✅):** #76 + #77 — kod+test geçen turda tamamlanmıştı,
> BU turda kullanıcı canlı ortamda TAM DOĞRULADI (CORE.md Üçüncü Ders'in gerektirdiği ikinci
> kontrol noktası): sepet → "Siparişi Onayla" → `/siparis`'e doğru yönlendi (#76 KAPANDI),
> `/siparis`'te SADECE "Gel Al" görünüyor, "Masada" seçeneği tamamen kayboldu (#77 KAPANDI).
> Not: "Gel Al" butonuna tıklayınca görünürde değişiklik olmaması BEKLENEN davranış — buton
> zaten seçili/idempotent (`aria-pressed=true`), tek seçenek kaldığı için tıklama aynı değeri
> tekrar set ediyor. WhatsApp butonunun pasif/gri olması da AYRI ve bilinen bir durum — şube
> telefon numaraları henüz tanımlanmadı (#58'in henüz kapanmamasının doğrudan sonucu, YENİ
> bug değil).

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

*(Tam turn-by-turn detay: `session_arşiv.md` [0-10], `session_arşiv_1.md` [11+].)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel. `lib/db/schema.ts` (users.role eklendi) kullanıcı tarafından manuel push edildi. ✅ Önceki turdaki `channel-options.ts` build kırığı düzeltildi, Vercel deploy YEŞİL (1d KAPANDI). |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 kod ile hizalı — ⚠️ ROADMAP.md'ye #62 (Personel Sipariş Paneli) hiç işlenmemiş, ayrı bir oturum/kalem olarak eklenmesi gerekebilir. ARCHITECTURE.md v1.12'ye güncellendi, henüz koda tam yansımadı (DB var, kod yok). |
| Test Suite | 🟢 `guest-gate.test.ts` (8 — kullanıcı tarafından koşuldu, PASS doğrulandı). Genel `npm test` hâlâ tekrar çalıştırılmadı. ⚠️ `users.role` migration'ı için TEST_MATRIX.md güncellemesi BEKLEMEDE (dosya paylaşılmadı). |
| Auth | 🟡 Twilio/Netgsm PARKLI. Genel giriş/kayıt akışı karar olarak netleşti, guest gate middleware'i KODLANDI ve repoda doğrulandı. Masaya Sipariş kanalı middleware'in kapsamı dışında AYRI bir yüzeyde (`/masaya-siparis/*`) yaşayacak — bu yüzey henüz kodlanmadı. Gel Al akışı için "Sepete Ekle" bypass guard'ı (#66) hâlâ eksik. **[Bu turda]** `/personel/*` role bazlı guard'ı ✅ TAMAMLANDI — 4 dosya (`types/index.ts`, `auth.ts`, `middleware.ts`, `types/next-auth.d.ts`) senkron, canlı build yeşil doğrulandı. |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE canlıda test edildi (#39 KAPANDI). ⚠️ Kaydet butonu `bg-olive-600` (kırık) → `bg-[#53502A]` (arbitrary value, çalışıyor) — kök neden #73'te açık. |
| Kullanıcı Kaydı (rıza esaslı) | 🟢 Backend+Frontend TAMAM, canlı test BAŞARILI, oturum+isim gösterimi DOĞRULANDI (#59 KAPANDI). Kanal seçimi zorunlu adımı henüz KODLANMADI (bkz. 1b). |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı, SADECE Gel Al'a özel (§2.9). Masaya kendi bağımsız mini-checkout'unu kullanacak (ARCHITECTURE.md v1.8) — henüz KODLANMADI. |
| Veritabanı | 🟢 Neon Postgres çalışıyor. `consentRegistrations` ve `order_history` migrate edildi. **[Bu turda]** `users.role` (`text`, `NOT NULL`, `DEFAULT 'customer'`) migrate edildi ve DOĞRULANDI (Tables görünümü, screenshot). `users` tablosu hâlâ 0 satır (#32 Twilio kısıtı). ⚠️ DB şifresi reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik (#63). ⚠️ `order_history.table_number` kolonu KARARLAŞTIRILDI, migration HENÜZ KOŞULMADI — tip netleşmeden koşulmamalı (#70). |
| Personel Sipariş Paneli (#62) | 🟢 **Masaya sekmesi TAMAMLANDI + canlı doğrulandı** (UI, `/api/personel/orders*` API'leri, polling, durum makinesi). `/personel/*` + `/api/personel/*` guard'ı ikisi de canlı build yeşil. **KALAN:** Gel Al onay kuyruğu (ikinci sekme) HENÜZ YAZILMADI. |
| Mimari Dokümantasyon | 🟡 ARCHITECTURE.md v1.12 — hâlâ bu turdaki değişiklikleri yansıtmıyor: §4.1'deki `users.role` "HENÜZ KOŞULMADI" notu KOŞULDU'ya, §2.9a'ya Masaya kısmının TAMAMLANDIĞI ve `order_history` şema genişletmesi (status/table_number/customer_notes) işlenmeli — bkz. SIRADAKİ GÖREVLER 1d. ⚠️ DEPENDENCIES.md v1.1 (Session 3) — genel olarak ESKİ, ayrı bir turda kapsamlı güncelleme gerekiyor (#71). |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 0a | #80 — masaüstünde (`SummaryPanel.tsx`) #79 fix'inin canlı doğrulaması notu (düşük öncelik, kullanıcı kararıyla #79/#75 kapatıldı) | 🟢 |
| 0c | #78 — Customizer sticky özet panelin collapsed halde "Sepete Ekle"yi gizlemesi için UX çözümü kararlaştırılıp uygulanmalı (bu turda ek ekran görüntüsüyle yeniden doğrulandı) | 🟢 |
| 1 | **[TAMAMLANDI, bu turda ✅]** #62 Masaya sekmesi (UI, `/api/personel/orders*` route'ları, polling, durum makinesi) uçtan uca kodlandı VE canlıda doğrulandı. Sırada: **#62'nin Gel Al onay kuyruğu** — ARCHITECTURE.md §2.9a'daki ikinci sekme, ilk-sipariş manuel onay akışı (`users.verificationStatus`/`contactAttempts` ile bağlantılı). | 🔴 |
| 1b | Genel giriş/kayıt akış kararlarını koda dök: (i) `/menu/customize/*` guest gate middleware'i TAMAMLANDI (repoda doğrulandı); (ii) `/masaya-siparis/[tableId]/*` yüzeyi (`page.tsx` + `customize/[id]/page.tsx` + kendi mini-checkout'u, sayfa girişinde `useCartStore.setTableId()` çağrılmalı) HENÜZ KODLANMADI — mimari önü açık, başlanabilir; (iii) "Sepete Ekle" bypass component-guard'ı (#66 — eklensin mi kararı bekliyor); (iv) kayıt sayfasında zorunlu kanal seçimi adımı hâlâ kodlanmadı | 🔴 |
| 1d | ARCHITECTURE.md §4.1'deki `users.role` "migration HENÜZ KOŞULMADI" notunu "KOŞULDU+DOĞRULANDI" olarak güncelle; ayrıca §2.9a'ya bu turda kapanan Masaya kısmının + `order_history` şema genişletmesinin (status/table_number/customer_notes) işlenmesi gerekiyor (bu turda sadece SESSION_INDEX işlendi, ARCHITECTURE.md hâlâ bekliyor) | 🟡 |
| 1e | DEPENDENCIES.md'yi kapsamlı güncelle — `RegistrationChannel`'ın TÜM tüketicileri taransın (#71), ayrıca `useCartStore.tableId`, `order_history`, `users.role` gibi bu sohbetlerde eklenen alan/tablo/store değişiklikleri haritaya işlensin | 🟠 |
| 1f | TEST_MATRIX.md paylaşılınca `users.role` doğrulama testini işle: sütun var/`NOT NULL`/default doğru, mevcut kullanıcı kırılmadı (şu an 0 satır olduğu için gerçek regresyon testi #32 çözülünce yapılabilir) | 🟡 |
| 2 | #57'yi TAM kapat — `/online-siparis` sayfası (marketplace linkleri) | 🔴 |
| 3 | **[YENİ]** #73 kök neden araştırması: `tailwind.config.ts extend.colors` custom token'ları neden `bg-*` sınıfı olarak derlenmiyor — sistematik tarama (`RegistrationForm.tsx` dahil diğer `bg-{custom}` kullanımları #38'de işaretli) | 🟠 |
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
| 23 | [TAMAMLANDI] `types/index.ts` görüldü, #68 (RegistrationChannel/FulfillmentChannel tip etkisi) netleşti ve kodlandı | ✅ |
| 24 | [TAMAMLANDI] Vercel build yeşil doğrulandı (1d) | ✅ |
| 25 | [TAMAMLANDI] #62'nin 3 mimari sorusu kapandı — ARCHITECTURE.md v1.12 | ✅ |
| 26 | ROADMAP.md'ye #62 (Personel Sipariş Paneli) için ayrı bir oturum/kalem eklenmesi düşünülmeli — şu an hiç yer almıyor | 🟢 |
| 27 | [TAMAMLANDI, bu turda] `users.role` migration'ı Neon'da koşuldu, `role text` sütunu Tables görünümünde doğrulandı | ✅ |
| 28 | [TAMAMLANDI, bu turda] #70 kapandı — `order_history.table_number`/`status`/`customer_notes` migration'ı Neon'da koşuldu ve doğrulandı | ✅ |
| 29 | [TAMAMLANDI, bu turda] #62 Masaya sekmesi (10 dosya) uçtan uca kodlandı, build+deploy yeşil, canlıda gerçek test siparişiyle doğrulandı | ✅ |

---

*BOWLERA SESSION_INDEX.md — v45 (v44'ten: #74 TAM KAPANDI ✅ — `AccountMenu.tsx`'e çıkış
butonu eklendi, `.catch()` ile gerçek bir unhandled-rejection bug'ı düzeltildi,
`AccountMenu.test.tsx` 7/7 PASS + 0 error ile kod+build+canlı+test dört kontrol noktası da
tamamlandı. SIRADAKİ GÖREVLER'den 0b düşürüldü, Açık Sorunlar tablosundan #74 çıkarıldı.
Güncellenme: 2026-08-09.*
