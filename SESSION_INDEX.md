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
> tek tek dosyayla teyit edilerek gerçek sonuçlarına kavuşturulmuştur (bkz. aşağıdaki
> "KAPANDI (bu sohbet)" bloğu). Kural teyit edildi: tamamlanmış görev silinirken
> MUTLAKA kapanış gerekçesi session_log.md'ye yazılmalı; aksi halde "tamamlandı"
> iddiası doğrulanamaz hale geliyor.

---

## 🎯 CURRENT FOCUS

```
Görev:    Oturum 4 devam ediyor. v2 sıkıştırmasında düşüp geri eklenen 7 açık sorun
          (#4/7/15/16/20/22/34) ve 2 karar (#11/#12) bu sohbette dosya dosya teyit
          edildi (Kural #2 — dosyasız çözüm üretilmedi). Sonuç: 5 madde kapandı
          (#4, #15, #16, #20, #35 — #35 zaten bu turda ayrıca teyit edildi),
          2 madde açık kaldı (#7, #22/Karar#11), 1 madde kısmi açık kaldı (#34),
          1 YENİ somut hata bulundu (MobileSummaryDrawer format fonksiyonu tutarsızlığı).
Blokaj:   🟠 Twilio TR SMS kısıtı (#32) — projenin TEK KALAN büyük darboğazı, kullanıcı
          ödemeyi henüz yapmadığı için bilinçli parklı. (#4 bu sohbette #32'ye
          birleştirilip ayrı madde olarak kapatıldı.)
Sıradaki: (1) Twilio kararı (#32), (2) DESIGN_SYSTEM.md'ye allerjen gösterim kuralı
          ekle (#7), (3) Signature Flavor'ın Main'e göre koşullu içeriği uygula
          (#22/Karar#11), (4) MobileSummaryDrawer'ın yerel format fonksiyonlarını
          lib/customizer-summary-format.ts ile konsolide et (YENİ), (5) VisualPreview
          çağıranlarının tam repo taraması ile #34'ü kesin kapat, (6) ARCHITECTURE.md
          §2.4'ü 5 adıma güncelle (#10), (7) ProfileForm Tailwind teyidi (#38).
```

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI (özet — hâlâ etkili olanlar + yeniden teyit edilmesi gerekenler)

