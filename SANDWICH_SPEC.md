# BOWLERA — SANDWICH_SPEC.md
> Bu belge "Sandviçini Oluştur" akışının tam kontratıdır.
> CUSTOMIZER_SPEC.md (Bowl) ile AYNI mimari desenleri kullanır ama TAMAMEN
> İZOLE bir store/spec'tir — bowl akışına dokunmaz (Seçenek A, kullanıcı onayı
> 2026-08-23).
> Kaynak: Subway + Jersey Mike's global sandviç zinciri UX analizi (web
> araştırması, 2026-08-23) + Bowlera'nın mevcut CUSTOMIZER_SPEC.md v1.2
> desenleri (adım guard'ı, ücretsiz kota mantığı, alt-varyant mekanizması).
> ⚠️ DURUM: Yapısal iskelet ONAYLANDI. Somut malzeme listesi + fiyat/kalori
> verisi ve ücretsiz kota sayıları HENÜZ SAĞLANMADI — bu belgede yer alan
> örnek malzeme adları SADECE YAPIYI GÖSTERMEK içindir, production verisi
> DEĞİLDİR (AGENT.md Kural #4 — Sahte Veri Yasağı). Kod aşamasına geçmeden
> önce gerçek `sandwich-data.json` içeriği paylaşılmalı.

---

## 0. İZOLASYON İLKESİ (Seçenek A)

```
useSandwichStore.ts   — AYRI Zustand store, useCustomizerStore.ts'e DOKUNMAZ
SANDWICH_SPEC.md       — AYRI kontrat dosyası (bu dosya)
app/sandwich/customize/[id]/page.tsx  — AYRI route, bowl route'unu ETKİLEMEZ
components/sandwich/*  — AYRI bileşen klasörü (components/customizer/ İLE
                          KARIŞTIRILMAZ)
```

Gerekçe (kullanıcı onaylı): Bowl akışı canlıda çalışıyor, ona dokunmak risk.
İki store arasında ORTAK kod tekrarı olacak (adım guard deseni, ücretsiz kota
mantığı) — bu BİLİNÇLİ bir trade-off, 3. bir ürün tipi geldiğinde ortak bir
çekirdeğe (`useProductCustomizerStore.ts`) geçiş DEĞERLENDİRİLEBİLİR (şimdi
DEĞİL — YAGNI, AGENT.md Kural #5).

`useCartStore.ts` PAYLAŞILIR — hem bowl hem sandviç aynı sepete eklenir
(ARCHITECTURE.md §1 Katman Sınırı Kural 7'deki "tek store, çoklu giriş
noktası" deseniyle tutarlı). Sepetteki `customization` alanı artık
`BowlCustomization | SandwichCustomization` union tipini taşıyabilmeli —
bu, `useCartStore.ts`'e dokunan TEK değişikliktir ve AYRI bir onay/KARAR
BİLDİRİMİ gerektirir (birden fazla modülü aynı anda değiştirme yasağı,
AGENT.md Kural #5).

---

## 1. AKIŞ FELSEFESİ

Subway ve Jersey Mike's araştırmasından çıkan iki farklı model sentezlendi:

- **Subway** — protein-first, tam serbest hat, boy (6"/30cm) ayrı zorunlu adım.
- **Jersey Mike's** — boy en başta, "Mike's Way" adında hazır paket kısayolu
  (tek tıkla klasik sebze+sos kombinasyonu doldurur, adımı ATLAMAZ, sadece
  varsayılan değer doldurur).

Bowlera'ya uyarlanan sıra **Subway'in gerçek sırasına sadık** kalacak şekilde
düzeltildi (önceki "Bread-first" önerisi kullanıcı tarafından reddedildi):
**Size → Bread → Protein → Cheese → Veggies → Sauce&Toast&Extras**.

Ayrıca **UX sırası ile operasyon/hazırlık sırası AYRI tutulur** (bkz. §9) —
bu, Bowlera'nın dijital-sipariş + arkada-personel-hazırlar modelinde
(Personel Sipariş Paneli #62 ile aynı felsefe) Subway'in fiziksel-hat
modelinden temel bir sapmadır ve BİLİNÇLİ bir tasarım kararıdır.

---

## 2. ADIM TANIMLARI

> ⚠️ Malzeme adları YER TUTUCUDUR — gerçek `sandwich-data.json` bekleniyor.

| Adım | İçerik (örnek/yer tutucu) | Seçim Tipi | Zorunlu mu |
|---|---|---|---|
| 1. Size | 15cm / 30cm | Tekli | ✅ Zorunlu |
| 2. Bread | [X çeşit ekmek — TBD] | Tekli | ✅ Zorunlu |
| 3. Protein | [X çeşit protein + **Bitkisel Protein** alt-varyant, bkz. §2.1] | Tekli + porsiyon | ✅ Zorunlu |
| 4. Cheese | [X çeşit peynir + "Peynirsiz" seçeneği] | Tekli/Yok | ⬜ Opsiyonel |
| 5. Veggies | [X çeşit sebze — ilk N ücretsiz, avokado her zaman ücretli] | Çoklu | ⬜ Opsiyonel |
| 6. Sauce & Toast & Extras | Sos (zorunlu, tekli) + Toast toggle (opsiyonel, şube-bağımlı, bkz. §2.2) + ücretli extras (double protein, extra peynir vb.) | Karma | ✅ (sadece sos) |

**Veggies ücretlendirme kuralı — Bowl Garden deseniyle BİREBİR AYNI mekanizma
tekrar kullanılır:**
```
İlk N seçim (avokado hariç) ücretsiz, N+1 ve sonrası ücretli.
Avokado kaçıncı sırada seçilirse seçilsin HER ZAMAN ücretli.
⚠️ N sayısı (Bowl'da 4'tü) sandviç için AYRI belirlenmeli — kullanıcıdan
teyit bekleniyor, 4 varsayılmadı (Kural #1 — tahmin etme).
```

### 2.1 Bitkisel Protein — Alt-Varyant Mekanizması

Bowl'daki CUSTOMIZER_SPEC.md §2.1 ile **AYNEN aynı desen** — kod DEĞİL,
davranış kopyalanır (izole store'lar olduğu için gerçek kod paylaşımı yok,
ama mantık birebir tekrarlanır):

```
"Bitkisel Protein" kartı → yerinde genişler → 2 alt-varyant (Soslu Nohut /
Meksika Fasulyesi) kart içinde gösterilir → ayrı adım/modal AÇILMAZ →
seçim yapılmadan "İlerle"ye basılırsa nextStep() ilk varyantı SESSİZCE atar.
```

Sandviçe özgü fark: Signature Flavor filtreleme YOK — Sauce adımında (§6)
tüm soslar her Protein için gösterilir (Bowl'daki `compatibleFlavorIds`
mekanizması bu spec'te ŞİMDİLİK devre dışı, ihtiyaç görülürse eklenebilir).

### 2.2 Toast Toggle — Şube-Bağımlı Özellik

```
Toast, sabit bir seçenek DEĞİL — şube config'ine bağlı opsiyonel bir
özelliktir (toast ekipmanı gerektirir). CONFIG_SCHEMA.md'ye
`branchConfig.hasToastEquipment: boolean` gibi bir alan eklenmesi
gerekebilir — bu ÇOK ŞUBELİ mimariyle (#92/#93/#94) doğrudan bağlantılı
ve HENÜZ KARARLAŞTIRILMADI (kullanıcı kararıyla #91'in ardına alındı).
Şimdilik: tek şubeli MVP'de sabit `true`/`false` env değeri ile
başlanabilir, migration'a gerek yok.
```

---

## 3. STATE MAKİNESİ

### 3.1 State Şeması

```ts
// store/useSandwichStore.ts — İZOLE store, useCustomizerStore.ts'e bağımlı DEĞİL

interface SandwichSelection {
  size: '15cm' | '30cm' | null
  bread: string | null
  protein: string | null
  proteinVariant: string | null   // SADECE protein='plant-based-protein' iken anlamlı
  proteinPortion: 'single' | 'double'
  cheese: string | null            // null = "Peynirsiz" bilinçli seçimi
  veggies: string[]                // ilk N ücretsiz (avokado hariç), sonrası ücretli
  sauce: string | null
  toasted: boolean                 // sadece branchConfig.hasToastEquipment true ise anlamlı
  extras: {
    doubleProtein: boolean         // proteinPortion zaten bunu karşılıyorsa BU ALAN GEREKSİZ
                                     // — DEPENDENCIES.md netleşene kadar TARTIŞMALI, bkz. §8
    extraCheese: boolean
    extraSauce: boolean
  }
}

interface SandwichState {
  currentStep: 1 | 2 | 3 | 4 | 5 | 6
  selections: SandwichSelection
  maxReachedStep: 1 | 2 | 3 | 4 | 5 | 6

  // Actions
  selectSize: (size: '15cm' | '30cm') => void
  selectBread: (id: string) => void
  selectProtein: (id: string, portion: 'single' | 'double') => void
  selectProteinVariant: (variantId: string) => void
  selectCheese: (id: string | null) => void
  toggleVeggie: (id: string) => void
  selectSauce: (id: string) => void
  toggleToast: () => void          // branchConfig.hasToastEquipment false ise no-op
  toggleExtra: (key: keyof SandwichSelection['extras']) => void
  applyMikesWayPreset: () => void  // 🆕 — kısayol, adım ATLAMAZ, sadece
                                     // veggies+sauce'a varsayılan doldurur,
                                     // kullanıcı sonrasında serbestçe değiştirebilir
  goToStep: (step: 1|2|3|4|5|6) => void   // step <= maxReachedStep+1 değilse no-op
  nextStep: () => void
  previousStep: () => void
  reset: () => void

  // Derived
  getTotals: () => { price: number; calories: number; protein: number; carbs: number; fat: number }
  isStepValid: (step: 1|2|3|4|5|6) => boolean
  getPrepOrder: () => PrepStep[]    // 🆕 — bkz. §9, UX sırasından BAĞIMSIZ
}
```

### 3.2 Adım Geçiş Guard'ı

Bowl'daki §3.2 ile AYNI mekanizma:

```ts
// ✅
const goToStep = (step) => set((state) => {
  if (step > state.maxReachedStep + 1) return state   // no-op, sessizce reddet
  return { currentStep: step }
})
```

URL'den doğrudan adım değişikliği (`?step=6`) engellenir — sayfa yüklenince
`maxReachedStep` kontrolü yapılır, geçersizse `currentStep=1`'e döner.

### 3.3 isStepValid — Adım Bazlı Validasyon

```
isStepValid(1): selections.size !== null
isStepValid(2): selections.bread !== null
isStepValid(3): selections.protein !== null
isStepValid(4): true (Cheese her zaman "valid" — opsiyonel, null geçerli bir seçim)
isStepValid(5): true (Veggies opsiyonel)
isStepValid(6): selections.sauce !== null (Toast/Extras opsiyonel, sos ZORUNLU)
```

### 3.4 nextStep() — Plant-Based Protein Otomatik Atama

Bowl §3.4 ile AYNI davranış:

```
eğer selections.protein === 'plant-based-protein'
   VE selections.proteinVariant === null
ise → nextStep() ilk varyantı SESSİZCE atar, kullanıcı bloklanmaz.
```

---

## 4. FİYAT/KALORİ HESAPLAMA — getTotals()

```ts
function getTotals(selections: SandwichSelection): Totals {
  const size = sandwichData.sizes.find(s => s.id === selections.size)
  const bread = sandwichData.breads.find(b => b.id === selections.bread)
  const proteinDef = sandwichData.proteins.find(p => p.id === selections.protein)
  const protein = proteinDef?.variants
    ? proteinDef.variants.find(v => v.id === selections.proteinVariant) ?? proteinDef.variants[0]
    : proteinDef

  const cheese = selections.cheese
    ? sandwichData.cheeses.find(c => c.id === selections.cheese)
    : null   // null → 0 katkı, "Peynirsiz" NaN üretmez

  const veggieItems = selections.veggies.map(id => sandwichData.veggies.find(v => v.id === id))
  const avocadoSelections = veggieItems.filter(v => v.id === 'avocado')
  const otherVeggies = veggieItems.filter(v => v.id !== 'avocado')
  const freeVeggies = otherVeggies.slice(0, FREE_VEGGIE_QUOTA)   // ⚠️ TBD, bkz. §2
  const paidVeggies = [...otherVeggies.slice(FREE_VEGGIE_QUOTA), ...avocadoSelections]

  const sauce = sandwichData.sauces.find(s => s.id === selections.sauce)

  const extrasPrice =
    (selections.extras.extraCheese ? sandwichData.extraPrices.cheese : 0) +
    (selections.extras.extraSauce ? sandwichData.extraPrices.sauce : 0)
    // doubleProtein zaten proteinPortion='double' fiyatına dahilse burada
    // TEKRAR sayılmamalı — §8'deki açık soru netleşmeden bu satır KESİN
    // yazılamaz (AGENT.md Kural #5 — aynı davranış iki yerde tanımlanmaz)

  return {
    price: sum(size, bread, protein, cheese, ...paidVeggies, sauce) + extrasPrice,
    calories: sum(size, bread, protein, cheese, ...veggieItems, sauce) + extrasCalories(selections.extras),
    protein: sum(..., key: 'protein'),
    // carbs, fat aynı mantıkla
  }
}
```

> ⚠️ Toast, kalori/fiyatı DEĞİŞTİRMEZ (aynı malzeme, farklı hazırlık) —
> `toasted: boolean` sadece `getPrepOrder()`'ı etkiler, `getTotals()`'ı
> ETKİLEMEZ.
> ⚠️ Seçim yokken (`null`) ilgili değerler `0` döner, `NaN` değil (BSC-3
> tutarlılığı, Bowl §4 ile aynı prensip).

---

## 5. VISUALPREVIEW — TEKNİK KARAR

Bowl §5 ile AYNI yaklaşım: **katmanlı CSS/SVG**, 3D/Canvas kullanılmaz.

```
z-index sırası (alttan üste):
1. Ekmek (sabit taban, selections.bread'e göre görsel değişir)
2. Protein katmanı        ← proteinVariant'a göre 2 ayrı katman (plant-based ise)
3. Cheese katmanı          ← null ise katman gösterilmez
4. Veggie katmanları        ← her biri ayrı katman (opacity toggle)
5. Sauce katmanı            ← "damla/sızma" efekti üstte
```

`public/images/layers/sandwich/` altında AYRI bir klasör — bowl katmanlarıyla
(`public/images/layers/`) KARIŞTIRILMAZ, dosya adı çakışması riski önlenir.

---

## 6. MOBİL UX

Bowl §6 ile AYNI sticky çekmece deseni — kapalı/açık durumları, VisualPreview
küçük versiyonu, "Sepete Ekle" butonu. Tek fark: çekmece açıkken **"Mike's
Way" kısayol butonu** en üstte sabit gösterilir (kullanıcı 6 adımı tek tek
geçmeden hızlı sipariş verebilsin — Jersey Mike's'ten alınan esin).

---

## 7. SEPETE EKLEME

```
Kural: "Sepete Ekle" butonu YALNIZCA isStepValid(6) true olduğunda aktif
       (size + bread + protein + sauce seçilmiş olmalı).
       BSC-6 (race condition) koruması — Bowl §7 ile AYNI isAdding.current kilidi.
```

```ts
const handleAddToCart = () => {
  if (isAdding.current || !isStepValid(6)) return
  isAdding.current = true
  const totals = getTotals(selections)
  addToCart({
    cartId: crypto.randomUUID(),
    bowlItem: null,
    customization: { type: 'sandwich', ...selections },   // union tipin ayırt edici alanı
    quantity: 1,
    unitPrice: totals.price,
    unitCalories: totals.calories,
  })
  reset()
  setTimeout(() => { isAdding.current = false }, 500)
}
```

> ⚠️ `useCartStore.ts`'teki `customization` alanının union tipe
> genişletilmesi (`BowlCustomization | SandwichCustomization`) AYRI bir
> onay gerektiren TEK değişikliktir — bu spec onaylandıktan SONRA, kod
> aşamasında ayrı bir KARAR BİLDİRİMİ ile sunulmalı.

---

## 8. AÇIK SORULAR — Kod Aşamasından ÖNCE Netleşmeli

| # | Soru | Neden Bloklayıcı |
|---|---|---|
| S1 | `sandwich-data.json` — gerçek ekmek/protein/peynir/sebze/sos listesi + fiyat/kalori | Sahte veri yasağı (Kural #4), kod bu veri olmadan yazılamaz |
| S2 | Veggies ücretsiz kota sayısı (Bowl'da 4'tü — sandviçte aynı mı?) | `FREE_VEGGIE_QUOTA` sabiti belirsiz |
| S3 | `extras.doubleProtein` ile `proteinPortion: 'double'` arasındaki ilişki — aynı şey mi, farklı mı? | Aynı davranışın iki yerde tanımlanma riski (Kural #5) |
| S4 | Toast — MVP'de tüm şubelerde var mı, yoksa config'e mi bağlı? | §2.2, CONFIG_SCHEMA.md'ye alan eklenip eklenmeyeceğini belirler |
| S5 | "Mike's Way" preset'inin TAM içeriği ne olacak (hangi sebze+sos kombinasyonu varsayılan)? | `applyMikesWayPreset()` fonksiyonunun içeriği bu veriye bağımlı |
| S6 | `useCartStore.customization` union tipi — bu değişiklik ayrı bir sohbette mi ele alınmalı? | Bowl akışına dokunan TEK nokta, izolasyon ilkesinin istisnası |

---

## 9. HAZIRLIK SIRASI / MUTFAK BİLETİ — getPrepOrder()

> 🆕 Kullanıcı onaylı ayrım: **UX seçim sırası ≠ fiziksel hazırlık sırası.**
> Bu bölüm SADECE Personel Sipariş Paneli (#62) tarafındaki ticket render'ını
> etkiler — müşterinin gördüğü adım sırasını DEĞİŞTİRMEZ.

```
Fiziksel hazırlık sırası (mutfak/operasyon gerçeği):
1. Bread          — kesilir/hazırlanır
2. Protein+Cheese  — ISLI ise burada toast ile birlikte olabilir
3. Toast           — varsa, ekipman+süre gerektirir (§2.2)
4. Veggies         — soğuk malzemeler, toast SONRASI eklenir
5. Sauce           — EN SON — sebzeler ıslanmasın diye
```

```ts
// store/useSandwichStore.ts
// Amaç:    selections state'ini UX sırasından bağımsız, mutfak hazırlık
//          sırasına göre yeniden düzenler
// Bağlı:   Personel Sipariş Paneli ticket render'ı (#62)
// Risk:    Sıra karışırsa mutfak toast'u unutur / sos ekmeği ıslatır /
//          sipariş yanlış hazırlanır
// Dokunma: UX adım sırası (§2) DEĞİŞTİRİLMEDEN bu fonksiyon güncellenebilir —
//          ikisi birbirinden BAĞIMSIZDIR, biri değişince diğeri otomatik
//          bozulmaz (ayrı fonksiyonlar, ayrı sorumluluklar)

function getPrepOrder(selections: SandwichSelection): PrepStep[] {
  const steps: PrepStep[] = [
    { label: 'Ekmek', value: selections.bread },
    { label: 'Protein + Peynir', value: `${selections.protein} + ${selections.cheese ?? 'peynirsiz'}` },
  ]
  if (selections.toasted) steps.push({ label: 'Toast', value: true })
  if (selections.veggies.length > 0) {
    steps.push({ label: 'Sebzeler', value: selections.veggies.join(', ') })
  }
  steps.push({ label: 'Sos', value: selections.sauce })
  return steps
}
```

> ⚠️ Çok şubeli mimariye (#92/#93/#94) geçişte, şubede toast ekipmanı yoksa
> bu fonksiyon `toasted` adımını otomatik atlar — `branchConfig`'e bağımlılık
> burada da netleşmeli (S4 ile aynı açık soru).

---

## 10. KALİTE KONTROL — SANDWICH SELF-CHECK

```
[ ] Adım geçiş guard'ı var mı?                → maxReachedStep kontrolü (§3.2)
[ ] Her adımın validasyonu tanımlı mı?         → isStepValid tüm 6 adımı kapsıyor mu? (§3.3)
[ ] Kalori/fiyat null-safe mi?                 → seçim yokken 0/"—" dönüyor mu? (§4)
[ ] Veggies ücretlendirme doğru mu?            → avokado hep ücretli, ücretsiz kota uygulanıyor mu? (§4, S2 netleşmeden KAPANAMAZ)
[ ] Toast, fiyat/kaloriyi etkiliyor mu?         → ETKİLEMEMELİ, sadece getPrepOrder()'ı etkilemeli (§4/§9)
[ ] proteinVariant null kalabiliyor mu?         → nextStep() otomatik atama yapıyor mu? (§3.4)
[ ] VisualPreview katman klasörü bowl'la çakışıyor mu? → AYRI klasör kullanılmalı (§5)
[ ] Sepete ekleme race condition korumalı mı?  → BSC-6 (§7)
[ ] getPrepOrder() UX sırasından bağımsız mı?  → İki fonksiyon birbirini bozmadan değişebiliyor mu? (§9)
[ ] useCartStore.customization union tipi AYRI onay gerektiriyor mu? → Kodlanmadan önce kullanıcıya sorulmalı (S6)
[ ] Tüm §8 açık soruları (S1-S6) kod aşamasından önce cevaplandı mı?
```

---

*BOWLERA SANDWICH_SPEC.md — v1.0 — 2026-08-23*
*Kaynak: CUSTOMIZER_SPEC.md v1.2 (desen referansı) · Subway/Jersey Mike's
global UX araştırması (web search, 2026-08-23) · Kullanıcı onayı: İzolasyon
ilkesi (Seçenek A), Subway-sadık adım sırası (Size→Bread→Protein→Cheese→
Veggies→Sauce&Toast&Extras), UX/operasyon sırası ayrımı (getPrepOrder()).*
*Durum: Yapısal iskelet ONAYLANDI. §8'deki 6 açık soru (S1-S6) cevaplanmadan
kod üretimine geçilemez (AGENT.md Kural #2 — eksik veriyle çözüm üretme).*
