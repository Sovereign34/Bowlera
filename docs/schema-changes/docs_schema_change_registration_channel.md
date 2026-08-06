# Şema Değişiklik Notu
`docs/schema-changes/20260806120000_registration_channel_eklendi.md`

**Tarih:** 2026-08-06 (Session 7)
**Değişiklik:** `types/index.ts`'e yeni tip eklendi — `RegistrationChannel`
**Kapsam:** SADECE ekleme, mevcut tip değişmedi

## Ne değişti
```ts
export type RegistrationChannel = "masaya-siparis" | "gel-al" | "online-platform"
```
`FulfillmentChannel` (`"pickup" | "dine-in"`) **DEĞİŞMEDİ** — geriye dönük tam uyumlu.

## Neden ayrı tip (birleştirilmedi)
- `FulfillmentChannel`, sadece "kendi sepetimizin" teslimat şeklini tanımlıyor (DB'ye,
  localStorage'a, mevcut testlere yazılı — dokunmak riskli migration olurdu).
- "Online Platformlarda Sipariş" sepete hiç girmiyor (kullanıcı Yemeksepeti/Getir/Trendyol'a
  yönlendiriliyor) — bu, `FulfillmentChannel`'in kapsamına concept olarak girmiyor
  (bkz. `types/index.ts` satır ~109'daki mevcut not: marketplace kanalları bilinçli hariç
  tutulmuştu).

## Eşleme (kayıt formu → mevcut sepet state'i)
| RegistrationChannel | Sonuç |
|---|---|
| `masaya-siparis` | `useCartStore.fulfillmentChannel = "dine-in"` (ön-dolgu), customizer'a girilir |
| `gel-al` | `useCartStore.fulfillmentChannel = "pickup"` (ön-dolgu), customizer'a girilir |
| `online-platform` | Sepete girilmez, marketplace'e yönlendirme yapılır |

## Etkilenen dosyalar
- `types/index.ts` — tip eklendi ✅ (bu tur)
- Kayıt formu component'i — henüz yazılmadı, `RegistrationChannel` burada kullanılacak
- `FulfillmentGate.tsx` / `/siparis` — DEĞİŞMEDİ, kanal zaten seçili gelecek ama gate kalıyor
  (kullanıcı onayı: "Kayıt sonrası seçim ön-tercih, /siparis'teki gate son onay olarak kalır")

## Geri alınabilirlik
Tam geri alınabilir — sadece yeni bir type eklendi, hiçbir mevcut alan/tip değiştirilmedi
veya silinmedi. Kullanılmazsa etkisizdir.
