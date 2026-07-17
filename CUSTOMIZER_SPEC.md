# BOWLERA — CUSTOMIZER_SPEC.md
> Bu belge sitenin en kritik ekranı olan "Kâseni Yarat" akışının tam kontratıdır.
> State makinesi, adım validasyonu, VisualPreview mantığı ve mobil UX burada tanımlanır.
> Bu akışa dokunan her görev önce bu dosyayı okumak zorundadır.
> Kaynak: MASTER_PLAN.md §3.3 (Kâse Özelleştirme Akışı) + §5.2 (Bileşen Yapısı) + §5.4 (Zustand)

---

## 1. AKIŞ FELSEFESİ

Doğrusal, bilişsel yükü azaltan **4 adım**. Kullanıcı önceki adımı tamamlamadan
sonrakine geçemez — CAVA'nın adım adım görselleştirilmiş sihirbaz UX'i referans
alınmıştır (MASTER_PLAN §2). Sağ tarafta (masaüstü) veya alt sticky çekmecede
(mobil) **sabit özet panel** her zaman görünür: canlı kase görseli, anlık
kalori/makro toplamı (ZORUNLU, her zaman görünür), güncel fiyat, "Sepete Ekle" butonu.

---

## 2. ADIM TANIMLARI

> Kaynak: MASTER_PLAN §3.3

| Adım | İçerik | Seçim Tipi | Zorunlu mu |
|---|---|---|---|
| 1. Taban | Kinoa, esmer pirinç, Akdeniz yeşillikleri, miks | Tekli | ✅ Zorunlu |
| 2. Protein | Somon, ızgara tavuk, fırın tofu, füme antrikot | Tekli/çift porsiyon | ✅ Zorunlu |
| 3. Toppings | Edamame, avokado, havuç turşusu, mor lahana | Max 4 ücretsiz, ekstra ücretli | ⬜ Opsiyonel (0-4 ücretsiz, 4+ ücretli) |
| 4. Sos | Acı mayonez, teriyaki, zeytinyağı-limon, tahin | Tekli | ✅ Zorunlu |

> Toppings adımı tek adım içinde opsiyonel olabilir ama **adımın kendisi atlanamaz** —
> kullanıcı "Toppings istemiyorum" diyerek 4. adıma geçebilmeli, ancak bu bilinçli
> bir seçim olmalı (boş state, atlanmış state değil).

---

## 3. STATE MAKİNESİ

### 3.1 State Şeması

```ts
// store/useCustomizerStore.ts — tam kontrat

interface CustomizerState {
  currentStep: 1 | 2 | 3 | 4
  selections: {
    base: string | null
    protein: string | null
    proteinPortion: 'single' | 'double'
    toppings: string[]          // max 4 ücretsiz, sonrası ekstra ücretli
    sauce: string | null
  }
  maxReachedStep: 1 | 2 | 3 | 4  // guard için — ileri atlama kontrolü

  // Actions
  selectBase: (id: string) => void
  selectProtein: (id: string, portion: 'single' | 'double') => void
  toggleTopping: (id: string) => void
  selectSauce: (id: string) => void
  goToStep: (step: 1 | 2 | 3 | 4) => void       // step <= maxReachedStep+1 değilse no-op
  nextStep: () => void                           // mevcut adım validasyonunu geçmeden ilerlemez
  previousStep: () => void
  reset: () => void

  // Derived (calculateTotals)
  getTotals: () => { price: number; calories: number; protein: number; carbs: number; fat: number }
  isStepValid: (step: 1 | 2 | 3 | 4) => boolean
}
```

### 3.2 Adım Geçiş Guard'ı

```
Kural: goToStep(N) çağrısı, YALNIZCA N <= maxReachedStep + 1 ise izin verilir.
       Doğrudan URL değişikliği (app/menu/customize/[id]?step=4) ile adım
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
> varlığı doğrulanır.

### 3.3 Adım Validasyonu (`isStepValid`)

| Adım | Geçerli sayılma koşulu |
|---|---|
| 1 | `selections.base !== null` |
| 2 | `selections.protein !== null` |
| 3 | Her zaman geçerli (opsiyonel — 0 topping de geçerli bir seçim) |
| 4 | `selections.sauce !== null` |

`nextStep()` çağrısı, mevcut adım `isStepValid` değilse **no-op** olur ve UI'da
kullanıcıya hangi seçimin eksik olduğu gösterilir (ör. "Lütfen bir taban seçin").

---

## 4. CANLI FİYAT/KALORİ HESAPLAMA

> Kaynak: MASTER_PLAN §5.5 — kalori bilgisi zorunlu, opsiyonel değil.

```ts
// getTotals() — her seçim değişikliğinde SummaryPanel tarafından okunur

