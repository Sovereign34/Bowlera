# BOWLERA — CRM KVKK Kontrol Listesi
> v1.1 — 2026-10-11 (K-07, K-11, K-12 ✅ CRM-3a kanıtıyla) · v1.0 — 2026-10-11 — TB-CRM-11 (kaynak: `RISK_DOMAINS.md` §4, `TEKNIK_BORC_CRM.md` v2.0)
>
> ⚠️ **Bu liste uygunluk ONAYI DEĞİLDİR.** RISK_DOMAINS §4: son karar mercii insan/hukuki danışmandır; AI yalnızca "bu alana bakılmalı" diye işaretler. Hukukçu yok → 🔵 maddeler `KVKK_KARAR_KAPANIS.md`'deki yazılı kabulle taşınır veya ileride hukuk görüşüyle kapanır. Hiçbir madde AI'ın "kontrol ettim, temiz" demesiyle ✅ olmaz.
>
> **Durum:** ✅ mevcut ve kanıtlı · 🟡 yapılacak (aşama DoD'u) · 🔵 insan/hukuk kararı gerekir
> **Kullanım:** Her CRM aşaması kapanırken kendi bölümündeki maddeler kanıtla ✅ yapılır. Kanıt = test adı, SQL çıktısı veya canlı doğrulama (cümle değil).

---

## CRM-1 — Rıza toplama (TB-CRM-17)

| ID | Kontrol | Nasıl doğrulanır | Durum |
|---|---|---|---|
| K-01 | Rıza ledger'ı append-only: `marketing_consents` / `crm_audit_log` / `customer_events` UPDATE/DELETE/TRUNCATE'e kapalı | `crm1_dogrulama.sql` / `crm2_dogrulama.sql` → `TEST_OK` | ✅ canlıda |
| K-02 | Her rıza satırı onay metninin sürümünü (`policy_version`) taşır; kutular işaretsiz gelir | Test + bayrak açılınca gerçek kayıtla `granted` satırı | 🟡 kod ✅, canlı doğrulama bayrak açılınca |
| K-03 | Onay metni (`consent-text.ts`) hukuken yeterli mi | İnsan/hukuk | 🔵 şu an TASLAK |
| K-04 | Rıza ledger'ındaki IP'nin saklama süresi; "silme talebi ↔ append-only ledger (ispat)" çakışması | İnsan/hukuk kararı (CRM-7 öncesi) | 🔵 açık |

## CRM-2 — Olay ve kaynak verisi (TB-CRM-18/08/26)

| ID | Kontrol | Nasıl doğrulanır | Durum |
|---|---|---|---|
| K-05 | Kaynak (UTM) çerezi yalnız "Kabul" ile yazılır; satır onay sürümünü (`attribution_consent_version`) taşır; Reddet/geri çekme → NULL | Canlı: Kabul ve Reddet denendi | ✅ kayıt akışı · 🟡 sipariş akışı (TB-CRM-39) |
| K-06 | Kaynak verisi 90 gün sonra silinir; silme işi yalnız sayıları loglar | Dry-run canlıda 0/0; ilk gerçek silme sonrası Vercel Logs (TB-CRM-40) | ✅ kod · 🟡 ilk gerçek çalışma |
| K-07 | `customer_events.payload` içinde gereksiz kişisel veri yok (minimizasyon) | `record-customer-event.ts` okundu: payload yalnız `{channel, payment_method}` (sipariş) ve boş (kayıt); telefon/ad/adres YOK. 360 ekranı payload'ı hiç okumaz (test: olay sorgusu yalnız `eventType` + `occurredAt` seçer) | ✅ 2026-10-11 |
| K-08 | Olay günlüğü saklama süresi (`customer_events`, `crm_audit_log`) belirlenmiş ve yazılı | İnsan kararı (TB-CRM-14 saklama) | 🔵 açık |

## CRM-3 — Müşteri paneli (TB-CRM-19)

| ID | Kontrol | Nasıl doğrulanır | Durum |
|---|---|---|---|
| K-09 | Staff ekranında telefon maskeli, harcama/sipariş tutarı yok — **API katmanında** (yalnız UI'da gizleme yetmez) | Route testi: staff oturumuyla yanıt maskeli; admin oturumuyla tam | 🟡 |
| K-10 | Staff yalnız atandığı şubeyi görür (`staff_branches`, TB-CRM-07 (b)) | Test: başka şubeyi isteyen staff reddedilir | 🟡 |
| K-11 | Her müşteri verisi okuması `crm_audit_log`'a düşer (kim, ne zaman, hangi müşteri/segment); okunan KİŞİSEL VERİ log'a yazılmaz | Canlı: Neon `crm_audit_log` satırları `customer_list_viewed` `{page, hasQuery}` ve `customer_viewed` `{}`; `actor`/`entity_id` uuid; aranan telefon audit'te YOK (`hasQuery:true` doğrulandı). Audit yazılamazsa veri gösterilmez (testle) | ✅ 2026-10-11 (admin; personel erişimi 3b'de) |
| K-12 | Liste ve 360 sorgularında `SELECT *` yok; yalnız ekranın ihtiyacı olan kolonlar döner (minimizasyon) | Liste: telefon, ad, sipariş sayısı, harcama, son sipariş (adres/e-posta YOK); 360: ekranda gösterilen alanlar. Kod + test (`customer-queries.test.ts`) | ✅ 2026-10-11 |

## CRM-4/5 — Segment ve gönderim kapısı (TB-CRM-20/21)

| ID | Kontrol | Nasıl doğrulanır | Durum |
|---|---|---|---|
| K-13 | `canSendMarketing` şu durumlarda REDDEDER: rıza yok · rıza geri çekilmiş · kanal doğrulanmamış (TB-CRM-15) · kill switch kapalı · sessiz saat · haftalık sınır dolu | Her durum için ayrı test (en az 6) | 🟡 · kill switch + test modu ✅ (`sending-gate.ts`, 23 test) |
| K-14 | Önizleme/dry-run gerçek gönderim yapmaz; alıcı listesi yalnız sayı + maskeli örnek gösterir | Test: dry-run'da sağlayıcı çağrısı 0 | 🟡 |
| K-15 | Sessiz saat aralığı mevzuata uygun mu | İnsan/hukuk (21:00–09:00 muhafazakâr varsayılan, mevzuat aralığı DOĞRULANMADI) | 🔵 |

## CRM-6 — Gönderim (TB-CRM-22)

| ID | Kontrol | Nasıl doğrulanır | Durum |
|---|---|---|---|
| K-16 | Ret (opt-out) çalışır: ret → ledger'a geri çekme satırı → sonraki gönderim reddedilir. Ticari iletide ret yolu yazılı | **Gerçek SMS ile** ret testi (TB-CRM-22 kapanış şartı) | 🟡 |
| K-17 | Ticari ileti içeriği zorunlulukları (gönderici adı, ret ifadesi vb.) | İnsan/hukuk — mevzuat gereklilikleri DOĞRULANMADI | 🔵 |
| K-18 | Log'a telefon / e-posta / ileti içeriği YAZILMAZ; yalnız sayı ve iç id | `console.*` taraması (`lib/crm`, cron route'ları) + log testi; kapı ve silme işi bu kalıpta ✅ | ✅ mevcut kod · 🟡 gönderim kodu yazılınca tekrar |
| K-19 | Test gönderimi yalnız `CRM_TEST_PHONES`'a gider; gerçek müşteri verisiyle test yok; append-only tablolara test satırı YAZILMAZ | `sending-gate` testleri ✅; Preview da aynı Neon'a bağlı (TB-CRM-10) | ✅ kapı · 🟡 pratikte dikkat |
| K-20 | Gönderim işi idempotent: cron çift tetiklenirse aynı kişiye iki ileti gitmez | Gerçek SMS ile çift tetikleme testi | 🟡 |

