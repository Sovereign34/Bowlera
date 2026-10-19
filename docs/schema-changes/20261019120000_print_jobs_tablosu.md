## Session: Fiş yazdırma Aşama 2a — 2026-10-19
## Açıklama: Siparişlerin mutfak ve kasa yazıcılarına TEK SEFER, kayıpsız basılması için `print_jobs` tablosu eklendi. Her (sipariş, istasyon) çifti için bir satır; satır "aldım" (claimed_at) ve "bastım" (printed_at) anlarını tutar.

### ÖNCE
`print_jobs` tablosu yoktu. Fiş yazdırma altyapısı yoktu.

### SONRA
```sql
CREATE TABLE IF NOT EXISTS print_jobs (
  order_id   uuid NOT NULL REFERENCES order_history(id) ON DELETE CASCADE,
  station    text NOT NULL,
  claimed_at timestamptz NOT NULL DEFAULT now(),
  printed_at timestamptz,
  PRIMARY KEY (order_id, station)
);
```
Drizzle: `lib/db/schema.ts` → `printJobs`.

### ETKİLENEN DOSYALAR
lib/db/schema.ts, lib/personel/print-jobs-queries.ts, app/api/personel/yazici/route.ts, ARCHITECTURE.md (tablo listesi)

### GERİ ALMA
`DROP TABLE print_jobs;` — başka tablo bu tabloya bağlı değil (FK sadece print_jobs → order_history). Yazıcı sekmesi (Aşama 2b) devreye alınmadan önce geri alınırsa kayıp yok.

### UYGULAMA SIRASI
1. Neon SQL Editor'de yukarıdaki SQL'i çalıştır.
2. Sonra kodu deploy et. (Tablo yokken /api/personel/yazici hata döner, sipariş akışı ETKİLENMEZ.)
