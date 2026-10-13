# 20261013100000_branch_item_availability_tablosu_eklendi

## Session: 38. sohbet (CRM dışı, menü) — 2026-10-13
## Açıklama
Menü ürünleri şube bazında "Tükendi" işaretlenebilsin. Ürün menüde KALIR (menu_items'a dokunulmaz);
yalnız o şubede, o an sipariş verilebilir mi bilgisi ayrı tabloda tutulur. Menü yapısı şube bazlı
OLMAZ (TB-CRM-07 (c) "şube bazlı menü ertelendi" kararıyla uyumlu).
Faz 1 yalnız `menu_items` ürünlerini kapsar. Malzeme tükenmesi (ingredients) Faz 3, kategori çalışma
saati Faz 2 — ayrı şema notları.

## Tasarım kararları
- Satır VAR ve `unavailable_until > now()` → tükendi. Satır yok veya süresi geçmiş → satılabilir.
- "Tekrar Var" = satır SİLİNMEZ, `unavailable_until = now()` yapılır (son işaretleyen `marked_by`'da kalır).
- Varsayılan bitiş: ertesi gün 00:00 İstanbul. Hesap UYGULAMA kodunda yapılır (DB varsayılanı yok).
  Türkiye'de yaz saati yok (UTC+3 sabit), bu yüzden güvenli.
- Anahtar (branch_id, menu_item_id): aynı ürüne iki kişi aynı anda basarsa upsert, çift satır olmaz.
- Ürün menüden silinirse satır da silinir (CASCADE). Şube silinemez (RESTRICT, branches ile aynı desen).
- CHECK/enum YOK (projedeki bilinçli desen).

## ÖNCE
Tablo yok. Tükendi bilgisi hiçbir yerde tutulmuyor.

## SONRA
```ts
export const branchItemAvailability = pgTable(
  "branch_item_availability",
  {
    branchId: uuid("branch_id").notNull().references(() => branches.id),
    menuItemId: text("menu_item_id").notNull().references(() => menuItems.id, { onDelete: "cascade" }),
    unavailableUntil: timestamp("unavailable_until", { withTimezone: true }).notNull(),
    markedBy: uuid("marked_by").notNull().references(() => users.id),
    createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
    updatedAt: timestamp("updated_at", { withTimezone: true }).defaultNow().notNull(),
  },
  (table) => ({ pk: primaryKey({ columns: [table.branchId, table.menuItemId] }) }),
)
```

## ETKİLENEN DOSYALAR
lib/db/schema.ts (+tablo), app/menu/page.tsx, components/menu/MenuPageClient.tsx, MenuCard.tsx,
QuickAddSheet.tsx, app/api/orders/gel-al/route.ts, personel paneli (yeni "Ürünler" sekmesi),
ARCHITECTURE.md §Veri Modeli.

## UYGULAMA SIRASI (3c dersi)
1. Migration SQL'i TEK BAŞINA çalıştır (doğrulama ile aynı çalıştırmada DEĞİL).
2. Doğrulama SQL'ini AYRI çalıştır; `to_regclass` NULL değilse tablo vardır.
3. Ancak ondan sonra kod push edilir.

## GERİ ALMA
`DROP TABLE branch_item_availability;` — başka tablo buna bağlı değil. Kod push edilmişse önce kod geri alınır.
