## Session: CRM kaynak verisi saklama süresi (TB-CRM-28/29) — 2026-10-11
## Açıklama: `consent_registrations` ve `order_history` tablolarına `attribution_consent_version` + `attribution_recorded_at` kolonları; 90 gün sonra kaynak verisini anonim özete toplayıp silen `crm_purge_attribution()` fonksiyonu; `attribution_summary` tablosu.

### ÖNCE
Kaynak kolonları (acquisition_source, utm_source/medium/campaign) süresiz duruyor; onay sürümü kaydı yok.

### SONRA
- Her iki tabloda: `attribution_consent_version text NULL`, `attribution_recorded_at timestamptz NULL`. `recorded_at`'i trigger kaynak alanları boştan doluya geçince doldurur (uygulama kodu değişmeden). Eski/test veriler için `created_at` / `ordered_at` ile geriye dönük dolduruldu.
- `attribution_summary`: hafta + tür (registration/order) + kaynak/ortam/kampanya başına sayı, gerçek satış sayısı ve ciro. KİŞİSEL VERİ YOK.
- `crm_purge_attribution(retention_days, dry_run)`: süresi dolan satırların kaynak kolonlarını ve `attribution_*` kolonlarını NULL yapar; önce özete ekler (tek deyim). Satır, sipariş ve toplamlar kalır.

### ETKİLENEN DOSYALAR
`lib/db/schema.ts` (4 kolon), `app/api/cron/purge-attribution/route.ts` (yeni), `vercel.json` (yeni), route testi. Onay sürümünü yazan kod ayrı adımda (read-attribution, consent-registration sorgusu).

### SIRA
1. Bu not `docs/schema-changes/` altına kaydedilir.
2. `20261011120000_crm_attribution_retention.sql` Neon SQL Editor'de koşulur.
3. `..._dogrulama.sql` koşulur; BEKLENEN: hata mesajı `TEST_OK` ile başlar.
4. SONRA `schema.ts`, cron route'u ve `vercel.json` push edilir.
5. Vercel'de `CRON_SECRET` eklenir.

### GERİ ALMA
```sql
DROP FUNCTION IF EXISTS crm_purge_attribution(integer, boolean);
DROP TRIGGER IF EXISTS trg_consent_registrations_attr_stamp ON consent_registrations;
DROP TRIGGER IF EXISTS trg_order_history_attr_stamp ON order_history;
DROP FUNCTION IF EXISTS crm_stamp_attribution_recorded_at();
DROP TABLE IF EXISTS attribution_summary;
ALTER TABLE consent_registrations DROP COLUMN IF EXISTS attribution_consent_version, DROP COLUMN IF EXISTS attribution_recorded_at;
ALTER TABLE order_history DROP COLUMN IF EXISTS attribution_consent_version, DROP COLUMN IF EXISTS attribution_recorded_at;
```
`schema.ts` değişikliği de geri alınır. ⚠️ Silme işi bir kez çalıştıktan sonra silinen kaynak verisi geri gelmez (özette toplu hâli kalır).

### Edge case notları
- Süre sayacı `attribution_recorded_at`'tir; yoksa `created_at`/`ordered_at`. Kaynak NULL satırlar işlenmez.
- "Gerçek satış" = status completed/served VE (nakit VEYA payment_status odendi) — onaylı karar (2026-10-10).
- Özet haftalık gruplanır; aynı hafta birden çok çalışmada toplanır (ON CONFLICT toplar).
- Neon'un kendi geri yükleme geçmişi silinen veriyi kısa süre tutabilir; politikaya yazılacak.
