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

> **[TAŞINDI — 2026-08-23, 400 satır eşiği]** 18. sohbet (#91 SEC-01/SEC-02 detay anlatısı) ve
> 17. sohbet (#90 detay anlatısı) blokları `session_arşiv_2.md`'ye taşındı (bkz. Arşiv Taşıma
> Kaydı altında). Kapanış gerekçesi: her iki blok da Açık Sorunlar #91/#90 satırlarında zaten
> tam özetli — aktif takip için gerekli değil, sadece turn-by-turn anlatı taşındı.
>
> **[TAŞINDI — 2026-09-03, 400 satır eşiği üçüncü kez aşıldı]** 19. sohbet (CRM/çok-şubeli
> vizyon keşfi), 20. sohbet (SANDWICH_SPEC.md v1.0/v1.1 üretimi) ve 22. sohbet (sandviç UI
> düzeltmeleri + checkout blokajı keşfi, geriye dönük işlendi) blokları `session_arşiv_2.md`'ye
> taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-09-03.md`). Kapanış gerekçesi: üçü de Açık
> Sorunlar #92/#93/#94 (19. sohbet), #95 (20. sohbet, S1/S2/S5 hâlâ bekliyor), #99-#104 (22.
> sohbet) ve Kritik Kararlar tablosunda zaten tam özetli — aktif takip için gerekli değil,
> sadece turn-by-turn anlatı taşındı.
> **[TAŞINDI — 2026-08-23, 400 satır eşiği ikinci kez aşıldı]** SEKİZİNCİ DERS (21. sohbet)
> bloğu (build hatası düzeltmesi, `sandwich-data.json` TEST VERİSİ üretimi, `Hero.tsx` CTA
> değişikliği, 6 adım bileşeni + eksik `page.tsx` kodlanması, 7 test dosyası/27 test PASS)
> `session_arşiv_2.md`'ye taşındı (eklenti: `session_arsiv_2_EKLENTI_2026-08-23-devam2.md`).
> Kapanış gerekçesi: içerik Açık Sorunlar #95/#96/#97/#98'de zaten tam özetli — aktif takip
> için gerekli değil, sadece turn-by-turn anlatı taşındı.

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

> ⚠️ **Bekleyen eklemeler (kullanıcı elle eklemeli):** `session_arsiv_1_EKLENTI_2026-08-10.md`,
> `session_arsiv_2_EKLENTI_2026-08-11.md`, `..._EKLENTI_2026-08-11-devam4.md`,
> `..._EKLENTI_2026-08-12.md`, `..._EKLENTI_2026-08-12-devam2.md`, `..._EKLENTI_2026-08-12-devam3.md`,
> `session_arsiv_2_EKLENTI_2026-08-23.md`, `..._EKLENTI_2026-08-23-devam2.md` (bu turda üretildi)
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
| 71 | 🟠 | DEPENDENCIES.md, `RegistrationChannel`'ın tüketicisi olarak `channel-options.ts`'i (ve muhtemelen görülmemiş başka dosyaları) listelemiyor — #68 kapanırken bu dosya atlandığı için canlı build kırılmıştı (düzeltildi, 1d KAPANDI). DEPENDENCIES.md bu sohbette paylaşıldı ama v1.1 (Session 3) — genel olarak ESKİ, `RegistrationChannel` tüketicileri dahil yeni alan/tablo/store değişiklikleri (tableId, order_history, users.role, vb.) hiç yansımamış. Ayrı bir turda kapsamlı güncellenmeli. | `DEPENDENCIES.md` |
| 73 | 🟠 | `tailwind.config.ts`'teki `extend.colors` custom token'ları (`olive-primary` doğrulandı, muhtemelen `olive-deep`/`bronze`/`espresso` de) `bg-*` sınıfı olarak KULLANILDIĞINDA derlenmiyor — `bg-red-500` (standart) çalışıyor, `bg-olive-primary` (custom) çalışmıyor, `bg-[#53502A]` (arbitrary) çalışıyor. Kök neden BULUNAMADI. **[Bu turda ek kanıt]:** `AddToCartButton.tsx`'te de AYNI kırık pattern görüldü (#50'de "hiç görülmedi" idi), aynı `bg-[#53502A]` workaround'ıyla düzeltildi — üçüncü dosyada doğrulanan tekrar, sistematik tarama gerekliliğini pekiştiriyor. `text-olive-primary`'nin çalışıp çalışmadığı hâlâ TEYİT EDİLMEDİ. | `tailwind.config.ts`, tüm `bg-{custom-token}` kullanan dosyalar |
| 81 | 🟢 | **[YENİ, bu turda — bilinçli erteleme]** Masaya Paneli'nde (1) iki personelin aynı siparişi eşzamanlı güncellemesine karşı optimistic lock yok (son yazan kazanır), (2) `usePersonelOrders` polling'i sekme arka plandayken duraklamıyor (Page Visibility API kullanılmadı). İkisi de MVP kapsamı dışı bırakıldı, kullanım yoğunlaşırsa ele alınmalı. | `hooks/usePersonelOrders.ts`, `app/api/personel/orders/[id]/route.ts` |
| 80 | 🟢 | **[YENİ — kullanıcı kararıyla, 2026-08-09]** #79/#75 kapatıldı (mobil canlıda doğrulandı: "Sepete Ekle sorunu çözüldü"). Masaüstü (`SummaryPanel.tsx`) fix'i AYRICA canlıda doğrulanmadı — kod+test tarafı aynı (`isReadyToAddToCart()`), risk düşük görülüyor ama not olarak açık bırakılıyor. #75'in orijinal çift-tık/duplicate senaryosu da bu turda ayrıca test edilmedi. | `components/customizer/SummaryPanel.tsx` |
| 78 | 🟢 | **[Kaynak bileşen bu turda teyit edildi — UX çözümü hâlâ AÇIK]** Customizer'da collapsed sticky özet panel (fiyat/kalori satırı + ▲ ikonu) seçim anında "Sepete Ekle" butonunu ve Base/Main/Flavor özetini GİZLİYOR — panel manuel genişletilmeden görünmüyor. Kaynak bileşenin `MobileSummaryDrawer.tsx` olduğu bu turda doğrulandı (bkz. #75) — SADECE o dosyadaki build-kırığı prop eksikliği düzeltildi, panel-görünürlüğü UX çözümüne bilinçli olarak DOKUNULMADI (Kural #5, ayrı karar). CORE.md §8 mimari varsayımı "Özet panel her zaman görünür... asla gizlenmez" ile çelişiyor. Çözüm yönü henüz kararlaştırılmadı (varsayılan yarı-açık / mikro-metin / otomatik ilk-açılış seçenekleri konuşuldu). | `components/customizer/MobileSummaryDrawer.tsx` |
| 92 | 🟠 | **[YENİ, bu turda (19. sohbet) — sadece analiz+öneri, KOD YOK]** Çok şubeli mimari: `branches` tablosu şemada HİÇ YOK. Kullanıcı 2./3. şubenin "herhangi an" açılabileceğini belirtti. `order_history` ve `consent_registrations`'da hangi siparişin/kaydın hangi şubeye ait olduğunu tutan bir alan yok — şu an TEK ŞUBE varsayımıyla kurulu. Geriye dönük eklemek, mevcut kayıtlara hangi şube olduğu konusunda varsayım atamayı gerektirir (veri belirsizliği riski). **Önerilen yön (ONAYLANMADI):** `branches` tablosu tek satırla (mevcut şube) şimdiden açılsın, `order_history.branch_id` + `consent_registrations.branch_id` nullable FK olarak eklensin; `users` ASLA şubeye bağlanmasın (CRM şubeler üstü kalmalı). Detay: `BOWLERA_COK_SUBELI_CRM_VIZYON.md` §3-4-6. **Açık karar:** 2. şube yaklaşık ne zaman planlanıyor — bu, işin bu turda mı yoksa ayrı sırada mı yapılacağını belirler. | `lib/db/schema.ts` (henüz dokunulmadı) |
| 93 | 🟡 | **[YENİ, bu turda (19. sohbet) — sadece analiz+öneri, KOD YOK]** Şubeye göre menü farklılığı: DB'de HİÇ menü/ürün tablosu yok — menü `menu-data.json`/`customizerCatalog.ts` gibi statik bir dosyada yaşıyor görünüyor (#24 ile bağlantılı, kesin dosya adı DOĞRULANMADI). Bu, #92'den daha KÖK bir mesele: "şubeye göre menü" kavramının DB tarafında hiç karşılığı yok, ölçeklenmeden statik dosya çoğaltmaya döner. **Önerilen yön (ONAYLANMADI):** global ürün kataloğu (marka kimliği — tüm şubelerde aynı tanım/kalori/alerjen) + `branch_menu_items` eşleme tablosu (`branch_id`+`product_id`+`is_available`+`price_override`, nullable). **KALAN:** menünün fiilen yaşadığı dosya (muhtemelen `menu-data.json` veya `customizerCatalog.ts`) GÖRÜLMEDEN kesin şema önerilemez (Kural #2). | `menu-data.json` veya `lib/customizer/customizerCatalog.ts` (dosya henüz istenmedi) |
| 94 | 🟢 | **[YENİ, bu turda (19. sohbet) — sadece analiz+öneri, KOD YOK]** CRM/attribution katmanı eksik: `consent_registrations`/`order_history`'de pazarlama kaynağı (Instagram/TikTok/Marketplace/Google/UTM) hiç tutulmuyor. **İsim çakışması riski:** mevcut `channel` alanları (her iki tabloda da var) FULFILLMENT kanalı (gel-al/masaya) anlamında — pazarlama kanalı DEĞİL. Yeni alanlar eklenirse `channel` yeniden kullanılmamalı, `acquisition_source`/`utm_campaign`/`utm_medium` gibi AYRI isimler kullanılmalı. Ayrıca `order_count`/`total_spend`/`days_to_repeat` gibi CRM metrikleri `users`'a KOLON olarak eklenmemeli — `order_history` üzerinden SQL VIEW olarak hesaplanmalı (senkron kayma riski). Kullanıcının "bu yapı ileride birçok modül/uygulamanın temel iskeleti olacak" vizyonuyla bağlantılı — PUSULA OS değerlendirmesindeki "event log yok, policy engine yok" bulgusuyla örtüşüyor (tam çözüm bu turun kapsamı dışı, sadece isim/yön kararı). Detay: `BOWLERA_COK_SUBELI_CRM_VIZYON.md` §5-6-7. | `lib/db/schema.ts` (henüz dokunulmadı) |

| 95 | 🟡 | **[YENİ, bu turda (21. sohbet)]** Sandviç akışı `lib/sandwich-data.json` TEST VERİSİ ile çalışıyor — S1 (gerçek fiyat/kalori/ürün isimleri), S2 (ücretsiz sebze kotası — şu an placeholder 4), S5 ("Mike's Way" preset içeriği — şu an placeholder sebze+sos) hâlâ gerçek veri bekliyor. Launch öncesi MUTLAKA değiştirilmeli, aksi halde sahte fiyat/kalori canlıya çıkar. | `lib/sandwich-data.json` |
| 96 | ✅ | **[BU TURDA KAPANDI]** Sandviç bileşen testleri (`SandwichCustomizer` + 6 adım bileşeni) yazıldı ve Codespaces'te doğrulandı: 7/7 dosya, 27/27 test PASS (2026-08-23 18:28). Yol boyunca 2 sorun çıktı, ikisi de çözüldü: `act()` eksikliği ve unutulan `StepSauceToastExtras.test.tsx` pushu. | `components/sandwich/*.test.tsx` |
| 97 | 🟠 | **[YENİ, bu turda (21. sohbet)]** CORE.md Dosya Haritası bu turda eklenen dosyaları yansıtmıyor: `StepBread/StepSize/StepProtein/StepCheese/StepVeggies/StepSauceToastExtras.tsx`, `app/sandwich/customize/[id]/page.tsx`, 7 test dosyası, `Hero.tsx` CTA değişikliği. Ayrı bir turda CORE.md güncellenmeli. | `CORE.md` |
| 98 | 🟢 | **[YENİ, bu turda (21. sohbet) — kapsam dışı bırakıldı]** Genel proje `npm test` çalıştırıldığında (sandviç kapsamı DIŞINDA) 7 dosya/9 test başarısız çıktı, `Header.test.tsx` dahil (kritik: "Çıkış Yap"a tıklayınca signOut callbackUrl="/" ile çağrılır" testi). Bu turda kasıtlı dokunulmadı — Kural #5 izolasyon. Ayrı bir turda ele alınmalı. | `components/layout/Header.test.tsx` + 6 diğer dosya (henüz listelenmedi) |
| 99 | 🔴 | **[YENİ, 22. sohbet — GERİYE DÖNÜK loglandı, sohbet kesildi]** Sandviç checkout'u BLOKLU: "Siparişi Onayla" adımında fiyat ne olursa olsun kırmızı "fiyatlandırılamadı" hatası çıkıyor, sipariş tamamlanamıyor. Kök neden ŞÜPHESİ (doğrulanmadı): `FulfillmentGate.tsx`/`ConfirmPickupOrderButton.tsx`'teki fiyatlandırma kontrolü sadece Bowl'un `bowlItem`/`customization` alanlarını tanıyor, `sandwichCustomization`'ı bilmiyor. Kullanıcıdan `grep -rn "fiyatlandırılamadı" --include="*.tsx" --include="*.ts" .` çıktısı istendi, YANIT GELMEDEN sohbet kesildi. | `components/checkout/FulfillmentGate.tsx` veya `ConfirmPickupOrderButton.tsx` (kesin dosya DOĞRULANMADI) |
| 100 | 🟡 | **[YENİ, 22. sohbet — kod üretildiği İDDİA EDİLDİ, push/test TEYİT EDİLMEDİ]** 4 UI düzeltmesi: (a) `Hero.tsx` buton düzeni `flex-wrap`→`grid grid-cols-2`, mobilde yan yana kalıcı; (b) `SandwichSummaryPanel.tsx`'e TEST VERİSİ rozeti eklendi; (c) `HeroImagePlaceholder.tsx` `aspect-square`→`aspect-[4/3]`+`max-h-72`, mobil taşma düzeltildi; (d) `SandwichCustomizer.tsx` sepete ekleme sonrası artık `/siparis`'e yönlendiriyor (`useRouter`, önceden `store.reset()`+aynı sayfa). | `components/home/Hero.tsx`, `components/sandwich/SandwichSummaryPanel.tsx`, `components/home/HeroImagePlaceholder.tsx`, `components/sandwich/SandwichCustomizer.tsx` |
| 101 | ✅ | **[BU TURDA KAPANDI, 2026-09-03, 23. sohbet]** 22. sohbetteki "Özel Kase" fallback bug'u (`item.bowlItem?.name ?? "Özel Kase"` sandviçlerde hep "Özel Kase" yazdırıyordu) `CartDrawer.tsx`'in bu turdaki motion yükseltmesiyle YENİDEN yazıldı VE test edildi — `CartDrawer.test.tsx`'teki "bowlItem null + sandwichCustomization dolu → Özel Sandviç; ikisi de null → Özel Kase" testi Codespaces'te PASS (8/8, 2026-09-03 06:16, ekran görüntüsü). Bowl davranışı da (`bowlItem?.name` önceliği) happy-path testinde doğrulandı. **KALAN:** push + canlı/production doğrulaması — bkz. #105. | `components/cart/CartDrawer.tsx` |
| 107 | 🟠 | **[YENİ, bu turda — kullanıcının paylaştığı rapor v1.1 tam metninden tespit edildi]** BOWLERA_MOTION_SYSTEM_RAPORU.md §3'ün önerdiği token mimarisi (tek nested `motionTokens.{duration,ease,spring}` objesi) ile `MenuCard.tsx`'in gerçekte import ettiği yapı (`durations`/`easings`/`springs` — üç ayrı top-level export, `durations.menuCardHover` gibi raporda hiç geçmeyen anahtarlarla) BİRBİRİYLE ÇELİŞİYOR. İkisi aynı `tokens.ts` olamaz — ya kod yazılırken rapordan loglanmadan sapıldı, ya da gerçek dosya üçüncü bir yapı. `tokens.ts` görülmeden çözülemez (Kural #2). DESIGN_SYSTEM.md §6.1a'ya not düşüldü (v1.4). **CategoryNav (P0-3) kodlanmadan önce netleşmeli** — aksi halde üçüncü bir tutarsız yapı daha eklenir. | `lib/motion/tokens.ts` (hâlâ görülmedi), `MenuCard.tsx`, `BOWLERA_MOTION_SYSTEM_RAPORU.md` §3 |
| 106 | 🟢 | **[GÜNCELLENDİ, bu turda — kısmen açıklandı]** DESIGN_SYSTEM.md §6.1'deki "Sayfa geçişleri" satırında `"[2026-09-03 güncellendi — önceki: 250ms, kullanıcı isteğiyle yavaşlatıldı]"` notu var (250ms→500ms) — bu değişiklik bu sohbette hiç konuşulmadı, SESSION_INDEX.md'nin hiçbir yerinde loglanmamıştı. **Kısmi açıklama bulundu:** kullanıcının paylaştığı rapor v1.1'in §28 sonunda "Page transitions *(token değeri 500ms'ye güncellendi, bileşen henüz kodlanmadı)*" notu var — yani token değeri değiştirilmiş ama SAYFA GEÇİŞİ BİLEŞENİNİN KENDİSİ HENÜZ KODLANMADI. Hâlâ belirsiz: (a) bu notu kullanıcı mı ekledi yoksa başka bir kaynaktan mı geldi (kullanıcıya bu turda soruldu); (b) `tokens.ts`'teki gerçek değer 500ms mi. | `DESIGN_SYSTEM.md` §6.1, `BOWLERA_MOTION_SYSTEM_RAPORU.md` §28, sayfa geçiş bileşeni (dosya adı doğrulanmadı) |
| 105 | 🟡 | **[2026-09-03, 23. sohbet — Motion System, kullanıcı kararıyla #99/#91'in PARALELİNDE]** Rapor P0-1 (CartDrawer): `lib/motion/tokens.ts` (YENİ) + `AnimatePresence`/spring slide/backdrop fade/içerik stagger/`useReducedMotion` eklendi, `CartDrawer.test.tsx` (YENİ, 8 test) Codespaces'te 8/8 PASS (ekran görüntüsüyle doğrulandı). **[BU TURDA — P0-2 MenuCard]** Canlı bulgu: rapor v1.0 tamamen hover-merkezliydi, mobilde efekt hiç görünmüyordu. Kullanıcı onayıyla `whileTap="hover"` (dokunma=hover ile aynı hedef) + ayrı giriş/çıkış transition'ı (çıkış: spring) eklendi; kullanıcı canlı geri bildirimiyle ("çok sert") spring `stiffness/damping`'den `duration/bounce` (0.45/0.15) tanımına çevrildi; `MenuCard.tsx`+`MenuCardImage.tsx` `springs.cardRelease` (tokens.ts) üzerinden merkezileştirildi (lokal duplikasyon kapandı — AÇIK MADDE: tokens.ts'in gerçek içeriği hiç görülmedi, varsayım). Rapor `BOWLERA_MOTION_SYSTEM_RAPORU.md` v1.0→v1.1'e güncellendi (§1a Dokunmatik Öncelik + §2/§3/§6/§7 senkronu). **KALAN:** (a) GitHub push edilmedi (CartDrawer + MenuCard + MenuCardImage); (b) canlı/production'da GÖZLE doğrulanmadı; (c) ✅ **[BU TURDA KAPANDI]** DESIGN_SYSTEM.md §6.1'e CartDrawer VE MenuCard satırları + yeni §6.1a Spring/Stagger Token Sözlüğü (`springs.cardRelease`/`drawer`/`tactile`/`badge` + `drawerContentStagger` — çoğu ⚠️ VARSAYIM olarak işaretli) + yeni §6.3 Dokunmatik Öncelik + §8 Self-Check maddesi işlendi (v1.2→v1.3); (d) ✅ **[BU TURDA KAPANDI]** CORE.md Dosya Haritası'na `lib/motion/tokens.ts`+`MenuCardImage.tsx`+rapor v1.1 referansı işlendi (v1.7), AGENT.md'ye kalıcı kural eklendi (v1.6); (e) `tokens.ts` dosyasının kendisi HÂLÂ hiç paylaşılmadı — DESIGN_SYSTEM.md §6.1a'daki 4 spring/stagger değeri VARSAYIM olarak işaretli kaldı, teyit edilmeli; (f) MenuCard testleri (`MenuCard.test.tsx`/`MenuCardImage.test.tsx`) yapısal, dokunma davranışını GERÇEK test etmiyor — tek güvenilir doğrulama telefonda canlı deneme. Sıradaki: CategoryNav (P0-3) — MenuCard'daki whileTap kararının buraya yansıması henüz konuşulmadı (§6.1'de not edildi: layoutId zaten state-bazlı, bu kuraldan etkilenmiyor). | `lib/motion/tokens.ts`, `components/cart/CartDrawer.tsx`, `CartDrawer.test.tsx`, `components/menu/MenuCard.tsx`, `components/menu/MenuCardImage.tsx`, `DESIGN_SYSTEM.md`, `CORE.md`, `BOWLERA_MOTION_SYSTEM_RAPORU.md` |
| 102 | 🟢 | **[YENİ, 22. sohbet — push/test TEYİT EDİLMEDİ]** `OrderSummary.tsx` satır 20 — CartDrawer'daki (#101) BİREBİR AYNI "Özel Kase" fallback bug'u burada da bulundu, aynı desenle genişletildi ("Özel Sandviç"). | `components/order/OrderSummary.tsx` |
| 103 | 🟢 | **[YENİ, 22. sohbet — push/test TEYİT EDİLMEDİ]** `OrderSummary.tsx`'e CartDrawer'daki gibi "Kaldır" butonu eklendi — eski fiyat düzeltmesinden ÖNCE sepete girmiş 0₺'lik test ürünlerini temizlemek için. | `components/order/OrderSummary.tsx` |
| 104 | 🟡 | **[YENİ, 22. sohbet — çözülmeden kaldı]** #100(d) fix'i sonrası `SandwichCustomizer.test.tsx`'in sepete-ekleme testleri artık `router.push` çağıracak — `next/navigation`'ın `useRouter`'ı test ortamında mock'lanmadıysa testler kırılabilir. Kullanıcıya "şimdi düzelteyim mi yoksa `npx vitest run components/sandwich` çalıştırıp kırmızı çıkanı mı paylaşırsın" soruldu, YANIT GELMEDEN sohbet kesildi. | `components/sandwich/SandwichCustomizer.test.tsx` |

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

*(Tam turn-by-turn detay: `session_arşiv.md` [0-10], `session_arşiv_1.md` [11+].)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel. `lib/db/schema.ts` (users.role eklendi) kullanıcı tarafından manuel push edildi. ✅ Önceki turdaki `channel-options.ts` build kırığı düzeltildi, Vercel deploy YEŞİL (1d KAPANDI). |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 kod ile hizalı — ⚠️ ROADMAP.md'ye #62 (Personel Sipariş Paneli) hiç işlenmemiş, ayrı bir oturum/kalem olarak eklenmesi gerekebilir. ARCHITECTURE.md v1.12'ye güncellendi, henüz koda tam yansımadı (DB var, kod yok). ⚠️ **[Bu turda]** `BOWLERA_COK_SUBELI_CRM_VIZYON.md` adlı YENİ, ayrı bir taslak vizyon belgesi üretildi (ARCHITECTURE.md'nin YERİNE geçmiyor) — çok şubeli mimari + CRM/attribution önerisi içeriyor, henüz resmi dosyalara (ARCHITECTURE.md) işlenmedi, sadece Açık Sorunlar #92/#93/#94'te özetlendi. |
| Test Suite | 🟢 `guest-gate.test.ts` (8 — kullanıcı tarafından koşuldu, PASS doğrulandı). **[BU TURDA]** `rate-limit.test.ts` (11) + `middleware.test.ts` (10) + `auth.test.ts` (13) = 33/33 PASS, Codespaces'te kullanıcı tarafından koşuldu ve doğrulandı — SEC-01/SEC-02 kapsamı. Genel `npm test` (TÜM proje, tüm dosyalar) hâlâ hiç çalıştırılmadı. ⚠️ `users.role` migration'ı için TEST_MATRIX.md güncellemesi BEKLEMEDE (dosya paylaşılmadı). |
| Auth | 🟡 Twilio/Netgsm PARKLI. Genel giriş/kayıt akışı karar olarak netleşti, guest gate middleware'i KODLANDI ve repoda doğrulandı. Masaya Sipariş kanalı middleware'in kapsamı dışında AYRI bir yüzeyde (`/masaya-siparis/*`) yaşayacak — bu yüzey henüz kodlanmadı. Gel Al akışı için "Sepete Ekle" bypass guard'ı (#66) hâlâ eksik. `/personel/*` role bazlı guard'ı ✅ TAMAMLANDI — 4 dosya senkron, canlı build yeşil doğrulandı. **[Önceki tur]** Telefon+şifre girişi (#82) VE şifre sıfırlama (#83) canlıda TAM doğrulandı (her iki döngü de test edildi) — ikisi de KAPANDI. Login sonrası isim gösterme sorunu (#84) de canlıda düzelmiş görüldü, KAPANDI (kök neden formel izole edilmedi). **[BU TURDA]** Güvenlik denetimi SEC-01 (rol revocation) + SEC-02 (login rate-limit) kod+test (33/33)+build+tsc TAMAM — canlı manuel doğrulama BEKLİYOR (#91). |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE canlıda test edildi (#39 KAPANDI). ⚠️ Kaydet butonu `bg-olive-600` (kırık) → `bg-[#53502A]` (arbitrary value, çalışıyor) — kök neden #73'te açık. |
| Kullanıcı Kaydı (rıza esaslı) | 🟢 Backend+Frontend TAMAM, canlı test BAŞARILI, oturum+isim gösterimi DOĞRULANDI (#59 KAPANDI). Kanal seçimi zorunlu adımı henüz KODLANMADI (bkz. 1b). |
| Checkout (`/siparis`) | 🟢 Bowl için kod tamam VE repoda doğrulandı, SADECE Gel Al'a özel (§2.9). Masaya kendi bağımsız mini-checkout'unu kullanacak (ARCHITECTURE.md v1.8) — henüz KODLANMADI. 🔴 **[22. sohbet]** Sandviç için checkout BLOKLU — fiyat ne olursa olsun "fiyatlandırılamadı" hatası çıkıyor, sipariş tamamlanamıyor, kök neden DOĞRULANMADI (bkz. #99). |
| Veritabanı | 🟢 Neon Postgres çalışıyor. `consentRegistrations` ve `order_history` migrate edildi. `users.role` (`text`, `NOT NULL`, `DEFAULT 'customer'`) migrate edildi ve DOĞRULANDI (Tables görünümü, screenshot). **[Bu turda]** `consentRegistrations.ipAddress` (nullable) + yeni `registrationBlockedAttempts` tablosu (#89) migrate edildi, 6 sorguyla DOĞRULANDI — diğer tablolar etkilenmedi. `users` tablosu hâlâ 0 satır (#32 Twilio kısıtı). ⚠️ DB şifresi reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik (#63). ⚠️ `order_history.table_number` kolonu KARARLAŞTIRILDI, migration HENÜZ KOŞULMADI — tip netleşmeden koşulmamalı (#70). **[Bu turda, 19. sohbet]** Neon'un TAM güncel şeması sorguyla doğrulandı: 5 tablo (`users`, `consent_registrations`, `order_history`, `password_reset_requests`, `registration_blocked_attempts`) — `branches` veya herhangi bir menü/ürün tablosu YOK (bkz. #92/#93). |
| Personel Sipariş Paneli (#62) | 🟢 Masaya sekmesi TAMAMLANDI + canlı doğrulandı. `/personel/*` + `/api/personel/*` guard'ı ikisi de canlı build yeşil. 🟡 **[BU TURDA]** Gel Al onay kuyruğu — canlı bulgu üzerine 3-durumlu revizyon (KARAR A): `confirmed` artık terminal değil ("Hazırlanıyor"), yeni terminal `completed` ("Teslim Edildi") eklendi. 7 kaynak + 5 test dosyası (2'si YENİ — projedeki ilk API route testleri) kodlandı, Codespaces'te 37/37 PASS. **SADECE canlı ortamda "Teslim Edildi" tıklama testi BEKLİYOR.** 🟡 Kayıt Onayları (4. sekme, #86) — 8 dosya kodlandı, Gel Al deseniyle tutarlı, tam repo zip'inden statik incelendi, `npm run build`/`tsc --noEmit` YEŞİL (kullanıcı Codespaces'te doğruladı, push edildi). Test seti + canlı doğrulama BEKLİYOR. 🟢 **[önceki tur]** Şifre Talepleri/Gel Al/Kayıt Onayları sekmelerine bekleyen sayısı rozeti eklendi (DESIGN_SYSTEM.md v1.2 §2.2 personel-paneli kırmızı istisnasıyla), push edildi — test/canlı doğrulama bekliyor. |
| Motion System (Bowlera Premium Motion Raporu, v1.1) | 🟡 **[BU TURDA]** Rapor v1.0→v1.1 (§1a Dokunmatik Öncelik eklendi — mobil trafik gerçeğiyle senkron). P0-1 CartDrawer kod+test TAMAM (8/8 PASS). P0-2 MenuCard kod TAMAM — `whileTap="hover"` + `springs.cardRelease` (duration/bounce, merkezi tokens.ts) — canlı iki tur geri bildirimle kalibre edildi ("mobilde görünmüyor" → "çok sert"). Hepsi PUSH/CANLI DOĞRULAMA BEKLİYOR (bkz. #105). Kalan: CategoryNav (P0-3, MenuCard kararının yansıması netleşmedi), AccountMenu/Header/Hero/Page transitions (P1), Cart badge/Customizer/VisualPreview (P2), Instagram marquee (P3). |
| Mimari Dokümantasyon | 🟡 ARCHITECTURE.md v1.12 — hâlâ bu turdaki değişiklikleri yansıtmıyor: §4.1'deki `users.role` "HENÜZ KOŞULMADI" notu KOŞULDU'ya, §2.9a'ya Masaya kısmının TAMAMLANDIĞI ve `order_history` şema genişletmesi (status/table_number/customer_notes) işlenmeli — bkz. SIRADAKİ GÖREVLER 1d. ⚠️ DEPENDENCIES.md v1.1 (Session 3) — genel olarak ESKİ, ayrı bir turda kapsamlı güncelleme gerekiyor (#71). ⚠️ **[Bu turda]** Çok şubeli mimari + CRM/attribution önerisi `BOWLERA_COK_SUBELI_CRM_VIZYON.md`'de taslak — ARCHITECTURE.md'ye HENÜZ İŞLENMEDİ, önce kullanıcı onayı gerekiyor (bkz. #92/#93/#94). |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| -5a | **[YENİ, 23. sohbet devamı, 2026-09-03 — bu turda karar verildi]** `lib/motion/tokens.ts` satır 61: `springs.cardRelease` `{stiffness:300, damping:24}`'ten `{duration:0.45, bounce:0.15}`'e DÜZELTİLMELİ — bu değer daha önce canlı testte 2 turda kalibre edilmişti ama koda hiç yansımamış (bkz. DESIGN_SYSTEM.md v1.5, §6.1a). Tek satırlık değişiklik, push+canlı doğrulama gerekiyor. | 🔴 |
| -5 | **[YENİ, 22. sohbet]** #99 — Sandviç checkout'u BLOKLU, "fiyatlandırılamadı" hatası her zaman çıkıyor. Kullanıcıdan `grep -rn "fiyatlandırılamadı" --include="*.tsx" --include="*.ts" .` çıktısı isteniyor, kök neden bulunup düzeltilmeli. **AYRICA:** #100-#104'teki 7 dosya değişikliğinin (Hero/SandwichSummaryPanel/HeroImagePlaceholder/SandwichCustomizer/CartDrawer/OrderSummary×2) hangilerinin fiilen push/test edildiği kullanıcıdan tek tek teyit alınmalı — hiçbiri varsayılan "tamam" sayılmasın. | 🔴 |
| -4b | **[YENİ, 2026-09-03 — kullanıcı kararıyla #99/#91'İN PARALELİNDE, önlerine geçmiyor]** Motion System rapor P0-2/P0-3: MenuCard (lift+image zoom), CategoryNav (`layoutId` active pill). P0-1 (CartDrawer) bu turda TAMAMLANDI (bkz. #105) — kod+test var, push/canlı doğrulama + DESIGN_SYSTEM.md/CORE.md senkronu hâlâ bekliyor. | 🟡 |
| -4 | **[YENİ, bu turda]** #92/#93/#94 — Çok şubeli mimari + şube-bazlı menü + CRM/attribution katmanı — SADECE analiz+öneri yapıldı (`BOWLERA_COK_SUBELI_CRM_VIZYON.md`), kod YOK. Kullanıcı kararıyla #91'DEN SONRAYA alındı. | 🟡 (kullanıcı kararıyla #91'in ardında) |
| -3 | **[YENİ, bu turda]** #91 — Güvenlik denetimi SEC-01/SEC-02 kod+test+build+tsc TAMAM. **KALAN:** canlıda (a) role-revocation 403 testi, (b) 6. yanlış şifre denemesinin reddi — ikisi de GÖZLE doğrulanmalı, sonra 5 dosya GitHub'a push edilmeli. | 🔴 |
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
| 1g | **[YENİ, bu turda]** SANDWICH_SPEC.md §8'deki 6 açık soru (S1-S6) netleştirilmeli — özellikle S1 (gerçek `sandwich-data.json` — ekmek/protein/peynir/sebze/sos + fiyat/kalori) BLOKLAYICI, kod üretimi bu veri olmadan başlayamaz | 🟡 |
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

*BOWLERA SESSION_INDEX.md — v74 (v73'ten: **[23. sohbet devamı, 2026-09-03, yeni sohbet]**
`tokens.ts` nihayet paylaşıldı. **#107 KAPANDI** ✅ — yapı çelişkisi çözüldü, gerçek kod düz
`durations/easings/springs` export'ları kullanıyor (raporun nested `motionTokens.*` önerisi
DEĞİL). 4 token değeri teyit edildi (`drawer`, `tactile`, `badge`, `drawerContentStagger` —
hepsi ✅, bkz. DESIGN_SYSTEM.md v1.5). **🔴 YENİ BULGU (ciddi):** satır 134-137'deki Kural #2
riski gerçekleşti — `MenuCard.tsx`'in mobil-tactile kalibrasyonunda kullandığı varsayılan
`springs.cardRelease` değeri (`duration:0.45/bounce:0.15`, canlı 2 turda kullanıcı tarafından
onaylanmıştı) `tokens.ts`'te YOK; dosyada hâlâ ESKİ değer (`stiffness:300/damping:24`,
"çok sert" bulunup terk edilen değer) duruyor. Yani canlıda MenuCard'ın gerçekten kalibre
edilmiş yumuşak spring'i mi yoksa terk edilen sert spring'i mi kullandığı ŞÜPHELİ — kod teyidi
öncesi varsayılan doğru kabul edilmişti, şimdi yanlış çıktı. **Karar bu turda verildi (kullanıcı
"sen karar ver" dedi):** canlı kullanıcı testi esas alınır, `tokens.ts` satır 61
`duration:0.45, bounce:0.15` olarak düzeltilmeli — bkz. yeni Açık Sorun -5a (🔴, en üst öncelik,
tek satırlık kod değişikliği). #106 hâlâ kısmen açık (hangi sohbette 250→500ms değiştiği
belirsiz), ama `tokens.ts`'teki yorum satırı değişikliğin kasıtlı/kullanıcı-istekli olduğunu
doğruluyor — pratik risk düşük, düşük öncelikte bırakıldı. Güncellenme: 2026-09-03.*
