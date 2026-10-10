## Session: CRM-1 (TB-CRM-17) — 2026-10-10
## Açıklama: CRM-1 Adım 1 (SADECE ŞEMA). Üç yeni tablo: `marketing_consents` (append-only rıza ledger'ı), `crm_audit_log` (append-only), `iys_sync_queue` (İYS aktarım kuyruğu). Neden: pazarlama izninin "ne zaman, hangi metin sürümüyle, hangi kanal için, verildi mi geri alındı mı" ispatı. Mevcut `consent_registrations` tek satır/upsert olduğu için geçmiş tutamaz, bu iş için YETERSİZ. Kod adımı (kayıt formu + yazım) bu notun kapsamı DIŞINDA.

### ÖNCE
Bu üç tablo yok. `consent_registrations` (KVKK kayıt rızası, telefonda tek satır) ve `users.email` (doğrulanmıyor, TB-CRM-15) mevcut.

### SONRA
- `marketing_consents(id uuid pk, phone text, channel text, action text, policy_version text, source text, branch_id uuid null → branches.id, ip_address text null, created_at timestamptz)`
  - `channel` IN ('sms','email'); `action` IN ('granted','revoked'); `source` IN ('registration','account','sms_reply','link','staff') — CHECK constraint (Drizzle bunları şema dosyasında NATIVE temsil etmez, `users.role` ile aynı durum: yeni değer eklenirse DB'de de güncellenmeli).
  - Güncel durum = (phone, channel) için EN SON satır. Geri alma = yeni `revoked` satırı.
  - UPDATE/DELETE/TRUNCATE trigger ile ENGELLİ (append-only).
  - `users`'a FK YOK (proje deseni: düz telefon eşleşmesi). Rıza marka seviyesinde; `branch_id` yalnız kayıt kaynağı.
- `crm_audit_log(id uuid pk, actor text, action text, entity text, entity_id text null, metadata jsonb default '{}', created_at)` — append-only, `metadata`'ya KİŞİSEL VERİ (telefon/e-posta/ad) YAZILMAZ.
- `iys_sync_queue(id uuid pk, consent_id uuid UNIQUE → marketing_consents.id, status, attempts, last_error, created_at, processed_at)` — status IN ('pending','sent','failed'). Bu aşamada sadece kuyruk dolacak, İYS'ye GERÇEK gönderim YOK (yöntem hukuk kararına bağlı, TB-CRM-03).

### ETKİLENEN DOSYALAR
`lib/db/schema.ts` (3 tablo + tip eklendi, mevcut tablolara dokunulmadı), `TEKNIK_BORC_CRM.md` (TB-CRM-17 durumu). Mevcut hiçbir sorgu/route bu tabloları okumaz/yazmaz → mevcut akışlar etkilenmez.

### ⚠️ RISK_DOMAINS §4 (KVKK) İŞARETİ — insan/hukuk onayı şart
Bu değişiklik kişisel veri (telefon, IP) işleyen yeni tablolar ekliyor. AI uygunluk onayı VEREMEZ. Hukuk görüşüne bağlı açık noktalar: (1) `ip_address` saklama amacı/süresi (2) ticari ileti onay metni (`policy_version` ile eşleşecek) (3) silme talebi ↔ append-only ledger çakışması: CRM-7'de erase, trigger'ı kontrollü şekilde aşan ayrı/yetkili bir yol gerektirecek — bu aşamada TASARLANMADI. TB-CRM-03 (sorumlu atanmadı) kapanmadan bu tablolara GERÇEK müşteri rızası yazan kod CANLIYA ALINMAZ.

### SIRA (ihlal edilirse FP-3 tekrarı olur, #121 dersi)
1. Bu not `docs/schema-changes/` altına kaydedilir.
2. `crm1_migration.sql` Neon SQL Editor'de koşulur.
3. `crm1_dogrulama.sql` koşulur; BEKLENEN sonuç: hata mesajı `TEST_OK` ile başlar (test satırı otomatik geri alınır).
4. SONRA `schema.ts` push edilir.

### GERİ ALMA
Tablolar yeni ve hiçbir kod okumadığı için güvenli:
```sql
DROP TABLE IF EXISTS iys_sync_queue;
DROP TABLE IF EXISTS crm_audit_log;
DROP TABLE IF EXISTS marketing_consents;
DROP FUNCTION IF EXISTS crm_forbid_mutation();
```
`schema.ts` değişikliği de geri alınır (3 tablo bloğu silinir). Veri girildikten SONRA geri alma = rıza kanıtı kaybı, bu yüzden canlı veri girmeden önce kararlı olunmalı.

### Edge case notları
- Aynı (phone, channel) için ardışık `granted` satırı serbest (ledger); güncel durum okuyan kod `ORDER BY created_at DESC, id` ile TEK satır seçmeli (aynı transaction'da eşit zaman damgası riski → CRM-5 kapısında test edilecek).
- Geçersiz channel/action/source → CHECK reddeder.
- `branch_id` NULL serbest (şube araması başarısız olsa rıza yazımı düşmesin).
- Telefon biçimi `users.phone` ile AYNI normalize biçimde yazılmalı (kod adımında doğrulanır).
