## Session 3 — 2026-07-18

### Yapılanlar
- store/useCustomizerStore.ts üretildi (Zustand — 5 adımlı customizer state'i)
- lib/customizer-pricing.ts üretildi (canlı fiyat hesaplama fonksiyonları)
- lib/customizer-data.ts üretildi (statik customizer verisi)
- 19 yeni test yazıldı: customizer-pricing.test.ts (10), useCustomizerStore.test.ts (9)
- npm test: 10 test dosyası, 53 test — tümü ✅
- Push ve deploy başarılı (kullanıcı raporuna dayanıyor, git log ile teyit edilmedi)

### Kararlar
- Store ve pricing mantığı CUSTOMIZER_SPEC.md v1.1 (5 adım) kontratına göre üretildi
  (içerik bu oturumda satır satır teyit edilmedi — Açık Sorun #11)

### Teknik Notlar
- Bu oturum, session açılışında SESSION_INDEX.md okunmadan başladı; kapanış
  güncellemesi sohbet özetine dayanılarak geriye dönük yapıldı
- Sitede görsel değişiklik yok — beklenen durum, çünkü store'u tüketen UI
  bileşenleri (page.tsx, StepBase.tsx, SummaryPanel.tsx, VisualPreview.tsx)
  henüz yazılmadı (Oturum 4 kapsamı olabilir, ROADMAP.md ile teyit gerekiyor)

### Açık Kalan
- Açık Sorun #11, #12, #13 (bkz. SESSION_INDEX.md)
-----
## Session 2 (devam) — 2026-07-18 — Customizer Marka Kararı: 4 Adımdan 5 Adıma Geçiş

### Yapılanlar
- Kullanıcı, kategori/filtre görevlerine geçmeden önce "Kâseni Yarat" akışının
  marka anlayışının netleşmediğini belirtti.
- Kullanıcı 5 adımlı bir customizer önerisi getirdi: Base → Main → Garden →
  Signature Flavor → Finish, artı "Make it Yours" ek seçenekleri (Extra
  Avocado/Sauce/Crunch, Double Main).
- MASTER_PLAN.md, CUSTOMIZER_SPEC.md, CONTENT_GUIDE.md okunarak öneri mevcut
  kanonla karşılaştırıldı, 3 çelişki tespit edildi ve kullanıcıya soruldu.
- 3 turlu netleştirme tamamlandı (adım sayısı, dil, ücretlendirme kuralları).
- Şema değişiklik notu, güncellenmiş MASTER_PLAN.md (v2.1), CUSTOMIZER_SPEC.md
  (v1.1), CORE.md (§8 düzeltmesi) ve SESSION_INDEX.md üretildi.

### Kararlar (neden alındı)
1. **4 adım → 5 adım.** Gerekçe: gurme mutfak mantığını korurken (şefin
   düşünme sırası) daha sezgisel bir akış; kullanıcı onayı alındı.
2. **İngilizce isimlendirme.** Gerekçe: premium/global konumlandırma; bu,
   CONTENT_GUIDE.md §1'in Türkçe marka sesi kuralına bilinçli bir istisnadır,
   yalnızca customizer adım/malzeme isimlerini kapsar.
3. **Garden: ilk 4 ücretsiz + avokado her zaman ücretli.** Gerekçe: kullanıcı
   "sen öner" dedi; Claude mevcut Toppings kuralıyla tutarlılığı ve kullanıcının
   orijinal önerisindeki "+" işaretli avokado ayrımını esas alarak önerdi,
   kullanıcı onayladı.
4. **Finish: ilk 1 ücretsiz, sonrası ücretli.** Gerekçe: kullanıcı seçimi.
5. **"Make it Yours" → Finish adımına entegre, ayrı adım değil; "Double Main"
   mevcut `mainPortion` mekanizmasını yeniden kullanır.** Gerekçe: kullanıcı
   seçimi + AGENT.md Kural #5 (aynı işlevin iki yerde tanımlanmasını önleme).

### Teknik notlar
- Bu oturumda kod değişikliği YAPILMADI — yalnızca kanon dokümanlar (CORE.md,
  MASTER_PLAN.md, CUSTOMIZER_SPEC.md, SESSION_INDEX.md) güncellendi. Kod
  tarafı (`store/useCustomizerStore.ts`, `types/index.ts`, `lib/menu-data.json`)
  Oturum 3 kapsamındadır.
- `ARCHITECTURE.md` §2.4 ve `DEPENDENCIES.md` bu kararı henüz yansıtmıyor —
  bu iki dosya bu görev kapsamında sağlanmadığı için güncellenemedi.
  SESSION_INDEX.md'ye Açık Sorun #10 olarak işlendi.
- Şema değişiklik notu dosyası: `20260718001123_customizer_5_adim_gecisi.md`
  (kullanıcı repoya `docs/schema-changes/` altına taşıyacak).
