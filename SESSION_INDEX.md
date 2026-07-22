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

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 4 devam ediyor. Karar #11 / Açık Sorun #22 TAM KAPANDI. "Bitkisel
          Protein" Main'i (Soslu Nohut / Meksika Fasulyesi alt-varyantı) uçtan uca
          uygulandı: types/index.ts (CustomizerMainItem, mainVariant), customizer-data.ts
          (plant-based-protein + variants + compatibleFlavorIds), useCustomizerStore.ts
          (mainVariant state, selectMainVariant, nextStep otomatik atama, getAvailableFlavors),
          customizer-pricing.ts (getTotals variant-aware — resolveMainItem), StepMain.tsx
          (inline varyant genişlemesi UI'ı). CUSTOMIZER_SPEC.md v1.2 zaten güncellenmişti.
          Kullanıcı GitHub'a yanlışlıkla ayrı bir branch'e (Sovereign34-patch-1) push etmiş,
          "Compare & pull request" ile main'e merge etti. Vercel Production'da 4 deploy de
          Ready: merge, getTotals refactor, useCustomizerStore update, StepMain enhance.
          Ekran görüntüleriyle main branch'in güncel dosyaları (types/store/lib/components,
          1 saat önce) taşıdığı ve canlı deploy'un Ready olduğu TEYİT EDİLDİ.
