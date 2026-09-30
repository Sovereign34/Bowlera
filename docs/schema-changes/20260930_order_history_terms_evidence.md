# order_history — sözleşme kabul kanıtı (Canlı Öncesi Rapor sıra 10-A)

Neon SQL Editor'de, kod push'undan ÖNCE çalıştır:

```sql
ALTER TABLE order_history
  ADD COLUMN IF NOT EXISTS terms_accepted_at timestamptz,
  ADD COLUMN IF NOT EXISTS terms_version text,
  ADD COLUMN IF NOT EXISTS terms_accepted_ip text;
```

Doğrulama:

```sql
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'order_history'
  AND column_name IN ('terms_accepted_at','terms_version','terms_accepted_ip');
```
Beklenen: 3 satır, hepsi nullable = YES. Eski siparişler NULL kalır.

Geri alma (gerekirse): `ALTER TABLE order_history DROP COLUMN terms_accepted_at, DROP COLUMN terms_version, DROP COLUMN terms_accepted_ip;`