| # | Karar | Durum |
|---|---|---|
| 1 | Customizer 5 adım: Base → Main → Garden → Signature Flavor → Finish | ✅ Uygulandı |
| 3-4 | Garden: ilk 4 ücretsiz + avokado her zaman ücretli / Finish: ilk 1 ücretsiz | ✅ Uygulandı |
| 5 | "Make it Yours" → Finish'e entegre, "Double Main" → `mainPortion` yeniden kullanır | ✅ Uygulandı |
| 6 | Slogan: "Sağlıklı Beslen, Sağlıklı Yaşa, Gücünü Hisset" | ✅ |
| 11 | Nohut/Meksika fasulyesi gibi Main'lerde Signature Flavor adımı atlanmıyor, içeriği/etiketi değişiyor | ❌ **Bu sohbette teyit edildi: hâlâ uygulanmamış.** `CUSTOMIZER_SPEC.md` §2'deki Main listesinde böyle bir koşullu davranış tanımlı değil. Aynı konu: Açık Sorun #22. |
| 12 | "Kâseni Yarat" sadece "Benim Kâsem" (`build-your-own-kasem`) ürününde | ⚠️ Bağlayıcı kapsam kuralı, bu sohbette ayrıca test edilmedi — hâlâ geçerli varsayılıyor |
| 13 | `FulfillmentChannel`: `"pickup"` \| `"dine-in"` (delivery yok), sepet/oturum seviyesinde tek alan | ✅ Canlıda doğrulandı |
| 14-16 | `â` karakteri kaldırıldı (menu-data.json, CartDrawer). Hero.tsx/StepBase.tsx bilinçli ertelendi (#27) | ✅ Bu sohbette `menu-data.json` içeriği tekrar görülüp `â` yokluğu doğrulandı |
| 15 | Customizer malzeme isimleri Türkçeye çevrildi (id'ler değişmedi) | ✅ Canlıda doğrulandı |
| 18 | CartDrawer portal fix (`createPortal` → `document.body`, backdrop-blur containing-block bug'ı için) | ✅ Canlıda doğrulandı |
| 19→20 | Auth: Twilio Verify + Auth.js JWT. DB: Neon Postgres (Vercel Marketplace), `users` tablosu (`phone`,`address`,`displayName`,`loyaltyPoints`,`verifiedAt`) | ✅ Kurulum tamam, build yeşil |
| 20 | 🆕 AuthenticatedUser tipi `address` alanıyla genişletildi, DB'de kalıcı saklanıyor | ✅ `types/index.ts`'te bu sohbette doğrulandı |
| 21-22 | Auth kod (route'lar, `auth.ts`, DB katmanı) + görünür giriş UI (`/giris`) | ✅ Kod tamam, `/giris` canlı doğrulandı; OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor |
| 23 | Adres/profil modeli: adres SADECE profil/sadakat verisi, checkout'u bloklamaz, `/hesap`'ta opsiyonel toplanır | ✅ Kod üretildi VE repo varlığı (route.ts, ProfileForm.tsx, page.tsx, rate-limit.ts — 4/4) doğrulandı (#41 kapandı) |
| 🆕 | CategoryNav sekmeleri `BowlItem.category` enum'unu genişletmez — "vegan"/"sicak-tahil" sekmeleri `tags[]` üzerinden sanal filtrelenir (şema değişikliği yok) | ✅ Bu sohbette `lib/menu-filters.ts`'te kod-içi gerekçesiyle doğrulandı (#35 kapandı) |

*(Tam gerekçe/tarih dökümü için: `session_log.md`.)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 7 | 🟡 | Allerjen gösterimi DESIGN_SYSTEM.md onayı bekliyor. **Bu sohbette dosya baştan sona okunarak kesinleştirildi: alerjen kelimesi hiç geçmiyor, Self-Check listesinde de yok. Veri modeli (menu-data.json, types/index.ts) alerjen bilgisini tam destekliyor — eksik olan sadece UI gösterim kuralı.** | `DESIGN_SYSTEM.md` (yeni bölüm eklenmeli) |
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor — 5 adıma hiç güncellenmedi (v1.4'te bilinçli kapsam dışı bırakıldı) | `ARCHITECTURE.md` §2.4, `CUSTOMIZER_SPEC.md` §3.1 |
| 22 | 🟡 | Signature Flavor'ın Main'e göre koşullu içerik göstermesi henüz uygulanmadı (Karar #11 ile aynı konu). **Bu sohbette CUSTOMIZER_SPEC.md §2 üzerinden kesin doğrulandı: hâlâ uygulanmamış.** | `CUSTOMIZER_SPEC.md` §2 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi | `lib/customizer-data.ts`, `lib/menu-data.json` |
| 27 | 🟢 | Hero.tsx CTA'sı ve StepBase.tsx açıklaması hâlâ `â` içeriyor (bilinçli ertelendi) | `components/home/Hero.tsx`, `StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce; `CUSTOMIZER_SPEC.md` §2 senkron değil | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — hem auth hem `/hesap` akışını canlıda test edilemez kılıyor. Çözüm: ücretli plan veya Netgsm/İleti Merkezi. Kullanıcı kararıyla bilinçli PARKLANDI. (#4 bu sohbette buraya birleştirildi.) | Twilio Console |
| 34 | 🟢 | `VisualPreview.tsx`'in `className` davranışı — **bu sohbette kısmi teyit edildi:** bilinen iki çağıran (`page.tsx`, `MobileSummaryDrawer.tsx`) className geçirmiyor, temiz. Repoda başka çağıran olup olmadığı taranmadı — tam kapanış için grep gerekiyor. | `components/customizer/VisualPreview.tsx` |
| 38 | 🟢 | `ProfileForm.tsx` Tailwind sınıfları (`bg-olive-600` vb.) DESIGN_SYSTEM.md ile teyit edilmedi | `components/account/ProfileForm.tsx` |
| 39 | 🟠 | `/hesap` akışı Twilio kısıtı yüzünden canlıda hiç fonksiyonel test edilemedi | `app/hesap/page.tsx` |
| 43 | 🆕 🟡 | `MobileSummaryDrawer.tsx`'in yerel `formatPrice`/`formatCalories` kopyası, gerçek `lib/customizer-summary-format.ts`'ten davranışsal olarak farklı: yerel kopya `value > 0` kontrolü yapıyor, gerçek modül `hasSelection` bayrağına bakıyor. Sonuç: seçili ama 0 TL'lik bir öğede (örn. ücretsiz Garden malzemesi) yerel kopya yanlışlıkla `"—"` gösterebilir, doğrusu `"0"` olmalı. Konsolide edilmeli — dosyanın kendi yorumunda (satır 7-9) zaten bu ihtiyaç not edilmiş, bu sohbette somut davranış farkı doğrulandı. | `components/customizer/MobileSummaryDrawer.tsx`, `lib/customizer-summary-format.ts` |

> **KAPANDI (bu sohbet):**
> - **#4** — Üçüncü parti API anahtarları sorunu #32 (Twilio) ile aynı konu, ayrı madde olarak gerekliliği kalmadı. #32'ye birleştirildi.
> - **#15** — TEST_MATRIX.md/DEPENDENCIES.md prosedürel hatırlatması, düşük risk, kod etkisi yok.
> - **#16** — `lib/customizer-summary-format.ts` implementasyonu görüldü, teste birebir uyuyor (`hasAnySelection`, `formatMetric`, `formatPrice`). Modül var ve doğru tasarlanmış. (Bu teyit sırasında #43 yeni madde olarak bulundu — yukarı bakınız.)
> - **#20** — 3/3 varsayım kapandı: ① `menu-data.json` içeriği görüldü, `BowlItem[]` şemasına yapısal olarak uyuyor (runtime doğrulaması hâlâ yok ama bu ayrı, bilinen bir nokta). ② `addToCart()` sonrası `reset()` çağrıldığı kod üzerinden zaten doğrulanmıştı. ③ `notFound()` Client Component içinde kullanımı Next.js'te desteklenen bir pattern, kod doğru.
> - **#35** — `lib/menu-filters.ts` görüldü: nav'daki 4 kategori ile `BowlItem.category`'nin 3'lü enum'ı arasındaki fark bir hata değil, kod-içi yorumla açıkça belgelenmiş bilinçli bir tasarım kararı (`vegan`/`sicak-tahil` sekmeleri `tags[]` üzerinden filtreleniyor). Test + implementasyon + gerekçe üçü tutarlı.
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
| 4 (devam) | 2026-07-18 → 07-21 (6 bölüm + arşiv düzeltme turu + teyit turu) | Sepet/kanal seçimi, Türkçeleştirme, â düzeltmesi, CartDrawer bugfix, auth mimarisi+kod+DB+UI, adres/profil (#23), test triyajı, menü animasyonu, ARCHITECTURE.md v1.3→v1.4, rate-limit üretimi, repo tutarsızlığı keşfi ve kapanışı (#42 kapandı), v2 sıkıştırma turunda düşen 7 açık sorun + 2 kararın geri bulunması VE dosya-dosya teyidi (#4/#15/#16/#20/#35 kapandı, #7/#22 açık teyit edildi, #34 kısmi, #43 yeni bulundu) | 🟡 Devam ediyor — Twilio (#32) tek darboğaz; #7/#22/#34/#43 kalan işler |

*(Tam turn-by-turn detay: `session_log.md`.)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — adres/profil dosyaları (4/4) + checkout dosyaları (5/5) + customizer-summary-format + menu-filters tek tek doğrulandı |
| Test Suite | 🟢 `Header.test.tsx` 3/3, `customizer-summary-format.test.ts`, `menu-filters.test.ts` bu sohbette incelendi — implementasyonlarla tutarlı. Genel `npm test` bu aralıkta tekrar çalıştırılmadı — bir sonraki tam çalıştırmada teyit edilmeli. |
| Auth | 🟢 Kod tamam, `/giris` canlı doğrulandı. 🟠 OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor (#32) |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı — kanal seçimi zorunlu |
| Veritabanı | 🟢 Neon Postgres çalışıyor |
| ARCHITECTURE.md | 🟢 v1.4 güncel ve repoda doğrulandı. §2.4 (5 adım, #10) ve kategori filtreleme (#35, artık kapalı) bilinçli/teyitli kapsam durumları |
| Menü Filtreleme | 🟢 `lib/menu-filters.ts` — kategori/alerjen/diyet filtreleri kod+test ile doğrulandı (#35 kapandı) |
| Customizer Özet Formatlama | 🟢 `lib/customizer-summary-format.ts` — kod+test ile doğrulandı (#16 kapandı), ama tüketici tarafında (`MobileSummaryDrawer.tsx`) bir tutarsızlık bulundu (#43) |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | Twilio kararı: ücretli plan veya yerel sağlayıcı — TEK büyük darboğaz (#32, parklandı) | 🟠 |
| 2 | 🆕 DESIGN_SYSTEM.md'ye allerjen gösterim kuralı ekle (#7) | 🟡 |
| 3 | 🆕 Signature Flavor'ın Main'e göre koşullu içeriğini uygula (#22/Karar#11) | 🟡 |
| 4 | 🆕 MobileSummaryDrawer'ın yerel format fonksiyonlarını gerçek modülle konsolide et (#43) | 🟡 |
| 5 | VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat | 🟢 |
| 6 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a güncelle (#10) | 🟡 |
| 7 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 8 | ProfileForm Tailwind sınıflarını DESIGN_SYSTEM.md ile teyit et (#38) | 🟢 |
| 9 | Genel `npm test` çalıştırıp güncel geçen/kalan sayıyı teyit et | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v5. Arşiv `session_log.md`'ye taşınmayı bekliyor (bu turun
detayları henüz taşınmadı — bir sonraki kapanışta mutlaka taşınmalı, aksi halde v2
ihlaliyle aynı hata tekrarlanır). v2 sıkıştırma turunda düşen 7 açık sorun + 2 karardan
5'i bu sohbette teyitle kapandı (#4,#15,#16,#20,#35), 2'si açık teyit edildi (#7,#22),
1'i kısmi kaldı (#34), 1 yeni madde bulundu (#43). Güncellenme: 2026-07-21.*
