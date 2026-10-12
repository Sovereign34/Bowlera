## Session: CRM-3d-1 müşteri etiketleri şeması (TB-CRM-19) — 2026-10-12
## Açıklama: Admin'in müşterilere atayabileceği SABİT etiket listesi için iki tablo: `crm_tags` (etiket tanımı) ve `customer_tags` (müşteri–etiket ataması). Etiketler serbest metin DEĞİL; böylece özel nitelikli/olumsuz bilgi (sağlık, din, "sorunlu müşteri") girilemez. Başlangıç etiketleri SQL ile eklenir, tanımlama ekranı sonraya.

### ÖNCE
Etiket tablosu yok. 3c ile yalnız `customer_notes` var; `users` sayfasında Etiketler bölümü yok.

### SONRA
- `crm_tags(id uuid PK, name text NOT NULL, created_at, archived_at NULL)`. **Drizzle'ın ifade edemedikleri:** `chk_crm_tags_name` CHECK (kırpılmış ve 1–30 karakter) ve `uq_crm_tags_name_lower` UNIQUE INDEX `lower(name)` (büyük/küçük harf farkıyla tekrar yok). Etiket SİLİNMEZ, `archived_at` ile arşivlenir.
- `customer_tags(customer_id → users, tag_id → crm_tags, added_by → users, created_at)`, birleşik PK `(customer_id, tag_id)`. `customer_id` FK'sı `ON DELETE CASCADE` (müşteri silinirse etiketi de gider; bu yalnız SQL'de, Drizzle ifade etmez). Atama KALDIRILABİLİR (satır silinir); kaldırma kaydı `crm_audit_log`'da kalır. Tablo append-only DEĞİL.
- Başlangıç etiketleri: "Sık müşteri", "Kurumsal sipariş", "Toplu sipariş". "Kampanyaya uygun" bilinçli YOK: pazarlama izni ayrı rıza kaydıyla yönetilir, etiketle karışmasın.

### ETKİLENEN DOSYALAR
`lib/db/schema.ts` (iki tablo, 3d-2'de), `TEKNIK_BORC_CRM.md` TB-CRM-19, `SESSION_INDEX.md`, `ARCHITECTURE.md` (bu turda verilmedi). Kod (3d-2): `lib/crm/customer-tag-{params,queries,access}.ts`, `lib/crm/audit.ts` (`customer_tag_added` / `customer_tag_removed`), 360 sayfasına Etiketler bölümü. ⚠️ 3d-2 öncesi `crm_audit_log.action` üzerinde CHECK var mı bakılır (`pg_constraint`); varsa yeni eylemler aynı turda eklenir.

### ⚠️ RISK_DOMAINS işareti
- **KVKK (§4): EVET.** Bu değişiklik `users`'a bağlı müşteri sınıflandırma verisi tutuyor. Serbest metin olmaması riski azaltır ama etiketlerin profilleme sayılıp sayılmadığı ve aydınlatma metninde yer alması gerekip gerekmediği **insan/hukuk kararı** (TB-CRM-47 ile aynı sınıf). Silme talebinde etiketler müşteriyle birlikte gider (`ON DELETE CASCADE`); `users` silme akışı CRM-7'de ayrıca çözülmeli (notlardaki FK engeli geçerli).
- Fiyat/ödeme (§2): Yok.
- Eşzamanlılık (§3): çift atama birleşik PK ile engellenir; iki yönetici aynı anda eklerse biri `unique_violation` alır (3d-2'de kullanıcıya zararsız yanıt).

### SIRA (bozulursa canlı akış kırılır)
1. Bu not `docs/schema-changes/` altına kaydedilir.
2. `20261012140000_crm3d_customer_tags_migration.sql` Neon SQL Editor'de TEK BAŞINA koşulur.
3. AYRI sorguyla `to_regclass` ile iki tablonun varlığı doğrulanır (3c dersi: 'TEST_OK' tabloyu kanıtlamaz).
4. `..._dogrulama.sql` ayrı koşulur; BEKLENEN: hata mesajı `TEST_OK` ile başlar.
5. SONRA `schema.ts` + kod push edilir.
6. Canlı doğrulama (drift sorguları + davranış testi) → TB ancak burada ✅ olur.

### GERİ ALMA
```sql
BEGIN;
DROP TABLE IF EXISTS customer_tags;
DROP TABLE IF EXISTS crm_tags;
COMMIT;
```
**Veri girildikten sonra geri almanın etkisi:** tüm etiket tanımları ve atamaları kaybolur (append-only değil, ispat kaybı yok; `crm_audit_log` satırları kalır).
**Kod geri alma sırası:** önce kod (schema.ts + 3d-2 dosyaları), sonra SQL.

### DRIFT KONTROLÜ (canlı şema = `schema.ts`)
```sql
SELECT table_name, column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name IN ('crm_tags','customer_tags') ORDER BY table_name, ordinal_position;

SELECT conrelid::regclass AS tablo, conname, pg_get_constraintdef(oid)
FROM pg_constraint WHERE conrelid IN ('crm_tags'::regclass, 'customer_tags'::regclass);

SELECT indexname FROM pg_indexes WHERE tablename IN ('crm_tags','customer_tags');
```
Fark varsa `schema.ts` ya da canlı DB düzeltilir, fark BU notta "bilinen drift" olarak yazılır.

### Edge case notları
- Migration idempotent (`IF NOT EXISTS`, `ON CONFLICT DO NOTHING`); ikinci koşuda hata vermez ve ikinci kez etiket eklemez.
- Postgres `lower()` Türkçe `I/İ` için yerel ayara bağlıdır; "ISIK" ile "ışık" aynı sayılmayabilir. Etiketler elle ve az sayıda eklendiği için kabul edildi.
- Arşivlenen etiket mevcut atamalarda kalır, yeni atamada listelenmez (3d-2 kuralı).
- `added_by` FK'sı yönetici hesabı silinmesini engeller; yönetici silme akışı şimdilik yok.
- Doğrulama bloğu `users` tablosundan ilk satırı kullanır, sonda `TEST_OK` ile geri alınır, kalıcı satır bırakmaz.
