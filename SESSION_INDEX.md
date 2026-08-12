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
> ⚠️ **TAŞIMA NOTU (2026-08-10, 13. sohbet devamı):** SESSION_INDEX.md 463 satıra ulaşınca
> (400 satır eşiği aşıldı, CORE.md §7.1 Adım 1), 4 kapanmış/güncelliğini yitirmiş CURRENT
> FOCUS bloğu (SOHBET KAYBI uyarısı, iki adet #62 Gel Al ara-durum bloğu, #82/#83/#84 kapanış
> bloğu) TAM metinleriyle `session_arşiv_1.md`'ye taşındı — kullanıcıya ayrı bir eklenti
> dosyası (`session_arsiv_1_EKLENTI_2026-08-10.md`) olarak verildi, kendi elinizle mevcut
> `session_arşiv_1.md`'nizin sonuna eklemeniz gerekiyor. Her taşınan madde için kapanış
> gerekçesi o dosyada mevcut.

---

## 🎯 CURRENT FOCUS

> **[YENİ SOHBET (devamı, 17.), 2026-08-12 — #90 YENİ: Customizer masaüstü layout, kod TAMAM,
> canlı doğrulama BEKLİYOR]**
> **(1) Bulgu:** Kullanıcı önce personel paneli genişlik sorunu sandı (o iz sonuçsuz kapandı —
> `page.tsx`/`layout.tsx`/`globals.css`/`MasayaPanel.tsx`/`GelAlPanel.tsx`/`GelAlOrderCard.tsx`/
> `KayitOnaylariPanel.tsx`/`PasswordResetPanel.tsx` tek tek kontrol edildi, hiçbirinde genişlik
> kısıtı bulunamadı — muhtemelen o paneller yeniden yazılırken kendiliğinden düzelmiş).
> Kullanıcı sonradan gerçek sayfayı düzeltti: `/menu/customize/[id]` ("Kâseni Oluştur" sonrası
> açılan sayfa) — masaüstünde Sepetim (`SummaryPanel`) görünüyor ama adım alanı (StepBase vb.)
> görünmüyor, pencere küçültülünce (mobil genişliğe inince) tekrar görünüyor.
> **(2) Kök neden:** `VisualPreview.tsx`'te kâse görseli `aspect-square w-full` — yükseklik
> genişlikle birebir orantılı. `page.tsx`'teki sarmalayıcı `mx-auto max-w-sm md:max-w-none`
> masaüstünde tavanı tamamen kaldırıyordu — sol grid kolonu (`minmax(0,1fr)`) geniş ekranlarda
> 700-900px'e büyüyünce görsel de aynı oranda devasalaşıp adım alanını ekranın çok aşağısına
> itiyordu (kayıp değil, sadece scroll ile ulaşılamayacak kadar aşağıda).
> **(3) Uygulanan çözüm (kullanıcı onayıyla, KARAR BİLDİRİMİ sonrası):** `app/menu/customize/
> [id]/page.tsx`'te 4 değişiklik — (a) görsel tavanı `md:max-w-none` → `md:max-w-[280px]`;
> (b) `<main>`e `md:h-screen md:overflow-hidden` (masaüstünde sayfa artık viewport'a kilitli);
> (c) sol kolona (`space-y-6`) `md:h-full md:overflow-y-auto md:pr-2` (sığmazsa SADECE bu kolon
> kendi içinde scroll olur, sayfa değil); (d) `SummaryPanel` sarmalayıcısına `md:sticky md:top-8
> md:self-start` (kaydırsan da sepet sabit kalır). DESIGN_SYSTEM.md kontrol edildi, çakışan
> kural yok (görsel boyutlandırma için tavan kuralı tanımlı değil). Tasarım skoru: 7/7.
> **(4) KALAN — ÜÇÜNCÜ DERS gereği TAM kapanmadı:** Kod üretildi ve dosya kullanıcıya verildi,
> ama Codespaces'te build/test koşulmadı VE kullanıcının kendi `page.tsx`'ine uygulayıp
> masaüstünde gerçekten tek ekrana sığdığını GÖZLE doğrulaması bekleniyor. `SummaryPanel`
> içeriği çok uzarsa (çok malzeme seçilirse) sticky panelin kendisi de taşabilir — canlı testte
> ayrıca gözlenmeli.

> ⚠️ **Arşiv taşıması — 2026-08-12 (devamı, #90 sonrası):** Kapanmış Gel Al 3-durumlu
> revizyon (KARAR A, 16. sohbet) CURRENT FOCUS bloğu `session_arşiv_2.md`'ye taşındı —
> CORE.md §7.1 Adım 1 (400 satır eşiği, bu turda eklenen #90 bloğu ile tekrar aşıldı).
> Kapanış gerekçesi: içerik Kritik Kararlar tablosunda (KARAR A satırı), Açık Sorunlar
> tablosunda (#62 satırı), GENEL DURUM'da (Personel Sipariş Paneli satırı) ve SIRADAKİ
> GÖREVLER'de (sıra 1) zaten tam özetli duruyor — "Teslim Edildi" canlı doğrulaması hâlâ
> BEKLİYOR durumda ama bu KALAN iş zaten dört tabloda da görünür, turn-by-turn anlatı
> ayrıca aktif takip gerektirmiyor. Taşıma bloğu ayrı eklenti
> (`session_arsiv_2_EKLENTI_2026-08-12-devam2.md`) olarak verildi, kendi elinizle
> `session_arşiv_2.md`'nin sonuna ekleyin.

> ⚠️ **Arşiv taşıması — 2026-08-12:** Kapanmış #89 CURRENT FOCUS bloğu (IP delili +
> engellenen deneme logu, uçtan uca tamamlandı notu) `session_arşiv_2.md`'ye taşındı —
> CORE.md §7.1 Adım 1 (400 satır eşiği, bu turdaki Gel Al 3-durumlu revizyon bloğu eklenince
> aşıldı). Kapanış gerekçesi: içerik Kritik Kararlar tablosunda (#89 satırı) ve Açık
> Sorunlar tablosunda (#89, ✅) zaten tam özetli duruyor. Taşıma bloğu ayrı eklenti
> (`session_arsiv_2_EKLENTI_2026-08-12.md`) olarak verildi, kendi elinizle
> `session_arşiv_2.md`'nin sonuna ekleyin.

> ⚠️ **Arşiv taşıması — 2026-08-12 (devamı, #90 sonrası, 3. kez):** Kapanmış #38 CURRENT
> FOCUS bloğu (14. sohbet, `RegistrationForm.tsx` kod+push tamam notu) `session_arşiv_2.md`'ye
> taşındı — CORE.md §7.1 Adım 1 (400 satır eşiği). Kapanış gerekçesi: içerik Açık Sorunlar
> tablosunda (#38 satırı) zaten tam özetli duruyor — canlı görsel doğrulama hâlâ BEKLİYOR ama
> bu KALAN iş o satırda görünür. Taşıma bloğu ayrı eklenti
> (`session_arsiv_2_EKLENTI_2026-08-12-devam3.md`) olarak verildi, kendi elinizle
> `session_arşiv_2.md`'nin sonuna ekleyin.

> ⚠️ **Arşiv taşıması — 2026-08-11 (devamı):** 1b(ii) kapsam-dışı kararının kapanmış
> CURRENT FOCUS bloğu `session_arşiv_2.md`'ye taşındı — CORE.md §7.1 Adım 1 (400 satır
> eşiği). Kapanış gerekçesi: karar Kritik Kararlar tablosunda, 1b satırında ve #66
> satırında zaten tam özetli duruyor.

> ⚠️ **Arşiv taşıması — 2026-08-11 (3. kez):** Sekme rozetleri + DESIGN_SYSTEM.md §2.2
> istisnası bloğu `session_arşiv_2.md`'ye (TAŞIMA BLOĞU #2 olarak) taşındı — CORE.md §7.1
> Adım 1 (400 satır eşiği #38 kapanışıyla tekrar aşıldı). Kapanış gerekçesi: içerik Açık
> Sorunlar tablosunda (#88), GENEL DURUM satırında ve DESIGN_SYSTEM.md v1.2 notunda zaten
> özetli. Taşıma bloğu ayrı eklenti (`session_arsiv_2_EKLENTI_2026-08-11.md`) olarak
> verildi, kendi elinizle `session_arşiv_2.md`'nin sonuna ekleyin.

> ⚠️ **Arşiv taşıması — 2026-08-11:** Kapanmış #85 CURRENT FOCUS bloğu
> `session_arşiv_2.md`'ye taşındı — CORE.md §7.1 Adım 1 (400 satır eşiği aşıldı).
> **[GÜNCELLEME, aynı gün]** Kullanıcı `session_arşiv_1.md`'nin hacimce şiştiğini belirtti
> ve YENİ bir dosya (`session_arşiv_2.md`) açılmasını istedi — bu blok başlangıçta ayrı bir
> eklenti (`session_arsiv_1_EKLENTI_2026-08-11.md`) olarak üretilmişti, sonradan doğrudan
> `session_arşiv_2.md`'nin İLK taşıma bloğu olarak yeniden paketlendi (kullanıcıya TAM
> dosya olarak verildi, ayrıca eklenmesine gerek yok). Kapanış gerekçesi: #85 Açık
> Sorunlar tablosunda (✅), Kritik Kararlar tablosunda ve GENEL DURUM satırında zaten
> özetli duruyor, turn-by-turn anlatı artık aktif takip gerektirmiyor.
> ⚠️ **Bekleyen madde:** `session_arsiv_1_EKLENTI_2026-08-10.md` (4 blok — SOHBET KAYBI,
> 2x Gel Al ara-durum, #82/#83/#84) hâlâ `session_arşiv_1.md`'nin sonuna eklenmemiş
> görünüyor — kronolojik olarak arşiv_1'e ait, arşiv_2'ye DEĞİL.

> ⚠️ **Arşiv taşıması — 2026-08-10:** 3 kapanmış CURRENT FOCUS bloğu (#74 çıkış butonu
> kapanışı, #62 Masaya sekmesi tam kapanışı, #79 masaüstü fix'i) `session_arşiv_1.md`'ye
> taşındı — CORE.md §7.1 Adım 1 (400 satır eşiği). Kapanış gerekçesi: hepsi Kritik Kararlar
> tablosunda ve/veya Açık Sorunlar tablosunda satır olarak zaten özetli duruyor, turn-by-turn
> anlatı artık aktif takip gerektirmiyor. Taşıma bloğu ayrı olarak sunulacak.

> ⚠️ **Arşiv taşıması — 2026-08-11 (devamı, 4. kez):** Kapanmış #86 Kayıt Onayları CURRENT
> FOCUS bloğu (build DOĞRULANDI notu) `session_arşiv_2.md`'ye taşındı — CORE.md §7.1 Adım 1
> (400 satır eşiği #89 IP delili eklenince tekrar aşıldı). Kapanış gerekçesi: içerik Açık
> Sorunlar tablosunda #86 satırında ve Kritik Kararlar tablosunda zaten özetli duruyor.
> Taşıma bloğu ayrı eklenti (`session_arsiv_2_EKLENTI_2026-08-11-devam4.md`) olarak verildi,
> kendi elinizle `session_arşiv_2.md`'nin sonuna ekleyin.

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
| 🆕 | **[BU TURDA — #82 KARARI, mimari revizyon]** Telefon eşleşirse "onay ekranı" fikri TERK EDİLDİ — gerçek güvenlik için tam telefon+şifre girişine geçildi (`bcryptjs`, `users.passwordHash`). `verificationStatus` giriş erişimini ETKİLEMEZ (sadece UI rozeti) — kimlik teyidi hâlâ personelin "preparing"e geçirme anı. | ✅ Karar netleşti, kod üretildi, canlıda TAM doğrulandı — #82 KAPANDI |
| 🆕 | **[BU TURDA — #83 KARARI]** Şifre sıfırlama tamamen manuel: müşteri talep açar → personel panelinde "Şifre Talepleri" sekmesinde görünür → personel 6 haneli kodu (crypto.randomInt) üretip WhatsApp/SMS'ten elle iletir. Otomatik gönderim YOK. | ✅ Karar netleşti, kod üretildi, canlıda TAM doğrulandı — #83 KAPANDI |
| 🆕 | **[BU TURDA — #85 bulgu 4 KARARI]** Gel Al'da eşzamanlı güncelleme koruması: `recordFailedContactAttempt` atomik SQL UPDATE'e çevrildi (ucuz+doğru, her koşulda yapılır). `confirmPickupOrder`/`rejectPickupOrder` için optimistic lock EKLENMEDİ — kullanıcı beyanı: tek personel/tek masaüstü panel, pratik risk düşük. Masaya/#81 ile aynı kapsam kararı, #87 olarak loglandı. | ✅ Karar netleşti, kod+test üretildi, 15/15 PASS, push edildi |
| 🆕 | **[BU TURDA — 1b(ii) KARARI, 2026-08-11]** `/masaya-siparis/[tableId]/*` (müşterinin kendi masasından sipariş vermesi) RESMEN KAPSAM DIŞI bırakıldı — gerekçe: dükkan küçük, personel masa siparişini zaten eliyle giriyor. **Personel-tarafı Masaya PANELİ (#62, `/personel` sekmesi) bu karardan ETKİLENMEDİ** — o zaten kod+canlı doğrulama ile TAMAMLANDI, sadece personelin kendi girdiği siparişleri yönetiyor. #66 (Sepete Ekle bypass guard) bu kapsam dışı bırakmadan bağımsız hâle geldi, hâlâ ayrı bir karar bekliyor. | ✅ Karar netleşti, kod değişikliği YOK (zaten kodlanmamıştı, sadece hedef listeden çıkarıldı) |
| 🗄️✅ | **[BU TURDA — #89 KARARI, 2026-08-11]** `consentRegistrations.phone` zaten unique+upsert olduğu için IP delili AMACI "aynı telefonu tekrar yazan" değil "farklı sahte telefonlarla aynı IP'den art arda deneyen"i yakalamak. `ipAddress` (nullable) consent tablosuna, ayrı INSERT-ONLY `registrationBlockedAttempts` tablosu (429'ların kalıcı logu) eklendi — upsert DEĞİL, çünkü "kaç kez denendi" bilgisi kaybolmamalı. Migration Neon'da koşuldu, 6 sorguyla doğrulandı (diğer tablolar etkilenmedi), test 6/6 PASS, Vercel yeşil. | ✅ Uçtan uca TAMAMLANDI |
| 🆕 | **[BU TURDA — Gel Al 3-durumlu revizyon, KARAR A, 2026-08-12]** Canlı bulgu: "Onayla" tıklanınca sipariş panelden kayboluyordu (`confirmed` BİLİNÇLİ olarak terminal tasarlanmıştı). `confirmed` artık terminal DEĞİL ("Hazırlanıyor"), yeni terminal `completed` ("Teslim Edildi") eklendi. Zincir: `pending→confirmed(Hazırlanıyor)→completed(Teslim Edildi)`. Migration gerekmedi (status düz text). | ✅ Karar netleşti, kod+test üretildi (37/37 PASS, Codespaces), canlı doğrulama (Teslim Edildi tıklaması) BEKLİYOR |

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
| 38 | 🟡 | **[BU TURDA — kod+push TAMAM, canlı doğrulama BEKLİYOR]** `RegistrationForm.tsx`'te AYNI #73 kırık deseni doğrulandı ve düzeltildi: submit butonundaki `bg-olive-primary`/`text-cream` VE iki linkteki `text-espresso` (bu üçü daha önce hiç test edilmemişti) arbitrary value'ya (`bg-[#53502A]`/`text-[#F4F0E7]`/`text-[#38221D]`) çevrildi. Kullanıcı GitHub'a push etti. **KALAN:** ÜÇÜNCÜ DERS gereği canlıda butonun gerçekten göründüğü GÖZLE doğrulanmadı. | `components/registration/RegistrationForm.tsx` |
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
| 71 | 🟠 | DEPENDENCIES.md, `RegistrationChannel`'ın tüketicisi olarak `channel-options.ts`'i (ve muhtemelen görülmemiş başka dosyaları) listelemiyor — #68 kapanırken bu dosya atlandığı için canlı build kırılmıştı (düzeltildi, 1d KAPANDI). DEPENDENCIES.md bu sohbette paylaşıldı ama v1.1 (Session 3) — genel olarak ESKİ, `RegistrationChannel` tüketicileri dahil yeni alan/tablo/store değişiklikleri (tableId, order_history, users.role, vb.) hiç yansımamış. Ayrı bir turda kapsamlı güncellenmeli. | `DEPENDENCIES.md` |
| 73 | 🟠 | `tailwind.config.ts`'teki `extend.colors` custom token'ları (`olive-primary` doğrulandı, muhtemelen `olive-deep`/`bronze`/`espresso` de) `bg-*` sınıfı olarak KULLANILDIĞINDA derlenmiyor — `bg-red-500` (standart) çalışıyor, `bg-olive-primary` (custom) çalışmıyor, `bg-[#53502A]` (arbitrary) çalışıyor. Kök neden BULUNAMADI. **[Bu turda ek kanıt]:** `AddToCartButton.tsx`'te de AYNI kırık pattern görüldü (#50'de "hiç görülmedi" idi), aynı `bg-[#53502A]` workaround'ıyla düzeltildi — üçüncü dosyada doğrulanan tekrar, sistematik tarama gerekliliğini pekiştiriyor. `text-olive-primary`'nin çalışıp çalışmadığı hâlâ TEYİT EDİLMEDİ. | `tailwind.config.ts`, tüm `bg-{custom-token}` kullanan dosyalar |
| 81 | 🟢 | **[YENİ, bu turda — bilinçli erteleme]** Masaya Paneli'nde (1) iki personelin aynı siparişi eşzamanlı güncellemesine karşı optimistic lock yok (son yazan kazanır), (2) `usePersonelOrders` polling'i sekme arka plandayken duraklamıyor (Page Visibility API kullanılmadı). İkisi de MVP kapsamı dışı bırakıldı, kullanım yoğunlaşırsa ele alınmalı. | `hooks/usePersonelOrders.ts`, `app/api/personel/orders/[id]/route.ts` |
| 80 | 🟢 | **[YENİ — kullanıcı kararıyla, 2026-08-09]** #79/#75 kapatıldı (mobil canlıda doğrulandı: "Sepete Ekle sorunu çözüldü"). Masaüstü (`SummaryPanel.tsx`) fix'i AYRICA canlıda doğrulanmadı — kod+test tarafı aynı (`isReadyToAddToCart()`), risk düşük görülüyor ama not olarak açık bırakılıyor. #75'in orijinal çift-tık/duplicate senaryosu da bu turda ayrıca test edilmedi. | `components/customizer/SummaryPanel.tsx` |
| 78 | 🟢 | **[Kaynak bileşen bu turda teyit edildi — UX çözümü hâlâ AÇIK]** Customizer'da collapsed sticky özet panel (fiyat/kalori satırı + ▲ ikonu) seçim anında "Sepete Ekle" butonunu ve Base/Main/Flavor özetini GİZLİYOR — panel manuel genişletilmeden görünmüyor. Kaynak bileşenin `MobileSummaryDrawer.tsx` olduğu bu turda doğrulandı (bkz. #75) — SADECE o dosyadaki build-kırığı prop eksikliği düzeltildi, panel-görünürlüğü UX çözümüne bilinçli olarak DOKUNULMADI (Kural #5, ayrı karar). CORE.md §8 mimari varsayımı "Özet panel her zaman görünür... asla gizlenmez" ile çelişiyor. Çözüm yönü henüz kararlaştırılmadı (varsayılan yarı-açık / mikro-metin / otomatik ilk-açılış seçenekleri konuşuldu). | `components/customizer/MobileSummaryDrawer.tsx` |


> **KAPANDI (BU TURDA ✅):** #82 + #83 + #84 — üçü de canlıda TAM doğrulandı. #82: orijinal
> kayıt şifresiyle (Neon'a elle dokunmadan) çıkış→giriş döngüsü BAŞARILI. #83: "Sıfırla" →
> üretilen geçici kod (460244) → o kodla giriş BAŞARILI. #84: Header'da isim ("bari")
> canlıda görünür durumda (ekran görüntüsüyle doğrulandı) — ⚠️ kök neden FORMEL olarak
> izole edilmedi (istenen SQL sorgusu hiç koşulmadı), muhtemelen #82'nin auth.ts/JWT-session
> değişikliklerinin yan etkisi, ama bu kanıtlanmadı; regresyon riski düşük görülüyor.
>
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
| Auth | 🟡 Twilio/Netgsm PARKLI. Genel giriş/kayıt akışı karar olarak netleşti, guest gate middleware'i KODLANDI ve repoda doğrulandı. Masaya Sipariş kanalı middleware'in kapsamı dışında AYRI bir yüzeyde (`/masaya-siparis/*`) yaşayacak — bu yüzey henüz kodlanmadı. Gel Al akışı için "Sepete Ekle" bypass guard'ı (#66) hâlâ eksik. `/personel/*` role bazlı guard'ı ✅ TAMAMLANDI — 4 dosya senkron, canlı build yeşil doğrulandı. **[Bu turda]** Telefon+şifre girişi (#82) VE şifre sıfırlama (#83) canlıda TAM doğrulandı (her iki döngü de test edildi) — ikisi de KAPANDI. Login sonrası isim gösterme sorunu (#84) de canlıda düzelmiş görüldü, KAPANDI (kök neden formel izole edilmedi). |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE canlıda test edildi (#39 KAPANDI). ⚠️ Kaydet butonu `bg-olive-600` (kırık) → `bg-[#53502A]` (arbitrary value, çalışıyor) — kök neden #73'te açık. |
| Kullanıcı Kaydı (rıza esaslı) | 🟢 Backend+Frontend TAMAM, canlı test BAŞARILI, oturum+isim gösterimi DOĞRULANDI (#59 KAPANDI). Kanal seçimi zorunlu adımı henüz KODLANMADI (bkz. 1b). |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı, SADECE Gel Al'a özel (§2.9). Masaya kendi bağımsız mini-checkout'unu kullanacak (ARCHITECTURE.md v1.8) — henüz KODLANMADI. |
| Veritabanı | 🟢 Neon Postgres çalışıyor. `consentRegistrations` ve `order_history` migrate edildi. `users.role` (`text`, `NOT NULL`, `DEFAULT 'customer'`) migrate edildi ve DOĞRULANDI (Tables görünümü, screenshot). **[Bu turda]** `consentRegistrations.ipAddress` (nullable) + yeni `registrationBlockedAttempts` tablosu (#89) migrate edildi, 6 sorguyla DOĞRULANDI — diğer tablolar etkilenmedi. `users` tablosu hâlâ 0 satır (#32 Twilio kısıtı). ⚠️ DB şifresi reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik (#63). ⚠️ `order_history.table_number` kolonu KARARLAŞTIRILDI, migration HENÜZ KOŞULMADI — tip netleşmeden koşulmamalı (#70). |
| Personel Sipariş Paneli (#62) | 🟢 Masaya sekmesi TAMAMLANDI + canlı doğrulandı. `/personel/*` + `/api/personel/*` guard'ı ikisi de canlı build yeşil. 🟡 **[BU TURDA]** Gel Al onay kuyruğu — canlı bulgu üzerine 3-durumlu revizyon (KARAR A): `confirmed` artık terminal değil ("Hazırlanıyor"), yeni terminal `completed` ("Teslim Edildi") eklendi. 7 kaynak + 5 test dosyası (2'si YENİ — projedeki ilk API route testleri) kodlandı, Codespaces'te 37/37 PASS. **SADECE canlı ortamda "Teslim Edildi" tıklama testi BEKLİYOR.** 🟡 Kayıt Onayları (4. sekme, #86) — 8 dosya kodlandı, Gel Al deseniyle tutarlı, tam repo zip'inden statik incelendi, `npm run build`/`tsc --noEmit` YEŞİL (kullanıcı Codespaces'te doğruladı, push edildi). Test seti + canlı doğrulama BEKLİYOR. 🟢 **[önceki tur]** Şifre Talepleri/Gel Al/Kayıt Onayları sekmelerine bekleyen sayısı rozeti eklendi (DESIGN_SYSTEM.md v1.2 §2.2 personel-paneli kırmızı istisnasıyla), push edildi — test/canlı doğrulama bekliyor. |
| Mimari Dokümantasyon | 🟡 ARCHITECTURE.md v1.12 — hâlâ bu turdaki değişiklikleri yansıtmıyor: §4.1'deki `users.role` "HENÜZ KOŞULMADI" notu KOŞULDU'ya, §2.9a'ya Masaya kısmının TAMAMLANDIĞI ve `order_history` şema genişletmesi (status/table_number/customer_notes) işlenmeli — bkz. SIRADAKİ GÖREVLER 1d. ⚠️ DEPENDENCIES.md v1.1 (Session 3) — genel olarak ESKİ, ayrı bir turda kapsamlı güncelleme gerekiyor (#71). |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| -2 | **[YENİ, bu turda]** #90 — `/menu/customize/[id]` masaüstü tek-ekrana-sığma düzeltmesi kodlandı, kullanıcıya verildi. **KALAN:** kendi `page.tsx`'ine uygulanmalı, Codespaces'te build koşulmalı, GitHub'a push edilmeli, masaüstünde GÖZLE doğrulanmalı. | 🟠 |
| -1 | **[TAMAMLANDI, bu turda ✅]** #84 — isim gösterme sorunu kullanıcı tarafından canlıda ("bari" görünür) doğrulandı. Kök neden SQL sorgusuyla izole edilmedi, kullanıcı deneyimi seviyesinde kapandı. | ✅ |
| 0 | **[TAMAMLANDI, bu turda ✅]** #83 — "Sıfırla" → üretilen geçici kodla (460244) giriş canlıda BAŞARILI test edildi. | ✅ |
| 0b | **[TAMAMLANDI, bu turda ✅]** #82 — Neon'a elle dokunmadan, orijinal kayıt şifresiyle çıkış→giriş döngüsü canlıda BAŞARILI test edildi. | ✅ |
| 0a | #80 — masaüstünde (`SummaryPanel.tsx`) #79 fix'inin canlı doğrulaması notu (düşük öncelik, kullanıcı kararıyla #79/#75 kapatıldı) | 🟢 |
| 0c | #78 — Customizer sticky özet panelin collapsed halde "Sepete Ekle"yi gizlemesi için UX çözümü kararlaştırılıp uygulanmalı (bu turda ek ekran görüntüsüyle yeniden doğrulandı) | 🟢 |
| 1 | #62 Masaya sekmesi TAMAMLANDI + canlı doğrulandı (önceki tur). Gel Al onay kuyruğu #85 KAPANDI (önceki tur). **[BU TURDA]** 3-durumlu revizyon (KARAR A) — canlı bulgu üzerine `confirmed` terminal olmaktan çıkarıldı, `completed` eklendi, 7 kaynak+5 test dosyası kodlandı, Codespaces'te 37/37 PASS. **KALAN:** canlı ortamda "Teslim Edildi" butonunun tıklanıp gerçekten `completed`'e geçtiğinin doğrulanması. | 🟠 |
| 1c | **[Bu turda]** #86 Kayıt Onayları (4. sekme) — kod+build tarafı KAPANDI (Codespaces'te `tsc --noEmit` + `npm run build` başarılı, GitHub'a push edildi). **KALAN:** test seti yazılmalı, canlı ortamda (Vercel deploy sonrası) Teyit Et/Reddet-Sil aksiyonları gerçek bir bekleyen kayıtla test edilmeli. | 🟡 |
| 1b | Genel giriş/kayıt akış kararlarını koda dök: (i) `/menu/customize/*` guest gate middleware'i TAMAMLANDI (repoda doğrulandı); (ii) `/masaya-siparis/[tableId]/*` yüzeyi (müşterinin kendi masasından sipariş vermesi) **[BU TURDA KAPSAM DIŞI BIRAKILDI — kullanıcı kararı, 2026-08-11: dükkan küçük, personel masa siparişini zaten eliyle giriyor. Personel-tarafı Masaya PANELİ (#62) bundan ETKİLENMİYOR, o zaten TAMAMLANDI.]**; (iii) "Sepete Ekle" bypass component-guard'ı (#66 — eklensin mi kararı bekliyor, 1b'den BAĞIMSIZ hâle geldi); (iv) **[BU TURDA KAPANDI ✅ — sadece doğrulama, kod değişikliği YOK]** kayıt sayfasında zorunlu kanal seçimi ZATEN kodluymuş: `useRegistrationForm.ts`'te `channel` state'i `useState<RegistrationChannel \| null>(null)` ile başlıyor (varsayılan seçim YOK) ve `submitRegistration()` içinde `if (!channel)` guard'ı POST'u engelliyor. Zincir uçtan uca teyit edildi: form→hook→`route.ts`→`upsertConsentRegistration`→`schema.ts`'teki `channel: text("channel").notNull()` — UI/API/DB üç katmanda da zorunlu, DB'ye kanal bilgisi olmadan hiçbir kayıt yazılamıyor. SESSION_INDEX'teki eski "hâlâ kodlanmadı" notu GÜNCELLİĞİNİ YİTİRMİŞTİ, düzeltildi. | 🟡 (ii) kapandı, (iv) kapandı, (iii) hâlâ açık |
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
| 30 | [TAMAMLANDI, bu turda] #89 IP delili + engellenen deneme logu — 4 dosya kodlandı, migration Neon'da koşuldu+6 sorguyla doğrulandı, test 6/6 PASS (Codespaces), Vercel deploy yeşil | ✅ |

---

*BOWLERA SESSION_INDEX.md — v62 (v61'den: kullanıcı 400-satır ihlalini fark etti, önceki
"taşınacak kapalı blok yok" değerlendirmesi YANLIŞ uygulanmıştı — dosyadaki emsale (#89/#86)
göre kriter "sıfır kalan iş" değil "içerik zaten Açık Sorunlar/Kritik Kararlar tablosunda özetli
mi". Düzeltme: Gel Al 3-durumlu revizyon (16. sohbet) ve #38 (14. sohbet) CURRENT FOCUS
blokları arşive taşındı, 439→416 satır. Ayrı bir denemede 3 kapanmış (✅) Açık Sorunlar
satırı (#50/#85/#70) da gerekçeyle silinmeye çalışıldı ama tek-satırlık kayıtları çok
satırlı gerekçe bildirimiyle değiştirmek net satır SAYISINI ARTIRDIĞI için bu adım GERİ
ALINDI — üçü de tabloda duruyor. KALAN: 416 satır hâlâ 400 eşiğinin 16 satır üstünde;
CURRENT FOCUS'ta taşınabilecek başka kapanmış anlatı bloğu kalmadı (geri kalanı ya zaten
kompakt arşiv bildirimleri ya da bu turun açık #90 bloğu). Güncellenme: 2026-08-12.*
