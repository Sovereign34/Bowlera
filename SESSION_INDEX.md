# BOWLERA — SESSION INDEX
> Bu dosya her session başında okunur. CORE.md ile birlikte verilir.
> Claude bu dosyadan anlık durumu, açık sorunları ve sıradaki görevleri anlar.
> Her session kapanışında TAM DOSYA olarak güncellenir.
> Şişmeyi önlemek için: tamamlanan görevler silinir, eski kararlar bu dosyanın altına taşınır.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 4 (devam ediyor). Bu sohbette en son: CartDrawer'da keşfedilen
          kritik bir görsel bug (Header'daki backdrop-blur, CartDrawer'ın
          position:fixed'ini viewport yerine Header kutusuna hapsediyordu,
          içerik Hero'ya taşıyordu) teşhis edildi, React Portal ile düzeltildi,
          push edildi ve 3 ekran görüntüsüyle CANLI doğrulandı — çakışma
          tamamen gitti. Bu düzeltmeyle birlikte, daha önce "push edilmeli"
          olarak bekleyen kanal seçimi altyapısının (FulfillmentChannel tipi,
          useCartStore alanı, FulfillmentChannelSelector bileşeni) da fiilen
          çalıştığı canlıda dolaylı olarak teyit edildi (seçici state tutuyor,
          arayüz tepki veriyor).
Faz:      Oturum 4 — customizer uçtan uca çalışıyor (test verisiyle), sepet
          teslimat kanalı seçtiriyor ve CANLIDA TEMİZ görünüyor (görsel bug
          kapatıldı). "Benim Kasem" başlığı, customizer taban/ana malzeme
          isimleri Türkçe — hepsi canlıda doğrulandı. Hâlâ İngilizce/â kalan
          2 yer BİLİNÇLİ OLARAK ERTELENDİ: Hero.tsx'teki "Kâseni Yarat" CTA
          metni ve StepBase.tsx'teki "Kâsenin tabanını seç." açıklaması
          (Açık Sorun #27 — değişmedi). Kullanıcı kaydı/auth konusu TASLAK
          aşamasında bekliyor (Karar #17, Açık Sorun #30).
Gerekçe:  Önceki turda kullanıcı 3 ekran görüntüsüyle CartDrawer'da Hero
          içeriğinin çekmeceye sızdığını bildirdi. Kod incelemesi (CartDrawer
          → Hero → Header sırasıyla) Header.tsx'teki `backdrop-blur`
          sınıfının CSS containing-block kuralı gereği CartDrawer'ın
          `fixed inset-0`'ını bozduğunu ortaya çıkardı. KARAR BİLDİRİMİ
          üretildi (Portal çözümü), onay alındı, kod yazıldı, kullanıcı
          push etti ve 3 ekran görüntüsüyle doğruladı.
Çıktı:    Repo: github.com/Sovereign34/Bowlera_site (main). Deploy: Vercel —
          bu sohbette CANLI doğrulandı: (1) Sepet çekmecesi artık temiz,
          Hero sızıntısı yok, (2) kanal seçici çalışıyor ve state tutuyor
          (Masaya Servis seçili kalmış görünüyor), (3) "Benim Kasem" başlığı
          â'sız, Base adımı Türkçe isimlerle ve kcal ile doğru çalışıyor.
```

⚠️ **DEĞİŞMEYEN KRİTİK BLOKAJ:** `customizerCatalog` ve "Benim Kâsem" ürünündeki
tüm fiyat/kalori/protein rakamları hâlâ TEST VERİSİ (uydurma). İsimler artık
Türkçe ama sayılar gerçek değil. PROD'a bu haliyle çıkmamalı (BSC-5, Açık
Sorun #24 — DEĞİŞMEDİ).

⚠️ **TASLAK (Karar #17 / Açık Sorun #30):** Kullanıcı kaydı/giriş yönü belirlendi
(telefon + SMS OTP, guest checkout korunuyor) ama teknik mimari (OTP sağlayıcısı,
auth store, DB şeması, hesap kurtarma akışı) hiç netleşmedi. Koda geçilmedi.

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
| 13 | Sepete teslimat kanalı **sepet/oturum seviyesinde tek alan** olarak eklendi (ürün/CartItem bazlı DEĞİL) — global chain pattern'iyle uyumlu. Kanal enum'u: `"pickup"` (Gel-Al) \| `"dine-in"` (Masaya Servis). Yemeksepeti/Getir/Trendyol bilinçli olarak DAHİL EDİLMEDİ. UI yeri: CartDrawer'ın en üstü. Persist ediliyor. **✅ CANLIDA DOĞRULANDI (bu sohbet) — seçici çalışıyor, state tutuyor.** | Bu sohbet — 2026-07-18 | Kullanıcı: "sepete giren ürünün hangi kanaldan teslim edileceği" + "kendi kuryemizi de öngör" |
| 14 | `â` karakteri render sorunu — kaynak veri doğru UTF-8 idi, encoding hatası değildi. Denenen ama garantisiz düzeltme: `lib/fonts.ts`'e `latin-ext`. **Asıl çözüm: â karakteri tamamen kaldırıldı** ("Benim Kasem", "Özel Kase") — bkz. Karar #16. | Bu sohbet — 2026-07-18 | Teknik teşhis + kullanıcı nihai tercihi |
| 15 | (Karar #2'nin geri alınması) `lib/customizer-data.ts`'teki tüm `name` alanları Türkçeye çevrildi. `id` alanları değiştirilmedi. **✅ CANLIDA DOĞRULANDI.** ⚠️ CUSTOMIZER_SPEC.md §2 senkron değil — ayrı görev (Açık Sorun #29). | Bu sohbet — 2026-07-18 | Kullanıcı: "İngilizce olmayan kelimeler" düzeltilsin |
| 16 | `â` karakteri `menu-data.json` ve `CartDrawer.tsx`'ten kaldırıldı, **✅ CANLIDA DOĞRULANDI.** Hero.tsx'teki CTA ve StepBase.tsx'teki açıklama BİLİNÇLİ OLARAK ERTELENDİ (Açık Sorun #27). | Bu sohbet — 2026-07-18 | Kullanıcı kararı — kapsam dışı bırakıldı |
| 17 | 🟠 **[TB — TASLAK, henüz kod yazılmadı]** Kullanıcı kaydı/giriş yöntemi: telefon numarası + SMS OTP, şifresiz. Guest checkout korunacak. Sadakat programı telefon numarasını kimlik anahtarı olarak kullanacak, puan mekaniği netleşmedi. Gerekçe: global + Türkiye emsal araştırması (McDonald's/Starbucks/Domino's, Yemeksepeti/Getir/Trendyol Yemek). ⚠️ Bilinen risk: "1 numara = 1 hesap" kısıtı hesap kurtarmada sorun yaratıyor (Yemeksepeti şikayetlerinden görüldü) — gün 1'de tasarlanmalı. **OTP sağlayıcısı, auth mimarisi, DB şeması henüz konuşulmadı → Açık Sorun #30.** | Bu sohbet — 2026-07-19 | Kullanıcı sorusu + web araştırması + kullanıcı onayı |
| 18 | **CartDrawer render bug fix:** `Header.tsx`'teki `backdrop-blur` sınıfı, CSS containing-block kuralı gereği `<header>`'ı `position:fixed` elemanları için yeni bir referans noktası yapıyordu — `CartDrawer`'ın `fixed inset-0`'ı viewport yerine Header'ın küçük kutusuna sıkışıyor, içerik Hero'nun üzerine taşıyordu. Çözüm: `CartDrawer` artık `createPortal` ile doğrudan `document.body`'ye render ediliyor (SSR güvenliği için `isMounted` + `useEffect` kontrolüyle). `Header.tsx`'e hiç dokunulmadı — `backdrop-blur` tasarım kararı korundu. **✅ CANLIDA DOĞRULANDI (3 ekran görüntüsü) — çakışma tamamen gitti.** | Bu sohbet — 2026-07-19 | Kullanıcı ekran görüntüsüyle bug bildirdi → kök neden analizi (CartDrawer→Hero→Header sırasıyla dosya incelemesi) → KARAR BİLDİRİMİ → onay → uygulama → canlı doğrulama |

---

## 🚨 SON SESSION ÖZETİ

| Alan | Değer |
|---|---|
| Son Session | 4 (devam) — 2026-07-19, aynı sohbet |
| Son Eylem | CartDrawer/backdrop-blur bug'ı Portal ile düzeltildi, push edildi, 3 ekran görüntüsüyle canlı doğrulandı |
| Blocker | 🔴 customizerCatalog + "Benim Kâsem" hâlâ TEST VERİSİ (Açık Sorun #24). 🟠 Auth mimarisi taslak (Açık Sorun #30). |
| Devam Noktası | Kanal seçimi altyapısı (tip, store, bileşen, CartDrawer) artık CANLIDA doğrulanmış sayılıyor. Kalan: `fonts.ts` (düşük öncelik, etkisi belirsiz) ve şema notunun push durumu teyit edilmeli. `unitCalorie7s` taraması bu sohbette 3 dosyada (SummaryPanel, AddToCartButton, MobileSummaryDrawer) yapıldı — temiz çıktı, ama CartItem[] gezen başka dosya olup olmadığı tam kapanmadı. |

---

## GENEL DURUM

| Alan | Değer |
|---|---|
| Proje | Bowlera — Healthy Bowls |
| Aktif Oturum | Oturum 4 — devam ediyor |
| Repo | `github.com/Sovereign34/Bowlera_site` |
| Menü Veri Kaynağı | ✅ `lib/menu-data.json` — 9 ürün, TEST fiyatlı build-your-own. â düzeltmesi canlıda doğrulandı. |
| Veri Modeli | ✅ `types/index.ts` — `unitCalories` düzeltildi + `FulfillmentChannel` eklendi. **Canlıda dolaylı doğrulandı** (kanal seçici çalışıyor). |
| Customizer Sepet Store | ✅ `store/useCartStore.ts` — `fulfillmentChannel` + `setFulfillmentChannel`. **Canlıda doğrulandı.** |
| Customizer Statik Veri | 🟡 `lib/customizer-data.ts` — isimler Türkçe (canlıda doğrulandı), rakamlar HÂLÂ TEST VERİSİ |
| Sepet UI | ✅ `CartDrawer.tsx` — Portal fix ile **canlıda temiz doğrulandı**, `FulfillmentChannelSelector` çalışıyor |
| Font | 🟡 `lib/fonts.ts`'e `latin-ext` eklendi — push durumu teyit edilmedi, düşük öncelik |
| Header (Sepet) | ✅ Canlıda doğrulandı — sepet ikonu → çekmece açılıyor, artık temiz |
| Görsel/Fotoğraf İçeriği | ⬜ Hâlâ bekleniyor |
| Üçüncü Parti Anahtarları | ⬜ Henüz temin edilmedi |
| Kullanıcı Kaydı/Auth | 🟠 **TASLAK** — yöntem kararı var (Karar #17), mimari yok |
| Sadakat Programı | 🟠 **TASLAK** — telefon numarasına bağlanacak, puan mekaniği netleşmedi |

---

## AÇIK SORUNLAR

| # | Öncelik | Açıklama | Oturum | Referans |
|---|---|---|---|---|
| 4 | 🟡 | Üçüncü parti API anahtarları temin edilmedi | Sonraki Faz | MASTER_PLAN §8 |
| 7 | 🟡 | Allergen gösterimi DESIGN_SYSTEM.md onayı bekliyor | Oturum 2 | DESIGN_SYSTEM.md §2 |
| 10 | 🟡 | ARCHITECTURE.md §2.4 ve DEPENDENCIES.md, 5 adımlı customizer'a göre güncel değil | Oturum 2 | `20260718001123_customizer_5_adim_gecisi.md` |
| 13 | 🟡 | `git log --oneline` ile push'lar hiç teyit edilmedi | Oturum 3 | — |
| 15 | 🟢 | TEST_MATRIX.md, DEPENDENCIES.md, session_log.md bu sohbette de yüklenmedi | Oturum 3→4 | CORE.md §7.1 |
| 16 | 🟡 | `lib/customizer-summary-format.ts` içeriği hâlâ hiç görülmedi — `MobileSummaryDrawer.tsx` içinde formatPrice/formatCalories geçici yerel kopya olarak duruyor, konsolide edilmeli | Oturum 4 | AGENT.md Kural #5 |
| 17 | 🟡 | `customizerCatalog` isimleri Türkçe ama rakamlar TEST VERİSİ | Oturum 4 | `lib/customizer-data.ts` |
| 18 | 🔴 | "Benim Kâsem" fiyatı hâlâ TEST (₺999) — gerçek fiyat bekleniyor | Oturum 4 | `lib/menu-data.json` |
| 20 | 🟢 | `app/menu/customize/[id]/page.tsx` içinde hâlâ 3 onay bekleyen varsayım var (menu-data export şekli, otomatik reset(), notFound() client component davranışı) | Oturum 4 | `app/menu/customize/[id]/page.tsx` |
| 22 | 🟡 | Signature Flavor'ın Main'e göre koşullu içerik göstermesi henüz uygulanmadı (Karar #11) | Oturum 4 | CUSTOMIZER_SPEC.md §2 |
| 24 | 🔴 | `customizer-data.ts` + `menu-data.json`'daki test rakamları PROD öncesi değiştirilmeli (BSC-5) | Oturum 4 | — |
| 25 | 🟢 | **KISMEN KAPANDI.** `unitCalorie7s`→`unitCalories` rename sonrası `SummaryPanel.tsx`, `AddToCartButton.tsx`, `MobileSummaryDrawer.tsx` incelendi — hiçbiri `CartItem` tipini kullanmıyor (customizer taslak state'i üzerinden çalışıyorlar), risk yok. `CartDrawer.tsx` da incelendi ve temiz. Diğer olası `CartItem[]` tüketicileri (checkout sayfası gibi, henüz yazılmadı) ortaya çıktıkça tekrar kontrol edilmeli. | Bu sohbet | `types/index.ts` |
| 26 | 🟡 | Sepette teslimat kanalı seçimi eklendi ama hiçbir yerde zorunlu kılınmıyor — checkout akışı henüz yok | Bu sohbet | `store/useCartStore.ts`, `app/siparis/page.tsx` (henüz yok) |
| 27 | 🟢 | **Bilinçli ertelendi.** Hero.tsx'teki "Kâseni Yarat" CTA'sı ve StepBase.tsx'teki "Kâsenin tabanını seç." hâlâ `â` içeriyor. | Bu sohbet | `components/home/Hero.tsx`, `components/customizer/StepBase.tsx` |
| 28 | 🟢 | Adım başlıkları (Base/Main/Garden/Signature Flavor/Finish) hâlâ İngilizce — netlik bekliyor | Bu sohbet | `components/customizer/Step*.tsx` |
| 29 | 🟢 | `CUSTOMIZER_SPEC.md` §2'deki İngilizce isim listesi `customizer-data.ts` ile senkron değil | Bu sohbet | `CUSTOMIZER_SPEC.md` |
| 30 | 🟠 | Karar #17 (telefon+OTP auth) sadece yön kararı — OTP sağlayıcısı, auth store/session, DB şeması, hesap kurtarma akışı, sadakat puan mekaniği hiç netleşmedi | Bu sohbet | Karar #17 |
> **KAPANDI (bu sohbet):** Karar #18 kapsamında CartDrawer/backdrop-blur görsel bug'ı — canlıda doğrulandı, artık açık sorun değil. #25 kısmen kapandı (3 dosya temiz).

---

## BOWLERA OTURUM DURUMU

| Oturum | İçerik | Durum |
|---|---|---|
| **Oturum 0** | Ajan altyapısı (14 dosya) | ✅ Üretildi — son onay bekliyor |
| **Oturum 1** | Next.js+Tailwind, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| **Oturum 2** | Menü sayfası, filtreleme, MenuCard, statik menü verisi | ✅ Tamamlandı |
| **Oturum 3** | Zustand store + Customizer masaüstü UI bileşenleri | ✅ Büyük ölçüde teyit edildi |
| **Oturum 4** | page.tsx, sepet, kanal seçimi (canlıda doğrulandı), Türkçeleştirme, â düzeltmesi, CartDrawer bugfix (canlıda doğrulandı), auth taslak kararı | 🟡 **Devam ediyor** — veri/fotoğraf blokajı sürüyor |
| **Kontrol Noktası** | Kullanıcı testi (5-10 kişi) | ⬜ Bekliyor |
| **Oturum 5** | Hakkımızda, Şubeler, İletişim, SEO, son kontrol | ⬜ Bekliyor |

**İlerleme özeti:** 5 oturumdan ~3'ü tamam, Oturum 4 yarıda. Sepet + kanal seçimi artık uçtan uca canlıda çalışıyor ve temiz. En kritik blokaj hâlâ kod değil — gerçek mutfak verisi (fiyat/kalori/protein) ve ürün fotoğrafları eksikliği. Auth/sadakat yeni taslak kapsam olarak açık duruyor.

---

## ÜRETİLEN KOD DOSYALARI

| Dosya | Durum | Repo | Deploy |
|---|---|---|---|
| `components/layout/Header.tsx` | ✅ Sepet ikonuna bağlı, bu sohbette dokunulmadı (backdrop-blur bilinçli korundu) | ✅ | ✅ Canlıda doğrulandı |
| `components/cart/CartBadge.tsx` | ✅ Değiştirilmedi | ✅ | ✅ |
| `store/useCustomizerStore.ts` | ✅ `goToStep` fix | ✅ | ⬜ |
| `components/home/Hero.tsx`, `HeroHeadline.tsx` | ✅ Slogan güncel | ✅ | ✅ Canlıda doğrulandı — ⚠️ CTA'daki â bilinçli ertelendi (#27) |
| `components/menu/MenuCard.tsx` | ✅ "Özelleştir" butonu | ✅ | ⬜ |
| `components/customizer/StepBase.tsx` | ✅ | ✅ | ✅ Canlıda doğrulandı — ⚠️ içindeki â bilinçli ertelendi (#27) |
| `components/customizer/StepMain.tsx` | ✅ | ✅ | ⬜ |
| `components/customizer/StepGarden.tsx` | ✅ | ✅ | ⬜ |
| `components/customizer/StepSignatureFlavor.tsx` | ✅ | ✅ | ⬜ |
| `components/customizer/StepFinish.tsx` | ✅ | ✅ | ✅ Canlıda doğrulandı |
| `app/menu/customize/[id]/page.tsx` | ✅ Başlık düzeltildi | ✅ | ✅ Canlıda dolaylı doğrulandı |
| `docs/schema-changes/20260718070000_...md` | ✅ | 🟡 Push durumu teyit edilmedi | — |
| `types/index.ts` | ✅ `unitCalories` + `FulfillmentChannel` | ✅ | ✅ Canlıda dolaylı doğrulandı |
| `store/useCartStore.ts` | ✅ `fulfillmentChannel` state + action | ✅ | ✅ Canlıda doğrulandı |
| `components/cart/FulfillmentChannelSelector.tsx` | ✅ | ✅ | ✅ Canlıda doğrulandı |
| `components/cart/CartDrawer.tsx` | ✅ **Bu sohbette Portal fix'i eklendi** (backdrop-blur bug'ı) | ✅ | ✅ **Canlıda doğrulandı, çakışma yok** |
| `lib/customizer-data.ts` | ✅ Türkçe isimler | ✅ | ✅ Canlıda doğrulandı |
| `lib/menu-data.json` | ✅ â'sız | ✅ | ✅ Canlıda doğrulandı |
| `lib/fonts.ts` | 🟡 `latin-ext`, etkisi belirsiz | 🟡 Push durumu teyit edilmedi | ⬜ |

> Dokunulmayan/ertelenen: `Hero.tsx` CTA metni, `StepBase.tsx` açıklama metni — hâlâ `â` içeriyor (Açık Sorun #27).
> `SummaryPanel.tsx`, `AddToCartButton.tsx`, `MobileSummaryDrawer.tsx` bu sohbette incelendi (unitCalorie7s taraması için) — hiçbiri değiştirilmedi, mevcut halleri temiz.

---

## SIRADAKİ GÖREVLER

| Sıra | Görev | Öncelik | Durum |
|---|---|---|---|
| 1 | `customizerCatalog` + "Benim Kâsem" TEST rakamlarını gerçek mutfak verisiyle değiştir (Açık Sorun #24) | 🔴 | ⬜ |
| 2 | Auth mimarisini netleştir: OTP sağlayıcısı seç, auth store/session tasarla, DB şeması çıkar, hesap kurtarma akışını planla (Açık Sorun #30) | 🟠 | ⬜ |
| 3 | Sadakat puan mekaniğine karar ver (Karar #17'nin eksik kısmı) | 🟠 | ⬜ |
| 4 | Teslimat kanalının checkout'ta zorunlu kılınması (Açık Sorun #26) | 🟡 | ⬜ |
| 5 | `fonts.ts` ve şema notunun push durumunu teyit et | 🟡 | ⬜ |
| 6 | Signature Flavor'ın Main'e göre koşullu içerik göstermesi (Karar #11, Açık Sorun #22) | 🟡 | ⬜ |
| 7 | `page.tsx`'teki 3 onay bekleyen varsayımı teyit et (Açık Sorun #20) | 🟢 | ⬜ |
| 8 | Adım başlıklarının Türkçeleştirilip çevrilmeyeceğine netlik getir (Açık Sorun #28) | 🟢 | ⬜ |
| 9 | Hero.tsx + StepBase.tsx'teki `â` (Açık Sorun #27, bilinçli ertelendi) | 🟢 | ⬜ |
| 10 | VisualPreview altına "Görsel temsilîdir" disclaimer'ı ekle (Karar #10) | 🟡 | ⬜ |
| 11 | CUSTOMIZER_SPEC.md'yi Türkçe isim listesiyle senkronize et (Açık Sorun #29) | 🟢 | ⬜ |
| 12 | `git log --oneline -10` ile push'ları teyit et (Açık Sorun #13) | 🟡 | ⬜ |

---

## 📜 GEÇMİŞ / ARŞİV — Bu Sohbet Detaylı Kayıt (2026-07-19 bloğu)

### CartDrawer / backdrop-blur Bug'ı — Teşhis ve Düzeltme
- Kullanıcı ekran görüntüsüyle sepet çekmecesinde Hero içeriğinin çakıştığını bildirdi.
- Sırayla `CartDrawer.tsx` (yapısal olarak temiz bulundu), `Hero.tsx` (temiz bulundu), `Header.tsx` (kök neden bulundu) incelendi.
- Kök neden: `Header.tsx`'teki `backdrop-blur` sınıfı, CSS'te `backdrop-filter` uyguluyor — bu özellik ata elemanı `position:fixed` çocukları için yeni bir containing block yapıyor. `CartDrawer` `<header>` içine render edildiği için `fixed inset-0`'ı viewport yerine Header'ın küçük kutusuna göre konumlanıyordu, içerik dışarı taşıp Hero'nun üstüne biniyordu.
- KARAR BİLDİRİMİ üretildi: React Portal ile `CartDrawer`'ı `document.body`'ye taşımak, `Header.tsx`'e dokunmamak (backdrop-blur tasarım kararı korunuyor).
- Kullanıcı onayladı, kod yazıldı (`createPortal` + SSR güvenliği için `isMounted` kontrolü), kullanıcı push etti.
- 3 ekran görüntüsüyle canlı doğrulandı: çakışma tamamen gitti, kanal seçici temiz çalışıyor, Base adımı sorunsuz.

### unitCalorie7s Taraması
- `SummaryPanel.tsx`, `AddToCartButton.tsx`, `MobileSummaryDrawer.tsx` istendi, incelendi.
- Sonuç: hiçbiri `CartItem` tipini kullanmıyor — customizer'ın kendi taslak state'inden (`useCustomizerStore.getTotals()`) besleniyorlar. Rename'den etkilenmiyorlar. `CartDrawer.tsx` da ayrıca incelendi, temiz.
- Açık Sorun #25 kısmen kapandı — henüz yazılmamış checkout/sipariş sayfası gibi gelecekteki `CartItem[]` tüketicileri için tekrar kontrol notu bırakıldı.

### Kullanıcı Kaydı / Auth Araştırması (TASLAK)
- Kullanıcı "bu siteye nasıl kayıt yapıyor" sorusunu sordu — yeni kapsam olarak açıldı.
- Netleştirme: checkout için hesap + sadakat/puan programı ikisi de istendi.
- Web araştırması: global (McDonald's, Starbucks, Domino's) ve Türkiye emsalleri (Yemeksepeti, Getir, Trendyol Yemek) hepsi telefon+SMS OTP, şifresiz giriş kullanıyor.
- Bilinen risk not edildi: "1 numara = 1 hesap" kısıtı hesap kurtarmada sorun yaratıyor (Yemeksepeti şikayetleri).
- Kullanıcı onayladı: telefon+OTP, guest checkout korunsun, puan mekaniği henüz netleşmedi.
- Karar #17 (taslak) ve Açık Sorun #30 olarak kayda geçirildi — kod yazılmadı.

---

## 📜 GEÇMİŞ / ARŞİV — Önceki Oturum 4 Bloğu Detaylı Kayıt (bu sohbetten önce)

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

*BOWLERA SESSION_INDEX.md — güncellendi, Session 4 (devam ediyor) — 2026-07-19*
