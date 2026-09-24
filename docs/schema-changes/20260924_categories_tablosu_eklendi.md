# Şema Değişikliği — `categories` tablosu eklendi + `menu_items.category` FK'landı

**Tarih:** 2026-09-24
**Karar sahibi:** Kullanıcı (bu sohbette onaylandı)

## Ne değişti

1. Yeni tablo: `categories` (id: text PK/slug, name: text, sort_order: integer, created_at)
2. `menu_items.category` artık `text` kalmaya devam ediyor AMA `categories.id`'ye
   `REFERENCES` (FOREIGN KEY, varsayılan RESTRICT) ile bağlandı.
3. `types/index.ts` → `BowlItem.category` sabit union'dan (`"signature"|"build-your-own"|"içecek"`)
   `string`'e gevşetildi. Yeni `Category` tipi eklendi.

## Neden

Kullanıcı kararı: kategoriler artık admin panelden yönetilecek (eklenip/silinebilecek),
sabit bir kod listesi olmayacak. Menüler: **İmza Ürünler, Bowl, Dürüm, Salata Bowl,
Sandviç, Tatlı, İçecek**. DB karşılığı Türkçe karakter İÇERMEYECEK (karışıklığı önlemek
için — kullanıcı talebi), sadece görünen ad Türkçe.

## Kategori silme davranışı — bilinçli tercih

Bir kategoriye bağlı ürün varken silme denenirse **Postgres FK constraint'i bunu
reddeder** (23503 hata kodu). Otomatik cascade (ürünleri de silme) veya otomatik
"kategorisiz" gruba düşürme YAPILMAZ — ikisi de sessiz veri kaybı riski taşır.
API route (`app/api/admin/categories/[id]/route.ts`) bu hatayı yakalayıp kullanıcıya
"önce ürünleri başka kategoriye taşıyın" mesajı gösterir.

## ⚠️ MİGRASYON SIRASI — ZORUNLU, atlanamaz

`menu_items` tablosunda halihazırda 8 test ürünü var (`category` değerleri eski
sistemden: `"signature"`, `"build-your-own"`, `"içecek"`). Bu değerler yeni
`categories.id` slug'larıyla (`imza-urunler`, `bowl`, `durum`, vb.) eşleşmiyor —
**kullanıcı bu 8 ürünün sadece test verisi olduğunu, gerçek ürün eklenmediğini
onayladı**, bu yüzden migration'ı "veri taşıma" değil "temiz sıfırlama" olarak
tasarladık:

```sql
-- 1. Test verisini temizle (kullanıcı onaylı — gerçek ürün yok)
DELETE FROM menu_items;

-- 2. categories tablosunu oluştur (drizzle-kit generate + push ile OTOMATİK üretilecek,
--    burada referans için elle yazıldı)
CREATE TABLE categories (
  id text PRIMARY KEY,
  name text NOT NULL,
  sort_order integer NOT NULL DEFAULT 0,
  created_at timestamptz NOT NULL DEFAULT now()
);

-- 3. 7 başlangıç kategorisini seed et
INSERT INTO categories (id, name, sort_order) VALUES
  ('imza-urunler', 'İmza Ürünler', 0),
  ('bowl',         'Bowl',         1),
  ('durum',        'Dürüm',        2),
  ('salata-bowl',  'Salata Bowl',  3),
  ('sandwic',      'Sandviç',      4),
  ('tatli',        'Tatlı',        5),
  ('icecek',       'İçecek',       6);

-- 4. menu_items.category'ye FK ekle (bu adımdan ÖNCE tablo boş olmalı, aksi halde
--    eski değerler yeni categories.id'lerle eşleşmediği için bu adım BAŞARISIZ olur)
ALTER TABLE menu_items
  ADD CONSTRAINT menu_items_category_fkey
  FOREIGN KEY (category) REFERENCES categories(id);
```

**Uygulama sırası:** (1) `DELETE FROM menu_items` (2) `drizzle-kit generate` ile
schema.ts'teki değişiklikten migration dosyası üret (3) migration'ı Neon'a uygula
(`drizzle-kit push` veya normal akışınız) (4) kategorileri seed et (yukarıdaki INSERT,
veya `/admin/categories/new` ekranından elle tek tek) (5) admin panelden yeni ürünleri
gir.

## Kapsam dışı bırakılanlar (ayrı görev)

- Kategori **düzenleme** (yeniden adlandırma) — sadece ekleme/silme kodlandı, kullanıcı
  talebi buydu. `id` (slug) oluşturulduktan sonra değiştirilemez.
- Public `/menu` sayfasının kategoriye göre filtrelenmesi/gösterilmesi — bu görev SADECE
  admin panel + `menu_items`/`categories` DB katmanını kapsıyor, public site'ın bu
  tabloyu okuması ayrı, önceden konuşulan bir karar bekliyor (bkz. bu sohbetteki "canlı
  `/menu`'nün veri kaynağı" tartışması — ISR + on-demand revalidate kararlaştırıldı ama
  henüz kodlanmadı).
- ✅ **Tamamlandı** — `app/admin/menu-items/[id]/page.tsx` artık kategorileri çekip
  `MenuItemForm`'a geçiriyor (`new/page.tsx` ile aynı desen).
- ✅ **Tamamlandı** — `app/api/admin/menu-items/[id]/route.ts`'teki PATCH artık FK ihlalini
  (23503, geçersiz/silinmiş kategori id'si) 400 ile kullanıcı dostu mesaja çeviriyor.
- ✅ **Tamamlandı** — `app/api/admin/menu-items/route.ts`'teki POST artık aynı FK-ihlali
  (23503, geçersiz kategori id'si) korumasına sahip, `[id]/route.ts`'teki PATCH ile aynı desen.
  **Kategori sistemi (schema, admin CRUD, form, her iki API route) artık uçtan uca tamam.**
