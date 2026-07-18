## Session: 2 — 2026-07-18
## Açıklama: "Kâseni Yarat" özelleştirme akışı 4 adımdan 5 adıma çıkarıldı.
Toppings adımı ikiye bölündü (Garden + Finish), Sos adımı "Signature Flavor"
(sos+baharat birleşik lezzet profili) olarak yeniden kavramsallaştırıldı,
Protein adımı "Main" olarak yeniden adlandırıldı. Tüm adım/malzeme isimleri
bilinçli bir marka kararıyla İngilizce'ye geçirildi (istisna — CONTENT_GUIDE.md
§1 Türkçe marka sesi kuralı sitenin geri kalanında geçerliliğini korur, bu
yalnızca customizer adım/malzeme isimlerini kapsar). Karar kullanıcı onayıyla
alınmıştır (3 turlu netleştirme: adım sayısı → dil → ücretlendirme kuralları).

### ÖNCE

```ts
interface CustomizerState {
  currentStep: 1 | 2 | 3 | 4
  selections: {
    base: string | null
    protein: string | null
    proteinPortion: 'single' | 'double'
    toppings: string[]          // max 4 ücretsiz, sonrası ücretli
    sauce: string | null
  }
  maxReachedStep: 1 | 2 | 3 | 4
}
```

Adım tablosu: 1. Taban → 2. Protein → 3. Toppings (max 4 ücretsiz) → 4. Sos

### SONRA

```ts
interface CustomizerState {
  currentStep: 1 | 2 | 3 | 4 | 5
  selections: {
    base: string | null
    main: string | null
    mainPortion: 'single' | 'double'
    garden: string[]              // max 4 ücretsiz (avokado her zaman ücretli), sonrası ücretli
    signatureFlavor: string | null
    finish: string[]              // max 1 ücretsiz, sonrası ücretli
    extras: {
      extraAvocado: boolean
      extraSauce: boolean
      extraCrunch: boolean
    }
  }
  maxReachedStep: 1 | 2 | 3 | 4 | 5
}
```

Adım tablosu: 1. Base → 2. Main → 3. Garden (max 4 ücretsiz + avokado her
zaman ücretli) → 4. Signature Flavor → 5. Finish (max 1 ücretsiz) — "Make it
Yours" ek seçenekleri (Extra Avocado / Extra Sauce / Extra Crunch) Finish
adımına alt-bileşen olarak entegre edildi, ayrı adım açılmadı. "Double Main"
için ayrı mekanizma açılmadı — mevcut `mainPortion: 'double'` yeniden
kullanıldı (Kural #5 Bağımlılık Disiplini: aynı işlev iki yerde tanımlanmaz).

### ETKİLENEN DOSYALAR
- `CORE.md` §8 Mimari Varsayımlar (4 adım → 5 adım satırı)
- `MASTER_PLAN.md` §3.3 (adım tablosu), §5.2 (VisualPreview katman sırası), §8 (Oturum 3 açıklaması)
- `CUSTOMIZER_SPEC.md` — tüm dosya (§1-8, state şeması, validasyon, getTotals, VisualPreview z-index, self-check)
- `SESSION_INDEX.md` — kritik teknik karar olarak eklendi
- İleride (Oturum 3 kapsamında, henüz yazılmadı): `store/useCustomizerStore.ts`, `types/index.ts` (CustomizerSelection tipi), `lib/menu-data.json` (garden/signatureFlavor/finish veri kategorileri)

### GERİ ALMA
1. `CUSTOMIZER_SPEC.md`, `MASTER_PLAN.md` §3.3/§5.2/§8, `CORE.md` §8'i bu
   notun "ÖNCE" bölümündeki 4 adımlı yapıya döndür.
2. Bu dosyayı `docs/schema-changes/` altında arşivde tut, silme — geri alma
   kararının gerekçesi ileride sorulabilir.
3. Oturum 3 henüz başlamadığı için kod tarafında geri alınacak bir dosya yok;
   yalnızca kanon dokümanlar geri alınır.
