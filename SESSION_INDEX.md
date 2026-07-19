# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 4 (devam ediyor). Bu sohbette (yeni sohbet — önceki Oturum 4
          bloğunun devamı): (1) customizer başlığından "— Kâseni Yarat" eki
          kaldırıldı, (2) sepete teslimat kanalı (Gel-Al/Masaya Servis) eklendi
          — CartItem.unitCalorie7s yazım hatası da düzeltildi, (3) customizer
          katalog isimleri Türkçeleştirildi (id'ler değişmedi), (4)
          "Benim Kâsem"/"Kâseni Yarat" içindeki â karakteri kullanıcı isteğiyle
          tamamen kaldırıldı ("Benim Kasem" oldu) — menu-data.json ve
          CartDrawer'daki "Özel Kâse" düzeltildi, (5) fonts.ts'e 'latin-ext'
          eklendi (deneysel, â sorununun asıl çözümü olmayabilir — sorun sonra
          â'yı tamamen kaldırarak çözüldü).
Faz:      Oturum 4 — customizer uçtan uca çalışıyor (test verisiyle), sepet
          artık teslimat kanalı seçtiriyor (CartDrawer içinde, henüz canlıda
          görsel doğrulanmadı). "Benim Kasem" başlığı ve customizer taban/ana
          malzeme isimleri Türkçe olarak canlıda DOĞRULANDI (ekran görüntüsü).
          Hâlâ İngilizce/â kalan 2 yer BİLİNÇLİ OLARAK ERTELENDİ (kullanıcı
          "bu kalsın" dedi): Hero.tsx'teki "Kâseni Yarat" CTA metni ve
          StepBase.tsx'teki "Kâsenin tabanını seç." açıklaması.
Gerekçe:  Önceki sohbet bloğunda page.tsx yazılmış, Header/CartBadge/CartDrawer
          bağlanmıştı ama push/deploy doğrulaması yarım kalmıştı. Bu sohbette
          kullanıcı "Push ettim" dedi, ardından yeni görevlere (sepet kanalı,
          Türkçeleştirme, â düzeltmesi) geçildi — her adımda KARAR BİLDİRİMİ
          üretildi, çoğunda onay alındı, bazılarında kullanıcı ekran
          görüntüsüyle canlı doğrulama sağladı.
Çıktı:    Repo: github.com/Sovereign34/Bowlera_site (main). Deploy: Vercel —
          bu sohbette 3 ekran görüntüsüyle CANLI doğrulandı: (1) "Benim Kasem"
          başlığı â'sız görünüyor, (2) Base adımında "Jasmin Pirinç"/"Esmer
          Pirinç" Türkçe isimlerle görünüyor (customizer-data.ts değişikliği
          canlıda teyitli), (3) Ana sayfada "Kâseni Yarat" CTA'sı hâlâ â
          gösteriyor (bilinçli olarak dokunulmadı). Sepet kanalı seçici
          (FulfillmentChannelSelector) HENÜZ canlıda görsel doğrulanmadı.
```

⚠️ **DEĞİŞMEYEN KRİTİK BLOKAJ:** `customizerCatalog` ve "Benim Kâsem" ürünündeki
tüm fiyat/kalori/protein rakamları hâlâ TEST VERİSİ (uydurma). İsimler artık
Türkçe ama sayılar gerçek değil. PROD'a bu haliyle çıkmamalı (BSC-5, Açık
Sorun #24 — DEĞİŞMEDİ).

⚠️ **YENİ RİSK (Açık Sorun #25):** `CartItem.unitCalorie7s` → `unitCalories`
olarak yeniden adlandırıldı ama bu alanı okuyan/yazan başka dosyalar
(`SummaryPanel.tsx`, `AddToCartButton.tsx` gibi) bu sohbette hiç görülmedi.
Push sonrası TypeScript derlemesi bu dosyalarda kırılabilir — kontrol
edilmeden production'a alınmamalı.

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI

| # | Karar | Tarih | Kaynak/Gerekçe |
|---|---|---|---|
| 1 | "Kâseni Yarat" akışı 4 adımdan **5 adıma** çıkarıldı: Base → Main → Garden → Signature Flavor → Finish | Oturum 2 — 2026-07-18 | Kullanıcı önerisi. Şema notu: `20260718001123_customizer_5_adim_gecisi.md` |
| 2 | ~~Adım/malzeme isimleri tamamen İngilizce~~ **GERİ ALINDI (bkz. Karar #15)** | Oturum 2 — 2026-07-18 | Premium/global algı kararıydı, kullanıcı bu sohbette geri aldı |
| 3 | Garden: ilk 4 seçim ücretsiz, Avokado her zaman ücretli | Oturum 2 — 2026-07-18 | Toppings kuralıyla tutarlılık |
| 4 | Finish: ilk 1 seçim ücretsiz, sonrası ücretli | Oturum 2 — 2026-07-18 | Kullanıcı seçimi |
| 5 | "Make it Yours" ayrı adım değil, Finish'e entegre; "Double Main" `mainPortion` mekanizmasını yeniden kullanır | Oturum 2 — 2026-07-18 | Kullanıcı seçimi + AGENT.md Kural #5 |
| 6 | Ana sayfa sloganı: **"Sağlıklı Beslen, Sağlıklı Yaşa, Gücünü Hisset"** | Oturum 4 — 2026-07-18 | Kullanıcı kararı |
| 9 | Header sepet ikonu client-side state'e taşındı (`"use client"`) | Oturum 4 — 2026-07-18 | Tutarlılık ve minimum dokunuş |
| 10 | VisualPreview illüstrasyon yerine **gerçek ürün fotoğrafı** kullanacak + "Görsel temsilîdir" disclaimer'ı eklenecek | Oturum 4 — 2026-07-18 | Kullanıcı kararı — henüz uygulanmadı |
| 11 | Nohut/Meksika fasulyesi gibi Main'lerde Signature Flavor adımı atlanmıyor, içeriği/etiketi değişiyor | Oturum 4 — 2026-07-18 | Kullanıcı kararı — henüz uygulanmadı |
| 12 | "Kâseni Yarat" sadece "Benim Kâsem" (`build-your-own-kasem`) ürününde | Oturum 4 — 2026-07-18 | Karar #7/#8'in düzeltmesi |
| 13 | Sepete teslimat kanalı **sepet/oturum seviyesinde tek alan** olarak eklendi (ürün/CartItem bazlı DEĞİL) — global chain pattern'iyle (Chipotle/Starbucks/McDonald's tarzı tek seferlik seçim) uyumlu. Kanal enum'u: `"pickup"` (Gel-Al) \| `"dine-in"` (Masaya Servis). Yemeksepeti/Getir/Trendyol bilinçli olarak bu enum'a DAHİL EDİLMEDİ — kullanıcı o akışta Bowlera sitesinden ayrılıp marketplace'e yönlendiriliyor, kendi sepet state'i tamamlanmıyor; bu ayrı bir UI linki olacak (henüz yazılmadı). İleride "delivery" (kendi kurye) eklenebilecek şekilde tasarlandı. UI yeri: CartDrawer'ın en üstü (checkout/ayrı sayfa değil) — şu an kanal bazlı fiyat/menü farkı olmadığı için. Persist ediliyor (sepetle birlikte localStorage'da kalıyor), `clearCart()` ile sıfırlanmıyor. | Bu sohbet — 2026-07-18 | Kullanıcı: "sepete giren ürünün hangi kanaldan teslim edileceği" + "kendi kuryemizi de öngör" |
| 14 | `â` karakteri (Kâseni/Kâsem) bazı Android/Chrome cihazlarda `å`'ya benzer render ediliyordu. Byte-seviyesi kontrol edildi — kaynak dosyalar (`menu-data.json`) baştan beri doğru UTF-8 (`â`, U+00E2) içeriyordu, bu bir encoding hatası DEĞİLDİ. Kesin kök neden teyit edilemedi (muhtemelen font glyph rendering/FOUT). Denenen ama garantisiz düzeltme: `lib/fonts.ts`'e `latin-ext` subset eklendi. **Asıl çözüm kullanıcı tercihiyle geldi: â karakteri tamamen kaldırıldı** ("Benim Kasem", "Özel Kase") — bkz. Karar #16. | Bu sohbet — 2026-07-18 | Teknik teşhis + kullanıcı nihai tercihi |
| 15 | (Karar #2'nin geri alınması) `lib/customizer-data.ts`'teki tüm `name` alanları İngilizceden Türkçeye çevrildi (örn. "Grilled Chicken" → "Izgara Tavuk"). `id` alanları BİLİNÇLİ OLARAK değiştirilmedi (store/pricing referans veriyor). Canlıda doğrulandı (Base adımında "Jasmin Pirinç"/"Esmer Pirinç" görünüyor). ⚠️ CUSTOMIZER_SPEC.md §2'deki isim listesi bu değişiklikle senkron DEĞİL — ayrı görev. | Bu sohbet — 2026-07-18 | Kullanıcı: "İngilizce olmayan kelimeler" düzeltilsin |
| 16 | `â` karakteri `menu-data.json`'da ("Benim Kasem") ve `CartDrawer.tsx`'te ("Özel Kase") kaldırıldı, canlıda doğrulandı. **Hero.tsx'teki "Kâseni Yarat" CTA metni ve StepBase.tsx'teki "Kâsenin tabanını seç." açıklaması BİLİNÇLİ OLARAK ERTELENDİ** — kullanıcı "Bu kalsın başka göreve geç" dedi. Bu iki dosya bu sohbette hiç görülmedi/istenmedi bir daha. | Bu sohbet — 2026-07-18 | Kullanıcı kararı — kapsam dışı bırakıldı |

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 4 (devam) — 2026-07-18, yeni sohbet penceresi |
| Son Eylem | ROADMAP.md + MASTER_PLAN.md ile genel ilerleme değerlendirmesi yapıldı (kod değişikliği değil) |
| Blocker | 🔴 customizerCatalog + "Benim Kâsem" hâlâ TEST VERİSİ (Açık Sorun #24, değişmedi) |
| Devam Noktası | Bu sohbette üretilen dosyaların push/deploy durumu KISMEN teyitli — aşağıdaki tabloya bak. `unitCalorie7s` rename sonrası kırılan dosya olup olmadığı kontrol edilmeli (Açık Sorun #25). |

---

## GENEL DURUM

| Alan | Değer |
|---|---|
| Proje | Bowlera — Healthy Bowls |
| Aktif Oturum | Oturum 4 — devam ediyor |
| Toplam Session | 4 (bu sohbet, önceki Oturum 4 bloğunun devamı sayılıyor) |
| Repo | `github.com/Sovereign34/Bowlera_site` |
| Menü Veri Kaynağı | ✅ `lib/menu-data.json` — 9 ürün (6 signature, 2 içecek, 1 build-your-own TEST fiyatlı ₺999). â düzeltmesi canlıda doğrulandı. |
| Veri Modeli | ✅ `types/index.ts` — `unitCalories` düzeltildi + `FulfillmentChannel` eklendi. Push/deploy doğrulanmadı. |
| Customizer Sepet Store | 🟡 `store/useCartStore.ts` — `fulfillmentChannel` + `setFulfillmentChannel` eklendi. Push/deploy doğrulanmadı. |
| Customizer Statik Veri | 🟡 `lib/customizer-data.ts` — isimler Türkçeleşti (canlıda doğrulandı), rakamlar HÂLÂ TEST VERİSİ |
| Sepet UI | 🟡 `CartDrawer.tsx`'e `FulfillmentChannelSelector.tsx` (yeni dosya) bağlandı — **canlıda henüz görsel doğrulanmadı** |
| Font | 🟡 `lib/fonts.ts`'e `latin-ext` eklendi — etkisi net değil (â sorunu başka yolla çözüldü) |
| Header (Sepet) | ✅ Önceki sohbet bloğunda bağlandı ve canlıda doğrulandı — sepet ikonu tıklanınca çekmece açılıyor |
| Sepet UI (CartBadge) | ✅ İçeriği önceki blokta görüldü, bu sohbette dokunulmadı |
| MenuCard | ✅ Önceki blokta "Özelleştir" butonu eklendi, bu sohbette dokunulmadı |
| Hero | 🟡 Slogan + CTA linki önceki blokta düzeltildi; bu sohbette "Kâseni Yarat" metnindeki â bilinçli olarak ERTELENDİ (Açık Sorun #27) |
| Görsel/Fotoğraf İçeriği | ⬜ Hâlâ bekleniyor — değişmedi |
| Üçüncü Parti Anahtarları | ⬜ Henüz temin edilmedi — değişmedi |

---

## AÇIK SORUNLAR

| # | Öncelik | Açıklama | Oturum | Referans |
|---|---|---|---|---|
| 4 | 🟡 | Üçüncü parti API anahtarları temin edilmedi | Sonraki Faz | MASTER_PLAN §8 |
| 7 | 🟡 | Allergen gösterimi DESIGN_SYSTEM.md onayı bekliyor | Oturum 2 | DESIGN_SYSTEM.md §2 |
| 10 | 🟡 | ARCHITECTURE.md §2.4 ve DEPENDENCIES.md, 5 adımlı customizer'a göre güncel değil | Oturum 2 | `20260718001123_customizer_5_adim_gecisi.md` |
| 13 | 🟡 | `git log --oneline` ile push'lar hiç teyit edilmedi | Oturum 3 | — |
| 15 | 🟢 | TEST_MATRIX.md, DEPENDENCIES.md, session_log.md bu sohbette de yüklenmedi | Oturum 3→4 | CORE.md §7.1 |
| 16 | 🟡 | `lib/customizer-summary-format.ts` içeriği hâlâ hiç görülmedi | Oturum 4 | AGENT.md Kural #5 |
| 17 | 🟡 | `customizerCatalog` isimleri Türkçe ama rakamlar TEST VERİSİ | Oturum 4 | `lib/customizer-data.ts` |
| 18 | 🔴 | "Benim Kâsem" fiyatı hâlâ TEST (₺999) — gerçek fiyat bekleniyor | Oturum 4 | `lib/menu-data.json` |
| 20 | 🟢 | **DÜZELTİLDİ — sohbette yanlışlıkla düşürülmüştü, geri eklendi.** `app/menu/customize/[id]/page.tsx` içinde hâlâ 3 onay bekleyen varsayım var: (a) menu-data.json export şekli — kapatılabilir; (b) sepete ekleme sonrası otomatik `reset()` — onaylanmadı; (c) `notFound()` client component'te 404 davranışı test edilmedi. Bu sohbette dosyaya sadece başlık düzeltmesi için dokunuldu, bu 3 varsayım hâlâ çözülmedi. | Oturum 4 | `app/menu/customize/[id]/page.tsx` |
| 22 | 🟡 | Signature Flavor'ın Main'e göre koşullu içerik göstermesi henüz uygulanmadı (Karar #11) | Oturum 4 | CUSTOMIZER_SPEC.md §2 |
| 24 | 🔴 | `customizer-data.ts` + `menu-data.json`'daki test rakamları PROD öncesi değiştirilmeli (BSC-5) | Oturum 4 | — |
| 25 | 🔴 | `CartItem.unitCalorie7s` → `unitCalories` yeniden adlandırıldı. Bu alanı kullanan başka dosyalar (SummaryPanel, AddToCartButton, MobileSummaryDrawer vb.) bu sohbette görülmedi — push öncesi `grep -r unitCalorie7s` ile taranmalı, aksi halde TypeScript derlemesi kırılabilir. | Bu sohbet | `types/index.ts`, `docs/schema-changes/20260718070000_...md` |
| 26 | 🟡 | Sepette teslimat kanalı seçimi eklendi ama **hiçbir yerde zorunlu kılınmıyor** — kullanıcı kanal seçmeden de sepete ekleyip "sipariş verebilir" (checkout akışı henüz yok). `app/siparis/page.tsx` yazılırken bu alanın zorunluluğu ele alınmalı. | Bu sohbet | `store/useCartStore.ts`, `app/siparis/page.tsx` (henüz yok) |
| 27 | 🟢 | **Bilinçli ertelendi.** Hero.tsx'teki "Kâseni Yarat" CTA'sı ve StepBase.tsx'teki "Kâsenin tabanını seç." hâlâ `â` içeriyor — kullanıcı isteğiyle bu sohbette dokunulmadı. | Bu sohbet | `components/home/Hero.tsx`, `components/customizer/StepBase.tsx` |
| 28 | 🟢 | Adım başlıkları (Base/Main/Garden/Signature Flavor/Finish) hâlâ İngilizce — Karar #15 kapsamına alınmadı, ayrı onay bekliyor (Türkçeye çevrilsin mi tam netleşmedi, kullanıcı konuyu değiştirdi). | Bu sohbet | `components/customizer/Step*.tsx` |
| 29 | 🟢 | `CUSTOMIZER_SPEC.md` §2'deki İngilizce isim listesi artık `customizer-data.ts` ile senkron değil (Karar #15 sonrası). | Bu sohbet | `CUSTOMIZER_SPEC.md` |
> Kapanan sorunlar (bu sohbet öncesi): #5, #6, #9, #11(eski), #12(eski), #14(eski), #19, #21, #23. Bu sohbette yeni açılanlar: #25, #26, #27, #28, #29. **#20 hâlâ açık** — bir önceki taslakta yanlışlıkla silinmişti, düzeltildi.

---

## BOWLERA OTURUM DURUMU

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (14 dosya) | ✅ Üretildi — son onay bekliyor |
| **Oturum 1** | Next.js+Tailwind, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard, statik menü verisi | ✅ Tamamlandı |
| **Oturum 3** | Zustand store + Customizer masaüstü UI bileşenleri | ✅ Büyük ölçüde teyit edildi |
| **Oturum 4** | page.tsx, VisualPreview/Mobil, sepet, + bu sohbette: kanal seçimi, Türkçeleştirme, â düzeltmesi | 🟡 **Devam ediyor** — veri/fotoğraf blokajı sürüyor |
| **Kontrol Noktası** | Kullanıcı testi (5-10 kişi) | ⬜ Bekliyor — Oturum 4 bitmeden başlamaz |
| **Oturum 5** | Hakkımızda, Şubeler, İletişim, SEO, son kontrol | ⬜ Bekliyor |

**İlerleme özeti (bu sohbette kullanıcıya verilen değerlendirme):** 5 oturumdan ~3'ü tamam, Oturum 4 yarıda — en kritik blokaj kod değil, gerçek mutfak verisi (fiyat/kalori/protein) ve ürün fotoğrafları eksikliği. Kontrol Noktası ve Oturum 5 hiç başlamadı.

---

## ÜRETİLEN KOD DOSYALARI (dokunulan/görülen tüm dosyalar — önceki blok + bu sohbet)

| Dosya | Durum | Test | Repo | Deploy |
|---|---|---|---|---|
| `components/layout/Header.tsx` | ✅ Önceki blokta CartBadge/CartDrawer'a bağlandı, `"use client"` oldu | ⬜ eski testler geçersiz olabilir | 🟡 Push edilmeli | ✅ Canlıda doğrulandı (sepet ikonu → çekmece açılıyor) |
| `components/cart/CartBadge.tsx` | ✅ Önceki blokta içeriği görüldü, değiştirilmedi | ⬜ | ✅ (önceden push edilmiş varsayılıyor) | ⬜ |
| `store/useCustomizerStore.ts` | ✅ Önceki blokta `goToStep` bug'ı düzeltildi | 🟡 fix sonrası yeni test eklenmeli | 🟡 Push edilmeli | ⬜ |
| `components/home/Hero.tsx`, `HeroHeadline.tsx` | ✅ Önceki blokta slogan güncellendi | 🟡 eski testler güncellenmedi | 🟡 Push edilmeli | ✅ Canlıda doğrulandı (slogan) — ⚠️ CTA'daki â bu sohbette bilinçli ertelendi (Açık Sorun #27) |
| `components/menu/MenuCard.tsx` | ✅ Önceki blokta "Özelleştir" butonu eklendi | 🟡 eski testler güncellenmedi | 🟡 Push edilmeli | ⬜ Canlıda henüz test edilmedi |
| `components/customizer/StepBase.tsx` | ✅ Önceki blokta yazıldı | — | 🟡 Push edilmeli | 🟡 Canlıda çalışıyor (ekran görüntüsüyle görüldü) — ⚠️ içindeki â bu sohbette bilinçli ertelendi (Açık Sorun #27) |
| `components/customizer/StepMain.tsx` | ✅ Önceki blokta yazıldı | — | 🟡 Push edilmeli | ⬜ |
| `components/customizer/StepGarden.tsx` | ✅ Önceki blokta yazıldı | — | 🟡 Push edilmeli | ⬜ |
| `components/customizer/StepSignatureFlavor.tsx` | ✅ Önceki blokta yazıldı | — | 🟡 Push edilmeli | ⬜ |
| `components/customizer/StepFinish.tsx` | ✅ Önceki blokta yazıldı | — | 🟡 Push edilmeli | ✅ Canlıda çalıştığı ekran görüntüsüyle görüldü |
| `app/menu/customize/[id]/page.tsx` | ✅ Önceki blokta yazıldı, **bu sohbette başlık düzeltildi** | ⬜ test yok | ✅ Push edildi (kullanıcı onayladı) | ✅ Canlıda dolaylı doğrulandı |
| `docs/schema-changes/20260718070000_cartitem_unitcalories_ve_fulfillment_channel.md` | ✅ **Bu sohbette yeni** | — | 🟡 Push edilmeli | — |
| `types/index.ts` | ✅ **Bu sohbette** `unitCalories` düzeltmesi + `FulfillmentChannel` eklendi | — | 🟡 Push/deploy doğrulanmadı | ⬜ |
| `store/useCartStore.ts` | ✅ **Bu sohbette** `fulfillmentChannel` state + action eklendi | — | 🟡 Push/deploy doğrulanmadı | ⬜ |
| `components/cart/FulfillmentChannelSelector.tsx` | ✅ **Bu sohbette yeni dosya** | — | 🟡 Push/deploy doğrulanmadı | ⬜ |
| `components/cart/CartDrawer.tsx` | ✅ **Bu sohbette** Selector bağlandı + "Özel Kase" â düzeltmesi | — | 🟡 Push/deploy doğrulanmadı | ⬜ |
| `lib/customizer-data.ts` | ✅ **Bu sohbette** tüm `name` alanları Türkçe | — | ✅ Push edildi | ✅ Canlıda doğrulandı (Jasmin Pirinç/Esmer Pirinç) |
| `lib/menu-data.json` | ✅ **Bu sohbette** "Benim Kasem" â'sız | — | ✅ Push edildi | ✅ Canlıda doğrulandı |
| `lib/fonts.ts` | 🟡 **Bu sohbette** `latin-ext` eklendi, etkisi belirsiz | — | 🟡 Push/deploy doğrulanmadı | ⬜ |

> Dokunulmayan/ertelenen: `components/home/Hero.tsx`'in CTA metni, `components/customizer/StepBase.tsx`'in açıklama metni — hâlâ `â` içeriyor, kullanıcı isteğiyle bu sohbette işlenmedi (Açık Sorun #27).
> Diğer tüm dosyaların (Footer, MenuCardImage/Badges/Info, CategoryNav, FilterPanel, SummaryPanel, SummaryTotals, VisualPreview, MobileSummaryDrawer vb.) durumu önceki session bloklarında olduğu gibi — bu sohbette değişmedi.

---

## SIRADAKİ GÖREVLER

| Sıra | Görev | Öncelik | Durum |
|---|---|---|---|
| 1 | `unitCalorie7s` kullanan başka dosya var mı taranmalı — push öncesi (Açık Sorun #25) | 🔴 | ⬜ |
| 2 | Bu sohbette üretilen dosyaları push et: şema notu, `types/index.ts`, `useCartStore.ts`, `FulfillmentChannelSelector.tsx`, `CartDrawer.tsx`, `fonts.ts` — sonra sepet kanalı seçicisini canlıda görsel doğrula | 🔴 | ⬜ |
| 3 | `customizerCatalog` + "Benim Kâsem" TEST rakamlarını gerçek mutfak verisiyle değiştir (Açık Sorun #24) | 🔴 | ⬜ |
| 4 | Teslimat kanalının checkout'ta zorunlu kılınması (Açık Sorun #26) — `app/siparis/page.tsx` yazılırken ele alınmalı | 🟡 | ⬜ |
| 5 | Signature Flavor'ın Main'e göre koşullu içerik göstermesi (Karar #11, Açık Sorun #22) | 🟡 | ⬜ |
| 6 | `page.tsx`'teki 3 onay bekleyen varsayımı teyit et (Açık Sorun #20) | 🟢 | ⬜ |
| 7 | Adım başlıklarının (Base/Main/...) Türkçeleştirilip çevrilmeyeceğine netlik getir (Açık Sorun #28) | 🟢 | ⬜ |
| 8 | Hero.tsx + StepBase.tsx'teki `â` — kullanıcı isterse ele alınacak (Açık Sorun #27, şu an bilinçli ertelendi) | 🟢 | ⬜ |
| 9 | VisualPreview altına "Görsel temsilîdir" disclaimer'ı ekle (Karar #10) | 🟡 | ⬜ |
| 10 | CUSTOMIZER_SPEC.md'yi Türkçe isim listesiyle senkronize et (Açık Sorun #29) | 🟢 | ⬜ |
| 11 | `git log --oneline -10` ile push'ları teyit et (Açık Sorun #13) | 🟡 | ⬜ |

---

## 📜 GEÇMİŞ / ARŞİV — Bu Sohbet Detaylı Kayıt

### Başlık Düzeltmesi
- `page.tsx`'teki h1, `{bowl.name} — Kâseni Yarat` yerine sadece `{bowl.name}` yapıldı. Tek satırlık izole değişiklik, kullanıcı push etti.

### Sepete Teslimat Kanalı
- Kullanıcı "sepete giren ürünün hangi kanaldan teslim edileceği" ihtiyacını belirtti. Global chain pattern'i (sepet/oturum seviyesinde tek seçim) araştırılıp önerildi, kullanıcı onayladı.
- Üçüncü "kanal" (Yemeksepeti/Getir/Trendyol) sorgulandı — kullanıcının markeplace'e yönlendirme anlamına geldiği netleşti, bunun ayrı bir CartItem kanalı olarak modellenmemesi gerektiği (siteden çıkış = sepet tamamlanmıyor) gerekçesiyle önerildi ve onaylandı.
- `types/index.ts`'e `FulfillmentChannel = "pickup" | "dine-in"` eklendi (ileride "delivery" eklenebilir şekilde). Aynı turda `CartItem.unitCalorie7s` yazım hatası da (kullanıcı onayıyla) `unitCalories` olarak düzeltildi.
- Şema değişiklik notu CORE.md §7.4 formatında üretildi.
- `useCartStore.ts`'e `fulfillmentChannel` state + `setFulfillmentChannel` action eklendi, persist otomatik kapsadı.
- UI yeri tartışıldı (CartDrawer içi / ayrı ekran / checkout) — CartDrawer'ın en üstü seçildi (kanal bazlı fiyat farkı olmadığı için basitlik tercih edildi).
- Kural #1 (20 satır disiplini) gereği `FulfillmentChannelSelector.tsx` ayrı bileşen olarak yazıldı, `CartDrawer.tsx`'e tek satır import+render ile bağlandı.

### â/å Sorunu ve Nihai Çözüm
- Kullanıcı ekran görüntüsüyle "Benim Kâsem" başlığının bazı cihazlarda `å` gibi göründüğünü bildirdi.
- `menu-data.json` byte seviyesinde (`\xc3\xa2`) kontrol edildi — kaynak veri doğru UTF-8 `â` içeriyordu, encoding hatası yoktu.
- Font glyph rendering / FOUT teorisi öne sürüldü, `lib/fonts.ts`'e deneysel olarak `latin-ext` subset eklendi (confidence: MEDIUM, kesin çözüm garantisi verilmedi).
- Kullanıcı sinirlendi ve `â` karakterinin tamamen kaldırılmasını istedi — bu noktada kullanıcı kaba bir dil kullandı, Claude nazikçe sınır koyup göreve devam etti.
- `menu-data.json`'da "Benim Kâsem" → "Benim Kasem", `CartDrawer.tsx`'te "Özel Kâse" → "Özel Kase" yapıldı, kullanıcı canlıda doğruladı.
- Hero.tsx ve StepBase.tsx'teki kalan `â`'lar için dosya istendi ama kullanıcı "Bu kalsın başka göreve geç" dedi — bilinçli olarak ertelendi.

### Customizer Malzeme İsimlerinin Türkçeleştirilmesi
- Kullanıcı İngilizce malzeme isimlerinden rahatsızlığını belirtti (Karar #2'nin geri alınması talebi).
- `lib/customizer-data.ts`'teki tüm `name` alanları Türkçeye çevrildi, `id` alanları bilinçli olarak değiştirilmedi (store/pricing referans bütünlüğü için).
- Canlıda ekran görüntüsüyle doğrulandı ("Jasmin Pirinç", "Esmer Pirinç").
- Adım başlıklarının (Base/Main/Garden/Signature Flavor/Finish) çevrilip çevrilmeyeceği netleşmeden kullanıcı konuyu değiştirdi — açık kaldı (Açık Sorun #28).

### İlerleme Değerlendirmesi
- Kullanıcı "Çok yolumuz kaldı mı?" diye sordu, ROADMAP.md + MASTER_PLAN.md §8 karşılaştırıldı.
- Dürüst değerlendirme verildi: 5 oturumdan ~3'ü tamam, Oturum 4 yarıda, asıl blokajın kod değil gerçek veri/fotoğraf eksikliği olduğu vurgulandı. Kontrol Noktası ve Oturum 5'in hiç başlamadığı belirtildi.

### SESSION_INDEX.md Düzeltmesi (bu blok)
- İlk üretilen SESSION_INDEX.md'nin bir öncekinden belirgin şekilde kısa olduğu kullanıcı tarafından fark edildi.
- Kontrol edildi: kapanmış kararların/sorunların özetlenmesi kasıtlı ve doğruydu, ama "ÜRETİLEN KOD DOSYALARI" tablosundaki 13 satır (çoğu hâlâ "🟡 Push edilmeli" — yani TAMAMLANMAMIŞ) ve Açık Sorun #20 (hâlâ çözülmemiş) yanlışlıkla silinmişti.
- Hata kabul edildi, eski + yeni tablo birleştirilerek düzeltildi.

---

## 📜 GEÇMİŞ / ARŞİV — Önceki Oturum 4 Bloğu (bu sohbetten önce)

### Header.tsx → CartBadge/CartDrawer Bağlantısı
- `Header.tsx` `"use client"` yapıldı, `useState` ile `isCartOpen` eklendi, `CartBadge`/`CartDrawer` bağlandı. Kalite 5/5, Güvenlik 8/8. Checkpoint alındı, canlıda doğrulandı (sepet ikonu → çekmece açılıyor, "Sepetiniz boş." görünüyor).

### goToStep Bug Fix
- `useCustomizerStore.ts`'teki `goToStep` fonksiyonunun `maxReachedStep`'i güncellemediği doğrulandı, tek satırlık izole fix uygulandı.

### app/menu/customize/[id]/page.tsx — Sıfırdan Yazım
- Dosya hiç yazılmamıştı, tüm bağımlılıklar tek tek görülüp üretildi. Bu süreçte `customizerCatalog`'un boş olduğu ve Step bileşenlerinin yazılmadığı keşfedildi. 3 varsayım kod içi yorumla işaretlendi (Açık Sorun #20 — hâlâ çözülmedi).

### Slogan ve Hero Değişiklikleri
- Slogan Hero'ya eklendi, sonra h1'in kendisiyle değiştirildi. `HeroHeadline.tsx`'in `WORDS` dizisi güncellendi.

### Customizer'a Giriş Noktaları Keşfi ve Düzeltmesi
- Hero CTA'sının 404 verdiği bulundu, MenuCard'a "Özelleştir" butonu eklendi, Hero CTA'sı geçici olarak `sig-teriyaki-tavuk`'a yönlendirildi, sonra düzeltildi (yalnızca `build-your-own-kasem`'e).

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 3 Detaylı Kayıt

### İlk Yarı — Store + Pricing + Data Üretimi
- `store/useCustomizerStore.ts`, `lib/customizer-pricing.ts`, `lib/customizer-data.ts` üretildi. `npm test`: 10 test dosyası, 53 test — tümü ✅.

### İkinci Yarı — Masaüstü UI Bileşenleri (KESİNTİ)
- Sıra: format yardımcı fonksiyonu → `SummaryTotals` → `AddToCartButton.tsx` → `SummaryPanel.tsx`. Sohbet kesildi, kullanıcı dosyaları manuel push etti.

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 2 Detaylı Kayıt

### CategoryNav.tsx + FilterPanel.tsx
- `lib/menu-filters.ts`, `CategoryNav.tsx`, `FilterPanel.tsx` üretildi. `npm test`: 8 test dosyası, 34 test — tümü ✅.

### Customizer 4→5 Adım Geçişi
- 5 adımlı akışa geçildi, şema değişiklik notu üretildi.

### MenuCard Container Hatası ve Düzeltmesi
- `MenuCard.tsx` içeriği yanlışlıkla `MenuCardImage.tsx` kopyasıydı, düzeltildi.

### Test Altyapısı / Vercel Build Hatası
- `vitest.config.ts` versiyon çakışması ve `tsconfig.json`/vitest tip çakışması çözüldü.

---

## 📜 GEÇMİŞ / ARŞİV — Oturum 0 Detaylı Kayıt

- Çekirdek üçlü (CORE.md, AGENT.md), referans üçlüsü (ARCHITECTURE.md, DESIGN_SYSTEM.md, CUSTOMIZER_SPEC.md), ikinci üçlü (DEPENDENCIES.md, ROADMAP.md, TEST_MATRIX.md), üçüncü üçlü (CONTENT_GUIDE.md, INTEGRATIONS.md, FAILURE_PATTERNS.md, CONFIG_SCHEMA.md) üretildi.
- Oturum 1'de logo aktarıldı, Header/Footer/Hero görsel olarak doğrulandı.

---

*BOWLERA SESSION_INDEX.md — düzeltildi, Session 4 (devam ediyor) — 2026-07-18*
