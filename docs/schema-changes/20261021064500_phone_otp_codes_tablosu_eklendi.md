## Session: SMS-OTP (Netgsm) — 2026-10-21
## Açıklama: Kayıt sonrası telefon doğrulama kodlarını (SMS OTP) saklayan `phone_otp_codes` tablosu eklendi. Kod DÜZ METİN saklanmaz (HMAC-SHA256 hash). Telefon bu tabloda TUTULMAZ (users.phone zaten var; KVKK için çoğaltma yok).

### ÖNCE
Tablo yok. Kayıt sonrası hesap `verification_status='pending'` kalır, personel manuel teyit eder.

### SONRA
```sql
CREATE TABLE IF NOT EXISTS phone_otp_codes (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id uuid NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  code_hash text NOT NULL,
  attempts integer NOT NULL DEFAULT 0,
  expires_at timestamptz NOT NULL,
  consumed_at timestamptz,
  created_at timestamptz NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS idx_phone_otp_codes_user_created
  ON phone_otp_codes (user_id, created_at DESC);
```
Drizzle karşılığı: `lib/db/schema.ts` sonuna `phoneOtpCodes` (bkz. teslim edilen snippet). Tabloyu Neon'a ELLE ekle, `db:push` KULLANMA.

### ETKİLENEN DOSYALAR
lib/db/schema.ts, ileride lib/auth/otp-store.ts, app/api/auth/otp/send|verify/route.ts. Mevcut tablolar/kolonlar DEĞİŞMEDİ (users.verification_status CHECK'i aynen kalır: 'pending'|'confirmed').

### GERİ ALMA
```sql
DROP TABLE IF EXISTS phone_otp_codes;
```
Kod tarafı bayrak (SMS_OTP_ENABLED) kapalıyken tabloya hiç dokunmaz; tablo silinirse personel onayı akışı etkilenmez.
