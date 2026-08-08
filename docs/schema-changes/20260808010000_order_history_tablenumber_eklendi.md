## Session: 12 devamı — 2026-08-08
## Açıklama:
Masaya Sipariş (§2.7b) akışında masa numarasının tutulması gerektiği kararlaştırıldı —
kullanıcı onayı bu sohbette alındı. Gerekçe: Masaya Sipariş'in amacı "QR'ı okut, saniyeler
içinde sipariş ver"; masa numarası olmadan personel siparişi hangi masaya götüreceğini
bilemez, müşteriye sorması QR akışının kazandırdığı sürtünmesiz deneyimi sıfırlar. Bu
mimari bir tercih değil, fiziksel bir zorunluluktur (dine-in sipariş sistemi masa eşlemesi
olmadan eksik sayılır). `order_history` tablosuna nullable `table_number` kolonu eklenir —
SADECE `channel="dine-in"` satırlarında dolu olacak, Gel Al (`channel="pickup"`)
satırlarında her zaman NULL kalacak.

### ÖNCE
`order_history` tablosu (Session 10'da migrate edildi ve doğrulandı). Bu notun kapsamı
SADECE eklenen kolonu belgeliyor — tablonun TAM kolon listesi ARCHITECTURE.md §3'te
`OrderHistoryEntry` hâlâ yer tutucu olduğu için bu dosyada da tekrarlanmıyor (Sahte Veri
Yasağı ruhu — bilinmeyen alanlar için varsayım yapılmadı). Bilinen/doğrulanmış tek kolon:
`channel` (`"dine-in" | "pickup"`, bkz. Açık Sorun #69 KAPANDI notu, ARCHITECTURE.md §2.7b).

### SONRA
Yeni kolon: `table_number`
- Nullable — `channel != "dine-in"` olan satırlarda her zaman NULL
- Tip: HENÜZ KESİNLEŞMEDİ (text mi integer mı — masa numaralandırma şemasının kendisi
  [ör. "14" mü "Masa 14" mü] netleşmeden karar verilemez). Migration koşulmadan önce bu
  netleştirilmeli — TODO: PROD, kodlama turunda karara bağlanacak.
- Index gereksinimi: Personel Sipariş Paneli'nin (#62, henüz tasarlanmadı) masa bazlı
  filtreleme/gruplama yapıp yapmayacağına bağlı — bu notun kapsamı dışında, #62 tasarım
  turunda netleşmeli.

### ETKİLENEN DOSYALAR
- `lib/db/schema.ts` — `order_history` tanımına kolon eklenmeli (migration HENÜZ KOŞULMADI)
- `ARCHITECTURE.md` — §2.3 (`CartState.tableId`), §2.7b (Masa numarası kararı), §3
  (`OrderHistoryEntry` yer tutucu notu), §4.1 (Deploy tablosu) — bu turda GÜNCELLENDİ (v1.11)
- `types/index.ts` — `OrderHistoryEntry` tipi tanımlandığında `table_number` dahil edilmeli;
  tip HENÜZ TANIMLI DEĞİL, bu notun kapsamı dışında
- Personel Sipariş Paneli (#62, henüz kodlanmadı) — masa bazlı görünüm/filtreleme
  gerektirebilir, tasarım turunda değerlendirilmeli
- `app/masaya-siparis/[tableId]/page.tsx` (henüz kodlanmadı) — sipariş tamamlanınca bu
  kolonu doldurmalı

### GERİ ALMA
Migration henüz koşulmadığı için bu aşamada geri alma gerekmiyor (bu not sadece kararı
belgeliyor). Migration koşulduktan sonra geri alma:
```sql
ALTER TABLE order_history DROP COLUMN table_number;
```
