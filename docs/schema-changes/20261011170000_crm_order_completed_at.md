## Session: CRM-4 hazırlık / TB-CRM-24 — 2026-10-11
## Açıklama: `order_history.completed_at` (nullable) eklendi, DB trigger'ı doldurur. CRM view'ları satış anını `COALESCE(completed_at, ordered_at)` ile okur. Neden: gece 23:50'de verilip ertesi gün teslim edilen sipariş yanlış güne düşüyordu; "son satın alma" ve "X gündür gelmedi" segmentleri (CRM-4) gerçek satış anına dayanmalı.

### ÖNCE
`order_history` yalnız `ordered_at` (sipariş verme anı) taşıyor. `v_customer_stats` / `v_customer_branch_stats` bu alandan `first_order_at` / `last_order_at` / `days_to_repeat` üretiyor.

### SONRA
- Kolon: `order_history.completed_at timestamptz NULL` (backfill YOK, eski siparişler NULL)
- Trigger fonksiyonu: `crm_stamp_order_completed_at()` (PL/pgSQL)
- Trigger: `trg_order_history_completed_at` — `BEFORE INSERT OR UPDATE OF status`, satır bazlı
  - status `completed` veya `served` olur ve `completed_at` NULL ise `now()` yazar
  - dolu değeri EZMEZ
  - UPDATE'te status DEĞİŞMEDİYSE damgalamaz (Neon'dan elle aynı status'le düzeltme eski siparişi bugüne yazmasın)
