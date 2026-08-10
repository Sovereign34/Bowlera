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
> ⚠️ **TAŞIMA NOTU (2026-08-10, 13. sohbet devamı):** SESSION_INDEX.md 463 satıra ulaşınca
> (400 satır eşiği aşıldı, CORE.md §7.1 Adım 1), 4 kapanmış/güncelliğini yitirmiş CURRENT
> FOCUS bloğu (SOHBET KAYBI uyarısı, iki adet #62 Gel Al ara-durum bloğu, #82/#83/#84 kapanış
> bloğu) TAM metinleriyle `session_arşiv_1.md`'ye taşındı — kullanıcıya ayrı bir eklenti
> dosyası (`session_arsiv_1_EKLENTI_2026-08-10.md`) olarak verildi, kendi elinizle mevcut
> `session_arşiv_1.md`'nizin sonuna eklemeniz gerekiyor. Her taşınan madde için kapanış
> gerekçesi o dosyada mevcut.

---

## 🎯 CURRENT FOCUS

> ⚠️ **Arşiv taşıması — 2026-08-10:** 3 kapanmış CURRENT FOCUS bloğu (#74 çıkış butonu
> kapanışı, #62 Masaya sekmesi tam kapanışı, #79 masaüstü fix'i) `session_arşiv_1.md`'ye
> taşındı — CORE.md §7.1 Adım 1 (400 satır eşiği). Kapanış gerekçesi: hepsi Kritik Kararlar
> tablosunda ve/veya Açık Sorunlar tablosunda satır olarak zaten özetli duruyor, turn-by-turn
> anlatı artık aktif takip gerektirmiyor. Taşıma bloğu ayrı olarak sunulacak.

> **[YENİ SOHBET (devamı, 13.), 2026-08-10 — #86 Kayıt Onayları (4. sekme), KOD TARAFI
> TAMAMLANDI, build/test/canlı doğrulama BEKLİYOR]**
> **(1) Kapsam:** `users.verificationStatus: "pending"→"confirmed"` — Gel Al'ın onayladığı
> SİPARİŞLERDEN (`orderHistory`) ayrı, ilgisiz bir akış: bu panel doğrudan KAYITLARI
> (`users`) onaylıyor. Liste `users.createdAt` sırasına göre (en eski üstte), Gel Al
> kuyruğuyla aynı desen. 2 aksiyon: Teyit Et (`verificationStatus="confirmed"`), Reddet/Sil
> (hem `users` hem `consentRegistrations` satırı `customerPhone` eşleşmesiyle KALICI silinir).
> **(2) Referans dosyalar zip'ten (`Bowlera_site-main`) tam repo taramasıyla doğrulandı:**
> `GelAlPanel.tsx`, `gel-al-queries.ts`, `gel-al/route.ts`, `gel-al/[id]/route.ts`,
> `api-guards.ts`, `usePersonelGelAlQueue.ts`, `GelAlOrderCard.tsx` — hepsi görüldü, aynı
> iskelet bilinçli olarak kopyalandı (Kural #5 gerekçesiyle ortak üst bileşene ÇIKARILMADI).
> **(3) Çakışma notu ele alındı:** Masaya'nın #82 auto-confirm'ü (`preparing`'e geçince
> `verificationStatus="confirmed"`) ve Gel Al'ın confirm'ü de aynı alana yazıyor — ama liste
> sorgusu zaten `verificationStatus="pending"` filtreli olduğu için gerçek bir çakışma değil,
> kayıt başka bir yoldan confirm olursa bu kuyruktan otomatik düşer.
> **(4) Gel Al'dan sapan tek nokta (bilinçli, KARAR BİLDİRİMİ'nde gerekçeli):** race
> durumunda 404 "zaten işlenmiş" dönebilmesi için `confirmRegistration`/`deleteRegistration`
> içine varlık kontrolü eklendi — Gel Al'ın basit UPDATE'inde bu kontrol yok, oradaki risk
> orderId bazlı olduğu için daha düşük görülmüştü.
> **(5) 8 dosya üretildi (kullanıcıya TAM dosya olarak verildi, "eklenecek" notu YOK —
> önceki turda bu konuda kullanıcı şikâyeti oldu, düzeltildi):** `types/index.ts` (tam dosya,
> `RegistrationApprovalEntry` eklendi), `lib/personel/kayit-onaylari-queries.ts`,
> `app/api/personel/kayit-onaylari/route.ts`, `app/api/personel/kayit-onaylari/[id]/route.ts`,
> `hooks/usePersonelRegistrationQueue.ts`, `components/personel/KayitOnayCard.tsx`,
> `components/personel/KayitOnaylariPanel.tsx`, `app/personel/page.tsx` (4. sekme eklenmiş
> tam dosya, `border-[#53502A]` bilinen-çalışan deseni kullanıldı, #73'teki kırık
> `border-olive-primary`'den kaçınıldı).
> **(6) [GÜNCELLEME, aynı sohbet devamı] Build tarafı DOĞRULANDI:** Kullanıcı Codespaces'te
> `tsc --noEmit` (hatasız) ve `npm run build` (route tablosu/boyut özeti üretildi — bu,
> Next.js'in SADECE başarılı derlemede yazdırdığı bir çıktı, dolaylı ama güvenilir kanıt)
> çalıştırdı, sonucu GitHub'a manuel push etti (bu arada ilgisiz 4 eski dosya —
> `orders/[id]/confirm`+`reject` route'ları, `WhatsAppOrderButton.tsx`+testi — kullanıcı
> tarafından BİLİNÇLİ olarak ayrıca silinmiş, kayıt onayları değişikliğiyle ilgisi yok).
> #86 build tarafı KAPANDI. **HÂLÂ DOĞRULANMADI:** test seti (Kural #6) yok, canlı ortamda
> (Vercel deploy sonrası) Teyit Et/Reddet-Sil aksiyonları gerçek bekleyen kayıtla hiç test
> edilmedi. middleware.ts'e DOKUNULMADI (öneki `/api/personel` zaten kapsıyor).

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
| 62 | 🟠 | Personel Sipariş Paneli — Masaya sekmesi TAMAMLANDI + canlı doğrulandı. **Gel Al onay kuyruğu:** 7 dosya kodlandı, tam repo zip'inden statik incelendi, `types/index.ts`+`page.tsx` senkron (HIGH confidence), **`npm run build` YEŞİL (kullanıcı doğruladı)**. **KALAN:** test seti yok + BSC-4/reduced-motion/bayat yorum bulguları (bkz. #85) + canlı ortamda 3 aksiyon (Onayla/Ulaşamadım/Reddet) hiç test edilmedi. | ARCHITECTURE.md §2.9a |
| 85 | 🟡 | **[YENİ, bu turda]** Gel Al kod incelemesi bulguları: (1) `GelAlPanel.tsx` `catch{}` sessiz — BSC-4, MasayaPanel'deki AYNI kalıbın tekrarı; (2) `GelAlOrderCard.tsx` `hover:scale-[1.02]` reduced-motion kontrolsüz; (3) `GelAlOrderCard.tsx` + `gel-al-queries.ts`'de BAYAT yorum ("types/index.ts'e eklenecek" — artık eklenmiş durumda, BEŞİNCİ DERS kalıbı); (4) eşzamanlı-güncelleme/optimistic-lock riski (#81'in Masaya'daki karşılığı) Gel Al için hiç loglanmamış; (5) test seti (Kural #6) hiç yok. Build'i etkilemiyor ama "tamamlandı" sayılmadan önce ele alınmalı. | `components/personel/GelAlPanel.tsx`, `GelAlOrderCard.tsx`, `lib/personel/gel-al-queries.ts` |
| 86 | 🟡 | **[Bu turda, build DOĞRULANDI]** Kayıt Onayları (4. sekme) — 8 dosya kodlandı, tam repo zip'inden statik incelendi, Gel Al deseniyle tutarlı. Kullanıcı Codespaces'te `tsc --noEmit` (hatasız) VE `npm run build` (route tablosu/size özeti başarıyla üretildi — Next.js bu tabloyu SADECE derleme başarılıyken yazdırır) çalıştırdı, GitHub'a push edildi. **Build tarafı KAPANDI.** **KALAN:** test seti (Kural #6) yok, canlı ortamda Teyit Et/Reddet-Sil hiç test edilmedi (ÜÇÜNCÜ DERS — kod+build ≠ kullanıcı deneyimi doğrulandı). | `lib/personel/kayit-onaylari-queries.ts`, `app/api/personel/kayit-onaylari/*`, `components/personel/KayitOnaylariPanel.tsx` |
| 63 | 🟠 | `npm install`: 12 açık/3 kritik güvenlik açığı — `npm audit fix --force` bilinçli KOŞULMADI | `package.json` |
| 66 | 🟢 | İmza kase "Sepete Ekle" butonu (customize'a girmeden direkt ekleme) guest gate middleware'i tarafından YAKALANMIYOR — component-seviyesi guard gerekiyor. **[Session 12 devamı, kapsam teyidi]:** bu, `/menu/customize/*` (Gel Al) bağlamına özgüdür — Masaya artık ayrı `/masaya-siparis/*` yüzeyinde olduğu ve zaten auth gerektirmediği için bu sorunla kesişmiyor. AÇIK KARAR (kullanıcıdan teyit bekliyor): 1b'nin ayrı alt-görevi mi, bilinçli açık mı? | `components/customizer/AddToCartButton.tsx` |
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
| Veritabanı | 🟢 Neon Postgres çalışıyor. `consentRegistrations` ve `order_history` migrate edildi. **[Bu turda]** `users.role` (`text`, `NOT NULL`, `DEFAULT 'customer'`) migrate edildi ve DOĞRULANDI (Tables görünümü, screenshot). `users` tablosu hâlâ 0 satır (#32 Twilio kısıtı). ⚠️ DB şifresi reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik (#63). ⚠️ `order_history.table_number` kolonu KARARLAŞTIRILDI, migration HENÜZ KOŞULMADI — tip netleşmeden koşulmamalı (#70). |
| Personel Sipariş Paneli (#62) | 🟢 Masaya sekmesi TAMAMLANDI + canlı doğrulandı. `/personel/*` + `/api/personel/*` guard'ı ikisi de canlı build yeşil. 🟠 Gel Al onay kuyruğu (3. sekme) — tip katmanı + `page.tsx` entegrasyonu teyit edildi, tam kod incelendi, `npm run build` YEŞİL. Test seti + BSC-4/reduced-motion bulguları (#85) + canlı doğrulama BEKLİYOR. 🟡 **[Bu turda]** Kayıt Onayları (4. sekme, #86) — 8 dosya kodlandı, Gel Al deseniyle tutarlı, tam repo zip'inden statik incelendi, **`npm run build`/`tsc --noEmit` YEŞİL (kullanıcı Codespaces'te doğruladı, push edildi)**. Test seti + canlı doğrulama BEKLİYOR. |
| Mimari Dokümantasyon | 🟡 ARCHITECTURE.md v1.12 — hâlâ bu turdaki değişiklikleri yansıtmıyor: §4.1'deki `users.role` "HENÜZ KOŞULMADI" notu KOŞULDU'ya, §2.9a'ya Masaya kısmının TAMAMLANDIĞI ve `order_history` şema genişletmesi (status/table_number/customer_notes) işlenmeli — bkz. SIRADAKİ GÖREVLER 1d. ⚠️ DEPENDENCIES.md v1.1 (Session 3) — genel olarak ESKİ, ayrı bir turda kapsamlı güncelleme gerekiyor (#71). |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| -1 | **[TAMAMLANDI, bu turda ✅]** #84 — isim gösterme sorunu kullanıcı tarafından canlıda ("bari" görünür) doğrulandı. Kök neden SQL sorgusuyla izole edilmedi, kullanıcı deneyimi seviyesinde kapandı. | ✅ |
| 0 | **[TAMAMLANDI, bu turda ✅]** #83 — "Sıfırla" → üretilen geçici kodla (460244) giriş canlıda BAŞARILI test edildi. | ✅ |
| 0b | **[TAMAMLANDI, bu turda ✅]** #82 — Neon'a elle dokunmadan, orijinal kayıt şifresiyle çıkış→giriş döngüsü canlıda BAŞARILI test edildi. | ✅ |
| 0a | #80 — masaüstünde (`SummaryPanel.tsx`) #79 fix'inin canlı doğrulaması notu (düşük öncelik, kullanıcı kararıyla #79/#75 kapatıldı) | 🟢 |
| 0c | #78 — Customizer sticky özet panelin collapsed halde "Sepete Ekle"yi gizlemesi için UX çözümü kararlaştırılıp uygulanmalı (bu turda ek ekran görüntüsüyle yeniden doğrulandı) | 🟢 |
| 1 | #62 Masaya sekmesi TAMAMLANDI + canlı doğrulandı (önceki tur). **[Bu turda]** Gel Al onay kuyruğu — 7 dosya kodlandı+incelendi, `npm run build` YEŞİL. **KALAN:** #85'teki 5 bulgu (test seti, BSC-4, reduced-motion, 2 bayat yorum, race-condition notu) ele alınmalı, sonra canlı doğrulama (Onayla/Ulaşamadım/Reddet üçü de). | 🟠 |
| 1c | **[Bu turda]** #86 Kayıt Onayları (4. sekme) — kod+build tarafı KAPANDI (Codespaces'te `tsc --noEmit` + `npm run build` başarılı, GitHub'a push edildi). **KALAN:** test seti yazılmalı, canlı ortamda (Vercel deploy sonrası) Teyit Et/Reddet-Sil aksiyonları gerçek bir bekleyen kayıtla test edilmeli. | 🟡 |
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

*BOWLERA SESSION_INDEX.md — v53 (v52'den: 400 satır eşiği aşıldığı için 4 kapanmış CURRENT
FOCUS bloğu `session_arşiv_1.md`'ye taşındı — bkz. üstteki TAŞIMA NOTU + ayrı eklenti
dosyası. İçerik/karar/durum DEĞİŞMEDİ, sadece dosya hafifletildi (463→~344 satır).
Güncellenme: 2026-08-10.*
