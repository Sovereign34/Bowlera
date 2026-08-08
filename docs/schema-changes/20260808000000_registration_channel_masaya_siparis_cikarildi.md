## Session: 12 (devamı) — 2026-08-08
## Açıklama: RegistrationChannel tipinden "masaya-siparis" değeri çıkarıldı (Açık Sorun #68 KAPANDI).
Sebep: §2.7b kararıyla Masaya Sipariş artık kayıt/rıza akışına hiç girmiyor — kendi auth'suz
`/masaya-siparis/*` yüzeyi var, fulfillmentChannel="dine-in" doğrudan orada set ediliyor.
Bu yüzden "masaya-siparis" değeri kayıt formunda artık hiçbir UI'dan seçilemeyen ölü bir dal
haline geldi. lib/db/schema.ts incelendi: consentRegistrations.channel sütunu Postgres enum
DEĞİL, düz `text("channel").notNull()` — DB seviyesinde bu değeri zorlayan/kısıtlayan bir
CHECK/enum yok, Drizzle'ın çıkardığı satır tipi de `channel: string` (literal union'a bağlı
değil). Bu nedenle migration GEREKMEDİ — sadece types/index.ts'teki TS union daraltıldı.

### ÖNCE
```ts
export type RegistrationChannel = "masaya-siparis" | "gel-al" | "online-platform"
```

### SONRA
```ts
export type RegistrationChannel = "gel-al" | "online-platform"
```

### ETKİLENEN DOSYALAR
- types/index.ts (RegistrationChannel daraltıldı, FulfillmentChannel ve RegistrationChannel
  yorumları senkronize edildi)
- ARCHITECTURE.md §2.7b (Açık Soru #68 KAPANDI olarak işaretlendi), §3 (Veri Modeli notu),
  §5 (Sorumluluk Sınırları — ilgili satır varsa)
- SESSION_INDEX.md (Açık Sorunlar tablosu #68 → 🟢, Kritik Kararlar tablosuna 🗄️ + bu dosya adı)

### GERİ ALMA
Union'a `"masaya-siparis"` değerini geri ekle:
```ts
export type RegistrationChannel = "masaya-siparis" | "gel-al" | "online-platform"
```
DB'de veri kaybı riski YOK — hiçbir satır silinmedi/değiştirilmedi, sadece TS tip daraltıldı.
Geri alma sonrası tek gereken adım types/index.ts'in bu satırını eski haline döndürmek.

### NOT (KOD DOSYASI DEĞİL, TAKİP GEREKİR)
`RegistrationChannel` tipini import eden/switch/case ile dallanan kod dosyaları bu turda
GÖRÜLMEDİ (ör. kayıt formu component'i, API route validasyonu varsa). TypeScript derleyicisi
"masaya-siparis" case'i kalan dosyalarda hata verecektir — bu BEKLENEN ve İSTENEN davranış
(compile-time'da tüm kullanım noktalarını yakalar), ama session kapanışında bu hataların
gerçekten çıkıp çıkmadığı `tsc --noEmit` ile doğrulanmalı.
