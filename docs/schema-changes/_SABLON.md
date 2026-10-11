# BOWLERA — Şema Değişikliği Notu ŞABLONU (CRM)
> Her şema değişikliği için bu şablon kopyalanır: `docs/schema-changes/<YYYYMMDDHHMMSS>_<kisa_ad>.md`
> Kaynak: CORE.md §7.4 + TEKNIK_BORC_CRM.md TB-CRM-09/10. **Not, kod push'undan ÖNCE yazılır.**
> Kopyalanan dosyada bu giriş bloğu silinir, `<…>` alanları doldurulur. BOŞ BIRAKILAN ALAN = not eksik sayılır.

---

## Session: <aşama / TB-CRM-NN> — <YYYY-MM-DD>
## Açıklama: <ne eklendi/değişti + NEDEN, 2-3 cümle>

### ÖNCE
<şu an canlıda ne var / ne yok>

### SONRA
<tablo/kolon/view/trigger/CHECK listesi. Drizzle'ın ifade edemedikleri (view, trigger, SECURITY DEFINER, CHECK) AYRICA işaretlenir>

### ETKİLENEN DOSYALAR
<`lib/db/schema.ts`, ilgili sorgu/route'lar, `TEKNIK_BORC_CRM.md` hangi TB, `SESSION_INDEX.md`, `ARCHITECTURE.md`>

### ⚠️ RISK_DOMAINS işareti
<KVKK (§4): kişisel veri işleniyor mu? Fiyat/ödeme (§2)? Eşzamanlılık (§3)? İşaret yoksa "Yok" yaz, boş bırakma. AI uygunluk onayı VEREMEZ; açık noktaları "insan/hukuk kararı" olarak listele>

### SIRA (bozulursa canlı akış kırılır)
1. Bu not `docs/schema-changes/` altına kaydedilir.
2. `<ad>_migration.sql` Neon SQL Editor'de koşulur.
3. `<ad>_dogrulama.sql` koşulur; BEKLENEN: hata mesajı `TEST_OK` ile başlar.
4. SONRA `schema.ts` + kod push edilir (kod, migration'dan ÖNCE çıkarsa tabloyu okuyan sayfalar kırılır).
5. Canlı doğrulama (aşağıdaki "DRIFT KONTROLÜ") + davranış testi → TB ancak burada ✅ olur.

### GERİ ALMA  ← ZORUNLU, boş bırakılamaz
```sql
-- Tek transaction; sıra bağımlılığın TERSİ (view → tablo → fonksiyon)
BEGIN;
<DROP/ALTER komutları>
COMMIT;
```
**Veri girildikten sonra geri almanın etkisi:** <hangi veri kaybolur? append-only/ledger tabloysa "kanıt kaybı" yaz>
**Kod geri alma sırası:** <önce kodu geri al, sonra SQL>

### DRIFT KONTROLÜ (canlı şema = `schema.ts`)
Migration sonrası, Neon'da çalıştır ve `schema.ts` ile karşılaştır:
```sql
-- kolonlar
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = '<tablo>' ORDER BY ordinal_position;

-- CHECK / FK / UNIQUE
SELECT conname, pg_get_constraintdef(oid)
FROM pg_constraint WHERE conrelid = '<tablo>'::regclass;

-- trigger (append-only koruması dahil)
SELECT tgname FROM pg_trigger
WHERE tgrelid = '<tablo>'::regclass AND NOT tgisinternal;

-- view'lar
SELECT viewname FROM pg_views WHERE schemaname = 'public';
```
Fark varsa: `schema.ts` ya da canlı DB düzeltilir, fark BU notta "bilinen drift" olarak yazılır.

### Edge case notları
<3-5 madde: tekrar çalıştırma (idempotent mi?), NULL davranışı, eski satırlar, eşzamanlı yazım, CHECK ihlali>

---

## EK KURALLAR (CRM'e özgü)

**1. Append-only tablolar** (`marketing_consents`, `crm_audit_log`, `customer_events`): UPDATE/DELETE/TRUNCATE trigger'la engelli.
Doğrulama sırasında test satırı yazılırsa SİLİNEMEZ → doğrulama her zaman atomik `DO` bloğuyla yapılır, sonda `RAISE EXCEPTION 'TEST_OK'` ile geri alınır:
```sql
DO $$
BEGIN
  -- test satırı yaz, beklenen ihlalleri dene (UPDATE/DELETE hata vermeli)
  RAISE EXCEPTION 'TEST_OK';  -- transaction geri alınır, satır kalmaz
END $$;
```

**2. Neon HTTP sürücüsü transaction DESTEKLEMEZ** → uygulama kodunda çok adımlı yazım sıralı yapılır; atomiklik gereken yer SQL fonksiyonu/`DO` bloğudur.

**3. Preview yok, DB tek:** `main`'e push = canlı; Preview ortamı da AYNI Neon'a bağlı. Test verisi gerçek DB'ye yazılır → test numaraları/hesapları not edilir, işi bitince temizlenir (append-only tablolara test satırı YAZILMAZ).

**4. SQL, sohbette AYRI kod bloğu olarak verilir** (mobilde Neon SQL Editor'e dosyadan kopyalamak zor).

**5. Aynı adlı dosya ezilir:** birden çok `route.ts` yüklerken farklı ad kullan (`consent-route.ts`, `gel-al-route.ts`).

**6. Kapanış:** "build geçti" yetmez; TB ancak canlı doğrulamayla (drift sorguları + davranış testi) ✅ olur.