function getTotals(selections: CustomizerSelection): Totals {
  const base = menuData.bases.find(b => b.id === selections.base)
  const protein = menuData.proteins.find(p => p.id === selections.protein)
  const toppings = selections.toppings.map(id => menuData.toppings.find(t => t.id === id))
  const sauce = menuData.sauces.find(s => s.id === selections.sauce)

  const freeToppings = toppings.slice(0, 4)
  const extraToppings = toppings.slice(4)   // 4. sonrası ücretli

  return {
    price: sum(base, protein, sauce, extraToppings /* freeToppings fiyata dahil değil */),
    calories: sum(base, protein, ...toppings, sauce, key: 'calories'),
    protein: sum(base, protein, ...toppings, sauce, key: 'protein'),
    // carbs, fat aynı mantıkla
  }
}
```

> ⚠️ `base`/`protein`/`sauce` seçilmemişken (`null`) `getTotals()` çağrılırsa
> ilgili değerler `0` döner — SummaryPanel `"—"` gösterir, `NaN`/hata değil
> (BSC-3 girdi doğrulama prensibiyle tutarlı).

---

## 5. VISUALPREVIEW — TEKNİK KARAR

> Kaynak: MASTER_PLAN §5.2

**Karar:** Three.js/Canvas gibi 3D çözümler MVP için gereksiz karmaşıklık ve
performans yükü getirir. **Katmanlı CSS/SVG illüstrasyon** yaklaşımı kullanılır.

### 5.1 Katman Mantığı

```
Her malzeme (taban, protein, topping, sos) önceden hazırlanmış şeffaf
PNG/SVG katmanı olarak z-index sırasıyla üst üste bindirilir:

z-index sırası (alttan üste):
1. Kase (sabit, her zaman görünür)
2. Taban katmanı     ← selections.base'e göre değişir
3. Protein katmanı    ← selections.protein'e göre değişir
4. Topping katmanları ← selections.toppings her biri ayrı katman (opacity toggle)
5. Sos katmanı        ← selections.sauce'e göre değişir
```

```tsx
// components/customizer/VisualPreview.tsx
// Amaç:    Seçimlere göre katmanlı görsel önizleme render eder
// Bağlı:   useCustomizerStore.selections
// Risk:    Yanlış katman gösterimi → kullanıcı yanlış ürünü sipariş eder algısı
// Dokunma: Yeni malzeme eklenirse ilgili PNG/SVG katmanı public/images/layers/'a eklenmeli

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

---

## 7. SEPETE EKLEME

```
Kural: "Sepete Ekle" butonu YALNIZCA isStepValid(4) true olduğunda aktiftir
       (yani base + protein + sauce seçilmiş olmalı).
       Tıklamada BSC-6 (race condition) koruması uygulanır — çift tıklama
       aynı ürünü iki kez eklemez (AGENT.md).
```

```ts
// handleAddToCart — CustomizerSpec §7 + AGENT.md BSC-6
const handleAddToCart = () => {
  if (isAdding.current || !isStepValid(4)) return
  isAdding.current = true
  const totals = getTotals(selections)
  addToCart({
    cartId: crypto.randomUUID(),
    bowlItem: null,
    customization: selections,
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
[ ] Her adımın validasyonu tanımlı mı?       → isStepValid tüm adımları kapsıyor mu? (§3.3)
[ ] Kalori/fiyat null-safe mi?               → seçim yokken 0/"—" dönüyor mu, NaN değil? (§4)
[ ] VisualPreview katman sırası doğru mu?    → z-index: kase→taban→protein→topping→sos (§5.1)
[ ] Mobil sticky çekmece davranışı var mı?   → açık/kapalı durumları tanımlı mı? (§6)
[ ] Sepete ekleme race condition korumalı mı? → BSC-6 uygulandı mı? (§7)
```

---

*BOWLERA CUSTOMIZER_SPEC.md — v1.0 — Session 1 — 2026-07-17*
*Kaynak: MASTER_PLAN.md §3.3, §5.2, §5.4, §5.5 · ARCHITECTURE.md §2.4 · AGENT.md (BSC-6)*
