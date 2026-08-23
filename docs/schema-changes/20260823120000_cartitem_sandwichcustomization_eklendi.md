# Şema Değişikliği — CartItem.sandwichCustomization eklendi

**Tarih:** 2026-08-23
**Görev:** Sandviç akışı — Sepete Ekle entegrasyonu (#S6)
**Onay:** Kullanıcı onaylı (bu turda, "Evet")

## Değişiklik
`types/index.ts` → `CartItem` tipine `sandwichCustomization?: SandwichCustomization` eklendi.

## Neden union DEĞİL, ayrı alan
`customization: CustomizerSelection` (Bowl'a özgü şekil) DEĞİŞTİRİLMEDİ. Kural #5 (izolasyon) gereği
yeni, tamamen opsiyonel bir alan eklendi. Sonuç: CartDrawer.tsx, CartBadge.tsx, checkout — mevcut hiçbir
Bowl tüketicisi etkilenmedi, tip daraltma/narrowing eklemeleri gerekmedi.

## Ayırt edici alan
Bowl kalemi: `customization` dolu, `sandwichCustomization` undefined.
Sandviç kalemi: `sandwichCustomization` dolu, `customization` undefined.
⚠️ İkisinin aynı anda dolu olmasını engelleyen runtime validasyon YOK — Açık Sorun (aşağıda).

## DB etkisi
YOK — bu alan sadece client-side sepet state'inde (`persist` ile localStorage `bowlera-cart`).
Sipariş DB'ye yazıldığında (order_history.items, jsonb) mevcut `OrderItemSummary` şekli kullanılıyor.

## Açık Sorun (bloklayıcı DEĞİL, checkout'a ulaşmadan çözülmeli)
`OrderItemSummary.menuNumber`, "BowlItem.id ile eşleşir" varsayımına dayanıyor. Sandviç kalemlerinin
`BowlItem.id`'si yok — checkout/order history akışına sandviç ulaştığında bu alan yeniden ele alınmalı.
Personel Sipariş Paneli (#62) şu an sandviç kalemini varsaymıyor. SESSION_INDEX.md'ye açık madde
olarak düşüldü.
