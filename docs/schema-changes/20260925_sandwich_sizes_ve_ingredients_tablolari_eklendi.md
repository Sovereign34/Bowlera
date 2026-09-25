## Session: 32. sohbet — 2026-09-25
## Açıklama:
"Kâseni Yarat" (customizer-data.ts) ve "Sandviçini Oluştur" (sandwich-data.json — hiç
sağlanmamıştı, SANDWICH_SPEC.md §8 S1) akışlarının malzeme listelerini statik dosyalardan
admin-yönetimli DB tablolarına taşımak için iki yeni tablo eklendi: `ingredients` (Bowl +
Sandviç ortak, `productType`/`slot` ayrımıyla) ve `sandwich_sizes` (sandviç boyu, admin
panelden manuel yönetilecek — kullanıcı kararı, bu sohbet).

Kullanıcı onaylı kararlar (bu sohbet):
1. Malzeme görselleri SADECE iş verisi (fiyat/kalori/isim/görsel) olarak admin'e taşınıyor —
   VisualPreview'daki şeffaf PNG/SVG katman illüstrasyonları (CUSTOMIZER_SPEC.md §5,
   SANDWICH_SPEC.md §5) bu tabloya DAHİL DEĞİL, tasarımcı elinden gelen ayrı bir varlık
   olmaya devam ediyor. (Seçenek A — CUSTOMIZER_SPEC.md §5'teki "gerçek fotoğraf kompozisyonu
   MVP'de değil" kararı korunuyor.)
2. Admin panelde TEK "Malzemeler" tablosu/CRUD kaynağı — Bowl ve Sandviç ayrı sekme/filtre
   olarak aynı tablodan beslenecek (SANDWICH_SPEC.md §0'daki izolasyon ilkesi SADECE runtime
   store/route/component katmanı için geçerli, admin veri kaynağı bu ilkenin kapsamı dışında).
3. Sandviç Veggies ücretsiz kota sayısı = 4 (Bowl Garden ile aynı, SANDWICH_SPEC.md §8 S2
   KAPANDI) — kod tarafında ayrı `FREE_VEGGIE_QUOTA` sabiti olarak tutulacak, DB'ye taşınmadı.
4. Sandviç boyu (15cm/30cm gibi) admin panelden manuel eklenebilir/düzenlenebilir bir liste
   olacak — sabit union DEĞİL.

### ÖNCE
`lib/db/schema.ts` içinde bu iki tablo yoktu. Customizer/Sandviç malzemeleri hiç DB'de
değildi — Bowl tarafı `customizer-data.ts` (statik), Sandviç tarafı ise SANDWICH_SPEC.md §8
S1 gereği HİÇ üretilmemişti (bloklayıcı açık soru).

### SONRA
```ts
export const sandwichSizes = pgTable("sandwich_sizes", {
  id: text("id").primaryKey(),
  name: text("name").notNull(),
  priceModifier: integer("price_modifier").notNull().default(0),
  sortOrder: integer("sort_order").notNull().default(0),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
})

export const ingredients = pgTable("ingredients", {
  id: text("id").primaryKey(),
  productType: text("product_type").notNull(),       // "bowl" | "sandwich"
  slot: text("slot").notNull(),                        // bkz. schema.ts yorumu
  name: text("name").notNull(),
  image: text("image").notNull(),
  price: integer("price").notNull(),
  calories: integer("calories").notNull(),
  protein: integer("protein").notNull(),
  carbs: integer("carbs"),
  fat: integer("fat"),
  allergens: text("allergens").array().notNull().default([]),
  parentIngredientId: text("parent_ingredient_id").references((): AnyPgColumn => ingredients.id),
  isAlwaysPaid: boolean("is_always_paid").notNull().default(false),
  compatibleFlavorIds: text("compatible_flavor_ids").array(),
  sortOrder: integer("sort_order").notNull().default(0),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
  updatedAt: timestamp("updated_at", { withTimezone: true }).defaultNow().notNull(),
})
```
Tam dosya: bu sohbette üretilen güncel `lib/db/schema.ts`.

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` (bu değişiklik)
- `drizzle.config.ts` üzerinden migration üretimi (bu notun kapsamı — aşağıdaki "Migration
  Adımları"na bkz.)
- SESSION_INDEX.md — migration Neon'da koşulup doğrulanınca "Veritabanı" satırına işlenmeli
- ARCHITECTURE.md §3 (VERİ MODELİ) — HENÜZ İŞLENMEDİ, açık iş olarak kalıyor (A8/#110 ile
  aynı kapsamda ele alınabilir)
- CUSTOMIZER_SPEC.md / SANDWICH_SPEC.md — store'lar bu tablodan okumaya geçtiğinde (AYRI bir
  tur, henüz kodlanmadı) her iki spec'in §3 (State Şeması) bölümü güncellenmeli

### GERİ ALMA
İki tablo da başka hiçbir mevcut tabloya FK ile bağlı DEĞİL (sadece kendi içlerinde self-FK,
`ingredients.parentIngredientId`) — geri almak için:
```sql
DROP TABLE IF EXISTS ingredients;
DROP TABLE IF EXISTS sandwich_sizes;
```
Veri kaybı riski YOK çünkü bu turda henüz hiçbir tüketici kod (store/API route) bu tablolardan
okumuyor — sadece şema var, geri alma tamamen izole.
