## Session: CRM-6 başlangıcı (checkpoint 14) — 2026-10-16
## Açıklama: `campaign_sends.status` CHECK kümesi genişler: `skipped_holdout` ve `skipped_gate` eklenir. Neden: holdout (%10 mesaj almayan kontrol grubu) ve kapı reddi, "gönderilmedi" ile "gönderilemedi (failed)" arasında AYRI görünmeli; aksi halde holdout analizi (gönderilen vs gönderilmeyen) yapılamaz ve `failed` sayısı şişer.

### ÖNCE
`campaign_sends.status`: `queued | sent | failed` (CHECK, yalnız SQL — Drizzle ifade etmez).
Haftalık sınır sayacı yalnız `queued + sent` sayar.

### SONRA
`campaign_sends.status`: `queued | sent | failed | skipped_holdout | skipped_gate`
CHECK adı sabitlenir: `campaign_sends_status_check`.
Sütun, tablo, indeks, UNIQUE (`campaign_sends_once_uq`: campaign_id + phone + channel) DEĞİŞMEZ.

### KURALLAR (CRM-6 kodu bunlara uyar)
1. `skipped_*` satırları haftalık sınıra SAYILMAZ (iletilmediler). Sayım sorgusu `queued + sent` ile kalır.
2. `UNIQUE (campaign_id, phone, channel)` skipped satırlar için de geçerlidir: bir kişiye bir kampanyada TEK satır yazılır. Bu yüzden `skipped_gate` yalnız KALICI reddedilen kişiler için yazılır (rıza yok / geri çekilmiş). Geçici reddeden (sessiz saat, haftalık sınır, kill switch, kanal doğrulanmamış, test modu listesi dışı, rıza durumu "bilinmiyor" = veri sorunu olabilir, karar hatası) için satır YAZILMAZ; sonraki cron çalışmasında yeniden denenir. Aksi halde gece 22:00'de reddedilen kişi o kampanyadan bir daha mesaj alamaz.
3. `skipped_holdout` deterministik hesaplanır (kampanya + telefon özetinden); satır yazılması yeniden hesabı değiştirmez, yalnız kaydı tutar.
4. `campaign_sends.phone` kişisel veridir; skipped satırlar da telefon taşır. Saklama/silme açık sorunu (K-08, K-24) bunları da kapsar.

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` — yalnız YORUMLAR (satır 781 ve 826); tip/sütun değişmez, `tsc` etkilenmez
- `docs/schema-changes/` — bu not
- `ARCHITECTURE.md` — CRM-6 kapanışında güncellenir (şimdi değil)
- İleride: `lib/crm/campaign-send-count-sql.ts` (değişmez; `queued+sent` kalır — doğrulanacak), CRM-6 gönderim çekirdeği (yeni)

### UYGULAMA
1. `crm6_sema_1.sql` Neon'da çalıştırılır (tek `DO` bloğu, atomik; mevcut status CHECK'ini adından bağımsız bulup düşürür, yenisini ekler).
2. `crm6_sema_1_dogrulama.sql` çalıştırılır → `TEST_OK`.
3. `schema.ts` yorum değişikliği push edilir.
`campaign_sends` CRM-5'te BOŞ olduğu için mevcut satır riski yoktur (doğrulama SQL'i bunu da gösterir).

### GERİ ALMA
Yalnız tablo boşken veya hiç `skipped_*` satırı yokken güvenlidir:
```sql
DO $$
BEGIN
  IF EXISTS (SELECT 1 FROM public.campaign_sends WHERE status LIKE 'skipped_%') THEN
    RAISE EXCEPTION 'skipped_* satırları var; önce bunlar ele alınmalı (silme/yeniden sınıflandırma kararı gerekir)';
  END IF;
  ALTER TABLE public.campaign_sends DROP CONSTRAINT IF EXISTS campaign_sends_status_check;
  ALTER TABLE public.campaign_sends
    ADD CONSTRAINT campaign_sends_status_check CHECK (status IN ('queued','sent','failed'));
END $$;
```
`skipped_*` satırı varsa geri alma KASITLI olarak reddedilir; o durumda satırlar önce raporlanır, silinmez (ispat/analiz verisi).
`schema.ts` yorumları git ile eski haline döner.