Blokaj:   🟠 Twilio TR SMS kısıtı (#32) — hâlâ TEK büyük darboğaz, bilinçli parklı.
Sıradaki: (1) Twilio kararı (#32), (2) MobileSummaryDrawer'ın yerel format
          fonksiyonlarını lib/customizer-summary-format.ts ile konsolide et (#43),
          (3) AGENT.md SELF-CHECK/YASAK LİSTE'ye alerjen satırını ekle (#44),
          (4) VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat,
          (5) ARCHITECTURE.md §2.4'ü 5 adıma güncelle (#10, artık Bitkisel Protein
          alt-varyantını da yansıtmalı), (6) ProfileForm Tailwind teyidi (#38),
          (7) CUSTOMIZER_SPEC.md'ye StepMain.tsx'te bulunan küçük netleştirmeyi işle:
          selectMain artık mainVariant'ı SADECE main id değişince sıfırlıyor (bkz.
          Karar #11 alt notu) — spec'te bu ayrım henüz açıkça yazılı değil (#49, yeni,
          düşük öncelik, dokümantasyon senkronu).
```

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI (özet — hâlâ etkili olanlar + yeniden teyit edilmesi gerekenler)

| # | Karar | Durum |
|---|---|---|
| 1 | Customizer 5 adım: Base → Main → Garden → Signature Flavor → Finish | ✅ Uygulandı |
| 3-4 | Garden: ilk 4 ücretsiz + avokado her zaman ücretli / Finish: ilk 1 ücretsiz | ✅ Uygulandı |
| 5 | "Make it Yours" → Finish'e entegre, "Double Main" → `mainPortion` yeniden kullanır | ✅ Uygulandı |
| 6 | Slogan: "Sağlıklı Beslen, Sağlıklı Yaşa, Gücünü Hisset" | ✅ |
| 11 | **[TAM KAPANDI — 2026-07-22]** "Bitkisel Protein" tek Main kartı + 2 alt-varyant (Soslu Nohut, Meksika Fasulyesi), inline genişleme UX'i, Signature Flavor bu Main için 3 flavor'a filtrelenir (Mediterranean Herb, Spicy Harissa, Lemon Garlic), varyant seçilmezse `nextStep()` ilk varyantı sessizce atar. `selectMain` SADECE main id değişince `mainVariant`'ı sıfırlar (Double Main ile çakışmayı önlemek için bulunan edge case düzeltmesi). `getTotals()` artık `resolveMainItem()` ile variant-aware (önceden bug'lıydı — Meksika Fasulyesi seçiliyken bile sabit 230kcal/10g dönüyordu, düzeltildi). 6 dosya uçtan uca güncellendi ve canlıda (Vercel Production) doğrulandı. | ✅ Uygulandı VE canlıda doğrulandı |
| 12 | "Kâseni Yarat" sadece "Benim Kâsem" (`build-your-own-kasem`) ürününde | ⚠️ Bağlayıcı kapsam kuralı, ayrıca test edilmedi — hâlâ geçerli varsayılıyor |
| 13 | `FulfillmentChannel`: `"pickup"` \| `"dine-in"` (delivery yok), sepet/oturum seviyesinde tek alan | ✅ Canlıda doğrulandı |
| 14-16 | `â` karakteri kaldırıldı (menu-data.json, CartDrawer). Hero.tsx/StepBase.tsx bilinçli ertelendi (#27) | ✅ `menu-data.json` içeriği görülüp `â` yokluğu doğrulandı |
| 15 | Customizer malzeme isimleri Türkçeye çevrildi (id'ler değişmedi) | ✅ Canlıda doğrulandı |
| 18 | CartDrawer portal fix (`createPortal` → `document.body`, backdrop-blur containing-block bug'ı için) | ✅ Canlıda doğrulandı |
| 19→20 | Auth: Twilio Verify + Auth.js JWT. DB: Neon Postgres (Vercel Marketplace), `users` tablosu (`phone`,`address`,`displayName`,`loyaltyPoints`,`verifiedAt`) | ✅ Kurulum tamam, build yeşil |
| 20 | AuthenticatedUser tipi `address` alanıyla genişletildi, DB'de kalıcı saklanıyor | ✅ `types/index.ts`'te doğrulandı |
| 21-22 | Auth kod (route'lar, `auth.ts`, DB katmanı) + görünür giriş UI (`/giris`) | ✅ Kod tamam, `/giris` canlı doğrulandı; OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor |
| 23 | Adres/profil modeli: adres SADECE profil/sadakat verisi, checkout'u bloklamaz, `/hesap`'ta opsiyonel toplanır | ✅ Kod üretildi VE repo varlığı (route.ts, ProfileForm.tsx, page.tsx, rate-limit.ts — 4/4) doğrulandı (#41 kapandı) |
| 🆕 | CategoryNav sekmeleri `BowlItem.category` enum'unu genişletmez — "vegan"/"sicak-tahil" sekmeleri `tags[]` üzerinden sanal filtrelenir (şema değişikliği yok) | ✅ `lib/menu-filters.ts`'te kod-içi gerekçesiyle doğrulandı (#35 kapandı) |
| 🆕 | Alerjen gösterimi: kalori/protein ile aynı zorunluluk statüsü, gizlenemez/opsiyonel yapılamaz; ayrı bir alarm rengi/logo degrade yok — Primary Olive ikon + imza yaprak/zeytin motif stili | ✅ `DESIGN_SYSTEM.md` §7 (7.0-7.5) eklendi ve dosya üzerinden doğrulandı (#7 kapandı) |

*(Tam gerekçe/tarih dökümü için: `session_log.md`.)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor — 5 adıma hiç güncellenmedi. Artık Bitkisel Protein alt-varyant mekanizmasını da (Karar #11) yansıtmalı. | `ARCHITECTURE.md` §2.4, `CUSTOMIZER_SPEC.md` §3.1 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi. `plant-based-protein.variants[]` içindeki değerler de bu kapsama dahil. | `lib/customizer-data.ts`, `lib/menu-data.json` |
| 27 | 🟢 | Hero.tsx CTA'sı ve StepBase.tsx açıklaması hâlâ `â` içeriyor (bilinçli ertelendi) | `components/home/Hero.tsx`, `StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce; `CUSTOMIZER_SPEC.md` §2 senkron değil | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — hem auth hem `/hesap` akışını canlıda test edilemez kılıyor. Çözüm: ücretli plan veya Netgsm/İleti Merkezi. Kullanıcı kararıyla bilinçli PARKLANDI. | Twilio Console |
| 34 | 🟢 | `VisualPreview.tsx`'in `className` davranışı — kısmi teyit edildi: bilinen iki çağıran (`page.tsx`, `MobileSummaryDrawer.tsx`) className geçirmiyor, temiz. Repoda başka çağıran olup olmadığı taranmadı — tam kapanış için grep gerekiyor. | `components/customizer/VisualPreview.tsx` |
| 38 | 🟢 | `ProfileForm.tsx` Tailwind sınıfları (`bg-olive-600` vb.) DESIGN_SYSTEM.md ile teyit edilmedi | `components/account/ProfileForm.tsx` |
| 39 | 🟠 | `/hesap` akışı Twilio kısıtı yüzünden canlıda hiç fonksiyonel test edilemedi | `app/hesap/page.tsx` |
| 43 | 🟡 | `MobileSummaryDrawer.tsx`'in yerel `formatPrice`/`formatCalories` kopyası, gerçek `lib/customizer-summary-format.ts`'ten davranışsal olarak farklı: yerel kopya `value > 0` kontrolü yapıyor, gerçek modül `hasSelection` bayrağına bakıyor. Sonuç: seçili ama 0 TL'lik bir öğede (örn. ücretsiz Garden malzemesi) yerel kopya yanlışlıkla `"—"` gösterebilir, doğrusu `"0"` olmalı. Konsolide edilmeli. | `components/customizer/MobileSummaryDrawer.tsx`, `lib/customizer-summary-format.ts` |
| 44 | 🟢 | DESIGN_SYSTEM.md §7 (Alerjen Gösterim Sistemi) eklendi ama AGENT.md'nin genel SELF-CHECK/YASAK LİSTE tablosuna buna karşılık gelen satır henüz eklenmedi — ayrı onay gerekiyor (Kural #5) | `AGENT.md` (SELF-CHECK/YASAK LİSTE tablosu) |
| 49 | 🆕 🟢 | `useCustomizerStore.ts`'teki `selectMain`'in "sadece main id değişince mainVariant sıfırlanır" davranışı (Double Main edge case düzeltmesi, bkz. Karar #11) `CUSTOMIZER_SPEC.md` §3.4'e henüz açıkça yazılmadı — kod ile spec arasında küçük bir dokümantasyon senkron eksikliği, davranışsal risk yok. | `CUSTOMIZER_SPEC.md` §3.4 |

> **KAPANDI (bu sohbet, önceki turlar):**
> - **#4** — Üçüncü parti API anahtarları sorunu #32 (Twilio) ile aynı konu, #32'ye birleştirildi.
> - **#15** — TEST_MATRIX.md/DEPENDENCIES.md prosedürel hatırlatması, düşük risk, kod etkisi yok.
> - **#16** — `lib/customizer-summary-format.ts` implementasyonu görüldü, teste birebir uyuyor (`hasAnySelection`, `formatMetric`, `formatPrice`). (Bu teyit sırasında #43 yeni madde olarak bulundu.)
> - **#20** — 3/3 varsayım kapandı (menu-data.json şema uyumu, addToCart()→reset() zinciri, notFound() Client Component kullanımı).
> - **#35** — `lib/menu-filters.ts` görüldü: nav'daki 4 kategori ile `BowlItem.category`'nin 3'lü enum'ı arasındaki fark bilinçli, kod-içi yorumla belgelenmiş bir tasarım kararı.
>
> **KAPANDI (bu sohbet, önceki tur — 2026-07-21):**
> - **#7** — `DESIGN_SYSTEM.md` §7 "Alerjen Gösterim Sistemi" eklendiği dosya üzerinden doğrulandı, hepsi tam ve tutarlı. Bu kapanış AGENT.md tarafında bir takip maddesi doğurdu → **#44**.
>
> **KAPANDI (bu sohbet, bu tur — 2026-07-22):**
> - **#22 / Karar #11** — "Bitkisel Protein" alt-varyant mekanizması uçtan uca uygulandı:
>   `types/index.ts` (CustomizerMainItem, mainVariant alanı), `customizer-data.ts`
>   (plant-based-protein main'i, variants + compatibleFlavorIds), `useCustomizerStore.ts`
>   (mainVariant state, selectMainVariant, nextStep otomatik atama, getAvailableFlavors),
>   `customizer-pricing.ts` (getTotals variant-aware düzeltmesi — ÖNCEDEN BUG'LIYDI,
>   Meksika Fasulyesi seçiliyken sabit 230kcal/10g dönüyordu), `StepMain.tsx` (inline
>   varyant genişlemesi UI'ı). Süreçte 2 self-correction yapıldı: (1) selectMain'in
>   mainVariant'ı her çağrıda sıfırlaması hatası (Double Main ile çakışma), (2) getTotals'ın
>   variant-aware olmaması. İkisi de StepMain.tsx/customizer-pricing.ts paylaşılınca
>   tespit edilip düzeltildi. Kullanıcı GitHub'a yanlış branch'e push etmiş, PR ile main'e
>   merge etti — ekran görüntüleriyle main branch güncel dosyaları taşıdığı ve Vercel
>   Production'da 4 deploy'un da Ready olduğu TEYİT EDİLDİ. Küçük bir dokümantasyon
>   senkron eksikliği #49 olarak yeni açıldı (davranışsal risk yok, düşük öncelik).
>
> Detaylı gerekçe/dosya alıntıları bu sohbetin geçmişinde; bir sonraki turda `session_log.md`'ye taşınmalı (henüz taşınmadı — Kural gereği bu not bırakıldı, aksi halde önceki v2 ihlaliyle aynı hataya düşülür).

---

## SESSION ÖZET (son 5)

| Session | Tarih | Ana içerik | Durum |
|---|---|---|---|
| 0 | — | Ajan altyapısı (14 dosya) | ✅ Tamamlandı |
| 1 | 2026-07-1x | Next.js+Tailwind kurulum, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| 2 | 2026-07-18 | Menü sayfası, filtreleme, MenuCard, statik veri, CategoryNav+FilterPanel, customizer 4→5 adım kararı | ✅ Tamamlandı |
| 3 | 2026-07-18 | Zustand store + pricing + customizer data, masaüstü UI bileşenleri (kesintiye uğradı) | ✅ Büyük ölçüde tamam |
| 4 (devam) | 2026-07-18 → 07-22 (9 bölüm + arşiv düzeltme turu + teyit turu + DESIGN_SYSTEM §7 turu + Bitkisel Protein turu) | Sepet/kanal seçimi, Türkçeleştirme, â düzeltmesi, CartDrawer bugfix, auth mimarisi+kod+DB+UI, adres/profil (#23), test triyajı, menü animasyonu, ARCHITECTURE.md v1.3→v1.4, rate-limit üretimi, repo tutarsızlığı keşfi ve kapanışı (#42 kapandı), v2 sıkıştırma turunda düşen 7 açık sorun + 2 kararın geri bulunması (#4/#15/#16/#20/#35 kapandı), DESIGN_SYSTEM.md §7 Alerjen Gösterim Sistemi eklendi (#7 kapandı, #44 yeni), Karar #11/#22 uçtan uca uygulandı ve canlıda doğrulandı (types/store/pricing/component, 2 self-correction, GitHub yanlış branch olayı çözüldü, #22 TAM kapandı, #49 yeni) | 🟡 Devam ediyor — Twilio (#32) şu an TEK darboğaz |

*(Tam turn-by-turn detay: `session_log.md`.)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel (types/store/lib/components, ~1 saat önce), Vercel Production'da 4/4 deploy Ready |
| Test Suite | 🟢 `Header.test.tsx` 3/3, `customizer-summary-format.test.ts`, `menu-filters.test.ts` incelendi — implementasyonlarla tutarlı. Genel `npm test` bu aralıkta tekrar çalıştırılmadı. 🟡 Bitkisel Protein için henüz test yok — `useCustomizerStore.test.ts`/`customizer-pricing.test.ts` paylaşılmadı (Test Koşulu bu sohbette önerildi, dosyaya işlenmedi). |
| Auth | 🟢 Kod tamam, `/giris` canlı doğrulandı. 🟠 OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor (#32) |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı — kanal seçimi zorunlu |
| Veritabanı | 🟢 Neon Postgres çalışıyor |
| ARCHITECTURE.md | 🟢 v1.4 güncel ve repoda doğrulandı. §2.4 (5 adım + Bitkisel Protein, #10) bilinçli/teyitli kapsam dışı durum |
| Menü Filtreleme | 🟢 `lib/menu-filters.ts` — kategori/alerjen/diyet filtreleri kod+test ile doğrulandı (#35 kapandı) |
| Customizer Özet Formatlama | 🟢 `lib/customizer-summary-format.ts` — kod+test ile doğrulandı (#16 kapandı), ama tüketici tarafında (`MobileSummaryDrawer.tsx`) bir tutarsızlık bulundu (#43) |
| Alerjen Gösterim Sistemi | 🟢 `DESIGN_SYSTEM.md` §7 tasarım kuralı olarak tanımlandı ve doğrulandı (#7 kapandı). 🟡 UI implementasyonu henüz yazılmadı. 🟢 AGENT.md Self-Check satırı ayrı iş olarak beklemede (#44) |
| Bitkisel Protein (Main alt-varyant) | ✅ Karar #11/#22 TAM kapandı — types/store/pricing/component uçtan uca uygulandı, main branch'te ve Vercel Production'da canlı doğrulandı. 🟢 #49 (küçük spec senkron notu) beklemede |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | Twilio kararı: ücretli plan veya yerel sağlayıcı — TEK büyük darboğaz (#32, parklandı) | 🟠 |
| 2 | MobileSummaryDrawer'ın yerel format fonksiyonlarını gerçek modülle konsolide et (#43) | 🟡 |
| 3 | DESIGN_SYSTEM.md §7'ye göre alerjen gösterimini MenuCard/Customizer/SummaryPanel'de fiilen uygula | 🟡 |
| 4 | AGENT.md SELF-CHECK/YASAK LİSTE tablosuna alerjen satırını ekle — ayrı onay gerekir (#44) | 🟢 |
| 5 | VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat | 🟢 |
| 6 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a (Bitkisel Protein dahil) güncelle (#10) | 🟡 |
| 7 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 8 | ProfileForm Tailwind sınıflarını DESIGN_SYSTEM.md ile teyit et (#38) | 🟢 |
| 9 | CUSTOMIZER_SPEC.md §3.4'e selectMain'in mainVariant sıfırlama davranışını yaz (#49) | 🟢 |
| 10 | Genel `npm test` çalıştırıp güncel geçen/kalan sayıyı teyit et, Bitkisel Protein testlerini ekle | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v8. Arşiv `session_log.md`'ye taşınmayı bekliyor (bu turun
detayları henüz taşınmadı — bir sonraki kapanışta mutlaka taşınmalı, aksi halde v2
ihlaliyle aynı hata tekrarlanır). v7'de Karar #11/#22 daraltılmıştı (spec+data hazır,
implementasyon bekliyor); bu turda types/store/pricing/component tamamlanarak #22 TAM
kapandı ve canlıda (Vercel Production, main branch) doğrulandı. Süreçte 2 self-correction
yapıldı (selectMain mainVariant sıfırlama hatası, getTotals variant-aware olmama bug'ı) —
ikisi de kod incelemesiyle proaktif tespit edildi. Kalan açık sorunlar: #10, #24, #27,
#28/29, #32, #34, #38, #39, #43, #44, #49.
Güncellenme: 2026-07-22.*
