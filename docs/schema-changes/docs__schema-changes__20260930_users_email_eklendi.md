# users.email eklendi (NOT NULL, unique değil)

**Tarih:** 2026-09-30
**Neden:** Sipariş sonrası sözleşme + ön bilgilendirme e-postası (Yemeksepeti modeli). E-posta kayıtta zorunlu.
**Kapsam:** Sadece `users` tablosu. `consent_registrations`'a e-posta YAZILMAZ.

## Koşma sırası (Neon SQL Editor) — SIRA ÖNEMLİ

DB sıfırlanıyor (bilinçli karar). Menü/kategori/malzeme tablolarına DOKUNMA.

```sql
-- 1) Müşteri verisini temizle (users'a FK veren tablo yok; CASCADE gerekmez)
TRUNCATE TABLE users, consent_registrations, order_history,
               password_reset_requests, registration_blocked_attempts;

-- 2) Kolonu ekle (tablo boş olduğu için NOT NULL sorunsuz)
ALTER TABLE users ADD COLUMN email text NOT NULL;
```

TRUNCATE FK hatası verirse DURMA ve hata metnini yaz — `CASCADE` ekleme.

## Deploy sırası
1. Neon'da yukarıdaki SQL (ÖNCE).
2. Kodu push et (schema.ts, validation.ts, create-user.ts, consent route, formlar BİRLİKTE).
3. Kod önce çıkarsa: `select().from(users)` yapan sorgular "email kolonu yok" diye patlar.

## Sıfırlama sonrası
- Admin/personel hesabın silindi: sitede kayıt ol, sonra Neon'da
  `UPDATE users SET role = 'admin' WHERE phone = '+90...';`

## Geri alma
`ALTER TABLE users DROP COLUMN email;` (silinen müşteri verisi geri gelmez.)
