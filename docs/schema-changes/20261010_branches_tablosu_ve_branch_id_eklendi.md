# branches tablosu + order_history.branch_id + consent_registrations.branch_id (TB-CRM-06 Adım 1)

## Session: CRM hazırlık — 2026-10-10
## Açıklama: 2. şube yakında açılacak. Hangi sipariş/kaydın hangi şubeye ait olduğu tutulmuyordu (Açık Sorun #92). `branches` tablosu açıldı, iki tabloya NULLABLE `branch_id` (FK) eklendi, mevcut kayıtlar mevcut şubeye (`bowlerapark`) bağlandı. `users` şubeye BAĞLANMAZ. Bu adımda davranış değişmez: yazım kodu Adım 2'de.

Neon SQL Editor'de, kod/schema.ts push'undan ÖNCE çalıştır (tekrar çalıştırmak güvenli):

```sql
CREATE TABLE IF NOT EXISTS branches (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  slug text NOT NULL UNIQUE,
  name text NOT NULL,
  is_active boolean NOT NULL DEFAULT true,
  created_at timestamptz NOT NULL DEFAULT now()
);

INSERT INTO branches (slug, name)
VALUES ('bowlerapark', 'Bowlerapark')
ON CONFLICT (slug) DO NOTHING;

ALTER TABLE order_history
  ADD COLUMN IF NOT EXISTS branch_id uuid REFERENCES branches(id);
ALTER TABLE consent_registrations
  ADD COLUMN IF NOT EXISTS branch_id uuid REFERENCES branches(id);

UPDATE order_history
SET branch_id = (SELECT id FROM branches WHERE slug = 'bowlerapark')
WHERE branch_id IS NULL;
UPDATE consent_registrations
SET branch_id = (SELECT id FROM branches WHERE slug = 'bowlerapark')
WHERE branch_id IS NULL;
```

Doğrulama:

```sql
SELECT slug, name, is_active FROM branches;
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE column_name = 'branch_id' AND table_name IN ('order_history','consent_registrations');
SELECT
  (SELECT count(*) FROM order_history WHERE branch_id IS NULL) AS orders_without_branch,
  (SELECT count(*) FROM consent_registrations WHERE branch_id IS NULL) AS consents_without_branch;
```
Beklenen: `branches` 1 satır (bowlerapark); 2 satır `branch_id` (uuid, nullable = YES); iki sayaç 0.

### ÖNCE
`order_history` ve `consent_registrations`'da şube bilgisi yok; `branches` tablosu yok.

### SONRA
`branches(id, slug UNIQUE, name, is_active, created_at)`; `order_history.branch_id` ve `consent_registrations.branch_id` uuid, nullable, FK → `branches.id`. Mevcut satırlar `bowlerapark`'a bağlı.

### ETKİLENEN DOSYALAR
`lib/db/schema.ts` (branches + 2 kolon). Yazım kodu Adım 2'de: `app/api/orders/gel-al/route.ts`, `lib/db/queries/consent-registration.ts`. Dokümanlar: ARCHITECTURE.md (§veri modeli), TEKNIK_BORC_CRM.md (TB-CRM-06).

### SIRA UYARISI
Önce bu SQL, SONRA `schema.ts` push'u. Sıra tersine çevrilirse `order_history` / `consent_registrations` okuyan her sorgu "column branch_id does not exist" hatası verir (users.email'deki ders).

### GERİ ALMA
```sql
ALTER TABLE order_history DROP COLUMN IF EXISTS branch_id;
ALTER TABLE consent_registrations DROP COLUMN IF EXISTS branch_id;
DROP TABLE IF EXISTS branches;
```
(Önce `schema.ts` değişikliği geri alınmalı/push edilmemeli.) Henüz hiçbir kod şube verisine bağımlı değil, geri alma güvenli.
