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

> **[YENİ SOHBET, 2026-08-08 — #62 Personel Sipariş Paneli, ARCHITECTURE.md v1.12]**
> Vercel build'in yeşil olduğu kullanıcı tarafından doğrulandı (1d KAPANDI). Ardından #62
> tartışıldı: ARCHITECTURE.md §2.9a'daki 3 açık mimari soru Claude'un önerisi + kullanıcı
> onayıyla KAPANDI:
> 1. **Personel Auth:** Mevcut Auth.js sistemine `users.role: "customer" | "staff"` alanı
>    eklenerek rol bazlı yetkilendirme (ayrı personel-hesap sistemi veya paylaşımlı-cihaz
>    PIN yerine) — gerekçe: mevcut session mekanizmasını tekrar kullanmak, iki paralel
>    auth mantığı yaratmamak.
> 2. **Real-Time Teknoloji:** Basit polling (WebSocket/SSE yerine) — kullanıcı tercihi.
> 3. **Onay Kuyruğu UI:** İki ayrı sekme/panel (Masaya real-time akışı / Gel Al onay
>    kuyruğu) — tek filtreli liste yerine; farklı veri şekli + farklı aksiyon seti
>    gerektirdiği için.
> **ARCHITECTURE.md v1.12'ye işlendi:** §1 Katman Sınırı Kuralı'na madde 13 eklendi
> (`users.role` migration'ının CORE.md §7.4 notu gerektirdiği uyarısı); §2.9a üç karar
> bloğuyla genişletildi; §3 `AuthenticatedUser` tipine `role` alanı planı not edildi
> (henüz kodlanmadı); §4.1 Deploy tablosuna migration bekleyen `users.role` kolonu notu
> eklendi.
> **Bu turda kod ÜRETİLMEDİ, migration KOŞULMADI** — sadece mimari karar dokümantasyonu
> (Kural #6 gereği, kod aşamasına geçilmeden önce bu KARAR BİLDİRİMİ + onay adımı
> tamamlanmalı). **Bir sonraki adım kodlama DEĞİL** — önce `users.role` için CORE.md §7.4
> formatında ayrı bir şema değişiklik notu üretilmeli (bkz. SIRADAKİ GÖREVLER 1).
> **Kullanıcı isteği üzerine bu turda SADECE SESSION_INDEX güncellendi** — TEST_MATRIX.md
> bilinçli olarak GÜNCELLENMEDİ (kod/test yok, güncellenecek bir şey de yoktu; bir sonraki
> gerçek test-etkili checkpoint'e bırakıldı).

> **[Önceki tur, aynı sohbet — Masa Numarası Kararı, ARCHITECTURE.md v1.11]** ⚠️ Önceki
> sohbet bu konuyu (masa numarası) konuşurken SESSION_INDEX güncellenmeden kesilmişti —
> DÖRDÜNCÜ DERS'in tarif ettiği durumun bir tekrarı, bu sohbette geriye dönük tamamlandı.
> **Karar (kullanıcı onaylı):** Masaya Sipariş akışında masa numarası TUTULACAK — terk
> edilmeyecek. Gerekçe: QR akışının amacı "okut, saniyeler içinde sipariş ver"; masa
> numarası olmadan personel siparişi hangi masaya götüreceğini bilemez, bu da sürtünmesiz
> deneyimi sıfırlar. Session 9-12 arası bu konu hiç ele alınmamış bir senkron boşluğuydu —
> §2.7a→§2.7b izolasyonu SADECE kimlik/rıza akışını kaldırmıştı, masa numarasını değil.
> **Uygulama kararları:** (1) Route path segment — `/masaya-siparis/[tableId]` (query param
> DEĞİL, projede o konvansiyon hiç yok); (2) `tableId`, `useCartStore`'a alan olarak yazılır
> (`CartState.tableId` + `setTableId()`) — ayrı state kurulmadı, paylaşılan sepetle tutarlı;
> (3) `order_history`'ye nullable `table_number` kolonu eklenecek (SADECE channel="dine-in").
> Bu (3), gerçek bir DB şema değişikliği — CORE.md §7.4 formatında ayrı not üretildi:
> `docs/schema-changes/20260808010000_order_history_tablenumber_eklendi.md`.
> **ARCHITECTURE.md v1.10 → v1.11:** §2.3 (`CartState.tableId`), §2.7b (Masa numarası kararı
> alt bölümü), §3 (`OrderHistoryEntry` yer tutucu notu), §4.1 (migration bekleyen kolon notu)
> güncellendi.
> ⚠️ **Öz-düzeltme (bu sohbette):** Bir önceki turda "`types/index.ts`'te `CartState`'e
> `tableId` eklerim" denmişti — bu YANLIŞTI. `CartState`, `types/index.ts`'te tanımlı değil,
> sadece ARCHITECTURE.md §2.3'te (`store/useCartStore.ts` kontratı olarak) dokümante
> ediliyor. Düzeltme bu turda doğru yere (§2.3) yapıldı.
> ⚠️ **#69'un kısmi yeniden değerlendirmesi:** #69 ("order_history.channel ayrımı YETERLİ,
> ek alan gerekmiyor") gerekçesiz düşürülmedi — hâlâ doğru (channel ayrımı için). Ama farklı
> bir soruyu (aynı kanal içinde HANGİ masa) hiç kapsamıyordu; bu yeni gereksinimle
> `table_number` kolonu ekleniyor. #69 KAPALI kalıyor, kapsamı genişletildi (bkz. Açık Soru
> #70, yeni).
> **Bu turda SADECE dokümantasyon üretildi** (ARCHITECTURE.md + şema notu) — `store/useCartStore.ts`
> kodu, `/masaya-siparis/[tableId]` route'u ve migration'ın kendisi HENÜZ YAZILMADI/KOŞULMADI.

> 🔴🐛 **[Önceki tur — CANLI BUILD KIRIĞI BULUNDU VE ÇÖZÜLDÜ]** Kullanıcı Vercel
> build log'u paylaştı: `components/registration/channel-options.ts` hâlâ
> `RegistrationChannel`'a `"masaya-siparis"` değeri atıyordu — bu değer #68 kararıyla
> (ARCHITECTURE.md v1.9, Session 12 devamı) tipten ÇIKARILMIŞTI, ama bu dosya o turda hiç
> görülmediği için güncellenmemiş kalmıştı. **Kök neden:** DEPENDENCIES.md'de
> `RegistrationChannel`'ın tüketicisi olarak `channel-options.ts` KAYITLI DEĞİLDİ — #68
> kapanırken bu yüzden atlandı. Bu, ÜÇÜNCÜ DERS'in (Session 8) bir varyantı: "kod+test
> yeterli değil" ilkesi burada "tip değişikliği tüm tüketicilere yayıldı mı" şekline
> genişletilmeli.
> **Düzeltme:** `channel-options.ts`'ten `"masaya-siparis"` seçeneği kaldırıldı — kullanıcı
> onayıyla uygulandı. Tek tüketici `RegistrationForm.tsx` görüldü, `.map()` ile dinamik
> render ediyor — sabit-index/sabit-genişlik varsayımı yok, kırılma riski taşımıyor
> (confidence: HIGH). DB etkisi yok — `consentRegistrations.channel` enum değil düz `text`,
> geçmiş `"masaya-siparis"` kayıtları (Session 9) etkilenmedi, sadece yeni kayıt formundan
> bu seçenek kalktı.
> **✅ [Bu turda doğrulandı] 1d KAPANDI:** Kullanıcı Vercel deploy'unun yeşil olduğunu
> teyit etti.
> **Açık Sorun #71 hâlâ AÇIK:** DEPENDENCIES.md, `RegistrationChannel`'ın tüketicisi olarak
> `channel-options.ts`'i (ve muhtemelen başka görülmemiş dosyaları) hiç listelemiyor — tip
> daraltma kararları verilirken bu dosya sistematik olarak taranmalı. DEPENDENCIES.md bu
> sohbette paylaşıldı (v1.1, Session 3) ama #71'in düzeltmesi (RegistrationChannel
> tüketicilerinin eksiksiz taranması) bu turun kapsamı dışında kaldı — ayrıca not: bu dosya
> da genel olarak ESKİ (`useCartStore.tableId`, `order_history` gibi yeni alanlar/tablolar
> haritada yok), bir sonraki uygun turda güncellenmeli.

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
| 🗄️ | **[YENİ SOHBET, 2026-08-08, KRİTİK — ARCHITECTURE.md v1.12]** #62'nin 3 mimari sorusu KAPANDI: (1) Personel auth = `users.role` alanıyla mevcut Auth.js'e rol bazlı yetki (2) Real-time = basit polling (3) Onay kuyruğu UI = iki ayrı sekme/panel (Masaya / Gel Al). `users.role` gerçek bir şema değişikliği — migration/CORE.md §7.4 notu HENÜZ ÜRETİLMEDİ. | ✅ Karar netleşti + doküman güncellendi, migration/kod HENÜZ YAZILMADI/KOŞULMADI |

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
| 62 | 🟡 | Personel Sipariş Paneli — 3 mimari soru (auth/real-time/UI) bu turda KAPANDI (bkz. Kritik Kararlar). Kalan: `users.role` şema değişiklik notu (CORE.md §7.4) + migration + panelin kendisi HENÜZ YAZILMADI. | `order_history`, `users.role` (henüz şemada yok), ARCHITECTURE.md §2.9a |
| 63 | 🟠 | `npm install`: 12 açık/3 kritik güvenlik açığı — `npm audit fix --force` bilinçli KOŞULMADI | `package.json` |
| 66 | 🟢 | İmza kase "Sepete Ekle" butonu (customize'a girmeden direkt ekleme) guest gate middleware'i tarafından YAKALANMIYOR — component-seviyesi guard gerekiyor. **[Session 12 devamı, kapsam teyidi]:** bu, `/menu/customize/*` (Gel Al) bağlamına özgüdür — Masaya artık ayrı `/masaya-siparis/*` yüzeyinde olduğu ve zaten auth gerektirmediği için bu sorunla kesişmiyor. AÇIK KARAR (kullanıcıdan teyit bekliyor): 1b'nin ayrı alt-görevi mi, bilinçli açık mı? | `components/customizer/AddToCartButton.tsx` |
| 70 | 🟡 | `order_history.table_number` kolonunun TİPİ netleşmedi (text mi integer mı — masa numaralandırma şemasının kendisine bağlı). Index gereksinimi (#62 Personel Paneli'nin masa bazlı filtreleme yapıp yapmayacağına bağlı) de HENÜZ belirsiz. Migration bu iki karar netleşmeden koşulmamalı. | `docs/schema-changes/20260808010000_order_history_tablenumber_eklendi.md`, `lib/db/schema.ts` |
| 71 | 🟠 | DEPENDENCIES.md, `RegistrationChannel`'ın tüketicisi olarak `channel-options.ts`'i (ve muhtemelen görülmemiş başka dosyaları) listelemiyor — #68 kapanırken bu dosya atlandığı için canlı build kırılmıştı (düzeltildi, 1d KAPANDI). DEPENDENCIES.md bu sohbette paylaşıldı ama v1.1 (Session 3) — genel olarak ESKİ, `RegistrationChannel` tüketicileri dahil yeni alan/tablo/store değişiklikleri (tableId, order_history, vb.) hiç yansımamış. Ayrı bir turda kapsamlı güncellenmeli. | `DEPENDENCIES.md` |

> **KAPANDI (bu turda):** 1d — Vercel build'in yeşil olduğu kullanıcı tarafından doğrulandı.
> **KAPANDI (bu turda):** #62'nin 3 açık mimari sorusu (personel auth, real-time teknoloji,
> onay kuyruğu UI) — ARCHITECTURE.md v1.12'ye işlendi. #62'nin KENDİSİ henüz kapanmadı
> (kod/migration yok), öncelik 🔴'dan 🟡'a düşürüldü çünkü artık bloklayan bir mimari
> belirsizlik yok, sadece üretim işi kaldı.
>
> **KAPANDI (önceki turlar):** #4, #7, #15, #16, #20, #22/Karar #11, #35, #43, #44, #49,
> #64, #65, #67, #68, #69 — detaylar `session_arşiv.md` ve `session_arşiv_1.md`'de.

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
| 12 (devamı, yeni sohbet) | 2026-08-08 | 1d KAPANDI (Vercel build yeşil, kullanıcı doğruladı). #62 tartışıldı — 3 mimari soru (personel auth, real-time, onay kuyruğu UI) kullanıcı onayıyla kapandı, ARCHITECTURE.md v1.12'ye işlendi. `users.role` migration'ı ayrı bir §7.4 notu gerektiriyor, henüz üretilmedi. | 🟡 #62 mimarisi tamam, üretim (şema notu → migration → kod) bekliyor |

*(Tam turn-by-turn detay: `session_arşiv.md` [0-10], `session_arşiv_1.md` [11+].)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel. ✅ **[Bu turda doğrulandı]** Önceki turdaki `channel-options.ts` tip hatasından kaynaklanan build kırığı düzeltildi, kullanıcı Vercel'de deploy'un YEŞİL olduğunu teyit etti (1d KAPANDI). |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 kod ile hizalı — ⚠️ ROADMAP.md'ye #62 (Personel Sipariş Paneli) hiç işlenmemiş, ayrı bir oturum/kalem olarak eklenmesi gerekebilir. ARCHITECTURE.md v1.12'ye güncellendi, henüz koda yansımadı. |
| Test Suite | 🟢 `guest-gate.test.ts` (8 — kullanıcı tarafından koşuldu, PASS doğrulandı). Genel `npm test` hâlâ tekrar çalıştırılmadı. |
| Auth | 🟡 Twilio/Netgsm PARKLI. Genel giriş/kayıt akışı karar olarak netleşti, guest gate middleware'i KODLANDI ve repoda doğrulandı. Masaya Sipariş kanalı middleware'in kapsamı dışında AYRI bir yüzeyde (`/masaya-siparis/*`) yaşayacak — bu yüzey henüz kodlanmadı. Gel Al akışı için "Sepete Ekle" bypass guard'ı (#66) hâlâ eksik. **[Bu turda]** Personel Paneli erişimi için `users.role` alanı kararlaştırıldı, HENÜZ şemada yok. |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Kullanıcı Kaydı (rıza esaslı) | 🟡 Backend+Frontend TAMAM, canlı test BAŞARILI. Oturum göstergesi eksik (#59). Kanal seçimi zorunlu adımı henüz KODLANMADI. |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı, SADECE Gel Al'a özel (§2.9). Masaya kendi bağımsız mini-checkout'unu kullanacak (ARCHITECTURE.md v1.8) — henüz KODLANMADI. |
| Veritabanı | 🟢 Neon Postgres çalışıyor. `consentRegistrations` ve `order_history` migrate edildi. ⚠️ DB şifresi reset bekliyor (#60). ⚠️ `npm audit`: 12 açık/3 kritik (#63). ⚠️ `order_history.table_number` kolonu KARARLAŞTIRILDI, migration HENÜZ KOŞULMADI — tip netleşmeden koşulmamalı (#70). ⚠️ **[Bu turda]** `users.role` kolonu KARARLAŞTIRILDI, migration HENÜZ KOŞULMADI — CORE.md §7.4 notu önce üretilmeli. |
| Personel Sipariş Paneli (#62) | 🟡 **[Bu turda]** 3 mimari soru (auth = rol bazlı, real-time = polling, onay kuyruğu UI = 2 sekme) kullanıcı onayıyla KAPANDI, ARCHITECTURE.md §2.9a v1.12'ye işlendi. Kalan: `users.role` şema değişiklik notu + migration, sonra kod. |
| Mimari Dokümantasyon | 🟢 ARCHITECTURE.md v1.12 — #62'nin 3 mimari kararı §2.9a'ya, `users.role` planı §3'e, migration notu §4.1'e işlendi. SESSION_INDEX.md v30 bu kararla senkron. ⚠️ DEPENDENCIES.md v1.1 (Session 3) — genel olarak ESKİ, ayrı bir turda kapsamlı güncelleme gerekiyor (#71). |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | **[GÜNCELLENDİ, bu turda]** `users.role: "customer" \| "staff"` için CORE.md §7.4 formatında şema değişiklik notu üret → migration koş → SONRA #62 Personel Sipariş Paneli'ni kodla (auth: rol bazlı middleware guard `/personel/*`, real-time: polling, UI: iki sekme — Masaya/Gel Al). Mimari önü tamamen açık. | 🔴 |
| 1b | Genel giriş/kayıt akış kararlarını koda dök: (i) `/menu/customize/*` guest gate middleware'i TAMAMLANDI (repoda doğrulandı); (ii) `/masaya-siparis/[tableId]/*` yüzeyi (`page.tsx` + `customize/[id]/page.tsx` + kendi mini-checkout'u, sayfa girişinde `useCartStore.setTableId()` çağrılmalı) HENÜZ KODLANMADI — mimari önü açık, başlanabilir; (iii) "Sepete Ekle" bypass component-guard'ı (#66 — eklensin mi kararı bekliyor); (iv) kayıt sayfasında zorunlu kanal seçimi adımı hâlâ kodlanmadı | 🔴 |
| 1c | `order_history.table_number` migration'ı koş — ÖNCE #70'in iki alt sorusu (kolon tipi: text/integer; index gereksinimi) netleşmeli. Şema notu hazır: `docs/schema-changes/20260808010000_order_history_tablenumber_eklendi.md` | 🟡 (#70 netleşmeden koşulamaz) |
| 1e | DEPENDENCIES.md'yi kapsamlı güncelle — `RegistrationChannel`'ın TÜM tüketicileri taransın (#71), ayrıca `useCartStore.tableId`, `order_history`, planlanan `users.role` gibi bu sohbetlerde eklenen alan/tablo/store değişiklikleri haritaya işlensin | 🟠 |
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
| 23 | [TAMAMLANDI] `types/index.ts` görüldü, #68 (RegistrationChannel/FulfillmentChannel tip etkisi) netleşti ve kodlandı | ✅ |
| 24 | [TAMAMLANDI, bu turda] Vercel build yeşil doğrulandı (1d) | ✅ |
| 25 | [TAMAMLANDI, bu turda] #62'nin 3 mimari sorusu kapandı — ARCHITECTURE.md v1.12 | ✅ |
| 26 | ROADMAP.md'ye #62 (Personel Sipariş Paneli) için ayrı bir oturum/kalem eklenmesi düşünülmeli — şu an hiç yer almıyor | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v30 (v29'dan: YENİ SOHBET — 1d KAPANDI (Vercel build yeşil
doğrulandı), #62'nin 3 mimari sorusu (personel auth, real-time teknoloji, onay kuyruğu UI)
Claude'un önerisi + kullanıcı onayıyla kapandı, ARCHITECTURE.md v1.12'ye işlendi. Değişen
bölümler: CURRENT FOCUS (yeni blok), KRİTİK KARARLAR (yeni satır — ARCHITECTURE.md v1.12),
AÇIK SORUNLAR (#62 açıklaması + öncelik güncellendi 🔴→🟡, KAPANDI notuna 1d ve #62-mimari
eklendi), SESSION ÖZET (Session 12 devamı satırı eklendi), GENEL DURUM (Repo — build
doğrulandı; Auth/Veritabanı/Personel Paneli/Mimari Dokümantasyon satırları güncellendi),
SIRADAKİ GÖREVLER (1 güncellendi — `users.role` şema notu önce, 24/25/26 eklendi).
Kullanıcı isteği üzerine bu checkpoint'te SADECE SESSION_INDEX güncellendi —
TEST_MATRIX.md bilinçli olarak GÜNCELLENMEDİ (bu turda üretilen/değişen bir test yok).
Dosya hâlâ 400 satır eşiğinin altında, taşıma tetiklenmedi.
Güncellenme: 2026-08-08.*
