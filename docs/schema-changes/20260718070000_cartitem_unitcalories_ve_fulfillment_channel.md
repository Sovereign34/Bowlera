## Session: 4 — 2026-07-18
## Açıklama: (1) CartItem.unitCalorie7s yazım hatası unitCalories olarak düzeltildi.
## (2) Sepete teslimat kanalı eklendi — ürün (CartItem) bazlı DEĞİL, sepet/store seviyesinde
## tek bir alan (fulfillmentChannel) olarak. Kanal: "pickup" (Gel-Al) | "dine-in" (Masaya Servis).
## Yemeksepeti/Getir/Trendyol bilinçli olarak bu enum'a DAHİL EDİLMEDİ — o akışta kullanıcı
## Bowlera sitesinden ayrılıp marketplace uygulamasına yönlendiriliyor, sepet tamamlanmıyor;
## bu nedenle ayrı bir UI bloğu (link/buton) olacak, cart state'iyle ilgisi yok.
## İleride kendi kurye/teslimat sistemi kurulursa "delivery" enum'a eklenecek — CartItem şemasında
## değişiklik gerekmeyecek, sadece FulfillmentChannel union'ına yeni değer eklenecek.

### ÖNCE
```ts
export type CartItem = {
  cartId: string
  bowlItem: BowlItem | null
  customization?: CustomizerSelection
  quantity: number
  unitPrice: number
  unitCalorie7s: number
}

type CartState = {
  cart: CartItem[]
  addToCart: (item: CartItem) => void
  removeFromCart: (cartId: string) => void
  clearCart: () => void
}
```

### SONRA
```ts
export type FulfillmentChannel = "pickup" | "dine-in"
// NOT: "delivery" (kendi kurye) ileride buraya eklenecek — CartItem şeması etkilenmez.

export type CartItem = {
  cartId: string
  bowlItem: BowlItem | null
  customization?: CustomizerSelection
  quantity: number
  unitPrice: number
  unitCalories: number
}

type CartState = {
  cart: CartItem[]
  fulfillmentChannel: FulfillmentChannel | null
  addToCart: (item: CartItem) => void
  removeFromCart: (cartId: string) => void
  setFulfillmentChannel: (channel: FulfillmentChannel) => void
  clearCart: () => void
}
```

### ETKİLENEN DOSYALAR
- `types/index.ts` — `CartItem.unitCalories` düzeltmesi + yeni `FulfillmentChannel` tipi
- `store/useCartStore.ts` — `fulfillmentChannel` state + `setFulfillmentChannel` action eklendi, persist zaten tüm store'u kapsadığı için ek konfigürasyon gerekmedi
- ⚠️ `unitCalorie7s` alanını okuyan/yazan başka dosya varsa (örn. `CartDrawer.tsx`, `SummaryPanel.tsx`, `AddToCartButton.tsx`) TypeScript derlemesi kırılacak — bu dosyalar henüz görülmedi, push öncesi `unitCalorie7s` için proje genelinde arama yapılmalı
- Henüz yazılmamış: kanal seçim UI bileşeni (muhtemelen `app/siparis/page.tsx` veya sepet/checkout akışında) — bu sohbette kapsam dışı, ayrı görev

### GERİ ALMA
1. `types/index.ts`'te `unitCalories` → `unitCalorie7s`, `FulfillmentChannel` tipini kaldır
2. `store/useCartStore.ts`'te `fulfillmentChannel` state ve `setFulfillmentChannel` action'ı kaldır
3. localStorage'daki `bowlera-cart` anahtarını temizlemek gerekebilir (persist edilen state şekli değişti — eski/yeni şema karışmasın diye kullanıcı tarayıcısında `localStorage.removeItem('bowlera-cart')` önerilir, opsiyonel)
