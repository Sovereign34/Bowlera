# Şema Değişikliği: order_history — Ödeme Alanları Eklendi

**Tarih:** 2026-08-30
**İlgili:** Açık Sorun #105 (Ödeme Altyapısı — PayTR)
**Durum:** ⚠️ TASLAK — Neon'da HENÜZ KOŞULMADI, kod HENÜZ push edilmedi
**Kaynak doğrulama:** Bu diff, kullanıcının paylaştığı GERÇEK `lib/db/schema.ts` (2026-08-30
itibarıyla güncel hali) görülerek yazıldı — önceki taslaktaki "görülmeden yazıldı" uyarısı
artık geçerli değil, sadece DB client import yolu düzeltmesi (`@/lib/db/client`) ayrıca
route dosyalarına işlendi.

## Gerekçe

Gel Al ve Kurye siparişlerinde nakit+online hibrit ödeme seçeneği eklendiği için
`order_history` tablosunun hangi siparişin nasıl/ne durumda ödendiğini bilmesi gerekiyor.
**Kritik kısıtlama (bkz. Kritik Kararlar tablosu):** ham kart verisi (numara/CVV) bu şemaya
ASLA girmez — sadece PayTR'ın döndürdüğü işlem referansı saklanır.

## `lib/db/schema.ts` Diff — `orderHistory` tablosuna eklenecek 3 alan

Mevcut tabloya (satır 141-157) `customerNotes` alanından SONRA eklenir:

```typescript
export const orderHistory = pgTable("order_history", {
  id: uuid("id").defaultRandom().primaryKey(),
  customerPhone: text("customer_phone").notNull(),
  channel: text("channel").notNull(), // "dine-in" | "pickup"
  items: jsonb("items").notNull(),
  totalPrice: numeric("total_price", { precision: 10, scale: 2 }).notNull(),
  orderedAt: timestamp("ordered_at", { withTimezone: true }).defaultNow().notNull(),
  status: text("status").notNull().default("pending"),
  tableNumber: text("table_number"),
  customerNotes: text("customer_notes"),

  // 🆕 [2026-08-30, #105] Ödeme altyapısı (PayTR). Postgres enum KULLANILMAZ (role/channel/
  // status pattern'iyle tutarlı), kod tarafında union ile sıkı kontrol edilir.
  // Şema notu: docs/schema-changes/20260830000000_order_history_payment_alanlari_eklendi.md
  // ⚠️ KRİTİK: Bu alanlar SADECE PayTR'ın döndürdüğü işlem referansını ve durumu tutar —
  // ham kart verisi (numara/CVV/son kullanma) BU TABLOYA VEYA BAŞKA HİÇBİR TABLOYA
  // ASLA YAZILMAZ (PCI-DSS SAQ A-EP kapsamında kalma kararı, bkz. Kritik Kararlar).
  paymentMethod: text("payment_method").notNull().default("nakit"), // "nakit" | "online"
  paymentStatus: text("payment_status").notNull().default("bekliyor"), // "bekliyor"|"odendi"|"basarisiz"|"iade_edildi"
  paymentProviderRef: text("payment_provider_ref"), // nullable — PayTR merchant_oid, ham kart verisi DEĞİL
})
```

**Not:** `paymentMethod='nakit'` olan siparişlerde `paymentStatus` genelde `'bekliyor'` kalır
(ödeme teslimatta alınır, sistem bunu otomatik takip etmez) — bilinçli tasarım kararı, nakit
siparişler için ayrı bir "teslimatta tahsil edildi" mekanizması bu kapsamda DEĞİL.

## `OrderHistoryRow`/`NewOrderHistoryRow` Tipleri

Değişiklik gerekmiyor — bu tipler `typeof orderHistory.$inferSelect`/`$inferInsert` ile
otomatik türetiliyor (satır 159-160), şema değişince kendiliğinden güncellenir.

## Bağlı Dosyalar (Bağımlılık Disiplini gereği taranmalı)

- `app/api/payment/paytr/init/route.ts` (YENİ) — bu turda üretildi
- `app/api/payment/paytr/callback/route.ts` (YENİ) — bu turda üretildi
- `lib/paytr.ts` (YENİ, önceki turda üretildi) — bu şemaya doğrudan yazmıyor, sadece
  route'lar üzerinden dolaylı bağlı
- Checkout akışı (mevcut sipariş oluşturma kodu — bu turda GÖRÜLMEDİ) — `paymentMethod`
  alanının varsayılan `'nakit'` değeriyle YENİ siparişleri kırmadan çalışması bekleniyor
  (geriye dönük uyumlu), ama checkout'un "ödeme şekli" seçimini bu alana YAZDIĞI kod
  HENÜZ YAZILMADI — ayrı bir görev (bkz. Açık Sorun #105 kalan kapsam)

## Migration SQL (TASLAK — Neon SQL Editor'de KOŞULMADI)

```sql
ALTER TABLE order_history
  ADD COLUMN payment_method text NOT NULL DEFAULT 'nakit',
  ADD COLUMN payment_status text NOT NULL DEFAULT 'bekliyor',
  ADD COLUMN payment_provider_ref text;
```

## Doğrulama Adımları (koşulduktan SONRA)

1. Neon Tables görünümünde 3 yeni sütunun göründüğünü doğrula
2. Mevcut satırların `payment_method='nakit'`, `payment_status='bekliyor'` ile dolduğunu kontrol et (geriye dönük uyumluluk — mevcut `order_history` satırları için KRİTİK, aksi halde `NOT NULL` kısıtı migration'ı başarısız kılar)
3. Drizzle tip senkronunu doğrula (proje `drizzle-kit` kullanıyorsa ilgili komutla)
