## Session: CRM-2 Adım A — 2026-10-10
## Açıklama: `customer_events` (append-only olay günlüğü), `v_customer_stats` + `v_customer_branch_stats` (TB-CRM-05 "gerçek satış" koşuluyla) ve attribution kolonları (TB-CRM-08: `acquisition_source`, `utm_source`, `utm_medium`, `utm_campaign`) eklendi. Neden: CRM segmentleri/raporları için tek, tutarlı satış tanımı ve müşteri zaman çizelgesi; pazarlama kaynağının ölçülebilmesi. Metrikler KOLON değil VIEW (#94: senkron kayma riski yok).

### ÖNCE
- `customer_events`, `v_customer_stats`, `v_customer_branch_stats` YOK.
- `consent_registrations` ve `order_history`'de attribution kolonu YOK.

### SONRA
- `customer_events(id, phone, event_type, occurred_at, branch_id→branches, order_id, payload jsonb, source_key UNIQUE, created_at)`
  - `event_type` CHECK: `customer_registered` | `order_placed` (genişletilirse DB CHECK de aynı turda güncellenir).
  - UPDATE/DELETE/TRUNCATE `crm_forbid_mutation()` trigger'ıyla engelli (CRM-1 ile aynı mekanizma).
  - `order_id` bilinçli olarak FK DEĞİL (projenin düz eşleşme deseni; `order_history` TRUNCATE'i bozulmasın).
  - `payload`'a telefon/ad/adres YAZILMAZ.
- `v_customer_stats`: `users.role='customer'` her müşteri için `order_count`, `total_spend`, `avg_order_value`, `first_order_at`, `last_order_at`, `days_to_repeat` (1. → 2. gerçek sipariş arası gün). Siparişi olmayana 0 döner.
- `v_customer_branch_stats`: (telefon, `branch_id`) kırılımı; `branch_id` NULL = şubesiz kayıt.
- Gerçek satış: `status IN ('completed','served') AND (payment_method='nakit' OR payment_status='odendi')`
  - ⚠️ **Onaylı tanıma EK KORUMA:** `AND payment_status NOT IN ('iade_edildi','tutarsizlik')`. Neden: onaylı koşul literal okununca "nakit + iade_edildi" sipariş satış sayılırdı; oysa TB-05 hariç listesi `iade_edildi`/`tutarsizlik` diyor ve kabul kriteri "iade toplamı bozmaz". İstenmezse view'lardan o satır silinir.
  - ⚠️ `order_history`'de teslim/tamamlanma zamanı YOK → "satış tarihi" = `ordered_at`. `order_completed` olayı geriye dönük üretilemez (şimdilik tanımlı değil).
- Attribution: iki tabloda dört nullable `text` kolon + uzunluk CHECK'i (`acquisition_source` ≤ 64, `utm_*` ≤ 100). Eski satırlar NULL = "bilinmiyor". `channel` KULLANILMAZ.

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` (yeni tablo + 8 kolon; view'lar Drizzle'da ifade edilemez → yorum)
- Sonraki adımlar: backfill (B), `consent/route.ts` + `consent-registration.ts` + `gel-al/route.ts` (C, attribution yazımı), test (D)
- `TEKNIK_BORC_CRM.md` (TB-CRM-05, TB-CRM-08, TB-CRM-18), `SESSION_INDEX.md`, `ARCHITECTURE.md`
- ⚠️ KVKK (RISK_DOMAINS §4): `customer_events` + attribution kişiye bağlı veri işlemesi. Aydınlatma metni / UTM saklama biçimi hukuk görüşü ister (TB-CRM-03). Yakalama kodu (C) hukuk görüşünden önce canlıya açılmaz.

### GERİ ALMA
Tek transaction'da, Neon SQL Editor'de (olay tablosu henüz gerçek veri taşımıyorsa güvenli; sonrasında DROP olay geçmişini siler):
```sql
BEGIN;
DROP VIEW IF EXISTS v_customer_branch_stats;
DROP VIEW IF EXISTS v_customer_stats;
DROP TABLE IF EXISTS customer_events;  -- trigger'lar tabloyla düşer
ALTER TABLE consent_registrations
  DROP CONSTRAINT IF EXISTS chk_consent_reg_attribution_len,
  DROP COLUMN IF EXISTS acquisition_source, DROP COLUMN IF EXISTS utm_source,
  DROP COLUMN IF EXISTS utm_medium, DROP COLUMN IF EXISTS utm_campaign;
ALTER TABLE order_history
  DROP CONSTRAINT IF EXISTS chk_order_history_attribution_len,
  DROP COLUMN IF EXISTS acquisition_source, DROP COLUMN IF EXISTS utm_source,
  DROP COLUMN IF EXISTS utm_medium, DROP COLUMN IF EXISTS utm_campaign;
COMMIT;
```
Attribution kolonları sonradan dolmuşsa DROP COLUMN o veriyi KAYBEDER. Kod `schema.ts`'i bu kolonlarla push ettikten sonra geri almak için önce kodu geri al.
