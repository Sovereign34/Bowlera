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
Görev (2026-08-01, yeni tur):    VisualPreview.tsx mimarisi denetlendi — kritik bir
          mimari çelişki bulundu (#52, yeni). Kod, `/public/images/layers/` altında
          her malzeme için gerçek görsel dosyası (`base-jasmine-rice.webp` gibi)
          bekliyor, ama bu klasör TAMAMEN BOŞ — hiçbir katman görseli yok. Bu,
          PHOTOGRAPHY_GUIDE.md §8'deki "VisualPreview CSS/SVG katman mantığıyla
          çalışıyor, gerçek fotoğraf gerekmez" notuyla doğrudan çelişiyor. Şu an
          müşteri customizer'da herhangi bir malzeme seçse bile önizleme boş krem
          renkli daire olarak kalıyor.
          **Karar (kullanıcı onayı ile):** Fotoğraf katmanlama yerine markaya uygun
          (Warm Cream/Espresso Brown/Primary Olive) vektörel ikon seti kullanılacak —
          global rakip modeli: Chipotle (metin-only, görsel yok) / Cava-Sweetgreen
          (düz ikon seti). Kod tarafında DEĞİŞİKLİK GEREKMİYOR — VisualPreview.tsx
          zaten dosya yolunu id'den esnek türetiyor, sadece ikon dosyaları
          `/public/images/layers/` altına eklenecek (üretici: kullanıcı bir
          tasarımcı bulacak ya da Claude AI ile taslak üretecek — netleşmedi).
          Ayrıca: dosyanın en üstündeki "GEÇMİŞ İHLAL KAYDI" notu (v2 sıkıştırma
          olayı) bu turda tekrar teyit edildi — kullanıcıya SESSION_INDEX.md'nin
          (bu dosya) doğru/güncel kaynak olduğu, SESSION_INDEX_v2.md'nin ise
          kayıttaki ihlalin ta kendisi olduğu için kullanılmaması gerektiği
          açıkça bildirildi.

Önceki tur (2026-07-22):
          Oturum 4 devam ediyor. Bu turda MASTER_PLAN.md ve ROADMAP.md — kod ile
          tutarlılık denetiminden geçirildi ve güncellendi:
          - MASTER_PLAN.md v2.1 → v2.2: Sitemap'e /giris ve /hesap eklendi (Auth/Hesap
            alt sistemi önceki sürümde hiç yoktu). Sipariş kanalı isimlendirmesi kodla
            senkronlandı ("Paket Servis/Gel Al" → "Gel Al (pickup)/Masada (dine-in)").
            Main listesi detayına BİLİNÇLİ dokunulmadı — CUSTOMIZER_SPEC.md zaten "tam
            kontrat" olarak referans veriliyor.
          - ROADMAP.md v1.1 → v1.3: Oturum 3 satırları bu sohbette bizzat görülen
            dosyalarla (useCustomizerStore.ts, customizer-pricing.ts,
            customizer-summary-format.ts) teyit edilip 🟢'ye güncellendi (AddToCartButton.tsx
            hâlâ görülmedi, 🟡 kaldı). Oturum 4'e durum sütunu eklendi. YENİ: "Oturum 4.5 —
            Auth/Hesap Sistemi" formal tablo olarak eklendi (kabul kriterleriyle) — Twilio
            SMS kısıtı (#32) buradaki tek açık blokaj olarak işaretlendi.
          Denetimde bulunan gerçek boşluklar kapatıldı: (1) Auth/DB/Hesap sistemi hiçbir
          üst-seviye plan belgesinde yoktu, artık MASTER_PLAN + ROADMAP'te var. (2) Bitkisel
          Protein Main listesi MASTER_PLAN'a bilinçli olarak taşınmadı (spec'e referans
          korundu, çoğaltma önlendi).
