## Session: 12 (devamı, yeni sohbet) — 2026-08-08
## Açıklama: Personel Sipariş Paneli'nin (Açık Sorun #62) personel kimlik doğrulaması
için `users` tablosuna rol bazlı yetkilendirme alanı ekleniyor. ARCHITECTURE.md §2.9a'da
(v1.12) kullanıcı onayıyla kapanan "Personel Auth Kararı"nın DB tarafı: ayrı bir
personel-hesap sistemi veya paylaşımlı-cihaz PIN'i yerine, mevcut Auth.js JWT session
mekanizmasına bir yetki katmanı eklenir — iki paralel auth mantığı yaratılmaz.

### ÖNCE
```ts
// types/index.ts — AuthenticatedUser
type AuthenticatedUser = {
  phone: string
  verifiedAt: string
  address?: string
  displayName?: string
  loyaltyPoints?: number
  verificationStatus?: "pending" | "confirmed"
}
```
DB (`lib/db/schema.ts`, `users` tablosu): `role` sütunu yok — tüm kayıtlar örtük olarak
müşteri kabul ediliyor, personel/müşteri ayrımı yapılamıyor.

### SONRA
```ts
// types/index.ts — AuthenticatedUser
type AuthenticatedUser = {
  phone: string
  verifiedAt: string
  address?: string
  displayName?: string
  loyaltyPoints?: number
  verificationStatus?: "pending" | "confirmed"
  role: "customer" | "staff"   // 🆕 — varsayılan "customer"
}
```
DB (`lib/db/schema.ts`, `users` tablosu): `role` sütunu eklenir — `text`, `NOT NULL`,
`DEFAULT 'customer'`. Postgres enum KULLANILMAZ — `consentRegistrations.channel` gibi
projedeki benzer alanlar da düz `text`; bu proje konvansiyonuyla tutarlı (bkz. #68 kapanış
gerekçesi, aynı kural).

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` — `users` tablosuna `role` sütunu eklenir (migration)
- `types/index.ts` — `AuthenticatedUser` tipine `role` alanı eklenir
- `auth.ts` — JWT session callback'ine `role` alanı eklenmeli (`session.user.role` okunabilir
  olmalı — Auth.js callback zincirinde `role` DB'den alınıp token'a/session'a taşınmalı)
- `middleware.ts` — `/personel/*` route'u için rol kontrolü eklenecek; mevcut matcher
  (`/menu/customize/:path*`) GENİŞLETİLECEK, `/masaya-siparis/*` istisnası (§1 madde 7)
  ETKİLENMEZ — ayrı bir prefix
- `ARCHITECTURE.md` §2.9a, §3, §4.1 — zaten bu kararla senkron (v1.12); migration
  koşulduğunda "HENÜZ KOŞULMADI" notları kaldırılmalı
- DEPENDENCIES.md — henüz `role`/`AuthenticatedUser` tüketicileri olarak `middleware.ts`
  ve `auth.ts` kayıtlı değil (Açık Sorun #71'in aynı türden bir tekrarını önlemek için
  bu dosya güncellenirken bilhassa taranmalı)

### GERİ ALMA
1. Vercel/hosting panelinden migration öncesi son başarılı deploy'a "Instant Rollback"
   (ARCHITECTURE.md §4.3)
2. DB: `ALTER TABLE users DROP COLUMN role;`
3. Kod: `role` alanına yapılan referanslar (`types/index.ts`, `auth.ts`, `middleware.ts`)
   revert edilir
4. Rollback sonrası SESSION_INDEX.md'ye 🔴 ile işaretlenir (ARCHITECTURE.md §4.3 /
   CORE.md §7.4)
