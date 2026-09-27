# Şema Notu — `users.role` + `users.verificationStatus` CHECK Constraint

> #135 P0 madde 4 (DB CHECK/enum constraint yok) — kapsam bilinçli olarak SADECE bu iki
> alanla sınırlandı (AGENT.md Kural #5, tek problem/tek çözüm). Diğer constraint'siz
> alanlar (`orderHistory.paymentStatus`/`paymentMethod`, `ingredients.productType`/`slot`,
> `passwordResetRequests.status`) bu turun KAPSAMI DIŞINDA — ayrı bir tur gerektirir.

## Neden

`lib/db/schema.ts`'in kendi Risk notu: `role` yanlış set edilirse personel olmayan biri
`/personel/*`'a erişebilir (yetki sızıntısı); `verificationStatus` yanlış set edilirse
doğrulanmamış biri sipariş tamamlayabilir (dolandırıcılık riski). Şu ana kadar bu iki alan
SADECE kod tarafındaki (`auth.ts`/`middleware.ts`) TS union kontrolüyle korunuyordu — DB'ye
elle/API'nin dışından yazılan geçersiz bir değer hiçbir şekilde engellenmiyordu.

RISK_DOMAINS.md madde 4 (KVKK) gereği bu not: değişiklik `users` tablosunu etkiliyor,
nihai onay AI'da değil kullanıcıda.

## ⚠️ ZORUNLU ÖN ADIM — migration'dan ÖNCE çalıştır

Mevcut satırlarda constraint dışı bir değer varsa `ALTER TABLE` BAŞARISIZ olur. Önce şunu
Neon SQL Editor'de çalıştır ve sonucu kontrol et:

```sql
SELECT DISTINCT role FROM users;
SELECT DISTINCT verification_status FROM users;
```

- Sonuç boşsa (tablo 0 satır) → doğrudan aşağıdaki migration'a geç.
- Sonuçta `role` için `'customer'`/`'staff'`/`'admin'` DIŞINDA bir değer, veya
  `verification_status` için `'pending'`/`'confirmed'` DIŞINDA bir değer görürsen →
  **DUR, migration'ı koşma** — önce o satırları düzelt veya bana bildir, constraint'i
  buna göre revize edelim.

## Migration (ön adım temizse koş)

```sql
ALTER TABLE users
  ADD CONSTRAINT chk_users_role
  CHECK (role IN ('customer', 'staff', 'admin'));

ALTER TABLE users
  ADD CONSTRAINT chk_users_verification_status
  CHECK (verification_status IN ('pending', 'confirmed'));
```

## Doğrulama (migration'dan SONRA)

```sql
SELECT conname, pg_get_constraintdef(oid)
FROM pg_constraint
WHERE conrelid = 'users'::regclass AND contype = 'c';
```

İki satır dönmeli: `chk_users_role` ve `chk_users_verification_status`, tanımlarıyla birlikte.

İsteğe bağlı canlı test (constraint'in gerçekten çalıştığını görmek için, PROD dışı bir
ortamda/dikkatle): geçersiz bir değerle `UPDATE users SET role = 'gecersiz-deger' WHERE ...`
denenirse Postgres'in `new row for relation "users" violates check constraint "chk_users_role"`
hatasıyla REDDETMESİ beklenir.

## Senkron uyarısı (kalıcı, gelecekteki değişiklikler için)

Drizzle ORM (bu projedeki sürüm) CHECK constraint'i şema dosyasında native temsil etmiyor —
yani `lib/db/schema.ts`'teki TS union'ı genişletmek (örn. yeni bir `"manager"` rolü eklemek)
bu DB constraint'ini OTOMATİK güncellemez. İleride böyle bir değişiklik yapılırsa, bu dosyanın
bir benzeri (yeni `ALTER TABLE ... DROP CONSTRAINT` + `ADD CONSTRAINT`) AYNI turda üretilip
koşulmalı — aksi halde yeni değer DB tarafından sessizce reddedilir (kod "başarılı" görünür,
INSERT/UPDATE runtime'da hata verir).

---

*Durum: kod tarafı (`schema.ts` yorumları) bu turda güncellendi. SQL migration'ı Neon SQL
Editor'de kullanıcı tarafından koşulup doğrulanmalı — henüz KOŞULMADI/DOĞRULANMADI.*
