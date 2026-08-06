# Şema Değişiklik Notu
`docs/schema-changes/20260806130000_consent_registrations_tablosu_eklendi.md`

**Tarih:** 2026-08-06 (Session 7)
**Değişiklik:** `lib/db/schema.ts`'e YENİ tablo — `consentRegistrations`
**Kapsam:** Ekleme — mevcut `users` tablosuna DOKUNULMUYOR

## Neden ayrı tablo (önceki turda kullanıcı onayıyla kararlaştırıldı)
`users.phone` `unique()+notNull()` ve Twilio-doğrulanmış kimliğe dayanıyor (Karar #17,
"1 numara = 1 hesap"). Doğrulamasız rıza kaydını aynı tabloya yazmak, gerçek numara
sahibi sonradan Twilio ile giriş yapmak istediğinde `unique` çakışmasına yol açar.
Ayrı tablo, Twilio/Netgsm akışına (#32/#56, parklandı ama silinmedi) hiç dokunmaz.

## Sapma notu — SESSION_INDEX'teki eski plandan
SESSION_INDEX'in (0e) adımı `users.verifiedAt`'i "rıza onay zamanı" olarak yeniden
yorumlamayı öngörmüştü — bu, AYNI tablo varsayımıyla yazılmıştı. Ayrı tablo kararı bu
turda alındığı için o adım GEÇERSİZ; yerine bu tabloda kendi `consentGivenAt` alanı
kullanılıyor. Anlam karışıklığı riski böylece ortadan kalkıyor.

## Yeni tablo
```ts
export const consentRegistrations = pgTable("consent_registrations", {
  id: uuid("id").defaultRandom().primaryKey(),
  phone: text("phone").notNull().unique(), // bu tabloda da 1 numara = 1 kayıt (upsert)
  name: text("name").notNull(),
  address: text("address"),               // opsiyonel — Karar #23 ile çakışmıyor
  age: integer("age"),                    // opsiyonel
  gender: text("gender"),                 // opsiyonel
  channel: text("channel").notNull(),     // RegistrationChannel: masaya-siparis|gel-al|online-platform
  consentGivenAt: timestamp("consent_given_at", { withTimezone: true }).notNull(),
  createdAt: timestamp("created_at", { withTimezone: true }).defaultNow().notNull(),
  updatedAt: timestamp("updated_at", { withTimezone: true }).defaultNow().notNull(),
})
```

## Davranış notu — TÜM kanallar DB'ye yazılır
Session 6 kararı gereği "online-platform" seçilse bile kayıt satırı oluşturulur (sonradan
merkezi numaradan manuel WhatsApp/SMS teyidi için — bkz. session_log.md Session 6, madde 6).
Sadece `masaya-siparis`/`gel-al` seçildiğinde `useCartStore.fulfillmentChannel` ön-doldurulup
customizer'a girilir; `online-platform`'da sepete hiç girilmez.

## Etkilenen dosyalar
- `lib/db/schema.ts` — tablo eklendi
- `lib/db/queries/consent-registration.ts` — yeni, upsert sorgusu
- `lib/registration/validation.ts` — yeni, girdi doğrulama
- `app/api/registration/consent/route.ts` — yeni, POST endpoint (auth GEREKTİRMEZ — bilinçli, BSC-7 rate-limit ile korunuyor)
- `lib/auth/rate-limit.ts` — `checkRegistrationRateLimit` eklendi (IP bazlı, auth yok çünkü)

## Geri alınabilirlik
Tam geri alınabilir — yeni tablo, mevcut `users` şemasına dokunulmadı.