- View'lar (`CREATE OR REPLACE`, kolon adı/tipi/sırası aynı): satış anı `COALESCE(completed_at, ordered_at)`
- ⚙️ Drizzle'ın ifade edemedikleri: trigger, fonksiyon, view'lar (sadece kolon `schema.ts`'te)

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` (`orderHistory.completedAt` + başlık notu)
- `TEKNIK_BORC_CRM.md`: TB-CRM-24 → ✅ (canlı doğrulamadan sonra)
- `SESSION_INDEX.md`, `ARCHITECTURE.md` (view/trigger notu)
- Uygulama kodu (route'lar, `updateOrderStatus`): DEĞİŞMEZ

### ⚠️ RISK_DOMAINS işareti
- **KVKK (§4):** Yok — yeni kişisel veri alanı değil, mevcut siparişin zaman bilgisi.
- **Fiyat/ödeme (§2):** view'lardaki ödeme filtreleri (`nakit` / `odendi`, `iade_edildi` / `tutarsizlik` hariç) AYNEN korundu; yalnız zaman alanı değişti.
- **Eşzamanlılık (§3):** iki personelin aynı anda durumu değiştirmesi trigger'da sorun çıkarmaz (dolu değer ezilmez).

### SIRA (bozulursa canlı akış kırılır)
1. Bu not `docs/schema-changes/` altına kaydedilir.
2. `20261011170000_crm_order_completed_at_migration.sql` Neon SQL Editor'de TEK SEFERDE koşulur.
3. `20261011170000_crm_order_completed_at_dogrulama.sql` koşulur; BEKLENEN: hata mesajı `TEST_OK` ile başlar.
4. SONRA `schema.ts` push edilir.
5. Canlı doğrulama (DRIFT KONTROLÜ) + bir gerçek siparişte davranış testi.

### GERİ ALMA
```sql
-- Sıra: view'lar (eski hâl) → trigger → fonksiyon → kolon. View'lar kolona bağlı, önce çözülmeli.
BEGIN;

CREATE OR REPLACE VIEW v_customer_branch_stats AS
SELECT customer_phone AS phone,
       branch_id,
       count(*) AS order_count,
       sum(total_price) AS total_spend,
       min(ordered_at) AS first_order_at,
       max(ordered_at) AS last_order_at
  FROM order_history oh
 WHERE status = ANY (ARRAY['completed'::text, 'served'::text])
   AND (payment_method = 'nakit'::text OR payment_status = 'odendi'::text)
   AND payment_status <> ALL (ARRAY['iade_edildi'::text, 'tutarsizlik'::text])
 GROUP BY customer_phone, branch_id;

CREATE OR REPLACE VIEW v_customer_stats AS
WITH real_sales AS (
  SELECT oh.id, oh.customer_phone, oh.total_price, oh.ordered_at,
         row_number() OVER (PARTITION BY oh.customer_phone ORDER BY oh.ordered_at, oh.id) AS rn
    FROM order_history oh
   WHERE oh.status = ANY (ARRAY['completed'::text, 'served'::text])
     AND (oh.payment_method = 'nakit'::text OR oh.payment_status = 'odendi'::text)
     AND oh.payment_status <> ALL (ARRAY['iade_edildi'::text, 'tutarsizlik'::text])
),
agg AS (
  SELECT rs.customer_phone,
         count(*) AS order_count,
         sum(rs.total_price) AS total_spend,
         avg(rs.total_price) AS avg_order_value,
         min(rs.ordered_at) AS first_order_at,
         max(rs.ordered_at) AS last_order_at,
         round(EXTRACT(epoch FROM min(rs.ordered_at) FILTER (WHERE rs.rn = 2)
                                - min(rs.ordered_at) FILTER (WHERE rs.rn = 1)) / 86400.0, 2) AS days_to_repeat
    FROM real_sales rs
   GROUP BY rs.customer_phone
)
SELECT u.phone,
       u.created_at AS registered_at,
       COALESCE(a.order_count, 0::bigint) AS order_count,
       COALESCE(a.total_spend, 0::numeric) AS total_spend,
       a.avg_order_value,
       a.first_order_at,
       a.last_order_at,
       a.days_to_repeat
  FROM users u
  LEFT JOIN agg a ON a.customer_phone = u.phone
 WHERE u.role = 'customer'::text;

DROP TRIGGER IF EXISTS trg_order_history_completed_at ON order_history;
DROP FUNCTION IF EXISTS crm_stamp_order_completed_at();
ALTER TABLE order_history DROP COLUMN IF EXISTS completed_at;

COMMIT;
```
**Veri girildikten sonra geri almanın etkisi:** `completed_at` değerleri silinir. Kanıt/ledger niteliği YOK (türetilmiş zaman bilgisi, `ordered_at` duruyor); kayıp yalnız o tarihler için "gerçek teslim anı" hassasiyetidir.
**Kod geri alma sırası:** önce `schema.ts` push'unu geri al (kolonu okuyan Drizzle sorgusu kırılmasın), sonra yukarıdaki SQL.

### DRIFT KONTROLÜ
```sql
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'order_history' AND column_name = 'completed_at';
-- BEKLENEN: timestamp with time zone | YES

SELECT tgname FROM pg_trigger
WHERE tgrelid = 'order_history'::regclass AND NOT tgisinternal;
-- BEKLENEN: listede trg_order_history_completed_at var (attribution trigger'ı da durur)

SELECT pg_get_viewdef('v_customer_stats'::regclass, true) LIKE '%completed_at%' AS stats_ok,
       pg_get_viewdef('v_customer_branch_stats'::regclass, true) LIKE '%completed_at%' AS branch_ok;
-- BEKLENEN: true | true
```

### Edge case notları
- **Eski siparişler:** `completed_at` NULL kalır → view'lar `ordered_at`'e düşer, mevcut raporlar aynı sonucu verir.
- **Aynı status'le UPDATE:** damgalamaz (testle kanıtlı).
- **completed → served:** `completed_at` ilk tamamlanma anında kalır, ezilmez.
- **Durum geri alınırsa** (ör. `completed` → başka): `completed_at` kalır, ama view'lar yalnız `completed`/`served` satırlarını saydığı için etkisi yok.
- **Test satırları:** doğrulama SQL'i atomik `DO` bloğuyla yazılır, `TEST_OK` ile geri alınır; `order_history` append-only DEĞİL ama gerçek tabloda test verisi kalmaz.
- **Drizzle tipi:** `OrderHistoryRow` artık `completedAt: Date | null` içerir. Bu tipte tam satır üreten test fixture/mock'lar `tsc` hatası verebilir → `npx tsc --noEmit` ile kontrol et.
- **View seçenekleri:** `CREATE OR REPLACE` sahip/yetkileri korur. View'lara özel `reloptions` (ör. `security_invoker`) tanımlıysa kontrol et: `SELECT relname, reloptions FROM pg_class WHERE relname IN ('v_customer_stats','v_customer_branch_stats');` (beklenen: NULL).
