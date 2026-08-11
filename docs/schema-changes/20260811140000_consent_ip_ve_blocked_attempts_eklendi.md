## Session: (devam) — 2026-08-11
## Açıklama: Kayıt akışında IP delili tutmak için `consentRegistrations.ipAddress` (nullable)
eklendi. Rate-limit tarafından reddedilen (429) denemeleri kalıcı loglamak için yeni
`registrationBlockedAttempts` tablosu eklendi. Amaç: sahte telefonla kayıt/deneme
girişimlerinde IP bazlı delil ve engellenen deneme geçmişi tutmak.

### ÖNCE
```ts
export const consentRegistrations = pgTable("consent_registrations", {
  id: uuid("id").defaultRandom().primaryKey(),
  phone: text("phone").notNull().unique(),
  name: text("name").notNull(),
  address: text("address"),
  age: integer("age"),
  gender: text("gender"),
  channel: text("channel").notNull(),
  consentGivenAt: timestamp("consent_given_at", { withTimezone: true }).notNull(),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
  updatedAt: timestamp("updated_at", { withTimezone: true }).defaultNow().notNull(),
})

// registrationBlockedAttempts tablosu YOKTU
```

### SONRA
```ts
export const consentRegistrations = pgTable("consent_registrations", {
  id: uuid("id").defaultRandom().primaryKey(),
  phone: text("phone").notNull().unique(),
  name: text("name").notNull(),
  address: text("address"),
  age: integer("age"),
  gender: text("gender"),
  channel: text("channel").notNull(),
  ipAddress: text("ip_address"), // 🆕 nullable — geriye dönük satırlarda NULL, yeni yazımda dolu
  consentGivenAt: timestamp("consent_given_at", { withTimezone: true }).notNull(),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
  updatedAt: timestamp("updated_at", { withTimezone: true }).defaultNow().notNull(),
})

// 🆕 YENİ TABLO
export const registrationBlockedAttempts = pgTable("registration_blocked_attempts", {
  id: uuid("id").defaultRandom().primaryKey(),
  ipAddress: text("ip_address").notNull(),
  attemptedAt: timestamp("attempted_at", { withTimezone: true }).defaultNow().notNull(),
})
```

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` — yukarıdaki iki değişiklik
- `lib/db/queries/consent-registration.ts` — `upsertConsentRegistration` artık `ipAddress`
  parametresi alıyor; yeni `logBlockedRegistrationAttempt(ipAddress)` fonksiyonu eklendi
- `app/api/registration/consent/route.ts` — zaten çıkarılan `ip` değişkeni her iki fonksiyona
  da geçirildi
- `ARCHITECTURE.md` — session kapanışında güncellenmeli (bu turun kapsamı dışı, açık madde)

### GERİ ALMA
1. `registrationBlockedAttempts` tablosunu DROP et (bağımlı veri yok, güvenli).
2. `consentRegistrations.ipAddress` sütununu DROP COLUMN ile kaldır (nullable olduğu için
   var olan satırları bozmadan geri alınabilir).
3. `upsertConsentRegistration` imzasını eski haline (`data` tek parametre) döndür, route.ts'teki
   çağrıyı ve `logBlockedRegistrationAttempt` çağrısını kaldır.

### AÇIK MADDE (kod dışı, ayrıca takip edilecek)
KVKK aydınlatma metnine "güvenlik ve kötüye kullanımı önleme amacıyla IP adresiniz kaydedilir"
maddesi eklenmeli — bu turun kapsamında değil.
