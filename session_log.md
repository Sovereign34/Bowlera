# BOWLERA — session_log.md
> Tam geçmiş. SADECE kullanıcı isteyince veya ilgili session numarası belirtilince açılır
> (CORE.md §1, Adım 2). SESSION_INDEX.md'nin "pusula" işlevini şişirmemek için buraya taşınmıştır.
> Her session kapanışında SADECE YENİ BLOK eklenir — bu dosya asla TAM DOSYA olarak yeniden
> üretilmez (AGENT.md Kural #4 / YASAK LİSTE).

---

## Session 0

- Çekirdek üçlü (CORE.md, AGENT.md), referans üçlüsü (ARCHITECTURE.md, DESIGN_SYSTEM.md, CUSTOMIZER_SPEC.md), ikinci üçlü (DEPENDENCIES.md, ROADMAP.md, TEST_MATRIX.md), üçüncü üçlü (CONTENT_GUIDE.md, INTEGRATIONS.md, FAILURE_PATTERNS.md, CONFIG_SCHEMA.md) üretildi.

## Session 1

- Next.js+Tailwind kurulum, font/renk, Header/Footer/Hero üretildi.
- Logo aktarıldı, Header/Footer/Hero görsel olarak doğrulandı.

## Session 2 (devam) — 2026-07-18 — Customizer Marka Kararı: 4 Adımdan 5 Adıma Geçiş

### Yapılanlar
- Kullanıcı, kategori/filtre görevlerine geçmeden önce "Kâseni Yarat" akışının marka anlayışının netleşmediğini belirtti.
- Kullanıcı 5 adımlı bir customizer önerisi getirdi: Base → Main → Garden → Signature Flavor → Finish, artı "Make it Yours" ek seçenekleri (Extra Avocado/Sauce/Crunch, Double Main).
- MASTER_PLAN.md, CUSTOMIZER_SPEC.md, CONTENT_GUIDE.md okunarak öneri mevcut kanonla karşılaştırıldı, 3 çelişki tespit edildi ve kullanıcıya soruldu.
- 3 turlu netleştirme tamamlandı (adım sayısı, dil, ücretlendirme kuralları).
- Şema değişiklik notu, güncellenmiş MASTER_PLAN.md (v2.1), CUSTOMIZER_SPEC.md (v1.1), CORE.md (§8 düzeltmesi) ve SESSION_INDEX.md üretildi.

### Kararlar (neden alındı)
1. **4 adım → 5 adım.** Gerekçe: gurme mutfak mantığını korurken daha sezgisel bir akış; kullanıcı onayı alındı.
2. **İngilizce isimlendirme.** Gerekçe: premium/global konumlandırma; CONTENT_GUIDE.md §1'in Türkçe marka sesi kuralına bilinçli bir istisna, yalnızca customizer adım/malzeme isimlerini kapsar. *(Sonradan geri alındı — bkz. Karar #15, Oturum 4.)*
3. **Garden: ilk 4 ücretsiz + avokado her zaman ücretli.** Gerekçe: kullanıcı "sen öner" dedi; mevcut Toppings kuralıyla tutarlılık esas alındı.
4. **Finish: ilk 1 ücretsiz, sonrası ücretli.** Gerekçe: kullanıcı seçimi.
5. **"Make it Yours" → Finish adımına entegre, ayrı adım değil; "Double Main" mevcut `mainPortion` mekanizmasını yeniden kullanır.** Gerekçe: kullanıcı seçimi + AGENT.md Kural #5.

### Teknik notlar
- Bu oturumda kod değişikliği YAPILMADI — yalnızca kanon dokümanlar güncellendi.
- `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md` bu kararı henüz yansıtmıyor — bu iki dosya kapsam dışında kaldığı için güncellenemedi. Açık Sorun #10 olarak işlendi.
- Şema değişiklik notu dosyası: `20260718001123_customizer_5_adim_gecisi.md`.

## Session 2 — CategoryNav.tsx + FilterPanel.tsx, MenuCard Fix, Test Altyapısı

- `lib/menu-filters.ts`, `CategoryNav.tsx`, `FilterPanel.tsx` üretildi. `npm test`: 8 test dosyası, 34 test — tümü ✅.
- `MenuCard.tsx` içeriği yanlışlıkla `MenuCardImage.tsx` kopyasıydı, düzeltildi.
- `vitest.config.ts` versiyon çakışması ve `tsconfig.json`/vitest tip çakışması çözüldü.

## Session 3 — 2026-07-18

### Yapılanlar
- `store/useCustomizerStore.ts` üretildi (Zustand — 5 adımlı customizer state'i).
- `lib/customizer-pricing.ts` üretildi (canlı fiyat hesaplama fonksiyonları).
- `lib/customizer-data.ts` üretildi (statik customizer verisi).
- 19 yeni test yazıldı: `customizer-pricing.test.ts` (10), `useCustomizerStore.test.ts` (9).
- `npm test`: 10 test dosyası, 53 test — tümü ✅.
- Push ve deploy başarılı (kullanıcı raporuna dayanıyor, git log ile teyit edilmedi).
- **İkinci Yarı — Masaüstü UI Bileşenleri (KESİNTİ):** Sıra: format yardımcı fonksiyonu → `SummaryTotals` → `AddToCartButton.tsx` → `SummaryPanel.tsx`. Sohbet kesildi, kullanıcı dosyaları manuel push etti.

### Kararlar
- Store ve pricing mantığı CUSTOMIZER_SPEC.md v1.1 (5 adım) kontratına göre üretildi (içerik bu oturumda satır satır teyit edilmedi — Açık Sorun #11).

### Teknik Notlar
- Bu oturum, session açılışında SESSION_INDEX.md okunmadan başladı; kapanış güncellemesi sohbet özetine dayanılarak geriye dönük yapıldı.
- Sitede görsel değişiklik yok — beklenen durum, çünkü store'u tüketen UI bileşenleri henüz yazılmadı.

### Açık Kalan
- Açık Sorun #11, #12, #13.

---

## Session 4 (devam) — 2026-07-18 — Checkpoint: Header → CartBadge/CartDrawer

### Yapılanlar
- `Header.tsx`, `CartBadge.tsx`, `CartDrawer.tsx` içerikleri kullanıcıdan alındı.
- Header client component'e çevrildi (`"use client"`), `useState` ile sepet çekmecesi açık/kapalı state'i eklendi.
- Sepet ikonuna `CartBadge` (adet göstergesi), header altına koşullu `CartDrawer` bağlandı.
- Kalite 5/5, Güvenlik 8/8. Checkpoint alındı, canlıda doğrulandı (sepet ikonu → çekmece açılıyor, "Sepetiniz boş." görünüyor).

### Kararlar (neden alındı)
- `useCartStore.ts` içeriği tekrar istenmedi — CartBadge/CartDrawer store erişimini kendi içinde kapsülüyor, Header sadece UI-local drawer state'ini tutuyor (AGENT.md Kural #5).
- Risk MEDIUM olarak işaretlendi çünkü `touches_cart_state: true`, gerçek karmaşıklık düşük.

### Teknik notlar
- Açık Sorun #19 kapandı.
- Yeni Açık Sorun #21 açıldı: Header'ın `"use client"` olmasının build/performansa etkisi push/deploy sonrası doğrulanmadı.
- Değişiklik izole: sadece `Header.tsx` dokunuldu.

## Session 4 (devam) — 2026-07-18 — Başlık Düzeltmesi, Teslimat Kanalı, â/å Sorunu, Türkçeleştirme, İlerleme Değerlendirmesi

### Başlık Düzeltmesi
- `page.tsx`'teki h1, `{bowl.name} — Kâseni Yarat` yerine sadece `{bowl.name}` yapıldı. Tek satırlık izole değişiklik, kullanıcı push etti.

### Sepete Teslimat Kanalı
- Kullanıcı "sepete giren ürünün hangi kanaldan teslim edileceği" ihtiyacını belirtti. Global chain pattern'i (sepet/oturum seviyesinde tek seçim) araştırılıp önerildi, kullanıcı onayladı.
- Üçüncü "kanal" (Yemeksepeti/Getir/Trendyol) sorgulandı — kullanıcının markeplace'e yönlendirme anlamına geldiği netleşti; bunun ayrı bir CartItem kanalı olarak modellenmemesi gerektiği (siteden çıkış = sepet tamamlanmıyor) gerekçesiyle önerildi ve onaylandı.
- `types/index.ts`'e `FulfillmentChannel = "pickup" | "dine-in"` eklendi (ileride "delivery" eklenebilir şekilde). Aynı turda `CartItem.unitCalorie7s` yazım hatası da `unitCalories` olarak düzeltildi.
- Şema değişiklik notu CORE.md §7.4 formatında üretildi.
- `useCartStore.ts`'e `fulfillmentChannel` state + `setFulfillmentChannel` action eklendi, persist otomatik kapsadı.
- UI yeri tartışıldı — CartDrawer'ın en üstü seçildi.
- Kural #1 (20 satır disiplini) gereği `FulfillmentChannelSelector.tsx` ayrı bileşen olarak yazıldı, `CartDrawer.tsx`'e tek satır import+render ile bağlandı.

### â/å Sorunu ve Nihai Çözüm
- Kullanıcı ekran görüntüsüyle "Benim Kâsem" başlığının bazı cihazlarda `å` gibi göründüğünü bildirdi.
- `menu-data.json` byte seviyesinde (`\xc3\xa2`) kontrol edildi — kaynak veri doğru UTF-8 `â` içeriyordu, encoding hatası yoktu.
- Font glyph rendering / FOUT teorisi öne sürüldü, `lib/fonts.ts`'e deneysel olarak `latin-ext` subset eklendi (confidence: MEDIUM).
- Kullanıcı `â` karakterinin tamamen kaldırılmasını istedi.
- `menu-data.json`'da "Benim Kâsem" → "Benim Kasem", `CartDrawer.tsx`'te "Özel Kâse" → "Özel Kase" yapıldı, kullanıcı canlıda doğruladı.
- Hero.tsx ve StepBase.tsx'teki kalan `â`'lar bilinçli olarak ertelendi (Açık Sorun #27).

### Customizer Malzeme İsimlerinin Türkçeleştirilmesi
- `lib/customizer-data.ts`'teki tüm `name` alanları Türkçeye çevrildi, `id` alanları bilinçli olarak değiştirilmedi (referans bütünlüğü için).
- Canlıda ekran görüntüsüyle doğrulandı ("Jasmin Pirinç", "Esmer Pirinç").
- Adım başlıklarının çevrilip çevrilmeyeceği netleşmeden konu değişti — açık kaldı (Açık Sorun #28).

### İlerleme Değerlendirmesi
- Kullanıcı "Çok yolumuz kaldı mı?" diye sordu, ROADMAP.md + MASTER_PLAN.md §8 karşılaştırıldı.
- Dürüst değerlendirme verildi: 5 oturumdan ~3'ü tamam, Oturum 4 yarıda, asıl blokajın kod değil gerçek veri/fotoğraf eksikliği olduğu vurgulandı.

### goToStep Bug Fix
- `useCustomizerStore.ts`'teki `goToStep` fonksiyonunun `maxReachedStep`'i güncellemediği doğrulandı, tek satırlık izole fix uygulandı.

### app/menu/customize/[id]/page.tsx — Sıfırdan Yazım
- Dosya hiç yazılmamıştı, tüm bağımlılıklar tek tek görülüp üretildi. `customizerCatalog`'un boş olduğu ve Step bileşenlerinin yazılmadığı keşfedildi. 3 varsayım kod içi yorumla işaretlendi (Açık Sorun #20 — hâlâ çözülmedi).

### Slogan ve Hero Değişiklikleri
- Slogan Hero'ya eklendi, sonra h1'in kendisiyle değiştirildi. `HeroHeadline.tsx`'in `WORDS` dizisi güncellendi.

### Customizer'a Giriş Noktaları Keşfi ve Düzeltmesi
- Hero CTA'sının 404 verdiği bulundu, MenuCard'a "Özelleştir" butonu eklendi, Hero CTA'sı geçici olarak `sig-teriyaki-tavuk`'a yönlendirildi, sonra düzeltildi (yalnızca `build-your-own-kasem`'e).

## Session 4 (devam) — 2026-07-19 (İlk Bölüm) — CartDrawer Bugfix ve Auth Mimarisi

### CartDrawer / backdrop-blur Bug'ı — Teşhis ve Düzeltme
- Kullanıcı ekran görüntüsüyle sepet çekmecesinde Hero içeriğinin çakıştığını bildirdi.
- Sırayla `CartDrawer.tsx` (temiz), `Hero.tsx` (temiz), `Header.tsx` (kök neden) incelendi.
- Kök neden: `Header.tsx`'teki `backdrop-blur`, CSS'te `backdrop-filter` uyguluyor — bu, ata elemanı `position:fixed` çocukları için yeni bir containing block yapıyor. `CartDrawer` `<header>` içine render edildiği için `fixed inset-0`'ı viewport yerine Header'ın küçük kutusuna göre konumlanıyordu.
- KARAR: React Portal ile `CartDrawer`'ı `document.body`'ye taşımak, `Header.tsx`'e dokunmamak.
- Kod yazıldı (`createPortal` + SSR güvenliği için `isMounted` kontrolü), kullanıcı push etti.
- 3 ekran görüntüsüyle canlı doğrulandı: çakışma tamamen gitti.

### unitCalorie7s Taraması
- `SummaryPanel.tsx`, `AddToCartButton.tsx`, `MobileSummaryDrawer.tsx` istendi, incelendi.
- Sonuç: hiçbiri `CartItem` tipini kullanmıyor — customizer'ın kendi taslak state'inden besleniyorlar. Rename'den etkilenmiyorlar.
- Açık Sorun #25 kısmen kapandı — gelecekteki `CartItem[]` tüketicileri için tekrar kontrol notu bırakıldı.

### Kullanıcı Kaydı / Auth Araştırması (TASLAK)
- Kullanıcı "bu siteye nasıl kayıt yapıyor" sorusunu sordu.
- Netleştirme: checkout için hesap + sadakat/puan programı ikisi de istendi.
- Web araştırması: global (McDonald's, Starbucks, Domino's) ve TR emsalleri (Yemeksepeti, Getir, Trendyol Yemek) hepsi telefon+SMS OTP, şifresiz giriş kullanıyor.
- Bilinen risk: "1 numara = 1 hesap" kısıtı hesap kurtarmada sorun yaratıyor.
- Kullanıcı onayladı: telefon+OTP, guest checkout korunsun. Karar #17 (taslak) ve Açık Sorun #30 olarak kayda geçirildi — kod yazılmadı.

### Auth Mimarisi Netleştirme
- `ARCHITECTURE.md`, `CONFIG_SCHEMA.md`, `INTEGRATIONS.md` incelendi — projede hiç veritabanı olmadığı tespit edildi. `CONFIG_SCHEMA.md`'de zaten `TWILIO_ACCOUNT_SID`/`TWILIO_AUTH_TOKEN`'ın planlı olduğu görüldü.
- 3 soru soruldu (OTP sağlayıcısı, session yönetimi, veritabanı). Kullanıcı ilk ikisi için öneri istedi, DB'de "henüz karar verme" dedi.
- Öneri: **Twilio Verify** + **Auth.js (NextAuth) JWT**. KARAR BİLDİRİMİ üretildi (Karar #19), onaylandı.
- `CONFIG_SCHEMA.md` (v1.1), `INTEGRATIONS.md` (v1.1, yeni §5), `ARCHITECTURE.md` (v1.2, yeni §2.7 + `AuthenticatedUser` tipi) güncellendi.
- Kod bu turda YAZILMADI — Açık Sorun #31 (sonraki bölümde kapandı).
- Kullanıcı, önceki SESSION_INDEX.md güncellemesinde arşiv bloklarının kırpıldığını fark etti — AGENT.md Kural #4 ihlali kabul edildi, tüm arşiv blokları TAM olarak geri kondu. *(Bu, projedeki ilk "arşiv kırpma" ihlaliydi — Session 4, 2026-07-19'da AGENT.md/CORE.md v1.1'e kural olarak eklendi.)*

## Session 4 (devam) — 2026-07-19 (İkinci Bölüm) — Auth Kod Üretimi ve Sonrası

### DB Kararının Revizyonu (Karar #19 → #20) ve Neon Kurulumu
- Kullanıcı "kayıtlı kullanıcı tekrar giriş yaparsa adresini nasıl bulur" diye sordu.
- JWT-only mimarinin (Karar #19) bunu çözemediği ortaya kondu — farklı cihaz/tarayıcıda "hafıza" sıfırlanıyor.
- Üç seçenek sunuldu: (1) DB'yi öne çek, (2) kapsamı daralt (adres her seferinde girilir), (3) localStorage. Dürüst değerlendirme: Seçenek 3 kimlik modeliyle çelişiyor, veri kaybı riski var. Seçenek 1 tavsiye edildi.
- Kullanıcı "Vercel'de DB olarak çözelim, Supabase'de limitim dolu" dedi.
- Web araştırması: Vercel native Postgres kaldırılmış, Marketplace üzerinden Neon/Prisma/Supabase/PlanetScale sunuluyor. Neon önerildi.
- 10+ ekran görüntüsüyle Neon Vercel Marketplace entegrasyonu kuruldu: Install → Region (Frankfurt) → **Auth toggle KAPATILDI** → Free plan → Create → Connect to Project (`bowlera-site`, database branch OLUŞTURULMADI, Custom Prefix `DATABASE` → env `DATABASE_URL`) → Connect.
- KARAR BİLDİRİMİ üretildi (Karar #20), kullanıcı onayladı.

### Auth Kod Üretimi ve Build Hatası Düzeltmeleri
- Sırayla üretildi: `package.json` (4 yeni bağımlılık: `next-auth@beta`, `twilio`, `drizzle-orm`+`drizzle-kit`, `@neondatabase/serverless`), `lib/db/schema.ts`, `lib/db/client.ts`, `types/index.ts` güncellemesi (`AuthenticatedUser.address`), `lib/auth/rate-limit.ts` (in-memory token-bucket, kod içinde bilinçli teknik borç olarak işaretli), `lib/auth/phone.ts` (TR telefon regex + normalize), `auth.ts` (Auth.js v5 Credentials provider), `app/api/auth/[...nextauth]/route.ts`, `app/api/auth/otp/send/route.ts`, `app/api/auth/otp/verify/route.ts`, `CONFIG_SCHEMA.md` (v1.2), `drizzle.config.ts`, iki test dosyası.
- Dosyalar önce yanlışlıkla zip olarak teslim edildi — AGENT.md Kural #9 ihlali kabul edildi, 14 dosya tek tek yeniden sunuldu.
- Build hata 1: `auth.ts`'te `verifiedAt: new Date().toISOString()` — Drizzle şeması `timestamp` (Date) beklerken string gönderilmiş. Düzeltildi.
- Build hata 2: `session.user.phone` ataması — Auth.js v5 beta tiplerine `phone` tanınmıyordu. `types/next-auth.d.ts` (module augmentation) eklendi.
- Kullanıcı tekrar push etti — build **yeşil** ✅.

### Twilio Kurulumu ve Türkiye SMS Kısıtı Keşfi
- Kullanıcı "Twilio ücretli mi" diye sordu — trial'ın kredi kartsız $15,50 kredi verdiği, Verify'ın ~$0,05/doğrulama olduğu bilgisi verildi.
- Twilio hesabı 10+ ekran görüntüsüyle kuruldu: Trial → onboarding → Console → Verify → Services → "Bowlera" servisi oluşturuldu (WhatsApp yanlışlıkla açılmıştı, kapatıldı) → Service SID alındı.
- Auth Token bir kez yanlışlıkla sohbette paylaşıldı — BSC-2 gereği "compromised" kabul edilip rotate edildi.
- Kullanıcı env değişkenlerini Vercel'e girdi.
- "Verified Caller ID" eklerken **"The verification has been blocked as this is a restricted country"** hatası alındı (Türkiye, SMS kanalı için).
- Web araştırmasıyla bunun hem trial-özel Caller ID doğrulaması hem de ayrı bir "Verify Geo Permissions" ayarı olduğu netleştirildi.
- Kullanıcı "Ücretsiz planda SMS yok, atlayıp devam edelim" dedi. Açık Sorun #32 olarak loglandı, iki çözüm yolu (ücretli plan / Türkiye'ye özel sağlayıcı) not edildi.

### Görev Sıralaması ve CategoryNav/FilterPanel Keşfi
- Claude, konuşma-içi hafızasına dayanarak "CategoryNav.tsx"ni "sıradaki" olarak önerdi.
- Kullanıcı MASTER_PLAN.md ve DESIGN_SYSTEM.md'yi yükledi, aynı anda "Sitede kullanıcı girişi görünmüyor" dedi — backend-only auth kodunun UI'sız olduğu tekrar netleştirildi.
- `MASTER_PLAN.md` §3.2 okunurken kategori isimlerinin `types/index.ts`'teki enum'la uyuşmadığı fark edildi (Açık Sorun #35).
- `CategoryNav.tsx` yüklendi — dosyanın zaten tam ve doğru olduğu görüldü.
- Önceki `npm test` çıktısında `FilterPanel.test.tsx`'in de geçtiği fark edildi — SESSION_INDEX arşivi kontrol edildiğinde ikisinin de Oturum 2'de zaten üretildiği doğrulandı. **Ders: konuşma-içi hafıza güncel olmayabilir, SESSION_INDEX arşivine güvenilmeli.**

### Öncelik Sıralaması, Disclaimer ve Görünür Giriş UI'ı
- Kullanıcı "SIRADAKİ GÖREVLER" listesini paylaştı, Claude önceliğe göre sıraladı.
- Kullanıcı "bunu da bu oturumda yap" dedi — görünür giriş UI'ı kapsama eklendi.
- `git log --oneline -10` çalıştırıldığında **"45↓ 0↑"** görüldü — local'in 45 commit gerisinde olduğu şüphesi doğdu.
- `VisualPreview.tsx`, `Header.tsx`, `CONTENT_GUIDE.md` yüklendi, disclaimer + hesap ikonu + `/giris` sayfası üretildi.
- `git fetch && git status` ile şüphe doğrulandı: local 45 commit geride, commit edilmemiş değişiklikler vardı. `git stash && git pull && git stash pop` — conflict olmadan temiz geçti.
- Üretilen 3 dosyanın (VisualPreview, Header, giris/page.tsx) zaten repoda, birebir aynı içerikte olduğu bulundu (`80b152c`, `a5426e3`, `345562e`) — mükerrer iş önlendi.

## Session 4 (devam) — 2026-07-19 (Üçüncü Bölüm) — Adres/Profil Özelliği ve Test Triyajı

### Boşluk Keşfi ve Tasarım Kararı
- Kullanıcı "burada büyük bir şey unuttuk, adres nerede kayıtlı" diye sordu.
- ARCHITECTURE.md okundu — Karar #20 ile senkron olmadığı (hâlâ "DB henüz yok" diyor, `AuthenticatedUser` tipinde `address` yok) keşfedildi, Açık Sorun #36 olarak loglandı.
- Netleştirme: adres sadece profil/sadakat verisi mi yoksa delivery mi? `types/index.ts`, `lib/db/schema.ts`, `auth.ts` sırayla incelendi.
- Kullanıcı "Sen karar ver devam et" dedi. KARAR BİLDİRİMİ üretildi (Karar #23): Seçenek (a) — adres SADECE profil/sadakat verisi, checkout bloklanmaz, `/hesap`'ta opsiyonel toplanır.

### Kod Üretimi
- 7 dosya üretildi: `lib/user/profile-validation.ts` (+`.test.ts`), `lib/db/queries/user-profile.ts`, `app/api/user/profile/route.ts` (GET/PATCH, SADECE `session.user.phone` kullanır), `components/account/useProfileForm.ts`, `components/account/ProfileForm.tsx`, `app/hesap/page.tsx`.
- İki açık varsayım bilinçli işaretlendi: (1) rate-limit — imza görülmediği için entegre edilmedi (#37), (2) Tailwind renk sınıfları tahmin edildi (#38).
- DB migration gerekmedi — kolonlar zaten vardı.
- Kullanıcı manuel kaydettiğini/push ettiğini bildirdi. *(Not: bu iddia Dördüncü Bölüm'de en az 1 dosya için YANLIŞ çıktı — bkz. #41.)*

### Canlı Doğrulama Girişimi ve Twilio Blokajı
- Deploy yeşil onaylandı. `/hesap` canlı testi Twilio kısıtı (#32) yüzünden mümkün olmadı.
- `/giris` sayfası ekran görüntüsüyle doğrulandı ama OTP gelmediği için akış orada durdu.
- Local dev-only auth bypass önerisi yapıldı, kullanıcı onayı beklenmeden kod YAZILMADI.
- Açık Sorun #39 olarak loglandı.

### Test Suite Triyajı (Codespace)
- `npm test`: 98 testten 3 fail, 95 geçti.
- 3 fail netleşti: `useCustomizerStore.test.ts`, `Hero.test.tsx`, `Header.test.tsx`.
- **Hero.test.tsx:** CTA'nın kasıtlı olarak `build-your-own-kasem`'e gittiği koddaki niyet yorumunda zaten yazılıydı — test stale çıktı. Düzeltildi, `npx vitest run` ile **3/3 ✅ canlı doğrulandı**.
- **Header.test.tsx:** Kod `aria-label="Sepeti aç"` kullanıyor, test tam string `'Sepet'` bekliyordu. `/sepet/i` regex'ine çevrildi. Kullanıcı "hepsini geçelim, deploy zaten yeşil" dedi — izole doğrulanmadı, Açık Sorun #40.
- **useCustomizerStore.test.ts:** Kullanıcı kararıyla ATLANDI — #17/#24 ile ilişkili olduğu netleşti, düzeltme yapılmadı.

## Session 4 (devam) — 2026-07-19 (Dördüncü Bölüm) — Menü Animasyonu, ARCHITECTURE.md v1.3, Rate-limit ve Repo Tutarsızlığı Keşfi

### 1. Menü kartı geçiş animasyonu — iyileştirme
- `app/menu/page.tsx`'teki scroll-reveal animasyonu 3 turda kademeli belirginleştirildi (scale/y/süre/stagger artırımları, DESIGN_SYSTEM §6.1-6.2 korunarak).
- `useReducedMotion()` kontrolü ve `opacity`+`transform`-only kısıtı her turda korundu.
- Kullanıcı canlıda ekran görüntüsü paylaştı — deploy başarılı.

### 2. ARCHITECTURE.md senkronizasyonu (#36 — kod tarafı bu turda tamamlandı, PUSH DURUMU BELİRSİZ)
- §1'e madde 8 (profil route kimliği sadece `session.user.phone`'dan) ve madde 9 (adres checkout'u bloklamaz) eklendi.
- §2.7 düzeltildi — "DB henüz yok" kaldırıldı. **Yeni §2.8** eklendi (profil route kontratı). §3'e `AuthenticatedUser.address` + `CartItem.fulfillmentChannel` (yeni keşfedilen eksiklik) eklendi. §4.1/§5 güncellendi. v1.2 → **v1.3**.
- ⚠️ Bu turda **PUSH EDİLMEDİ**.

### 3. Rate-limit entegrasyonu (#37) — KRİTİK KEŞİF: dosya grubu repoda yok
- **Keşif:** GitHub'da `api/user` klasörü **hiç yok**. Karar #23 kapsamında "üretildi ve push edildi" denen 7 dosyadan `app/api/user/profile/route.ts` **hiç push edilmemiş**. SESSION_INDEX'in bu notu **yanlış olduğu doğrulandı** — bu, **Açık Sorun #41'in (SESSION_INDEX/repo tutarsızlığı) kökeni**.
- Bağımlı 4 dosya kullanıcıdan tek tek istenip görüldü: `auth.ts`, `useProfileForm.ts`, `profile-validation.ts` (MAX_ADDRESS_LENGTH=300, MAX_NAME_LENGTH=60), `user-profile.ts`.
- KARAR: Mevcut `checkOtpRateLimit`'e dokunulmadı; ayrı bucket (`profileBuckets`) + `checkProfileRateLimit` (5dk'da 10 istek, telefon bazlı) `rate-limit.ts`'e eklendi.
- `route.ts` **sıfırdan üretildi** — GET (rate-limitsiz), PATCH (rate-limitli, 429+`Retry-After`, `session.user.phone` ile kimlik, BSC-3).
- İki dosya teslim edildi, **push edilmedi**.

### Kararlar
| Karar | Gerekçe |
|---|---|
| Animasyon 3 turda kademeli artırıldı | Kullanıcı geri bildirimi adım adım geldi, küçük geri alınabilir değişiklik tercih edildi |
| `checkOtpRateLimit`'e dokunulmadı, ayrı fonksiyon eklendi | Mevcut fonksiyonun testi görülmedi — risk alınmadı |
| Profil PATCH rate-limit anahtarı `session.user.phone` (IP değil) | Route auth zorunlu, phone sahtelenemez |
| GET'e rate-limit eklenmedi | Salt okuma, kötüye kullanım maliyeti ihmal edilebilir |
| `route.ts` sıfırdan üretildi | Dosyanın repoda hiç bulunmadığı doğrulandı |

### Teknik Notlar
- 🔴 SESSION_INDEX/repo tutarsızlığı doğrulandı: 7 dosyadan en az 1'i (`route.ts`) repoda yok. Diğer 6'sı tek tek doğrulanmadı — 3'ü (`useProfileForm.ts`, `profile-validation.ts`, `user-profile.ts`) dolaylı teyit edildi, `ProfileForm.tsx`/`app/hesap/page.tsx` teyit edilmedi.
- `rate-limit.ts`, `route.ts`, ARCHITECTURE.md v1.3 — hiçbiri push edilmedi.

### Sembol Özeti
📁 (3 dosya) · 🔧 (3 mimari/tasarım kararı) · 🔴 (SESSION_INDEX/repo tutarsızlığı keşfi — bu turda çözülmedi)

## Session 4 (devam) — 2026-07-20 (Beşinci Bölüm) — Repo Doğrulama Turu: #41/#37/#26/#36/#33/#40 Kapanışları

> ⚠️ Bu blok, `session_log.md`'de önceden "ÖZET DÜZEYİNDE, TURN-BY-TURN KAYIT YOK" olarak
> işaretlenmiş Beşinci Bölüm notunun YERİNE geçer. Gerçek gerekçeler, kullanıcının ayrıca
> yüklediği v2 (sıkıştırılmış) SESSION_INDEX dosyasında bulundu ve buraya taşındı — Açık
> Sorun #42 bu blokla KAPANDI olarak işaretlenmiştir.

### Header — Oturum Farkındalığı
- Header hesap ikonu oturum-farkında hale getirildi: `app/layout.tsx`'e `SessionProvider` eklendi, `Header.tsx`'e `useSession()` entegre edildi. Kullanıcı push etti. → **Açık Sorun #33 kapandı.**

### Header.test.tsx — İki Ayrı Sorunun Tespiti ve Düzeltmesi
- `useSession()` eklenmesi `Header.test.tsx`'i kırdı: `SessionProvider` olmadan test 3/3 fail veriyordu → `vi.mock('next-auth/react')` ile çözüldü.
- Aynı testte, önceki bir oturumda "düzeltme üretildi ama izole doğrulanmadı" denen eski bir sorun da bu vesileyle ortaya çıktı: sepet butonu testi hâlâ eski tam-string `'Sepet'` bekliyordu (gerçek `aria-label`: `"Sepeti aç"`) — bu, o eski düzeltmenin repoya hiç yansımadığını gösterdi. `/sepet/i` regex'ine çevrilerek düzeltildi.
- 3/3 ✅ canlı ekran görüntüsüyle doğrulandı. → **Açık Sorun #40 kapandı.**

### Repo Doğrulama Turu — Kod/Doküman Karşılaştırmasıyla Tek Tek Teyit
- **#41 (SESSION_INDEX/repo tutarsızlığı) kapandı:** Karar #23 kapsamında "üretildi" denen 4 dosya (`app/api/user/profile/route.ts`, `components/account/ProfileForm.tsx`, `app/hesap/page.tsx`, `lib/auth/rate-limit.ts`) tek tek repoda görülüp doğrulandı — hepsi mevcut.
- **#37 (profile route rate-limit'siz) kapandı:** `checkProfileRateLimit` fonksiyonunun `route.ts`'e fiilen entegre edilmiş olduğu bulundu — önceki oturumda "bilinçli atlandı" denen entegrasyon bu arada tamamlanmış.
- **#26 (teslimat kanalı checkout'ta zorunlu değil) kapandı:** `app/siparis/page.tsx` + `OrderSummary.tsx` + `FulfillmentGate.tsx` + `WhatsAppOrderButton.tsx` (+ test dosyası) tek tek görülüp doğrulandı — kanal seçilmeden CTA aktif olamıyor, sahte/hardcode şube numarası kullanılmamış (BSC-5 temiz).
- **#36 (ARCHITECTURE.md senkron değil) kapandı:** `ARCHITECTURE.md` v1.4'ün repodaki güncel hâli olduğu, kod tarafıyla (checkout, adres/profil, DB, `fulfillmentChannel`) tam örtüştüğü teyit edildi. **Not:** §2.4 (5 adımlı customizer state'i) bu doğrulamanın kapsamı DIŞINDA bırakıldı — Açık Sorun #10 ayrı bir madde olarak açık kalmaya devam ediyor, #36 ile karıştırılmamalı.

### Teknik Notlar
- Bu turun kapanışları, önceki bir sohbette üretilmiş sıkıştırılmış (v2) bir SESSION_INDEX dosyasında kayıtlıydı; o dosya `session_log.md`'ye hiç taşınmamıştı — arşiv kırpma riski bu şekilde ortaya çıktı ve düzeltildi.
- Genel `npm test` bu turda tekrar çalıştırılmadı — sadece `Header.test.tsx` izole doğrulandı. `WhatsAppOrderButton.test.tsx` görüldü (kod sağlam) ama izole çalıştırılmadı.

### Açık Kalan (bu turda KAPANMAYAN, netliğe kavuşan)
- #10 — ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor, v1.4'te bilinçli olarak bu güncellemenin dışında bırakıldı.
- #32 — Twilio TR SMS kısıtı, projenin tek kalan büyük darboğazı.
- #38, #39, #35, #24/#17/#18, #27, #28/#29 — değişmedi.

### ⚠️ Bu Turda da Fark Edilmeyen Ayrı Bir Sorun (sonradan tespit edildi)
- v2 SESSION_INDEX dosyası, bu turun ürünüydü ve kendi içinde AÇIK/GEÇERLİ KARARLAR ile AÇIK SORUNLAR tablolarını "hâlâ etkili olanlar" gerekçesiyle sıkıştırırken, hiçbir kapanış notu olmadan 7 açık sorunu (#4, #7, #15, #16, #20, #22, #34) ve 2 kararı (#11, #12) tablolardan düşürmüştür. Bu, ayrı bir sonraki oturumda (bkz. SESSION_INDEX.md güncel sürüm) fark edilip düzeltilmiştir.

## Session 4 (devam) — 2026-07-20 → 07-22 (Altıncı–Onbirinci Bölüm) — ⚠️ ÖZET DÜZEYİNDE, TURN-BY-TURN KAYIT YOK

> Bu blok, dürüstlük gereği açıkça işaretlenmiştir: bu bölümlerin ayrıntılı turn-by-turn
> dökümü hiçbir sohbette bulunamadı — sadece SESSION_INDEX.md'nin özet tablosunda tek satırlık
> bir iz kaldı. Aşağıdaki madde, o özet satırının olduğu gibi taşınmasıdır; gerekçe/karar detayı
> YOKTUR. İleride bu bölümlerin gerçek dökümü bulunursa bu blok değiştirilmeli, silinmemelidir.

- Kapsanan konular (özet): Türkçeleştirme devamı, DESIGN_SYSTEM.md §7 (alerjen gösterim sistemi
  tasarımı, → Açık Sorun #7 kapandı), Karar #11/#22 (Bitkisel Protein Main alt-varyantının uçtan
  uca üretimi — canlıda doğrulandı), MobileSummaryDrawer.tsx format yardımcı fonksiyon
  konsolidasyonu (→ #43 kapandı), AGENT.md v1.3 alerjen self-check protokol maddesi (→ #44
  kapandı), CUSTOMIZER_SPEC.md §3.5 güncellemesi (→ #49 kapandı), MASTER_PLAN.md v2.2 + ROADMAP.md
  v1.3 tutarlılık denetimi ve güncellemesi (Auth/Hesap sitemap'e ve Oturum 4.5'e işlendi — bu
  denetim sırasında #50 ve #51 yeni açık sorun olarak fark edildi).
- Kapanan: #7, #43, #44, #49.
- Yeni açılan: #50 (`AddToCartButton.tsx` hiç görülmedi, BSC-6 teyit edilmedi), #51
  (`useCartStore.ts` hiç görülmedi, CartDrawer persist davranışı teyit edilmedi).

## Session 5 — 2026-08-01 → 2026-08-02 (3 tur)

### Tur 1 — 2026-08-01 — VisualPreview.tsx Mimari Çelişkisi

- `VisualPreview.tsx` mimarisi denetlendi — kritik bir mimari çelişki bulundu (→ Açık Sorun #52,
  yeni). Kod, `/public/images/layers/` altında her malzeme için gerçek görsel dosyası
  (`base-jasmine-rice.webp` gibi) bekliyor, ama bu klasör TAMAMEN BOŞ — hiçbir katman görseli yok.
  Bu, PHOTOGRAPHY_GUIDE.md §8'deki "VisualPreview CSS/SVG katman mantığıyla çalışıyor, gerçek
  fotoğraf gerekmez" notuyla doğrudan çelişiyor. Şu an müşteri customizer'da herhangi bir malzeme
  seçse bile önizleme boş krem renkli daire olarak kalıyor.
- **Karar (kullanıcı onayı ile):** Fotoğraf katmanlama yerine markaya uygun (Warm Cream/Espresso
  Brown/Primary Olive) vektörel ikon seti kullanılacak — global rakip modeli: Chipotle (metin-only,
  görsel yok) / Cava-Sweetgreen (düz ikon seti). Kod tarafında DEĞİŞİKLİK GEREKMİYOR —
  VisualPreview.tsx zaten dosya yolunu id'den esnek türetiyor, sadece ikon dosyaları
  `/public/images/layers/` altına eklenecek (üretici: kullanıcı bir tasarımcı bulacak ya da Claude
  AI ile taslak üretecek — netleşmedi).
- Ayrıca: dosyanın en üstündeki "GEÇMİŞ İHLAL KAYDI" notu (v2 sıkıştırma olayı) bu turda tekrar
  teyit edildi.
- Netgsm sözleşmesi bu turda onaylandı olarak not edildi. *(⚠️ Bu, Session 6'da "esnaf odası/marka
  tescili isteniyor" bulgusuyla çelişiyor — netleştirilmesi gereken bir tutarsızlık, Session 6 log
  bloğunda ayrıca işaretlendi.)*

### Tur 2 — 2026-08-01 — Pazaryeri Müşteri Verisi Erişimi Araştırması

- Yemeksepeti'nin resmi openapi.json şeması incelendi — `order.Customer` şemasındaki TÜM kişisel
  alanlar (isim, telefon, ulusal kimlik, teslimat adresi) açıkça "Masked for identity protection"
  olarak işaretli, sadece platformun ürettiği anonim müşteri ID'si veriliyor. Bu, bilinçli bir
  platform politikası — teknik eksiklik değil. Trendyol Go/Migros Yemek için de aynı mantığın
  geçerli olduğu varsayılıyor (ayrı ayrı teyit edilmedi).
- **Bulunan gerçek yol:** Adisyo'nun "BOOSTFEEL Müşteri Sadakat Entegrasyonu" pazaryeri API'sinden
  veri ÇEKMİYOR — QR kod tabanlı, müşterinin FİZİKSEL ziyarette (gel-al) kendi isteğiyle dijital
  sadakat kartına kaydolmasına dayanıyor (Apple/Google Wallet, Adisyo/Simpra POS entegrasyonu
  üzerinden). Önerilen pratik yöntem: pazaryeri paket siparişlerine "QR ile üye ol, indirim kazan"
  kartı eklemek — platform ToS'unu ihlal etmeyen, müşteriyi kendi isteğiyle veri paylaşmaya davet
  eden meşru yol.
- Bu bulgu, Karar #12'deki (loyaltyPoints mekaniği henüz netleşmedi) açık soruyla doğrudan
  bağlantılı — sadakat mekaniği tasarlanırken Boostfeel benzeri bir QR-kayıt akışı ile
  `users.loyaltyPoints` alanının nasıl besleneceği birlikte düşünülmeli.

### Tur 3 — 2026-08-02 — Hakkımızda Sayfası, â→a Kararının İlk Uygulaması, Governance Notu

- Hakkımızda sayfası (`/hakkimizda`) sıfırdan oluşturuldu — MASTER_PLAN.md §3 sitemap girdisi
  karşılandı, önceki site denetiminde tespit edilen 404 kapandı. 6 dosya üretildi: page.tsx,
  AboutHero.tsx, AboutStory.tsx, AboutValues.tsx, AboutImagePlaceholder.tsx, page.test.tsx. Test
  sonucu kullanıcı tarafından koşuldu ve doğrulandı: Vitest, 2/2 test geçti (happy path + edge
  case).
- **Gerçek veri işlendi:** Kullanıcı gerçek şube adresini paylaştı — Çağlayan Park Sokak No:30,
  Kağıthane, İstanbul. AboutStory.tsx'e kuruluş anlatısı olarak işlendi (global marka VİZYONU
  olarak çerçevelendi, mevcut durummuş gibi sunulmadı). ⚠️ Bu adres HENÜZ Şubeler sayfası/
  Footer.tsx/JSON-LD şemasına işlenmedi — CONTENT_GUIDE.md §4 NAP tutarlılık kuralı gereği bu
  senkron zorunlu, yeni açık iş olarak eklendi (→ #54).
- **Site-geneli yazım kararı:** Kullanıcı onayıyla "kâse"→"kase" (â kaldırma) kararı alındı.
  Hero.tsx'te uygulandı (CTA: "Kaseni Oluştur", alt paragraf sağlıklı beslenme odaklı yeniden
  yazıldı — tedarikçi vurgusu kaldırıldı). CONTENT_GUIDE.md'deki "Kâseni Yarat" örnekleri ve
  StepBase.tsx HENÜZ güncellenmedi — karar kısmen uygulandı (#27 kısmen kapandı, → #53 yeni
  açıldı).
- **Governance düzeltmesi:** AGENT.md/CORE.md'deki "400 satır eşiği" kuralı bir yanlış anlaşılma
  sonucu kısa süreliğine kaldırılıp aynı gün içinde AYNEN geri getirildi. Net kural değişikliği
  yok, sadece versiyon numaraları arttı (AGENT.md v1.5, CORE.md v1.4).
- Ayrıca bu turda: AGENT.md dosya karışıklığı (yanlışlıkla PUSULA projesinin dosyasıyla yeniden
  yüklenmişti) fark edilip doğru sürüm tekrar istenip teyit edildi.

### Sembol Özeti (Session 5)
📁 (6 dosya: Hakkımızda sayfası) · 🔧 (2 mimari karar — vektörel ikon, â→a) · 🆕 (#52, #53, #54)
· ⚠️ (Netgsm "onaylandı" notu — Session 6'da çelişki olarak yeniden açıldı)

## Session 6 — 2026-08-05 — Netgsm Blokajı, WhatsApp OTP Fallback Kararı ve Uygulaması

### Bağlam
- Kullanıcı Netgsm SMS başlık başvurusunda esnaf odası kaydı (9000 TL) veya marka tescili (uzun süre)
  isteniyor diye blokaja girdiğini bildirdi. Twilio'nun TR SMS kısıtından (#32) sonra ikinci bir
  sağlayıcı engeliyle karşılaşıldı. *(⚠️ Bu, Session 5 Tur 1'deki "Netgsm sözleşmesi onaylandı"
  notuyla çelişiyor — netleştirilmesi gereken bir tutarsızlık olarak kayda geçirilmiştir, bu turda
  ayrıca çözülmedi.)*
- Araştırma: SMS başlık onayında hiyerarşi netleştirildi — vergi levhasında ticari ünvan (Bowlera)
  yazıyorsa esnaf odası/marka tescili GEREKMİYOR; yoksa işyeri açma ruhsatı (zaten restoran açılışı
  için alınacak) da yeterli olabiliyor. Esnaf odası/marka tescili sadece bu ikisi de yoksa gerekiyor.
- Kullanıcı, işyeri açma ruhsatı aşamasında Bowlera adını kullanabileceğini teyit etti.

### Karar (kullanıcı onayı ile) — Hibrit OTP Kanalı
- WhatsApp OTP birincil kanal, SMS ikincil/fallback kanal olarak kullanılacak.
- **Kritik bulgu:** Twilio Verify Service zaten `channel: "whatsapp"` parametresini destekliyor —
  ayrı bir Meta/WhatsApp Cloud API entegrasyonu GEREKMİYOR, mevcut Twilio hesabı üzerinden yürütülebilir.
- `verify/route.ts` DEĞİŞMEDİ — Twilio doğrulama kanaldan bağımsız çalışıyor (sadece kod/telefon).

### Kod Üretimi
- `lib/auth/send-otp.ts` (yeni) — `sendOtpWithFallback()`: WhatsApp→SMS sırasıyla dener, ikisi de
  başarısız olursa son hatayı fırlatır.
- `app/api/auth/otp/send/route.ts` (güncellendi) — yeni fallback modülünü çağırıyor, response'a
  hangi kanaldan gönderildiği (`channel`) eklendi.
- `lib/auth/send-otp.test.ts` (yeni) — happy path (WhatsApp başarılı), edge case (WhatsApp düşer,
  SMS'e geçer), failure path (ikisi de başarısız, hata fırlatılır).
- Kalite Skoru: 5/5. Güvenlik Skoru: 8/8.

### Test Doğrulaması ve Push (aynı gün, sonraki tur)
- Kullanıcı `npx vitest run lib/auth/send-otp.test.ts` çalıştırdı — ekran görüntüsüyle **3/3 PASS**
  doğrulandı (happy path, edge case, failure path). Loglardaki `OTP_CHANNEL_FAILED` kayıtları
  failure-path testinin kasıtlı çift-kanal hatası senaryosuna ait — hata değil, BSC-4
  loglamasının çalıştığının kanıtı.
- Kod push edildi.

### Twilio Upgrade Denemesi ve Maliyet Netleşmesi
- Kullanıcı Twilio Console'da "Upgrade"e tıkladı — hesap Trial modunda, WhatsApp Sender kurulumu
  için minimum $20 istendiği görüldü. Kullanıcı bu tutarı şu an ödemek istemedi.
- Netgsm'in "vergi levhasına ticari ünvan işletme" alternatifinin de Ticaret Sicili Gazetesi'nde
  ilan gerektirdiği (yani gerçekte ~9000 TL'ye eşdeğer olduğu) kullanıcı tarafından netleştirildi —
  önceki turda öne sürülen "ücretsiz alternatif" iddiası bu turda GERİ ÇEKİLDİ.

### Alternatif Kimlik Doğrulama Yollarının Elenmesi
- **Google/sosyal giriş araştırıldı:** Google OAuth API'sinin kullanıcının telefon numarasını
  PAYLAŞMADIĞI doğrulanmış üçüncü parti kaynaklarla teyit edildi (ilgili scope hiç yok) — Google
  girişi telefon toplama ihtiyacını çözmüyor, bu amaçla ELENDİ.
- **Online yemek platformları üzerinden "sosyal giriş" araştırıldı:** Yemeksepeti/Getir/Trendyol
  gibi platformların kimlik sağlayıcı (identity provider) OLMADIĞI, resmi/genel bir "___ ile giriş
  yap" API'lerinin bulunmadığı doğrulandı — bu yol tamamen ELENDİ.

### 🔧 BÜYÜK MİMARİ KARAR — Twilio/Netgsm Parklandı, Rıza Esaslı Toplama + WhatsApp Yönlendirme
- Twilio ($20 Upgrade) ve Netgsm (9000 TL, Ticaret Sicili ilanı) yolları PARKLANDI — ikisi de
  maliyetli, acil değil.
- **Kararlaştırılan yeni akış (kullanıcı onayı ile, DENEME aşaması — kullanıcı açıkça "zaman
  geçtikçe karara varırız" dedi, nihai değil):**
  1. Kayıt İKİ tetikleyiciden biriyle başlar: (a) kullanıcı kendi isteğiyle "Kayıt Ol", (b)
     customizer'da ürün seçimine başlarken henüz kayıtlı değilse otomatik yönlendirme.
  2. Kayıt formu ZORUNLU alanlar: ad-soyad, telefon, rıza (KVKK) checkbox — SMS/WhatsApp kod
     doğrulaması YOK, aktif rıza onayı yeterli görülüyor. Adres OPSİYONEL kalır (Karar #23 ile
     ÇAKIŞMIYOR — amacı zamanla çoklu-şube güçlü veri tabanı oluşturmak). Opsiyonel: yaş, cinsiyet.
  3. Kayıt adı sitede "Merhaba, [isim]" olarak header'da gösterilir.
  4. Kayıt tamamlanınca 3 kanal seçimi sunulur: Masaya Servis / Gel-Al / Online Sipariş.
  5. Masaya Servis + Gel-Al: kullanıcı sitede customizer'la ürün seçer, sepete ekler. Sepet
     tamamlanınca TEK, merkezi işletme WhatsApp numarasına (normal/kişisel WhatsApp, Business API
     DEĞİL) yönlendirilir. Bu tamamlanma anı = DB yazma tetikleyicisi.
  6. Online Sipariş: kullanıcı Yemeksepeti/Getir/Trendyol'a yönlendirilir. Platform API'leri
     müşteri verisini maskelediği için (Session 5 Tur 2'de doğrulandı) otomatik doğrulama teknik
     olarak KAPALI — bunun yerine kayıt sonrası aynı merkezi numaradan MANUEL teyit (önce WhatsApp,
     olmazsa SMS'e düşülür).
  7. Rıza metnine eklenecek not: "Online platform siparişleriniz otomatik doğrulanamadığından,
     kaydınızı teyit etmek için önce WhatsApp, olmazsa SMS yoluyla tarafınızla iletişime
     geçilecektir."
  8. Şu an tek aktif şube (Kağıthane) olduğu için tek merkezi numara yeterli; çoklu şube senaryosu
     (merkezi mi, şube-bazlı mı) İLERİYE ERTELENDİ.
- **Marka/UX değerlendirmesi (kullanıcı istedi, yapıldı):** İlk değerlendirmede "sepet terki" ve
  "WhatsApp hacim/spam" riskleri öne sürüldü; kullanıcı haklı olarak düzeltti — gel-al/masaya
  servis müşterisi zaten FİZİKSEL olarak gelecek (online-platform anonim kullanıcı davranışıyla
  kıyaslamak yanlıştı), normal/kişisel WhatsApp + düşük/fiziksel-sınırlı hacim = Business API'nin
  çözmeye çalıştığı ölçek sorunu burada geçerli değil. Kabul edilen risk: ileride hacim büyürse
  resmi WhatsApp Business API'ye geçiş "ne zaman" sorusu olacak, ayrı bir gelecekteki karar.

### 🔴 Kritik Keşif — WhatsAppOrderButton.tsx Zaten Var
- Yeni bir "#58 — WhatsApp yönlendirme, sıfırdan yazılacak" görevi tanımlanmışken, kullanıcının
  paylaştığı gerçek `session_log_yeni_blok.md` (Session 4, Beşinci Bölüm) incelenince
  `WhatsAppOrderButton.tsx`'in ZATEN VAR OLDUĞU ve daha önce doğrulandığı görüldü.
- Kullanıcıdan dosya istendi, incelendi: buton BİLİNÇLİ olarak kalıcı disabled bırakılmış (şube
  telefon numarası tanımlanmadığı, `lib/integrations/whatsapp.ts`/`buildWhatsAppOrderLink()` henüz
  yazılmadığı için — INTEGRATIONS.md §0'a bağlı, CORE §9 gereği bilinçli bağlanmamış).
  Yani #58, sıfırdan UI değil, var olan iskeleti tamamlama işi.
- **Ders (protokol doğrulaması):** CORE.md'nin "eksik context'le kod üretme, eksik dosyaları iste"
  kuralı burada neredeyse var olan bir bileşenin sıfırdan yeniden yazılmasını önledi.

### Dosyalama Sorunu (aynı gün, ayrı bir tur)
- Kullanıcı bir SESSION_INDEX.md kopyasını session_log formatındaki bir blokla karıştırıp tek belge
  olarak yapıştırdı — CORE.md §7.1/AGENT.md Kural #4'e göre session_log.md'nin SADECE YENİ BLOK
  aldığı, TAM DOSYA olarak asla yeniden üretilmediği hatırlatıldı, karışıklık teşhis edildi.
- Ardından kullanıcı v14 (Netgsm/WhatsApp OTP kararının hemen sonrası, test koşulmamış hâli)
  SESSION_INDEX.md'yi tekrar yükledi — bu, o ana kadar üretilen v15→v17 güncellemelerinin
  kullanıcıya/repoya hiç ulaşmadığı şüphesini doğurdu. Kullanıcı bunun "eski kopyayı düzeltmek
  için" bilinçli bir yükleme olduğunu, karmaşadan çekindiği için yaptığını açıkladı — v17 tek
  doğru kaynak olarak teyit edilip tekrar verildi.

### Açık Kalan / Yeni Açılan (bu Session'ın toplamı)
- **#56 (KAPANDI/PARKLANDI):** Twilio WhatsApp Business Sender onay süreci — Trial hesabın $20
  istemesi yüzünden parklandı, acil değil.
- **#32 (PARKLANDI):** Twilio TR SMS kısıtı — Netgsm ve WhatsApp fallback'le birlikte parklandı,
  #57/#58 mimarisi öncelikli hale geldi.
- **#57 (yeni, 🔴):** Rıza (KVKK) esaslı telefon+adres toplama formu — aydınlatma metni + checkbox
  + backend format doğrulama + `users` şemasına opsiyonel `age`/`gender` alanı. Henüz kodlanmadı.
- **#58 (yeni, 🟡, kapsam netleşti):** `lib/integrations/whatsapp.ts` + `buildWhatsAppOrderLink()`
  + gerçek şube WhatsApp numarası + `WhatsAppOrderButton.tsx`'in bu fonksiyona bağlanması. Henüz
  kodlanmadı — kodlama için `INTEGRATIONS.md` §0, `app/siparis/page.tsx` ve gerçek merkezi WhatsApp
  numarası kullanıcıdan istendi, bu Session kapanışı itibarıyla HENÜZ gelmedi.

### Sembol Özeti (Session 6)
📁 (3 dosya: `send-otp.ts`, `send/route.ts`, `send-otp.test.ts`) · 🔧 (2 büyük mimari karar —
hibrit OTP kanalı, ardından rıza-esaslı toplama + WhatsApp yönlendirme) · 🆕 (#56→parklandı, #57,
#58) · 🔴 (WhatsAppOrderButton keşfi, dosyalama/senkron sorunu) · ⚠️ (Netgsm "onaylandı" notu
çelişkisi hâlâ çözülmedi — Session 5 ile Session 6 arasında)
