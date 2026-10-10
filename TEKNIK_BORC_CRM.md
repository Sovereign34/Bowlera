# BOWLERA — TEKNIK_BORC_CRM.md
> v1.4 — 2026-10-10 (CRM-2 Adım C2a işlendi: TB-CRM-08 durumu, UTM saklama kararı = çerez, Açık sorular #5/#7 güncellendi; yeni TB-CRM-26 çerez bandı/politikası). v1.3 — 2026-10-10 (CRM-2 Adım A+B+C1 işlendi: TB-CRM-05 ✅, TB-CRM-08 şema ✅, TB-CRM-18 durumu; yeni TB-CRM-24/25; Açık sorular güncellendi). v1.2 — 2026-10-10 (CRM-1 Adım 1+2 işlendi: TB-CRM-17 durumu). v1.1 — 2026-10-10 (TB-05 ve TB-06 Adım 3 kararları işlendi). v1.0 — 2026-10-09 (CRM hazırlık oturumu). Kaynak: `Bowlera_CRM_Teknik_Uygulama_Plani.md` + SESSION_INDEX v122 + `lib/db/schema.ts` (Bowlera_site-main_22.zip).
> **Amaç:** CRM'in canlıya çıkması için gereken HER ŞEYİ numaralı teknik borç olarak tutmak. Bu dosya SESSION_INDEX.md'yi şişirmemek için ayrıdır; index'te yalnızca **#161** satırı (ID listesi + durum) bulunur. Detay, kabul kriteri ve gerekçe BURADA.
> **Numara şeması:** `TB-CRM-NN`. Index'teki "#" numaraları açık sorun içindir, karışmaz. Her TB, index'teki bir # ile eşleşiyorsa "Kaynak" sütununda belirtilir.
> **Durum:** ✅ çözüldü · 🟡 açık/yapılabilir · 🔵 karar bekliyor · ⛔ dış bağımlılık/bloklu
> **Kapanış kuralı:** TB ancak **canlıda doğrulanınca** ✅ olur ("build geçti" yetmez). Kapanan TB'nin satırı silinmez, gerekçeyle ✅ yapılır; dosya şişerse CORE.md §7.1 mantığıyla gerekçeli taşınır.
> **Süreç (her aşama):** [KARAR BİLDİRİMİ] → şema notu (`docs/schema-changes/`, CORE.md §7.4, kod push'undan ÖNCE) → kod + test → canlı doğrulama → kapanış.

---

## 1. Kararlar (bu oturumda alındı)

| Tarih | Karar | Etki |
|---|---|---|
| 2026-10-09 | **2. şube yakında açılacak → şube altyapısı CRM'den ÖNCE kurulur** (#92 yönü ONAYLANDI; CRM planı Karar #4 "brand_id/branch_id şimdi eklenmesin" bu konuda GEÇERSİZ) | TB-CRM-06 CRM'in ilk işi; CRM tabloları şube-bilinçli tasarlanır |
| 2026-10-09 | Testler çalışıyor (kullanıcı beyanı) | TB-CRM-04 🟡 (2026-10-10 güncellendi: çalışıyor ama 24 dosya/42 test kırık; #141 yeşil paketle kapanır) |
| 2026-10-09 | Alan adı alınacak (kullanıcı) | TB-CRM-01 ilerliyor |
| 2026-10-09 | Netgsm belgeleri hazırlanıyor (kullanıcı) | TB-CRM-02 ilerliyor |
| 2026-10-10 | **Mevcut şube: `Bowlerapark` (slug `bowlerapark`).** TB-CRM-06 üç adıma bölündü ve ONAYLANDI: Adım 1 şema (branches + iki nullable `branch_id`, davranış değişmez), Adım 2 yazım kodu (gel-al route + kayıt sorgusu, testli), Adım 3 NOT NULL kararı. `consent_registrations.branch_id` DAHİL. | TB-CRM-06 |
| 2026-10-10 | TB-06 Adım 1+2 canlıda doğrulandı; testler çalıştırıldı: branch kodu yeşil, genel paket kırık (TB-CRM-04 düzeltildi) | TB-CRM-04, TB-CRM-06 |
| 2026-10-10 | **TB-06 Adım 3 KARARI: `branch_id` nullable KALIR** (şube araması hata verirse sipariş düşmesin). NOT NULL, ikinci şube + şube seçimi (TB-CRM-07) gerçek akışa girdikten sonra yeniden değerlendirilir. Şubesiz kayıt izleme sorgusu tutulur | TB-CRM-06 kapandı |
| 2026-10-10 | **TB-05 "gerçek satış" tanımı ONAYLANDI:** `status IN ('completed','served') AND (payment_method='nakit' OR payment_status='odendi')`. `confirmed` (onaylı ama teslim edilmemiş) SATIŞ SAYILMAZ; `rejected`, `iptal_edildi`, `pending`, `preparing`, `ready`, `basarisiz`, `iade_edildi`, `tutarsizlik` de hariç | TB-CRM-05, CRM-2/CRM-4 |
| 2026-10-10 | **CRM-2 tasarımı ONAYLANDI (kullanıcı):** metrikler `order_history` üzerindeki VIEW'lardan (olay tablosundan DEĞİL); `customer_events` append-only (`customer_registered`, `order_placed`; `order_completed` YOK — `order_history`'de tamamlanma zamanı yok); attribution iki tabloda dört nullable kolon (`acquisition_source`, `utm_source`, `utm_medium`, `utm_campaign`), `channel` kullanılmaz; sıra A şema → B backfill → C yakalama/yazım → D test. ⚠️ `Bowlera_CRM_Teknik_Uygulama_Plani.md` oturumda HİÇ yüklenmedi — olay tipleri/payload plandan değil asistan önerisinden | TB-CRM-05, -08, -18 |
| 2026-10-10 | **`customer_registered` zamanı = `users.created_at`** (kullanıcı onayı); `source_key` = `customer_registered:<users.id>` / `order_placed:<order_history.id>` (backfill ve canlı yazım AYNI anahtar) | TB-CRM-18 |
| 2026-10-10 | **UTM/attribution saklama biçimi = ÇEREZ (kullanıcı kararı;** `sessionStorage` önerisine rağmen). Çerez bandı/politikası olup olmadığına açık yanıt gelmedi, `layout.tsx`'te bant YOK → "yok" varsayıldı; yakalama `CRM_ATTRIBUTION_ENABLED` bayrağı arkasında KAPALI. Asistan varsayımları (ONAY BEKLİYOR): ilk temas, çerez `bowlera_attr`, 30 gün (geçici, TB-CRM-14), yalnız UTM/dış yönlendiren sinyalinde yazılır | TB-CRM-08, TB-CRM-26 |
| 2026-10-10 | **Onaylı TB-05 koşuluna EK KORUMA (asistan önerisi):** `AND payment_status NOT IN ('iade_edildi','tutarsizlik')` — nakit + iade/tutarsızlık sipariş satış SAYILMAZ. Şema notunda ve sohbette açıkça bildirildi, açık itiraz gelmedi; AYRI onay bekliyor (Açık sorular #7). İstenmezse iki view'dan tek satır silinir | TB-CRM-05 |

## 2. Şemadan doğrulanan gerçekler (planı düzelten noktalar)

- Plan Bölüm 2, `status` için `bekliyor|odendi|…` yazıyor; bunlar **`payment_status`** değerleri. `order_history.status` ise Gel Al: `pending|confirmed|rejected|completed|iptal_edildi`, Masaya: `pending|preparing|ready|served`.
- **Nakit siparişte `payment_status` bilinçli olarak sürekli `bekliyor` kalır** — "sadece `odendi` olanları say" nakit satışları yok sayar.
- `order_history.channel` = fulfillment kanalı (`pickup|dine-in`); pazarlama/şube kanalı DEĞİL. Yeni alanlar `channel` adını kullanmaz.
- `order_history`'ye INSERT eden **tek yer**: `app/api/orders/gel-al/route.ts` (satır ~506). Masaya checkout'u henüz kodlanmadı → şube alanı eklemek şimdi en ucuz an. DB 2026-10-01'de sıfırlandı → geriye dönük "hangi şube?" belirsizliği yok.
- `users.phone`, `consent_registrations.phone` UNIQUE; FK konvansiyonu yok (düz `phone` eşleşmesi) — CRM bu konvansiyonu sürdürür.
- `users.email` NOT NULL (e-posta kanalı veri tarafında hazır), ama DOĞRULANMIYOR (#152).
- `rate_limits` tablosu mevcut; `@netgsm/sms` bağımlılıkta VAR ama kodda KULLANILMIYOR; Twilio OTP kodu var (PARKLI).
- Kodda `users.loyaltyPoints` yorumu hâlâ "#30" diyor, index'te #30 satırı yok (arşivde) → TB-CRM-12.

## 3. Borç listesi

### A. Önkoşullar ve kararlar (CRM-0)

| ID | Başlık | Durum | Bloklar | Kaynak | Kabul kriteri (canlı) |
|---|---|---|---|---|---|
| TB-CRM-01 | Alan adı + pazarlama/işlemsel e-posta sağlayıcısı (Resend/Brevo, SPF/DKIM). Gmail SMTP (~500/gün, spam) pazarlama için kullanılamaz | ⛔ kullanıcı alan adı alıyor | CRM-5/6 e-posta kanalı | E3, #150 | Alan adından giden test e-postası spam'e düşmeden gelir; SPF/DKIM geçer; `send-order-email.ts` yeni sağlayıcıya geçmiş |
| TB-CRM-02 | Netgsm hesabı + belgeler + gönderici başlığı. **Netgsm'e sorulacak:** OTP/bilgi SMS'i ile ticari ileti SMS'i ayrı başlık/onay gerektiriyor mu? Gelen SMS (RET) / webhook desteği var mı? | ⛔ belgeler hazırlanıyor | CRM-6 SMS, ret akışı | #32, #56 | Gerçek numaraya gerçek SMS gider; ret yöntemi (SMS veya link) netleşir; `@netgsm/sms` gerçekten kullanılır |
| TB-CRM-03 | Hukuk/İYS: ticari ileti onay metni, İYS aktarım yöntemi, saklama süreleri, silme talebi ↔ rıza ledger'ı (ispat) çakışması. **Sorumlu: BELİRSİZ** | 🔵 sorumlu atanmadı | CRM-1 canlıya alma (kod yazılabilir), CRM-5/6, CRM-7 | #160, #156, #152, E5, #6 | Yazılı hukuk görüşü; onay metni `policy_version` olarak kodda; İYS süreci yazılı |
| TB-CRM-04 | Test altyapısı (Vitest) | 🟡 **Çalışıyor ama paket YEŞİL DEĞİL** (Codespaces, 2026-10-10 `npx vitest run`: 77 dosyada 24 dosya / 442 testte 42 test kırık, 400 geçti, 1 unhandled error; `tsc --noEmit` temiz). Örnek kırıklar: `components/sandwich/Step*` — bileşen `catalog`'u DB'den okuyor (store), testler eski `sandwich-data.json` ile çalışıyor → seçenekler render olmuyor (kaynak okumasıyla tespit; eski halle `git stash` karşılaştırması YAPILMADI). Branch işi (`lib/branches`, `consent-registration`) 12/12 yeşil | CRM-1 öncesi kırıkların onarımı | #141, #98 | **Not (2026-10-10):** CRM-1 paketi (`npx vitest run lib/crm`) ayrı koşuluyor, 11/11 yeşil; eski kırıklar (örn. `sandwich-catalog`, `profile-validation`) CRM değişikliklerinden ÖNCE de vardı (kullanıcı beyanı, nedeni doğrulanmadı). **Açık iş:** (1) 24 kırık dosyanın dökümü + onarım planı (2) para/hukuk etkili CRM kodundan (`canSendMarketing` vb.) ÖNCE paket yeşil olmalı (3) #141 kapanışı yeşil paketle yazılır |
| TB-CRM-05 | **"Gerçek satış" tanımı** (`v_customer_stats` koşulu). **Onaylı tanım (2026-10-10):** `status IN ('completed','served') AND (payment_method='nakit' OR payment_status='odendi')`. Hariç: `rejected`, `iptal_edildi`, `pending`, `confirmed`, `preparing`, `ready`, `basarisiz`, `iade_edildi`, `tutarsizlik` | ✅ **KARAR + UYGULAMA CANLIDA DOĞRULANDI (2026-10-10):** `v_customer_stats` / `v_customer_branch_stats` Neon'da; `crm2_dogrulama.sql` Bölüm 2 → `TEST_OK` (9 durum kombinasyonu sentetik veriyle, atomik geri alındı: yalnız `completed|served` + nakit/`odendi` sayıldı; iade/iptal/ret/`confirmed`/ödenmemiş online/tutarsızlık HARİÇ). Ek koruma: `payment_status NOT IN ('iade_edildi','tutarsizlik')` (bkz. Kararlar). Kalan: view'ı okuyan rapor/segment kodu CRM-3/4'te | CRM-2, CRM-4 | Plan K1 | Taslak onaylanır; her durum kombinasyonu için test (iade/iptal toplamı bozmaz) |
| TB-CRM-06 | **Şube mimarisi (CRM-0b):** `branches` tablosu (id, slug, name, is_active) + mevcut şube seed; `order_history.branch_id` ve `consent_registrations.branch_id` (nullable FK, backfill = mevcut şube, sonra NOT NULL kararı); `users` ASLA şubeye bağlanmaz; `gel-al/route.ts` branch_id yazar | ✅ **Adım 1 (şema) + Adım 2 (yazım kodu) tamam, kullanıcı canlıda doğruladı (2026-10-10: yeni kayıt ve Gel Al siparişi `branch_id` dolu).** ✅ **Adım 3 KARARI VERİLDİ (2026-10-10, kullanıcı onayı): nullable KALIR** (şube araması hata verirse sipariş düşmesin, `getDefaultBranchId` null döner); "şubesiz kayıt var mı" izleme sorgusu tutulur; NOT NULL ikinci şube + şube seçimi (TB-CRM-07) gerçek akışa girdikten sonra yeniden değerlendirilir. **Kalan küçük iş:** "şubesiz kayıt var mı" izleme sorgusu. Bilinen boşluk: `gel-al` insert'i için route testi yok, canlı SQL ile kapatıldı | TÜM CRM (tabloların şekli) | #92, #93 | Şema notu push'tan önce; Neon'a elle SQL + `schema.ts` senkron; mevcut sipariş akışı canlıda bozulmadan şube alanıyla yazılır; Gel Al siparişi canlıda test edilir |
| TB-CRM-07 | Şube ürün kararları: (a) müşteri sipariş verirken şubeyi nasıl seçer? (b) personel hesabı hangi şubeleri görür (öneri: `staff_branches(user_id, branch_id)`)? (c) şube bazlı menü/fiyat (#93) CRM kapsamında mı? | 🔵 karar bekliyor | TB-06 UI, CRM-3 maskeleme/yetki | #92, #93 | Üç karar yazılı; yetki matrisi şube sütunuyla güncel |
| TB-CRM-08 | Attribution: `acquisition_source`, `utm_*` (ayrı isimler; `channel` yeniden kullanılmaz); metrikler kolon değil VIEW | 🟡 **[2026-10-10] Şema ✅ canlıda** (iki tabloda 4+4 kolon + uzunluk CHECK; doğrulama Bölüm 1 `8`). **C2a (kayıt akışı) kod ✅:** `lib/crm/attribution.ts`, `read-attribution.ts`, `components/layout/AttributionCapture.tsx`, `config.ts` (`CRM_ATTRIBUTION_ENABLED`, KAPALI), `layout.tsx`, `consent/route.ts`, `consent-registration.ts`; `lib/crm` 41/41 PASS, deploy yeşil (kullanıcı beyanı), canlıda davranış değişmedi. **KALAN:** C2b sipariş akışı (`gel-al/route.ts`; karar: ilk temas mı sipariş anı mı), Adım D; hukuk (TB-CRM-03) + çerez bandı (TB-CRM-26) gelmeden bayrak açılmaz | CRM-2 | #94 | Kayıt/sipariş anında kaynak yazılır; view'dan okunur |
| TB-CRM-09 | Migration protokolü: view/trigger/SECURITY DEFINER `schema.ts`'te ifade edilemez → elle SQL + `docs/schema-changes` + `schema.ts` yorumu; Neon ↔ `drizzle push` çakışması ve drift kontrolü | 🟡 | CRM-1 | schema.ts notu, CORE §7.4 | CRM'e özel migration şablonu + "canlı şema = kod şeması" kontrol adımı |
| TB-CRM-10 | Canlı DB güvenliği: Preview yok (`main`'e direkt push), Preview da aynı Neon → her CRM migration'ına geri alma adımı; `CRM_SENDING_ENABLED` varsayılan KAPALI; test verisi/numara izolasyonu | 🟡 | CRM-1…6 | #(CURRENT FOCUS dersleri) | Kill switch kapalıyken hiçbir gönderim yok (testle); her şema notunda GERİ ALMA bölümü dolu |
| TB-CRM-11 | `RISK_DOMAINS.md` §4 (KVKK) → CRM kontrol listesine çevrilir: saklama süresi, silme, minimizasyon, log'a kişisel veri yazmama | 🟡 | CRM-1, CRM-7 | RISK_DOMAINS §4 | Liste CRM aşama DoD'larına işlenmiş |
| TB-CRM-12 | `users.loyaltyPoints` (#30): CRM DIŞI kalır; index'te #30 satırı yok, kodda referans var → kayıt geri açılır veya yorum güncellenir | 🟡 | — | #30 | Tek kayıt: ya index'te açık kayıt ya kod yorumu düzeltilmiş |
| TB-CRM-13 | Cron altyapısı kararı: Vercel Cron (plan limiti doğrulanacak) vs Hetzner n8n | 🔵 | CRM-6 | Plan K6 | Karar + secret'lı endpoint çalışır |
| TB-CRM-14 | Başlangıç eşikleri: haftalık sınır, sessiz saatler, holdout %, atıf penceresi, saklama süresi (config) | 🔵 | CRM-4/5/6/7 | Plan K7 | `lib/crm/config.ts` değerleri onaylı |
| TB-CRM-15 | E-posta doğrulaması (kayıtta ve `/hesap`'ta doğrulanmıyor): yanlış adrese pazarlama gitme riski | 🟡 | CRM-5/6 e-posta | #152 | Doğrulanmamış e-posta pazarlamaya uygun sayılmaz (kapı kuralı) VEYA doğrulama akışı canlıda |
| TB-CRM-16 | OTP/SMS rate-limit (SMS pumping, maliyet): `IP:telefon` anahtarı yetersiz | 🟢 | Netgsm canlıya alınırken | #146 | Telefon bazlı ve global limit; canlıda aşım testi |
| TB-CRM-24 | `order_history`'de teslim/tamamlanma zamanı YOK: "satış tarihi" = `ordered_at`; `order_completed` olayı ve satış zamanına dayalı segment/rapor (CRM-4/7) buna bağlı. Karar: `completed_at` kolonu eklensin mi? | 🔵 karar bekliyor | CRM-4/7 doğruluğu | CRM-2 bulgusu | Karar yazılı; eklenirse personel paneli durum geçişi `completed_at`'i yazar, view buna geçer |
| TB-CRM-26 | Çerez bandı + çerez politikası: `bowlera_attr` pazarlama çerezi (ilk temas kaynağı, 30 gün) şart-olmayan çerezdir; sitede çerez bandı bileşeni YOK (`layout.tsx` ile görüldü, kullanıcıdan açık teyit gelmedi). Bant eklenince `AttributionCapture` yalnız onay verilmişse yazmalı; politikaya çerez adı/amacı/ömrü yazılmalı | 🔵 hukuk/karar bekliyor | `CRM_ATTRIBUTION_ENABLED` açılması | C2a | Bant + politika canlıda; çerez onaysız yazılmaz (testle); bayrak ancak bundan sonra açılır |
| TB-CRM-25 | `CRM_CUSTOMER_EVENTS_ENABLED` KAPALIYKEN oluşan kayıt/siparişler için `customer_events` boşluğu: bayrak açılmadan ÖNCE backfill SQL'i (idempotent) TEKRAR koşulmalı | 🟡 | CRM-2 canlıya alma | CRM-2 C1 | Bayrak açma öncesi sayım eşitliği: `olay_kayit = users(role='customer')`, `olay_siparis = order_history` |

### B. CRM aşamaları (sıra: önce TB-06 ve TB-05 kararları)

| ID | Aşama | Kapsam | Şube etkisi | Session | Kabul kriteri (canlı) |
|---|---|---|---|---|---|
| TB-CRM-17 | CRM-1 🟡 **[2026-10-10] Adım 1 şema ✅ (Neon `TEST_OK`) + Adım 2 kod ✅ (`lib/crm/*`, 11/11 PASS, `tsc` temiz, deploy yeşil, canlı form çalışıyor, bayrak `CRM_CONSENT_COLLECTION_ENABLED` KAPALI). KAPANIŞ: canlıda gerçek kayıtla `granted` satırı — bayrak açılınca; bayrak TB-CRM-03 hukuk onayı + `lib/crm/consent-text.ts` onaylı metin gerektirir (şimdilik TASLAK). Açık: IP saklama süresi, silme↔append-only (CRM-7).** | `marketing_consents` ledger (append-only), `crm_audit_log`, `iys_sync_queue`, kayıt formunda işaretsiz SMS/e-posta kutuları | Rıza MARKA seviyesinde (şubesiz); `branch_id` yalnız kayıt kaynağı olarak | 2–3 | Gerçek kayıtla izin satırı oluşur; UPDATE/DELETE hata verir; kayıt onay metni `policy_version` taşır |
| TB-CRM-18 | CRM-2 🟡 **[2026-10-10] Adım A şema ✅** (`customer_events` + 2 view + attribution; `TEST_OK`) **+ Adım B backfill ✅** (3 `customer_registered` + 28 `order_placed`; ikinci koşuda çoğalmadı, 3/3/28/28) **+ Adım C1 olay yazımı ✅ kod** (`lib/crm/record-customer-event.ts`, `lib/crm` 22/22 PASS, deploy yeşil, bayrak `CRM_CUSTOMER_EVENTS_ENABLED` KAPALI, canlıda davranış değişmedi). **KALAN:** C2 attribution yakalama, D test (uygulama kodu seviyesinde). **KAPANIŞ:** bayrak açılıp canlıda yeni kayıt/siparişle olay satırı oluşunca (TB-03 hukuk + TB-CRM-25 ön adımı) | `customer_events` + backfill, `v_customer_stats` (TB-05 koşuluyla) | `payload.branch_id`; ek view `v_customer_branch_stats` | 2 | İptal/iade toplamı bozmaz; backfill ikinci çalışmada çoğalmaz |
| TB-CRM-19 | CRM-3 | Admin müşteri listesi + 360, not, etiket, maskeleme | Staff şube kapsamı (TB-07) | 3–4 | Staff'ta telefon maskeli/harcama yok (API katmanında); her okuma audit'e düşer |
| TB-CRM-20 | CRM-4 | Segment config + filtreler | Şube bazlı segment filtresi | 2 | Segment sayıları SQL ile elle doğrulanır |
| TB-CRM-21 | CRM-5 | Şablonlar, kampanya taslağı, `canSendMarketing` kapısı, önizleme | `campaigns.branch_id` nullable (null = tüm şubeler); şablon değişkenleri şube adresi | 3 | Kapı 5 durumda reddeder (testle); önizleme dry-run |
| TB-CRM-22 | CRM-6 | Dispatch cron, ret akışı, holdout, kill switch | Şubeye göre hedefleme | 3–4 | **Gerçek SMS ile** ret ve cron çift tetikleme testi (kapanış için şart) |
| TB-CRM-23 | CRM-7 | Raporlar, erase, export | Şube kırılımlı rapor | 2–3 | Erase sonrası sipariş toplamları tutarlı; export loglanır |

**Tahmini toplam:** CRM-0b (şube) 1–2 + CRM-1…7 17–22 = **18–24 session**. Pazarlamaya başlamadan önce en az CRM-0b → CRM-1 → CRM-3 bitmeli.

## 4. Bağımlılık özeti

```
TB-06 (şube) ──┬─> TB-17 CRM-1 ──> TB-18 CRM-2 ──> TB-19 CRM-3 ──> TB-20 CRM-4 ──> TB-21 CRM-5 ──> TB-22 CRM-6 ──> TB-23 CRM-7
TB-05 (satış) ─┘            (TB-05 → CRM-2)        (TB-07 → CRM-3)                  (TB-14 eşikler)  (TB-01/02/03/13 şart)
TB-03 hukuk → CRM-1 CANLIYA ALMA, CRM-5/6      TB-09/10/11 → her aşamanın DoD'u
```

## 5. Açık sorular (kullanıcıya)

1. 2. şubenin tahmini açılış tarihi (TB-07 önceliği için).
2. TB-05 taslak "gerçek satış" tanımı onaylı mı? (özellikle `confirmed` = teslim edilmedi sayılır mı?) → **YANITLANDI 2026-10-10: onaylı; `confirmed` sayılmaz.**
3. Hukuk/İYS sorumlusu kim? (TB-03)
4. `npm test` tarihi ve test sayısı (TB-04 → #141 kapanışı).
5. **UTM/attribution saklama biçimi:** → **YANITLANDI 2026-10-10: ÇEREZ.** Çerez bandı/politikası var mı? → AÇIK YANIT YOK, "yok" varsayıldı (TB-CRM-26). Yeni açık soru: sipariş (`order_history`) kaynağı ilk temas mı, sipariş anındaki temas mı? (C2b'yi bloklar)
6. `Bowlera_CRM_Teknik_Uygulama_Plani.md` oturumda yüklenmedi (iki kez istendi) — CRM-2 olay tipleri/payload asistan önerisi; plana aykırılık varsa düzeltilecek.
7. TB-05 ek koruma (`payment_status NOT IN ('iade_edildi','tutarsizlik')`) AYRICA onaylanıyor mu?
