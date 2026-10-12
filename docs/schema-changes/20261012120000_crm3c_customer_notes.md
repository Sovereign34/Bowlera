## Session: CRM-3c adım 1 (TB-CRM-19) — 2026-10-12
## Açıklama: Müşteri notları için `customer_notes` tablosu (append-only). Bu adımda HİÇBİR kod okumaz/yazmaz; yalnız şema + elle SQL.

### KARAR (kullanıcı onayı 2026-10-12)
- Not düzenlenmez/silinmez; düzeltme = yeni not. Gövde 1–500 karakter.
- Yazma: personel yalnız şube kapsamındaki müşteriye, admin hepsine. **Okuma: yalnız admin** (personel notu göremez).
- Her yazma/okuma audit'e düşer, audit yazılamazsa işlem yapılmaz (fail-closed).
- Forma "sağlık, din, siyasi görüş vb. özel veri yazmayın" uyarısı (3c-3).

### ⚠️ RISK_DOMAINS §4 (KVKK) İŞARETİ
Bu değişiklik `users` ile ilişkili YENİ kişisel veri (serbest metin müşteri notu) ekliyor. AI uygunluk onayı veremez; son karar insan/hukuk (hukukçu yok → `KVKK_KARAR_KAPANIS.md` yazılı kabul). Serbest metin özel nitelikli veri içerebilir; teknik azaltıcılar: 500 karakter, uyarı metni, yalnız admin okur, audit.

### ÖNCE
`customer_notes` yok.

### SONRA
`customer_notes` tablosu + `customer_notes_block_mutation()` fonksiyonu + `trg_customer_notes_append_only` (BEFORE UPDATE OR DELETE) + `(customer_id, created_at DESC)` indeksi.

### ETKİLENEN DOSYALAR
`lib/db/schema.ts` (yalnız `customerNotes` eklenir; aşağıdaki blok). Başka kod YOK.

### schema.ts BLOĞU (SQL koştuktan SONRA push)
```ts
// --- 🆕 CRM-3c (TB-CRM-19) adım 1 — 2026-10-12 ---
// Şema notu: docs/schema-changes/20261012120000_crm3c_customer_notes.md
// Amaç:    Müşteri notları (admin okur; personel yalnız yazar). APPEND-ONLY (trigger): düzenleme/silme yok, düzeltme yeni nottur.
// Bağlı:   Bu adımda HİÇBİR kod okumaz/yazmaz. Sonraki adım (3c-2): lib/crm yazma/okuma + audit; 3c-3: arayüz.
// Risk:    `body` serbest metin = özel nitelikli veri girme riski (KVKK). Append-only olduğu için yazılan SİLİNEMEZ; silme/erase
//          CRM-7'de ayrıca çözülmeli (trigger + FK `users` silmeyi engeller). Log'a `body` YAZILMAZ.
// Dokunma: CHECK (1–500) ve trigger yalnız SQL'de (Drizzle ifade etmez). Uzunluk sınırı değişirse DB + kod aynı turda.
export const customerNotes = pgTable("customer_notes", {
  id: uuid("id").defaultRandom().primaryKey(),
  customerId: uuid("customer_id").notNull().references(() => users.id),
  authorId: uuid("author_id").notNull().references(() => users.id),
  branchId: uuid("branch_id").references(() => branches.id), // nullable — yazarın şube bağlamı belirsizse NULL
  body: text("body").notNull(), // 1–500 (CHECK, yalnız SQL)
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
})
export type CustomerNoteRow = typeof customerNotes.$inferSelect
export type NewCustomerNoteRow = typeof customerNotes.$inferInsert
```

### SQL 1 — MIGRATION (Neon SQL Editor, kod push'undan ÖNCE)
```sql
BEGIN;

CREATE TABLE customer_notes (
  id          uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  customer_id uuid NOT NULL REFERENCES users(id),
  author_id   uuid NOT NULL REFERENCES users(id),
  branch_id   uuid REFERENCES branches(id),
  body        text NOT NULL,
  created_at  timestamptz NOT NULL DEFAULT now(),
  CONSTRAINT customer_notes_body_len CHECK (char_length(body) BETWEEN 1 AND 500)
);

CREATE INDEX customer_notes_customer_idx ON customer_notes (customer_id, created_at DESC);

CREATE FUNCTION customer_notes_block_mutation() RETURNS trigger AS $$
BEGIN
  RAISE EXCEPTION 'customer_notes append-only: % engellendi', TG_OP;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_customer_notes_append_only
  BEFORE UPDATE OR DELETE ON customer_notes
  FOR EACH ROW EXECUTE FUNCTION customer_notes_block_mutation();

COMMIT;
```

### SQL 2 — DOĞRULAMA (atomik; sonunda HER ZAMAN geri alınır, kalıcı satır bırakmaz)
Beklenen çıktı: hata mesajı `TEST_OK`. Başka bir mesaj = başarısız.
```sql
DO $$
DECLARE u uuid; ok_update boolean := false; ok_delete boolean := false; ok_len boolean := false;
BEGIN
  SELECT id INTO u FROM users LIMIT 1;
  IF u IS NULL THEN RAISE EXCEPTION 'TEST_FAIL: users bos'; END IF;
  INSERT INTO customer_notes (customer_id, author_id, body) VALUES (u, u, 'test notu');
  BEGIN UPDATE customer_notes SET body = 'x' WHERE customer_id = u; EXCEPTION WHEN OTHERS THEN ok_update := true; END;
  BEGIN DELETE FROM customer_notes WHERE customer_id = u; EXCEPTION WHEN OTHERS THEN ok_delete := true; END;
  BEGIN INSERT INTO customer_notes (customer_id, author_id, body) VALUES (u, u, repeat('a', 501)); EXCEPTION WHEN check_violation THEN ok_len := true; END;
  IF NOT (ok_update AND ok_delete AND ok_len) THEN
    RAISE EXCEPTION 'TEST_FAIL update=% delete=% len=%', ok_update, ok_delete, ok_len;
  END IF;
  RAISE EXCEPTION 'TEST_OK';
END $$;
```
Sonra: `SELECT count(*) FROM customer_notes;` → **0** olmalı.

### GERİ ALMA (zorunlu)
```sql
BEGIN;
DROP TRIGGER IF EXISTS trg_customer_notes_append_only ON customer_notes;
DROP FUNCTION IF EXISTS customer_notes_block_mutation();
DROP TABLE IF EXISTS customer_notes;
COMMIT;
```
Not: tabloda satır varsa trigger DELETE'i engellediği için önce trigger düşürülür (yukarıdaki sıra bunu yapar); satırlı tablo geri alınırsa notlar KAYBOLUR.