## CRM-7 — Silme, dışa aktarım, raporlar (TB-CRM-23)

| ID | Kontrol | Nasıl doğrulanır | Durum |
|---|---|---|---|
| K-21 | Silme talebi akışı (e-postayla başvuru, D4=B) çalışır; silme sonrası sipariş toplamları tutarlı | Test + canlı deneme hesabıyla | 🟡 |
| K-22 | Rıza ledger'ı (silinemez) için anonimleştirme/ispat yaklaşımı | İnsan/hukuk kararı (K-04 ile birlikte) | 🔵 |
| K-23 | Dışa aktarım loglanır: kim, ne zaman, hangi segment, kaç kayıt (içerik log'da yok) | Test | 🟡 |
| K-24 | Saklama süreleri tek tabloda: kaynak 90 gün ✅; olay, audit, ledger, IP 🔵 | Belge güncel (`/kvkk`, `/cerez-politikasi` ile tutarlı) | 🔵 |

## Her aşamada (süreç)

| ID | Kontrol | Nasıl doğrulanır | Durum |
|---|---|---|---|
| K-25 | KVKK'ya dokunan her değişiklikte SELF-CHECK işareti: "bu değişiklik `users` / `consent_registrations` / `order_history` / `marketing_consents` / `customer_events` tablosunu etkiliyor" + "uygunluk onayı = insan" satırı | Yanıtta işaret var | 🟡 her tur |
| K-26 | Yurt dışı aktarım (Vercel ABD, Neon Frankfurt, Google): aydınlatmada açık yazı ✅; standart sözleşme e-postaları gönderildi | TB-CRM-35 | ✅ metin · 🟡 e-postalar |
| K-27 | E-posta kanalı için adres doğrulanmadan pazarlama gitmez | TB-CRM-15 | 🟡 |

---

## Aşama kapanış özeti (DoD'a işlenecek)

| Aşama | Zorunlu maddeler (kanıtla ✅) | İnsan kararı bekleyen |
|---|---|---|
| CRM-1 | K-01, K-02 | K-03, K-04 |
| CRM-2 | K-05, K-06, K-07 | K-08 |
| CRM-3 | K-09, K-10, K-11, K-12 | — |
| CRM-4/5 | K-13, K-14 | K-15 |
| CRM-6 | K-16, K-18, K-19, K-20, K-27 | K-17 |
| CRM-7 | K-21, K-23 | K-22, K-24 |
| Her aşama | K-25, K-26 | — |

*BOWLERA CRM_KVKK_CHECKLIST.md — v1.0 — 2026-10-11*
*Kaynak: RISK_DOMAINS.md §4 · TEKNIK_BORC_CRM.md v2.0 · KVKK_KARAR_KAPANIS.md (içeriği bu turda görülmedi; D1–D4 kararları SESSION_INDEX ve TEKNIK_BORC'tan alındı).*