Blokaj:   🟠 Twilio TR SMS kısıtı (#32) — hâlâ TEK büyük darboğaz, artık hem SESSION_INDEX
          hem ROADMAP'te (Oturum 4.5) açıkça blokaj olarak işaretli.
Sıradaki: Kalan açık sorunların hepsi 🟡/🟢 düşük öncelikli:
          (1) ARCHITECTURE.md §2.4'ü 5 adıma (+ Bitkisel Protein) güncelle (#10),
          (2) customizerCatalog + "Benim Kâsem" fiyatı — fotoğraf çekimine bağlı (#24),
          (3) Hero.tsx/StepBase.tsx'teki `â` karakteri (#27),
          (4) Customizer adım başlıklarının Türkçeleştirilmesi/spec senkronu (#28/29),
          (5) VisualPreview.tsx çağıranlarının tam repo taraması (#34),
          (6) ProfileForm.tsx Tailwind sınıflarının DESIGN_SYSTEM.md ile teyidi (#38),
          (7) AddToCartButton.tsx — hiç görülmedi, BSC-6 (çift tıklama koruması) teyit
          edilmeli (ROADMAP.md Oturum 3 satırından yeni fark edilen açık uç — #50, yeni).
```

---

## 📌 KRİTİK TEKNİK/TASARIM KARARLARI (özet — hâlâ etkili olanlar + yeniden teyit edilmesi gerekenler)

| # | Karar | Durum |
|---|---|---|
| 1 | Customizer 5 adım: Base → Main → Garden → Signature Flavor → Finish | ✅ Uygulandı |
| 3-4 | Garden: ilk 4 ücretsiz + avokado her zaman ücretli / Finish: ilk 1 ücretsiz | ✅ Uygulandı |
| 5 | "Make it Yours" → Finish'e entegre, "Double Main" → `mainPortion` yeniden kullanır | ✅ Uygulandı |
| 6 | Slogan: "Sağlıklı Beslen, Sağlıklı Yaşa, Gücünü Hisset" | ✅ |
| 11 | "Bitkisel Protein" tek Main kartı + 2 alt-varyant, inline genişleme, flavor filtreleme | ✅ Uygulandı, canlıda doğrulandı, spec tam senkron. MASTER_PLAN'a bilinçli taşınmadı (spec referansı korundu). |
| 12 | "Kâseni Yarat" sadece "Benim Kâsem" (`build-your-own-kasem`) ürününde | ⚠️ Bağlayıcı kapsam kuralı, ayrıca test edilmedi — hâlâ geçerli varsayılıyor |
| 13 | `FulfillmentChannel`: `"pickup"` \| `"dine-in"` (delivery yok), sepet/oturum seviyesinde tek alan | ✅ Canlıda doğrulandı VE MASTER_PLAN.md v2.2 sitemap'i artık bu isimlendirmeyle senkron |
| 14-16 | `â` karakteri kaldırıldı (menu-data.json, CartDrawer). Hero.tsx/StepBase.tsx bilinçli ertelendi (#27) | ✅ `menu-data.json` içeriği görülüp `â` yokluğu doğrulandı |
| 15 | Customizer malzeme isimleri Türkçeye çevrildi (id'ler değişmedi) | ✅ Canlıda doğrulandı |
| 18 | CartDrawer portal fix (`createPortal` → `document.body`, backdrop-blur containing-block bug'ı için) | ✅ Canlıda doğrulandı (raporlandı — `useCartStore.ts` bu sohbette bizzat görülmedi, ROADMAP.md Oturum 4'te 🟡 işaretli) |
| 19→20 | Auth: Twilio Verify + Auth.js JWT. DB: Neon Postgres (Vercel Marketplace), `users` tablosu (`phone`,`address`,`displayName`,`loyaltyPoints`,`verifiedAt`) | ✅ Kurulum tamam, build yeşil. MASTER_PLAN.md v2.2 sitemap'ine ve ROADMAP.md'ye (Oturum 4.5) işlendi. |
| 20 | AuthenticatedUser tipi `address` alanıyla genişletildi, DB'de kalıcı saklanıyor | ✅ `types/index.ts`'te doğrulandı |
| 21-22 | Auth kod (route'lar, `auth.ts`, DB katmanı) + görünür giriş UI (`/giris`) | ✅ Kod tamam, `/giris` canlı doğrulandı; OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor |
| 23 | Adres/profil modeli: adres SADECE profil/sadakat verisi, checkout'u bloklamaz, `/hesap`'ta opsiyonel toplanır | ✅ Kod üretildi VE repo varlığı (route.ts, ProfileForm.tsx, page.tsx, rate-limit.ts — 4/4) doğrulandı (#41 kapandı) |
| 🆕 | CategoryNav sekmeleri `BowlItem.category` enum'unu genişletmez — "vegan"/"sicak-tahil" sekmeleri `tags[]` üzerinden sanal filtrelenir (şema değişikliği yok) | ✅ `lib/menu-filters.ts`'te kod-içi gerekçesiyle doğrulandı (#35 kapandı) |
| 🆕 | Alerjen gösterimi: kalori/protein ile aynı zorunluluk statüsü, gizlenemez/opsiyonel yapılamaz | ✅ `DESIGN_SYSTEM.md` §7 VE `AGENT.md` v1.3 protokol karşılığı tam (#7 ve #44 kapandı) |

*(Tam gerekçe/tarih dökümü için: `session_log.md`.)*

---

## 🚨 AÇIK SORUNLAR (borçlar — güncel liste)

| # | Öncelik | Açıklama | Referans |
|---|---|---|---|
| 10 | 🟡 | ARCHITECTURE.md §2.4 hâlâ 4 adımlı customizer state'ini yansıtıyor — 5 adıma (+ Bitkisel Protein alt-varyantına) hiç güncellenmedi | `ARCHITECTURE.md` §2.4, `CUSTOMIZER_SPEC.md` §3.1 |
| 24/17/18 | 🟡 | `customizerCatalog` + "Benim Kâsem" fiyatı hâlâ TEST VERİSİ — fotoğraf çekimine bilinçli ertelendi | `lib/customizer-data.ts`, `lib/menu-data.json` |
| 27 | 🟢 | Hero.tsx CTA'sı ve StepBase.tsx açıklaması hâlâ `â` içeriyor (bilinçli ertelendi) | `components/home/Hero.tsx`, `StepBase.tsx` |
| 28/29 | 🟢 | Customizer adım başlıkları hâlâ İngilizce; `CUSTOMIZER_SPEC.md` §2 senkron değil | `components/customizer/Step*.tsx` |
| 32 | 🟠 | Twilio TR SMS kısıtı — hem auth hem `/hesap` akışını canlıda test edilemez kılıyor. Çözüm: ücretli plan veya Netgsm/İleti Merkezi. Kullanıcı kararıyla bilinçli PARKLANDI. ROADMAP.md Oturum 4.5'te de blokaj olarak işaretli. | Twilio Console, `ROADMAP.md` Oturum 4.5 |
| 34 | 🟢 | `VisualPreview.tsx`'in `className` davranışı — kısmi teyit edildi, tam repo taraması eksik | `components/customizer/VisualPreview.tsx` |
| 38 | 🟢 | `ProfileForm.tsx` Tailwind sınıfları (`bg-olive-600` vb.) DESIGN_SYSTEM.md ile teyit edilmedi | `components/account/ProfileForm.tsx` |
| 39 | 🟠 | `/hesap` akışı Twilio kısıtı yüzünden canlıda hiç fonksiyonel test edilemedi (aslında #32'nin bir sonucu) | `app/hesap/page.tsx` |
| 50 | 🆕 🟢 | `AddToCartButton.tsx` bu sohbette hiç görülmedi — BSC-6 (çift tıklama koruması) ve geçersiz adımda disabled davranışı teyit edilmedi. ROADMAP.md Oturum 3 denetimi sırasında fark edildi. | `components/customizer/AddToCartButton.tsx` |
| 51 | 🆕 🟢 | `useCartStore.ts` bu sohbette hiç görülmedi — CartDrawer portal fix'inin (Karar #18) hâlâ geçerli olduğu ve persist davranışının çalıştığı raporlanmış ama dosya üzerinden teyit edilmemiş. ROADMAP.md Oturum 4 denetimi sırasında fark edildi. | `store/useCartStore.ts` |
| 52 | 🆕 🟡 | **Mimari çelişki:** VisualPreview.tsx + `lib/customizer-visual-layers.ts`, `/public/images/layers/` altında her malzeme için gerçek görsel dosyası bekliyor — klasör tamamen boş, PHOTOGRAPHY_GUIDE.md §8'in "CSS/SVG yeterli" notuyla çelişiyor. Karar: vektörel ikon seti üretilecek (fotoğraf değil), kod değişmeyecek. PHOTOGRAPHY_GUIDE.md §8 notu da bu karara göre düzeltilmeli (ayrı bir açık iş). | `components/customizer/VisualPreview.tsx`, `lib/customizer-visual-layers.ts`, `PHOTOGRAPHY_GUIDE.md` §8 |

> **KAPANDI (önceki turlar):** #4, #7, #15, #16, #20, #22/Karar #11, #35, #43, #44, #49 —
> detaylar önceki SESSION_INDEX sürümlerinde ve bu sohbetin geçmişinde.
>
> **KAPANDI (bu sohbet, bu tur — 2026-07-22):**
> - **Doküman tutarlılık denetimi** — Kullanıcı isteğiyle MASTER_PLAN.md ve ROADMAP.md,
>   kodun (CUSTOMIZER_SPEC.md, types, store) güncel durumuyla karşılaştırıldı. 3 gerçek
>   boşluk bulundu: (1) Auth/Hesap sistemi hiçbir üst-seviye plan belgesinde yoktu —
>   MASTER_PLAN.md v2.2 sitemap'ine ve ROADMAP.md'ye (yeni "Oturum 4.5" tablosu, kabul
>   kriterleriyle) işlendi. (2) Sipariş kanalı isimlendirmesi ("Paket Servis/Gel Al")
>   kodla ("pickup"/"dine-in") uyuşmuyordu — MASTER_PLAN.md'de netleştirildi. (3) ROADMAP.md
>   çok eskiydi (v1.1, 18 Temmuz) — Oturum 3 satırları bu sohbette görülen dosyalarla teyit
>   edilip güncellendi, Oturum 4'e durum sütunu eklendi. Bitkisel Protein Main listesi
>   BİLİNÇLİ olarak MASTER_PLAN'a taşınmadı (CUSTOMIZER_SPEC.md zaten "tam kontrat"
>   referansı — Kural #5, gereksiz çoğaltma önlendi). Bu denetim sırasında 2 yeni açık
>   uç fark edildi: AddToCartButton.tsx (#50) ve useCartStore.ts (#51) — ikisi de bu
>   sohbette hiç görülmedi, sadece raporlanan durumlarına güvenildi.
>
> Detaylı gerekçe/dosya alıntıları bu sohbetin geçmişinde; bir sonraki turda `session_log.md`'ye
> taşınmalı (henüz taşınmadı, bu tur da dahil).
>
> **BU TUR (2026-08-01):**
> - VisualPreview.tsx incelendi, #52 (yeni, yukarıda) açıldı — fotoğraf katmanlama yerine
>   vektörel ikon sistemine geçiş kararlaştırıldı, kod değişikliği gerekmiyor.
> - SESSION_INDEX.md vs SESSION_INDEX_v2.md karışıklığı çözüldü — v2'nin kayıtlı ihlalin
>   kendisi olduğu (bu dosyanın en üstündeki not) kullanıcıya tekrar doğrulandı, bu dosyanın
>   (SESSION_INDEX.md) tek geçerli kaynak olduğu teyit edildi. Yeni bir kapanış gerekmedi,
>   zaten var olan uyarı notu geçerliliğini korudu.

---

## SESSION ÖZET (son 5)

| Session | Tarih | Ana içerik | Durum |
|---|---|---|---|
| 0 | — | Ajan altyapısı (14 dosya) | ✅ Tamamlandı |
| 1 | 2026-07-1x | Next.js+Tailwind kurulum, font/renk, Header/Footer, Hero | ✅ Tamamlandı |
| 2 | 2026-07-18 | Menü sayfası, filtreleme, MenuCard, statik veri, CategoryNav+FilterPanel, customizer 4→5 adım kararı | ✅ Tamamlandı |
| 3 | 2026-07-18 | Zustand store + pricing + customizer data, masaüstü UI bileşenleri (kesintiye uğradı) | ✅ Büyük ölçüde tamam, bu sohbette dosya-dosya teyit edildi |
| 4 (devam) | 2026-07-18 → 07-22 (11 bölüm) | Sepet/kanal seçimi, Türkçeleştirme, â düzeltmesi, CartDrawer bugfix, auth mimarisi+kod+DB+UI, adres/profil (#23), test triyajı, menü animasyonu, ARCHITECTURE.md v1.3→v1.4, rate-limit üretimi, repo tutarsızlığı keşfi (#42 kapandı), v2 sıkıştırma turunda düşen maddelerin geri bulunması, DESIGN_SYSTEM.md §7 (#7 kapandı), Karar #11/#22 Bitkisel Protein uçtan uca (canlıda doğrulandı), MobileSummaryDrawer format konsolidasyonu (#43), AGENT.md v1.3 alerjen self-check (#44), CUSTOMIZER_SPEC.md §3.5 (#49), **MASTER_PLAN.md v2.2 + ROADMAP.md v1.3 tutarlılık denetimi ve güncellemesi** (Auth/Hesap sitemap'e ve Oturum 4.5'e işlendi, #50/#51 yeni fark edildi) | 🟡 Devam ediyor — Twilio (#32) TEK gerçek darboğaz |
| 5 | 2026-08-01 | Netgsm sözleşmesi onaylandı (vergi levhası pazartesi yüklenecek — Twilio/#32 çözümü netleşiyor). Menü içerik/görsel yükleme süreci netleştirildi (CMS yok, kod+deploy ile — 40-50 ürün tek seferlik iş). **VisualPreview.tsx mimari denetimi:** `/public/images/layers/` klasörünün boş olduğu ve PHOTOGRAPHY_GUIDE.md §8 notuyla çeliştiği tespit edildi (#52, yeni). Fotoğraf katmanlama yerine vektörel ikon sistemine geçiş kararlaştırıldı. SESSION_INDEX.md vs SESSION_INDEX_v2.md karışıklığı kalıcı olarak çözüldü (v2 = kayıtlı ihlalin kendisi, kullanılmayacak). | 🟡 Devam ediyor — #32 çözüme yaklaşıyor, #52 yeni açıldı |

*(Tam turn-by-turn detay: `session_log.md`.)*

---

## GENEL DURUM (özet)

| Alan | Değer |
|---|---|
| Repo | `github.com/Sovereign34/Bowlera_site` — main branch güncel, Vercel Production'da deploy'lar Ready |
| Planlama Belgeleri | ✅ MASTER_PLAN.md v2.2 ve ROADMAP.md v1.3 artık kod ile hizalı (Auth/Hesap, kanal isimlendirmesi, Oturum 3/4 durumları) |
| Test Suite | 🟢 `Header.test.tsx`, `customizer-summary-format.test.ts`, `menu-filters.test.ts` doğrulandı. Genel `npm test` bu aralıkta tekrar çalıştırılmadı. |
| Auth | 🟢 Kod tamam, `/giris` canlı doğrulandı, artık MASTER_PLAN/ROADMAP'te resmi. 🟠 OTP fonksiyonel test Twilio kısıtı yüzünden yapılamıyor (#32) |
| Kullanıcı Profili/Adres | 🟢 Kod tamam VE repoda doğrulandı. 🟠 Twilio kısıtı yüzünden canlıda hâlâ test edilemiyor (#39) |
| Checkout (`/siparis`) | 🟢 Kod tamam VE repoda doğrulandı — kanal seçimi zorunlu |
| Veritabanı | 🟢 Neon Postgres çalışıyor |
| ARCHITECTURE.md | 🟢 v1.4 güncel ve repoda doğrulandı. §2.4 (5 adım + Bitkisel Protein, #10) bilinçli/teyitli kapsam dışı durum |
| Menü Filtreleme | 🟢 `lib/menu-filters.ts` — kod+test ile doğrulandı |
| Customizer Özet Formatlama | ✅ `lib/customizer-summary-format.ts` — kod+test ile doğrulandı VE `MobileSummaryDrawer.tsx` konsolide edildi |
| Alerjen Gösterim Sistemi | ✅ `DESIGN_SYSTEM.md` §7 VE `AGENT.md` v1.3 protokol karşılığı tam. 🟡 UI implementasyonu henüz yazılmadı. |
| Bitkisel Protein (Main alt-varyant) | ✅ Kod + spec + canlı doğrulama tam. MASTER_PLAN'a bilinçli taşınmadı (spec referansı). |
| Sepet (`useCartStore.ts`, `AddToCartButton.tsx`) | 🟡 Bu sohbette hiç görülmedi — CartDrawer bugfix'i raporlandı ama teyit edilmedi (#50, #51 yeni) |
| Customizer Görsel Önizleme (VisualPreview) | 🔴 Kod çalışıyor ama görsel katmanların hepsi eksik (`/public/images/layers/` boş) — şu an boş daire gösteriyor. Vektörel ikon seti üretimi bekleniyor (#52, yeni) |

---

## SIRADAKİ GÖREVLER (öncelik sırasıyla)

| Sıra | Görev | Öncelik |
|---|---|---|
| 1 | Twilio kararı: ücretli plan veya yerel sağlayıcı — TEK büyük darboğaz (#32, parklandı) | 🟠 |
| 1b | Vektörel ikon seti üretimi (25-30 malzeme, marka paletiyle uyumlu) — kullanıcı üretici bulacak/Claude taslak üretecek, netleşmedi (#52, yeni) | 🟡 |
| 1c | PHOTOGRAPHY_GUIDE.md §8 notu düzeltilmeli — "CSS/SVG yeterli" ifadesi kodla çelişiyor (#52 ile bağlantılı) | 🟢 |
| 2 | `AddToCartButton.tsx` + `useCartStore.ts` paylaşılırsa BSC-6 ve persist davranışını teyit et (#50/#51, yeni) | 🟢 |
| 3 | ARCHITECTURE.md §2.4'ü 5 adımlı customizer'a (Bitkisel Protein dahil) güncelle (#10) | 🟡 |
| 4 | DESIGN_SYSTEM.md §7'ye göre alerjen gösterimini MenuCard/Customizer/SummaryPanel'de fiilen uygula | 🟡 |
| 5 | `customizerCatalog` + fiyat verisi — fotoğraf çekimine bağlı (#24) | 🟡 (dış olay) |
| 6 | VisualPreview çağıranlarının tam repo taraması ile #34'ü kesin kapat | 🟢 |
| 7 | ProfileForm Tailwind sınıflarını DESIGN_SYSTEM.md ile teyit et (#38) | 🟢 |
| 8 | Hero.tsx/StepBase.tsx'teki `â` karakterini düzelt (#27) | 🟢 |
| 9 | Customizer adım başlıklarını Türkçeleştir / spec ile senkronla (#28/29) | 🟢 |
| 10 | Genel `npm test` çalıştırıp güncel geçen/kalan sayıyı teyit et | 🟢 |

---

*BOWLERA SESSION_INDEX.md — v11. Arşiv `session_log.md`'ye taşınmayı bekliyor (Session 4
ve Session 5 detayları henüz taşınmadı — dosya 400 satırın altında, taşıma zorunlu değil).
v10'da (2026-07-22) MASTER_PLAN.md ve ROADMAP.md kod ile hizalanmış, #50/#51 açılmıştı.
Bu turda (2026-08-01, Session 5): Netgsm/vergi levhası ilerlemesi kaydedildi, menü içerik
yükleme süreci netleşti, **#52 (VisualPreview mimari çelişkisi) açıldı** — fotoğraf
katmanlama yerine vektörel ikon sistemine geçiş kararlaştırıldı, kod değişikliği
gerekmiyor. SESSION_INDEX.md vs SESSION_INDEX_v2.md karışıklığı kalıcı çözüldü.
Kalan açık sorunlar: #10, #24, #27, #28/29, #32, #34, #38, #39, #50, #51, #52.
Güncellenme: 2026-08-01.*
