## Session: [devam, 2026-08-09] — Personel Sipariş Paneli (#62) + Masa Numarası (#70)
## Açıklama:
`order_history` tablosu şu ana kadar sadece TAMAMLANMIŞ siparişlerin geçmiş/sadakat kaydı
olarak tasarlanmıştı (durum yoktu). Personel Sipariş Paneli'nin (Masaya + Gel Al, iki sekme,
real-time polling) çalışabilmesi için bu tablo "aktif kuyruk" olarak da kullanılacak —
sipariş anında satır oluşup `status` alanı personel tarafından güncellenecek, tamamlanan
kayıt aynı satırda kalıcı geçmiş olarak duracak (ayrı "aktif sipariş" tablosu YOK — Bağımlılık
Disiplini: senkron riski taşıyan iki tablo yerine tek tablo + durum makinesi tercih edildi).

3 kolon ekleniyor:
- `status` — durum makinesi. Masaya: `pending→preparing→ready→served` / Gel Al:
  `pending→confirmed`/`rejected`. Postgres enum KULLANILMAZ (projede `role`/`channel` ile
  aynı pattern — düz `text`, kod tarafında union ile sıkı kontrol, DB seviyesinde CHECK
  constraint yok, serbest string riski bilinçli kabul edildi).
- `table_number` — SADECE `channel === "dine-in"` için anlamlı, nullable. Tip kararı (#70):
  `text` — masa adları sayısal olmayabilir ("Bahçe 3", "Teras 2" gibi), projede enum yerine
  düz text tercih ediliyor (`role`/`channel` ile tutarlı).
- `customer_notes` — nullable, serbest metin.

**Index kararı (#70):** `status` üzerine evet (panel `WHERE status = 'pending' AND channel = ...`
şeklinde aktif kuyruğu sorgulayacak), `table_number` üzerine hayır (sadece görüntülenecek,
filtrelenmeyecek).

### ÖNCE
```ts
export const orderHistory = pgTable("order_history", {
  id: uuid("id").defaultRandom().primaryKey(),
  customerPhone: text("customer_phone").notNull(),
  channel: text("channel").notNull(), // "dine-in" | "pickup"
  items: jsonb("items").notNull(),
  totalPrice: numeric("total_price", { precision: 10, scale: 2 }).notNull(),
  orderedAt: timestamp("ordered_at", { withTimezone: true }).defaultNow().notNull(),
})
```

### SONRA
```ts
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
})
```

### MIGRATION SQL (Neon'da elle koşulacak)
```sql
ALTER TABLE order_history
  ADD COLUMN status text NOT NULL DEFAULT 'pending',
  ADD COLUMN table_number text,
  ADD COLUMN customer_notes text;

CREATE INDEX idx_order_history_status ON order_history (status);
```

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` (bu şema notuyla birlikte tam dosya artifact olarak üretildi)
- `types/index.ts` — `OrderHistoryEntry` tipi eklenecek (bir sonraki adım, panel kodlanırken)
- `ARCHITECTURE.md` §2.9a / §4.1 — bir sonraki turda güncellenmeli (migration koşulduktan sonra)
- SESSION_INDEX.md — Açık Sorun #70 KAPANACAK, #62'nin "kalan" notu güncellenecek

### GERİ ALMA
```sql
DROP INDEX IF EXISTS idx_order_history_status;
ALTER TABLE order_history
  DROP COLUMN status,
  DROP COLUMN table_number,
  DROP COLUMN customer_notes;
```
Var olan satırlar (varsa) `status`/`table_number`/`customer_notes` olmadan zaten çalışıyordu —
geri alma veri kaybına yol açmaz (bu 3 kolon hiçbir yerde henüz okunmuyor/yazılmıyor).
