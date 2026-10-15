## Session: CRM-5 / TB-CRM-21 Adım 2 — 2026-10-15
## Açıklama: Kampanya şablonları (sürümlü, değişmez içerik), kampanya taslakları ve gönderim kaydı tabloları eklenir. Sürümlü yapı, gönderilmiş ticari ileti içeriğinin sonradan değiştirilememesi (ispat) içindir; gönderim kaydı haftalık sınır sayacını ve çift gönderim korumasını (K-20) DB düzeyinde mümkün kılar. Bu turda YALNIZ şema: hiçbir kod bu tabloları okumaz/yazmaz.

### ÖNCE
Canlıda `campaign_templates`, `campaign_template_versions`, `campaigns`, `campaign_sends` YOK. `crm_tags`, `branches`, `users` var (FK hedefleri). `canSendMarketing` (saf katman) kodda var ama haftalık sınır için sayılacak bir kayıt tablosu yok.

### SONRA
- `campaign_templates` (id, name, channel, created_by, created_at, archived_at). **Yalnız SQL:** CHECK name 1–60, CHECK channel IN ('sms','email'), UNIQUE INDEX `lower(name)`.
- `campaign_template_versions` (id, template_id FK, version, body, created_by, created_at). UNIQUE (template_id, version). **Yalnız SQL:** CHECK version>=1, CHECK body boş değil, **trigger'lar:** `trg_ctv_no_row_change` (UPDATE/DELETE), `trg_ctv_no_truncate` (TRUNCATE) — APPEND-ONLY, fonksiyon `campaign_template_versions_append_only()`.
- `campaigns` (id, name, template_version_id FK→sürüm, segment nullable, tag_id nullable FK→crm_tags, branch_id nullable FK→branches [null = tüm şubeler], status default 'draft', created_by, created_at, updated_at). **Yalnız SQL:** CHECK name 1–80, CHECK status IN ('draft','ready','cancelled'), indeks (status, created_at DESC).
- `campaign_sends` (id, campaign_id FK, phone, channel, status, created_at, updated_at). UNIQUE (campaign_id, phone, channel). **Yalnız SQL:** CHECK phone boş değil, CHECK channel, CHECK status IN ('queued','sent','failed'), indeks (phone, channel, created_at DESC).
- Şube adresi değişkeni KAPSAM DIŞI (kullanıcı kararı: şimdilik çıkar; `branches`'te adres kolonu yok).

### ETKİLENEN DOSYALAR
`lib/db/schema.ts` (4 tablo + `unique` importu + üst yorum satırı — blok `schema-crm5-ekleme.ts`'te), `TEKNIK_BORC_CRM.md` (TB-CRM-21 durumu), `SESSION_INDEX.md`, `CRM_KVKK_CHECKLIST.md` (K-20 kısmen DB düzeyinde karşılanır; K-24 saklama tablosuna `campaign_sends` satırı), `ARCHITECTURE.md` (şema listesi — verilmedi, GÜNCELLENMEDİ). Okuyan/yazan kod YOK.

### ⚠️ RISK_DOMAINS işareti
- **KVKK (§4): EVET.** `campaign_sends.phone` kişisel veridir. Açık, **insan/hukuk kararı:** saklama süresi (K-08/K-24), silme talebi ↔ gönderim kaydı çakışması (K-21/K-22, CRM-7). Bu not uygunluk onayı VERMEZ.
- **Eşzamanlılık (§3): EVET.** (a) Sürüm numarası yarışı → UNIQUE ihlali, uygulama yeniden dener. (b) Çift gönderim → `campaign_sends_once_uq` DB düzeyinde engeller (K-20'nin yalnız DB kısmı; gerçek cron çift tetikleme testi CRM-6).
- **Fiyat/ödeme (§2): Yok.**

### SIRA (bozulursa canlı akış kırılır)
1. Bu not `docs/schema-changes/` altına kaydedilir.
2. `crm5_migration.sql` Neon SQL Editor'de koşulur.
3. `crm5_dogrulama.sql` koşulur; BEKLENEN: hata mesajı `TEST_OK` ile başlar.
4. SONRA `schema.ts` bloğu + push (bu turda okuyan kod yok → kırılma riski düşük, sıra yine de korunur).
5. Canlı doğrulama (DRIFT KONTROLÜ) → TB-CRM-21 şema kısmı ancak burada ✅ olur.

### GERİ ALMA  ← ZORUNLU
```sql
BEGIN;
DROP TABLE IF EXISTS campaign_sends;
DROP TABLE IF EXISTS campaigns;
DROP TABLE IF EXISTS campaign_template_versions;
DROP TABLE IF EXISTS campaign_templates;
DROP FUNCTION IF EXISTS campaign_template_versions_append_only();
COMMIT;
```
**Veri girildikten sonra geri almanın etkisi:** `campaign_template_versions` içerik-ispat kaydıdır → silinirse gönderilmiş iletilerin metni KANITI KAYBOLUR. `campaign_sends` silinirse haftalık sınır sayacı sıfırlanır → fazla ileti riski. Bu yüzden veri girildikten sonra geri alma YAPILMAZ; önce kampanyalar `cancelled` yapılır.
**Kod geri alma sırası:** önce kodu geri al (okuyan/yazan kod eklendiyse), sonra SQL.

### DRIFT KONTROLÜ (canlı şema = `schema.ts`)
```sql
SELECT table_name, column_name, data_type, is_nullable FROM information_schema.columns
WHERE table_name IN ('campaign_templates','campaign_template_versions','campaigns','campaign_sends')
ORDER BY table_name, ordinal_position;

SELECT conrelid::regclass AS tablo, conname, pg_get_constraintdef(oid) FROM pg_constraint
WHERE conrelid IN ('campaign_templates'::regclass,'campaign_template_versions'::regclass,'campaigns'::regclass,'campaign_sends'::regclass)
ORDER BY 1, 2;

SELECT tgname FROM pg_trigger WHERE tgrelid = 'campaign_template_versions'::regclass AND NOT tgisinternal ORDER BY 1;
-- BEKLENEN: 2 satır (trg_ctv_no_row_change, trg_ctv_no_truncate)
```
TRUNCATE trigger'ı `crm5_dogrulama.sql`'de DENENMEZ (FK nedeniyle TRUNCATE zaten hata verir ve yanlış "engelli" sonucu doğururdu) — yalnız trigger varlığı yukarıdan teyit edilir.

### Edge case notları
1. **Tekrar çalıştırma:** migration idempotent (IF NOT EXISTS, CREATE OR REPLACE FUNCTION, DROP TRIGGER IF EXISTS). Ama kısmen kurulu eski tablo farklı kolonla varsa IF NOT EXISTS onu düzeltmez → drift kontrolü şart.
2. **NULL anlamı:** `branch_id` null = tüm şubeler; `segment`/`tag_id` null = o süzme yok. Üçü de null = "tüm rızalı müşteriler" — bunun taslakta onay gerektirmesi Adım 3/4 UYGULAMA kararıdır (DB engellemez).
3. **Taslak kilidi:** `ready` olduktan sonra kampanyanın hedefini/şablonunu değiştirmeyi DB engellemez (yalnız sürüm içeriği değişmez); kilit uygulama kodunda olacak. Açık risk.
4. **E-posta konusu (subject)** kolonu YOK: e-posta kanalı alan adı/sağlayıcı (TB-CRM-01) gelene dek kullanılamaz; gelince nullable `subject` eklenir (ayrı şema notu).
5. **Durum kümeleri** (`campaigns.status`, `campaign_sends.status`) asistan önerisidir, kullanıcı onayı yok; CRM-6 genişletebilir (CHECK güncellenir). Ad uzunlukları (60/80) iç etiket sınırıdır, SMS metin sınırı DEĞİL (sağlayıcı sınırı doğrulanmadı, `body` için üst sınır konmadı).
