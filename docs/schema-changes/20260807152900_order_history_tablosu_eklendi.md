## Session: 10 — 2026-08-07

## Açıklama
Kasa paneli (masaya sipariş + gel-al birleşik yönetim) mimarisinin bir parçası olarak,
tamamlanan siparişlerin sayaç/geçmiş kaydı için yeni bir tablo ekleniyor: `order_history`.
POS sistemi gerçek sipariş/ödeme kaydını zaten tutacağı için Bowlera tarafında ayrı bir
`orders` tablosu KURULMUYOR — bu tablo yalnızca sadakat/geçmiş amaçlı özet kayıttır.

Kimlik eşleşmesi `consentRegistrations.phone` ile düz `text` alan eşleşmesi olarak
kuruldu (katı FK constraint YOK — `consentRegistrations` upsert edilebilir olduğu için
kırılganlık yaratmaması amacıyla). Kullanıcıya arayüzde hitap her zaman
`consentRegistrations.name` üzerinden yapılacak, telefon numarası ekranda gösterilmeyecek
(Açık Sorun #59 ile bağlantılı — kayıt sonrası kullanıcı adı gösterimi).

Kayıt granülerliği: sipariş-bazlı TEK SATIR (ürün-bazlı ayrı satır değil) — gerekçe,
"kaç kez sipariş verildi" sayacının satır sayısıyla doğrudan eşleşmesi (2 kase + 1 içecek
tek ziyaretse tek satır olmalı, 3 değil). Ürün detayları `items` alanında JSONB olarak
tutulur: `[{ menuNumber, price, quantity }, ...]`.

### ÖNCE
```ts
// lib/db/schema.ts — sadece users + consentRegistrations tabloları vardı
// Sipariş geçmişi/sayaç kaydı için hiçbir tablo yoktu.
```

### SONRA
```ts
// lib/db/schema.ts — eklenecek tablo
// Amaç:    Tamamlanan gel-al/masaya siparişlerinin sayaç+geçmiş kaydı (sadakat zemini)
// Bağlı:   consentRegistrations.phone (join ile — düz eşleşme, FK constraint YOK çünkü
//          consentRegistrations upsert/güncellenebilir, katı FK kırılganlık yaratır)
// Risk:    phone eşleşmesi bozulursa sipariş geçmişi yanlış kullanıcıya görünür
// Dokunma: consentRegistrations.phone değişirse (şimdilik değişmiyor, ileride olursa)
//          bu tablo etkilenir

export const orderHistory = pgTable("order_history", {
  id: uuid("id").defaultRandom().primaryKey(),
  customerPhone: text("customer_phone").notNull(),
  channel: text("channel").notNull(), // "dine-in" | "pickup"
  items: jsonb("items").notNull(), // [{ menuNumber, price, quantity }]
  totalPrice: numeric("total_price", { precision: 10, scale: 2 }).notNull(),
  orderedAt: timestamp("ordered_at", { withTimezone: true }).defaultNow().notNull(),
})

export type OrderHistoryRow = typeof orderHistory.$inferSelect
export type NewOrderHistoryRow = typeof orderHistory.$inferInsert
```

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` — yeni `orderHistory` tablo tanımı eklenir
- `ARCHITECTURE.md` §3 (Veri Modeli) — yeni tablo dokümante edilmeli (bu dosya hâlâ
  Session 4 seviyesinde, `consentRegistrations` de dahil güncel değil — ayrı, daha
  kapsamlı bir güncelleme gerekiyor, bu notun kapsamı dışında)
- Kasa paneli API route'ları (henüz yazılmadı) — `order_history`'ye INSERT yapacak
- `docs/schema-changes/` klasörü — bu not buraya taşınır (kullanıcı repo'ya taşır)

### GERİ ALMA
1. Migration henüz koşulmadı — bu aşamada geri alma "migration'ı hiç uygulamama" ile eşdeğer
2. Migration koşulduktan sonra geri alma gerekirse: `npx drizzle-kit drop` ile tablo
   şemadan çıkarılır, ardından `npx drizzle-kit push` ile senkronize edilir
3. ⚠️ Tablo koşulduktan sonra veri birikirse, drop işlemi o veriyi KALICI OLARAK SİLER —
   geri alma öncesi kullanıcı onayı zorunlu (AGENT.md Kural #3)
