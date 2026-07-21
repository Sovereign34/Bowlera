# BOWLERA — CUSTOMIZER_SPEC.md
> Bu belge sitenin en kritik ekranı olan "Kâseni Yarat" akışının tam kontratıdır.
> State makinesi, adım validasyonu, VisualPreview mantığı ve mobil UX burada tanımlanır.
> Bu akışa dokunan her görev önce bu dosyayı okumak zorundadır.
> Kaynak: MASTER_PLAN.md v2.1 §3.3 (Kâse Özelleştirme Akışı) + §5.2 (Bileşen Yapısı) + §5.4 (Zustand)
> v1.1 (18 Temmuz 2026): 4 adımdan 5 adıma geçildi — bkz. `20260718001123_customizer_5_adim_gecisi.md`
> v1.2 (21 Temmuz 2026): Main adımına "Bitkisel Protein" alt-varyant mekanizması eklendi
> (Karar #11'in nihai hali) — bkz. §2.1 (yeni) ve §3.4 (yeni). SESSION_INDEX.md Açık Sorun #22.

---

## 1. AKIŞ FELSEFESİ

Doğrusal, bilişsel yükü azaltan **5 adım**. Kullanıcı önceki adımı tamamlamadan
sonrakine geçemez — CAVA'nın adım adım görselleştirilmiş sihirbaz UX'i referans
alınmıştır (MASTER_PLAN §2). Adım isimleri bilinçli olarak İngilizce'dir
(premium/global konumlandırma kararı — CONTENT_GUIDE.md §1'in Türkçe marka
sesi kuralına bu ekranda bilinçli bir istisna uygulanır; genel hedef "ilk kez
gören bir müşterinin 10 saniye içinde sipariş verebilmesi"dir). Sağ tarafta
(masaüstü) veya alt sticky çekmecede (mobil) **sabit özet panel** her zaman
görünür: canlı kase görseli, anlık kalori/makro toplamı (ZORUNLU, her zaman
görünür), güncel fiyat, "Sepete Ekle" butonu.

---

## 2. ADIM TANIMLARI

> Kaynak: MASTER_PLAN §3.3 v2.1

| Adım | İçerik | Seçim Tipi | Zorunlu mu |
|---|---|---|---|
| 1. Base | Jasmine Rice, Brown Rice, Quinoa, Mixed Greens, Spinach, Half Rice + Half Greens | Tekli | ✅ Zorunlu |
| 2. Main | Grilled Chicken, Crispy Chicken, Beef, Falafel, Shrimp, Salmon, Tofu, **Plant-Based Protein** (alt-varyant, bkz. §2.1) | Tekli/çift porsiyon | ✅ Zorunlu |
| 3. Garden | Cherry Tomato, Cucumber, Corn, Pickled Onion, Red Cabbage, Carrot, Avocado | Çoklu — max 4 ücretsiz | ⬜ Opsiyonel |
| 4. Signature Flavor | Mediterranean Herb, Smoky BBQ, Lemon Garlic, Spicy Harissa, Teriyaki Sesame, Sweet Chili (Main'e göre filtrelenebilir, bkz. §2.1) | Tekli — sos+baharat birleşik profil | ✅ Zorunlu |
| 5. Finish | Feta, Parmesan, Roasted Seeds, Crispy Onion, Fresh Herbs, Lime, Chili Flakes | Çoklu — max 1 ücretsiz | ⬜ Opsiyonel |

**Garden ücretlendirme kuralı:** İlk 4 seçim (Avokado hariç) ücretsizdir,
5. ve sonrası ücretlidir. **Avokado, listede kaçıncı sırada seçilirse
seçilsin her zaman ücretlidir** — premium malzeme olarak ayrı fiyatlandırılır,
ücretsiz kotaya dahil edilmez.

**Finish ücretlendirme kuralı:** İlk 1 seçim ücretsizdir, 2. ve sonrası
ücretlidir.

**"Make it Yours" ek seçenekleri** — Finish adımına alt-bileşen olarak
entegre edilir, ayrı bir adım açılmaz:
- Extra Avocado
- Extra Sauce
- Extra Crunch

"Double Main" ayrı bir mekanizma değildir — 2. adımdaki mevcut çift
porsiyon seçeneği (`mainPortion: 'double'`) bu işlevi zaten karşılar,
aynı davranış iki yerde tanımlanmaz (AGENT.md Kural #5 Bağımlılık
Disiplini).

> Garden ve Finish adımları opsiyonel olabilir ama **adımların kendisi
> atlanamaz** — kullanıcı "hiçbir şey istemiyorum" diyerek sonraki adıma
> geçebilmeli, ancak bu bilinçli bir seçim olmalı (boş state, atlanmış
> state değil).

### 2.1 Plant-Based Protein — Alt-Varyant Mekanizması (Karar #11, YENİ — v1.2)

> Kaynak: SESSION_INDEX.md Karar #11 / Açık Sorun #22 — bu sohbette kullanıcı
> onayıyla netleştirildi (2026-07-21).

**Gerekçe:** Nohut/fasulye bazlı bitkisel proteinler ayrı Main satırları
olarak listeye eklenmez (liste şişer, Falafel/Tofu ile kavramsal çakışma
olur). Bunun yerine tek bir Main kartı — **"Bitkisel Protein"** —
altında 2 alt-varyant sunulur: **Soslu Nohut** ve **Meksika Fasulyesi**
(ileride 3. bir varyant eklenebilir — kapalı bir liste değil).

**Etkileşim modeli — inline genişleme:**
```
Kullanıcı "Bitkisel Protein" kartına dokunur
  → kart YERİNDE genişler, 2 alt-seçenek (Soslu Nohut / Meksika Fasulyesi)
    kart içinde gösterilir
  → AYRI bir adım/modal AÇILMAZ (5 adımlık akış bozulmaz)
  → kullanıcı bir varyant seçer VEYA seçmeden "İlerle"ye basar
```

**Validasyon kuralı — seçim yapmayanı bloklamaz:**
```
isStepValid(2) DEĞİŞMEZ: sadece selections.main !== null bakar.
selections.mainVariant seçilip seçilmediği validasyona dahil DEĞİLDİR.

nextStep() çağrısında:
  eğer selections.main === 'plant-based-protein'
     VE selections.mainVariant === null
  ise → mainVariant otomatik olarak ilk varyanta ("chickpea-simmered" /
        Soslu Nohut) SESSİZCE atanır, kullanıcı bloklanmaz.

Gerekçe: Kural Önceliği #2 (BÜTÜNLÜK) — sipariş/mutfak verisi asla null
kalamaz, ama kullanıcı akışı da (Kural Önceliği #4, verimlilik) bir
alt-seçim yüzünden durdurulamaz. UI'da özet panelde bu durumda
"Soslu Nohut (varsayılan)" gibi bir ipucu gösterilmesi ÖNERİLİR (zorunlu
değil — UI görevi ayrı onay gerektirir).
```

**Signature Flavor filtreleme kuralı:**
```
selections.main === 'plant-based-protein' iken 4. adımda (Signature Flavor)
TÜM 6 flavor değil, sadece main.compatibleFlavorIds içinde listelenenler
gösterilir: Mediterranean Herb, Spicy Harissa, Lemon Garlic.
(Smoky BBQ, Teriyaki Sesame, Sweet Chili gizlenir — Meksika/Akdeniz
nohut-fasulye profiliyle gurme açıdan uyumsuz sayılır.)

Diğer 7 Main için bu alan tanımsızdır (undefined) → davranış DEĞİŞMEZ,
tüm 6 flavor gösterilmeye devam eder. Filtreleme SADECE main.compatibleFlavorIds
tanımlıysa devreye girer (opt-in, geriye dönük uyumlu).
```

---

## 3. STATE MAKİNESİ

### 3.1 State Şeması (GÜNCELLENDİ — v1.2)

```ts
// store/useCustomizerStore.ts — tam kontrat

interface CustomizerSelection {
  base: string | null
  main: string | null
  mainVariant: string | null    // 🆕 v1.2 — SADECE main='plant-based-protein' iken anlamlı, diğer Main'ler için her zaman null
  mainPortion: 'single' | 'double'
  garden: string[]              // max 4 ücretsiz (avokado hariç), sonrası ücretli
  signatureFlavor: string | null
  finish: string[]              // max 1 ücretsiz, sonrası ücretli
  extras: {
    extraAvocado: boolean
    extraSauce: boolean
    extraCrunch: boolean
  }
}

interface CustomizerState {
  currentStep: 1 | 2 | 3 | 4 | 5
  selections: CustomizerSelection
  maxReachedStep: 1 | 2 | 3 | 4 | 5  // guard için — ileri atlama kontrolü

  // Actions
  selectBase: (id: string) => void
  selectMain: (id: string, portion: 'single' | 'double') => void
  selectMainVariant: (variantId: string) => void   // 🆕 v1.2
  toggleGardenItem: (id: string) => void
  selectSignatureFlavor: (id: string) => void
  toggleFinishItem: (id: string) => void
  toggleExtra: (key: keyof CustomizerSelection['extras']) => void
  goToStep: (step: 1 | 2 | 3 | 4 | 5) => void   // step <= maxReachedStep+1 değilse no-op
  nextStep: () => void                           // mevcut adım validasyonunu geçmeden ilerlemez;
                                                   // 🆕 v1.2: plant-based-protein + mainVariant=null ise
                                                   // ilk varyantı sessizce atar (bkz. §2.1)
  previousStep: () => void
  reset: () => void

  // Derived (calculateTotals)
  getTotals: () => { price: number; calories: number; protein: number; carbs: number; fat: number }
  isStepValid: (step: 1 | 2 | 3 | 4 | 5) => boolean
  getAvailableFlavors: () => SignatureFlavor[]   // 🆕 v1.2 — main.compatibleFlavorIds'e göre filtreler, bkz §2.1
}
```

### 3.2 Adım Geçiş Guard'ı

```
Kural: goToStep(N) çağrısı, YALNIZCA N <= maxReachedStep + 1 ise izin verilir.
       Doğrudan URL değişikliği (app/menu/customize/[id]?step=5) ile adım
       atlanamaz — sayfa yüklenince maxReachedStep kontrolü yapılır,
       geçersizse currentStep=1'e geri döner.
```

```ts
// ❌ — guard yok
const goToStep = (step) => set({ currentStep: step })

// ✅ — guard var
const goToStep = (step) => set((state) => {
  if (step > state.maxReachedStep + 1) return state   // no-op, sessizce reddet
  return { currentStep: step }
})
```

> AGENT.md Self-Check: "Customizer adım sırası atlanabiliyor mu?" → bu guard'ın
> varlığı doğrulanır. 4 adımdan 5 adıma geçişte tip aralığı (`1|2|3|4` →
> `1|2|3|4|5`) güncellenmiştir, guard mantığının kendisi değişmemiştir.

### 3.3 Adım Validasyonu (`isStepValid`)

| Adım | Geçerli sayılma koşulu |
|---|---|
| 1 | `selections.base !== null` |
| 2 | `selections.main !== null` — **`mainVariant` bu kontrole dahil değildir (bkz. §2.1, §3.4)** |
| 3 | Her zaman geçerli (opsiyonel — 0 garden öğesi de geçerli bir seçim) |
| 4 | `selections.signatureFlavor !== null` |
| 5 | Her zaman geçerli (opsiyonel — 0 finish öğesi de geçerli bir seçim) |

`nextStep()` çağrısı, mevcut adım `isStepValid` değilse **no-op** olur ve UI'da
kullanıcıya hangi seçimin eksik olduğu gösterilir (ör. "Lütfen bir base seçin").

### 3.4 mainVariant Varsayılan Atama Kuralı (YENİ — v1.2)

```ts
// nextStep() içinde, step 2 → step 3 geçişinde ek kontrol:
const nextStep = () => set((state) => {
  if (!isStepValid(state.currentStep)) return state   // mevcut davranış değişmedi

  let selections = state.selections
  if (
    state.currentStep === 2 &&
    selections.main === 'plant-based-protein' &&
    selections.mainVariant === null
  ) {
    // Kullanıcı alt-varyant seçmeden ilerledi — sessizce ilk varyantı ata.
    // Gerekçe: §2.1 — sipariş verisi asla null kalamaz (Kural Önceliği #2, BÜTÜNLÜK),
    // ama kullanıcı akışı da bloklanmaz (Kural Önceliği #4, verimlilik).
    const firstVariant = menuData.mains
      .find(m => m.id === 'plant-based-protein')
      ?.variants?.[0]
    if (firstVariant) {
      selections = { ...selections, mainVariant: firstVariant.id }
    }
  }

  return { currentStep: state.currentStep + 1, selections, maxReachedStep: Math.max(state.maxReachedStep, state.currentStep + 1) }
})
```

> ⚠️ Diğer 6 Main için bu blok hiç tetiklenmez — `main !== 'plant-based-protein'`
> koşulu erken çıkış sağlar, mevcut davranış hiçbir şekilde etkilenmez.

---

## 4. CANLI FİYAT/KALORİ HESAPLAMA

> Kaynak: MASTER_PLAN §5.5 — kalori bilgisi zorunlu, opsiyonel değil.

```ts
// getTotals() — her seçim değişikliğinde SummaryPanel tarafından okunur

function getTotals(selections: CustomizerSelection): Totals {
  const base = menuData.bases.find(b => b.id === selections.base)

  // 🆕 v1.2 — Main değerleri artık variant-aware:
  // main.variants tanımlıysa (plant-based-protein), fiyat/kalori/protein
  // seçili mainVariant'tan okunur; tanımsızsa (diğer 6 Main) eski davranış
  // aynen sürer (main objesinin kendi price/calories/protein alanları).
  const mainDef = menuData.mains.find(m => m.id === selections.main)
  const main = mainDef?.variants
    ? mainDef.variants.find(v => v.id === selections.mainVariant) ?? mainDef.variants[0]
    : mainDef

  const gardenItems = selections.garden.map(id => menuData.gardenItems.find(g => g.id === id))

  // 🆕 v1.2 — Signature Flavor listesi Main'e göre filtrelenmiş olabilir (bkz §2.1),
  // ama seçili flavor'ın toplam hesabı DEĞİŞMEZ — filtre sadece UI seçenek listesini
  // daraltır, zaten seçilmiş bir flavor'ın fiyat/kalori mantığı aynı kalır.
  const flavor = menuData.signatureFlavors.find(f => f.id === selections.signatureFlavor)

  const finishItems = selections.finish.map(id => menuData.finishItems.find(f => f.id === id))

  // Garden ücretlendirme: avokado her zaman ücretli, diğerlerinden ilk 4'ü ücretsiz
  const avocadoSelections = gardenItems.filter(g => g.id === 'avocado')
  const otherGarden = gardenItems.filter(g => g.id !== 'avocado')
  const freeGarden = otherGarden.slice(0, 4)
  const paidGarden = [...otherGarden.slice(4), ...avocadoSelections]

  // Finish ücretlendirme: ilk 1 ücretsiz, sonrası ücretli
  const paidFinish = finishItems.slice(1)

  const extrasPrice =
    (selections.extras.extraAvocado ? menuData.extraPrices.avocado : 0) +
    (selections.extras.extraSauce ? menuData.extraPrices.sauce : 0) +
    (selections.extras.extraCrunch ? menuData.extraPrices.crunch : 0)

  return {
    price: sum(base, main, flavor, ...paidGarden, ...paidFinish) + extrasPrice,
    calories: sum(base, main, ...gardenItems, flavor, ...finishItems, key: 'calories') + extrasCalories(selections.extras),
    protein: sum(base, main, ...gardenItems, flavor, ...finishItems, key: 'protein') + extrasProtein(selections.extras),
    // carbs, fat aynı mantıkla — extras her zaman kalori/makroya dahil edilir,
    // yalnızca fiyata ücretli/ücretsiz ayrımı uygulanır
  }
}
```

> ⚠️ `base`/`main`/`signatureFlavor` seçilmemişken (`null`) `getTotals()`
> çağrılırsa ilgili değerler `0` döner — SummaryPanel `"—"` gösterir,
> `NaN`/hata değil (BSC-3 girdi doğrulama prensibiyle tutarlı).
> ⚠️ Avokado hem Garden adımında (tekli ekleme) hem "Extra Avocado" ekstrasında
> (Finish adımı alt-bölümü) seçilebilir — bu iki ayrı state alanı (`garden`
> vs `extras.extraAvocado`), fiyat hesabında çakışma olmadan ayrı ayrı toplanır.
> 🆕 v1.2: `mainVariant === null` iken (adım 2'den henüz ilerlenmediyse)
> `main` değeri `mainDef.variants[0]`'a fallback eder — bu SADECE önizleme
> içindir, gerçek sepete ekleme her zaman §3.4'teki atama sonrası kesinleşmiş
> `mainVariant` değerini kullanır.

---

## 5. VISUALPREVIEW — TEKNİK KARAR

> Kaynak: MASTER_PLAN §5.2

**Karar:** Three.js/Canvas gibi 3D çözümler MVP için gereksiz karmaşıklık ve
performans yükü getirir. **Katmanlı CSS/SVG illüstrasyon** yaklaşımı kullanılır.

### 5.1 Katman Mantığı

```
Her malzeme (Base, Main, Garden, Signature Flavor, Finish) önceden
hazırlanmış şeffaf PNG/SVG katmanı olarak z-index sırasıyla üst üste
bindirilir:

z-index sırası (alttan üste):
1. Kase (sabit, her zaman görünür)
2. Base katmanı            ← selections.base'e göre değişir
3. Main katmanı             ← selections.main'e göre değişir (🆕 v1.2: plant-based-protein
                                için mainVariant'a göre 2 ayrı katman — soslu-nohut.png / meksika-fasulyesi.png)
4. Garden katmanları         ← selections.garden her biri ayrı katman (opacity toggle)
5. Signature Flavor katmanı  ← selections.signatureFlavor'a göre değişir
6. Finish katmanları         ← selections.finish her biri ayrı katman (opacity toggle)
```

```tsx
// components/customizer/VisualPreview.tsx
// Amaç:    Seçimlere göre katmanlı görsel önizleme render eder
// Bağlı:   useCustomizerStore.selections
// Risk:    Yanlış katman gösterimi → kullanıcı yanlış ürünü sipariş eder algısı
// Dokunma: Yeni malzeme eklenirse ilgili PNG/SVG katmanı public/images/layers/'a eklenmeli.
//          🆕 v1.2: plant-based-protein için variant bazlı 2 ayrı katman dosyası gerekir
//          (public/images/layers/main-chickpea-simmered.png, main-mexican-beans.png) — bu
//          dosyalar henüz üretilmedi, açık iş olarak SESSION_INDEX.md'ye eklenmeli.

{layers.map((layer) => (
  <motion.img
    key={layer.id}
    src={layer.src}
    initial={{ opacity: 0, scale: 0.9 }}
    animate={{ opacity: layer.active ? 1 : 0, scale: layer.active ? 1 : 0.9 }}
    transition={{ duration: 0.25, ease: 'easeOut' }}
    className="absolute inset-0"
  />
))}
```

> İleride marka bütçesi büyürse gerçek ürün fotoğrafı kompozisyonuna
> (server-side image composition) geçiş planlanabilir — bu ROADMAP.md'de
> ayrı bir faz olarak not edilmeli, MVP kapsamında değil.

---

## 6. MOBİL UX

> Kaynak: MASTER_PLAN §5.2

```
Masaüstü:  Adım paneli (sol) + Özet panel (sağ, sabit) yan yana
Mobil:     Dikey akışa döner —
           - Adımlar tam ekran kart olarak sırayla gösterilir
           - Özet panel ekranın altında sabit (sticky) bir ÇEKMECE olarak durur
           - Çekmece yukarı kaydırılarak açılır (tam ekran değil, kullanıcı
             her an toplam fiyat/kaloriyi görür ama ana odak seçim adımında kalır)
```

**Çekmece durumları:**
| Durum | Görünüm |
|---|---|
| Kapalı (varsayılan) | Sadece fiyat + kalori özeti tek satır, "▲ Detay" ipucu |
| Açık | Tam özet: seçilen malzemeler, VisualPreview küçük versiyon, "Sepete Ekle" |

> 🆕 v1.2: "Bitkisel Protein" kartının inline genişlemesi (§2.1) mobilde
> tam ekran kart içinde gerçekleşir — kartın kendi yüksekliği artar, sayfa
> mobil dikey akıştan çıkmaz, ayrı bir alt-sayfa/modal açılmaz.

---

## 7. SEPETE EKLEME

```
Kural: "Sepete Ekle" butonu YALNIZCA isStepValid(5) true olduğunda aktiftir
       (yani base + main + signatureFlavor seçilmiş olmalı — Garden ve Finish
       opsiyonel olduğu için 5. adımın kendisi her zaman "valid" sayılır,
       zorunlu olan 1, 2 ve 4. adımların tamamlanmış olmasıdır).
       Tıklamada BSC-6 (race condition) koruması uygulanır — çift tıklama
       aynı ürünü iki kez eklemez (AGENT.md).
```

```ts
// handleAddToCart — CustomizerSpec §7 + AGENT.md BSC-6
const handleAddToCart = () => {
  if (isAdding.current || !isStepValid(5)) return
  isAdding.current = true
  const totals = getTotals(selections)
  addToCart({
    cartId: crypto.randomUUID(),
    bowlItem: null,
    customization: selections,   // 🆕 v1.2: mainVariant dahil — §3.4'teki atama sayesinde
                                   // plant-based-protein seçiliyse bu alan asla null değildir
    quantity: 1,
    unitPrice: totals.price,
    unitCalories: totals.calories,
  })
  reset()   // customizer state'i temizle, sonraki kullanım için hazır
  setTimeout(() => { isAdding.current = false }, 500)
}
```

---

## 8. KALİTE KONTROL — CUSTOMIZER SELF-CHECK

```
[ ] Adım geçiş guard'ı var mı?              → maxReachedStep kontrolü uygulandı mı? (§3.2)
[ ] Her adımın validasyonu tanımlı mı?       → isStepValid tüm 5 adımı kapsıyor mu? (§3.3)
[ ] Kalori/fiyat null-safe mi?               → seçim yokken 0/"—" dönüyor mu, NaN değil? (§4)
[ ] Garden/Finish ücretlendirme doğru mu?    → avokado her zaman ücretli, Garden 4/Finish 1 ücretsiz limiti uygulanıyor mu? (§4)
[ ] Extras çakışması kontrol edildi mi?      → garden.avocado ile extras.extraAvocado ayrı toplanıyor mu? (§4)
[ ] VisualPreview katman sırası doğru mu?    → z-index: kase→Base→Main→Garden→Signature Flavor→Finish (§5.1)
[ ] Mobil sticky çekmece davranışı var mı?   → açık/kapalı durumları tanımlı mı? (§6)
[ ] Sepete ekleme race condition korumalı mı? → BSC-6 uygulandı mı? (§7)
[ ] mainVariant null kalabiliyor mu?          → 🆕 v1.2: nextStep() otomatik atama yapıyor mu? (§3.4)
[ ] Signature Flavor filtresi diğer Main'leri bozuyor mu? → 🆕 v1.2: compatibleFlavorIds sadece plant-based-protein'de mi devrede? (§2.1)
```

---

*BOWLERA CUSTOMIZER_SPEC.md — v1.2 — Oturum 4 — 2026-07-21*
*Kaynak: MASTER_PLAN.md v2.1 §3.3, §5.2, §5.4, §5.5 · ARCHITECTURE.md §2.4 · AGENT.md (BSC-6)*
*Değişiklik geçmişi: v1.0 (Session 1) → v1.1 (Oturum 2, 4 adımdan 5 adıma geçiş) →
v1.2 (Oturum 4, Bitkisel Protein alt-varyant mekanizması + Signature Flavor filtreleme,
Karar #11 / Açık Sorun #22 kapanışı, bkz. SESSION_INDEX.md)*
