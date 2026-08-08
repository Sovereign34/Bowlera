# BOWLERA — CONFIG_SCHEMA.md
> Bu belge `.env.local` şemasının tam kontratıdır.
> Env değişkeni/API key ile ilgili her görev önce bu dosyayı okumak zorundadır.
> Kaynak: INTEGRATIONS.md + ARCHITECTURE.md §4.1 (Deploy) + AGENT.md BSC-2

---

## 1. TEMEL KURAL

```
Hiçbir API key/secret client bundle'a veya repo'ya commit edilmez (BSC-2).
Tüm değerler platform dashboard'undan (Vercel vb.) environment variable olarak girilir.
`.env.local` yalnızca lokal geliştirme için kullanılır ve `.gitignore`'dadır.
```

---

## 2. ENV DEĞİŞKENLERİ ŞEMASI

| Değişken | Zorunlu | Scope | Açıklama | Kaynak |
|---|---|---|---|---|
| `NEXT_PUBLIC_SITE_URL` | ✅ | Client + Server | Canonical site URL — SEO/JSON-LD için | CONTENT_GUIDE.md §5 |
| `ADISYO_API_KEY` | ⬜ (sonraki faz) | Server-only | Adisyo pazaryeri entegrasyon anahtarı | INTEGRATIONS.md §1 |
| `SEPETTAKIP_API_KEY` | ⬜ (sonraki faz) | Server-only | SepetTakip pazaryeri entegrasyon anahtarı | INTEGRATIONS.md §1 |
| `MARKETPLACE_WEBHOOK_SECRET` | ⬜ (sonraki faz) | Server-only | Webhook imza doğrulama secret'ı (BSC-3) | INTEGRATIONS.md §1 |
| `WHATSAPP_BRANCH_PHONE_[ŞUBE_KODU]` | ⬜ (Oturum 5) | Server-only | Şube başına WhatsApp numarası | INTEGRATIONS.md §2 |
| `TWILIO_ACCOUNT_SID` | ⬜ **PARKLI (#32/#56)** | Server-only | Twilio hesap kimliği — eski OTP girişi (`/giris`, Session 8'de arayüzden kaldırıldı) + gelecekte SMS bildirimi (§4) ortak kullanır | INTEGRATIONS.md §4, §5 |
| `TWILIO_AUTH_TOKEN` | ⬜ **PARKLI (#32/#56)** | Server-only | Twilio hesap secret'ı — yukarıdaki ile aynı durum | INTEGRATIONS.md §4, §5 |
| `TWILIO_VERIFY_SERVICE_SID` | ⬜ **PARKLI (#32/#56)** | Server-only | Twilio Verify servis kimliği — eski telefon+OTP girişi, artık birincil akış değil | INTEGRATIONS.md §5 |
| `AUTH_SECRET` | ✅ | Server-only | Auth.js (NextAuth) JWT imzalama secret'ı — oturum bütünlüğü. **Artık `/kayit-ol` (rıza esaslı kayıt) tarafından da kullanılıyor**, Twilio'dan bağımsız zorunlu kalır | INTEGRATIONS.md §5, ARCHITECTURE.md §2.7 |
| `DATABASE_URL` | ✅ | Server-only | Neon Postgres bağlantı string'i — `users`, `consentRegistrations` (Session 8), `order_history` (Session 10) tabloları | ARCHITECTURE.md §3 (AuthenticatedUser), Karar #20 |
| `CMS_API_TOKEN` | ⬜ (büyüme fazı) | Server-only | Sanity/Contentful erişim anahtarı | ARCHITECTURE.md §2.2 |
| `CMS_PROJECT_ID` | ⬜ (büyüme fazı) | Server-only | Sanity/Contentful proje kimliği | ARCHITECTURE.md §2.2 |

> ⚠️ **[Bu güncelleme]** `TWILIO_*` üç değişken de Session 8'de **⬜ PARKLI** durumuna
> düşürüldü. Sebep: `app/giris/page.tsx` (Twilio OTP) arayüzden kaldırıldı, birincil
> giriş/kayıt akışı `/kayit-ol`'a taşındı (ARCHITECTURE.md §2.7). Twilio/Netgsm nihai kararı
> hâlâ AÇIK (#32/#56) — bu satırlar SİLİNMEDİ çünkü karar geri dönüşlü olabilir, sadece
> "şu an zorunlu değil" durumuna güncellendi. Production'da bu değişkenler halihazırda
> girilmiş olabilir (geçmiş kurulum) — bu tabloya göre artık "zorunlu" sayılmamaları,
> platformdan silinmeleri gerektiği anlamına GELMEZ, sadece yeni deploy/kurulumlarda
> zorunlu ön koşul olmadıkları anlamına gelir.

> `NEXT_PUBLIC_` prefix'i **yalnızca** client'a güvenle açılabilecek değerler için kullanılır —
> hiçbir API key bu prefix'i almaz (BSC-2).

> `DATABASE_URL`, Vercel Marketplace Neon entegrasyonu tarafından Production ve Preview
> environment'larına **otomatik enjekte edilir** (Custom Prefix: `DATABASE` → `DATABASE_URL`).
> Lokal geliştirmede `vercel env pull` ile `.env.local`'e çekilir, elle girilmez.

---

## 3. ORTAM BAZLI KAPSAM

| Ortam | Kullanım |
|---|---|
| Development (`.env.local`) | Lokal test, gerçek anahtarlar yerine test/sandbox anahtarları önerilir |
| Preview (PR deploy) | Sadece `NEXT_PUBLIC_SITE_URL` ve sandbox anahtarları — üretim anahtarı asla |
| Production | Tüm zorunlu değişkenler platform dashboard'unda, gerçek anahtarlarla |

> `DATABASE_URL` istisnadır: Neon entegrasyonu Development environment'ına dahil edilmedi
> (bilinçli seçim, bkz. kurulum kaydı) — lokal geliştirme `vercel env pull` ile Preview/Production
> bağlantısını kullanır. İleride ayrı bir dev branch gerekirse bu satır güncellenir.

---

## 4. `.env.local.example` ŞABLONU

```bash
# Site
NEXT_PUBLIC_SITE_URL=http://localhost:3000

# Pazaryeri Entegrasyonu (sonraki faz — INTEGRATIONS.md §1)
ADISYO_API_KEY=
SEPETTAKIP_API_KEY=
MARKETPLACE_WEBHOOK_SECRET=

# WhatsApp Köprüsü (Oturum 5 — INTEGRATIONS.md §2)
WHATSAPP_BRANCH_PHONE_KADIKOY=

# Telefon + OTP Girişi — PARKLI (#32/#56, Session 8'de arayüzden kaldırıldı)
# NOT: Bu üçü artık zorunlu DEĞİL — sadece Twilio/Netgsm kararı netleşirse tekrar
# devreye girer. AUTH_SECRET aşağıda AYRI ve HÂLÂ ZORUNLU (kayıt akışı için de kullanılıyor).
TWILIO_ACCOUNT_SID=
TWILIO_AUTH_TOKEN=
TWILIO_VERIFY_SERVICE_SID=

# Auth.js JWT İmzalama — ZORUNLU (Twilio'dan bağımsız; /kayit-ol rıza esaslı kayıt akışı da kullanır)
AUTH_SECRET=

# Veritabanı (Neon Postgres — Vercel Marketplace entegrasyonu, Karar #20)
# users + consentRegistrations (Session 8) + order_history (Session 10) tabloları
# Elle doldurulmaz — `vercel env pull` ile çekilir.
DATABASE_URL=

# Bildirim (lansman sonrası — INTEGRATIONS.md §4)
# TWILIO_ACCOUNT_SID / TWILIO_AUTH_TOKEN yukarıda tanımlı (şu an parklı), tekrar eklenmez

# CMS (büyüme fazı — ARCHITECTURE.md §2.2)
CMS_API_TOKEN=
CMS_PROJECT_ID=
```

> Bu dosya repo köküne `.env.local.example` olarak eklenir — gerçek değerler asla commit
> edilmez, sadece anahtar isimleri.

---

## 5. YENİ DEĞİŞKEN EKLEME PROTOKOLÜ

```
1. Değişken bu dosyaya (Bölüm 2 tablosu) eklenir — zorunlu/opsiyonel, scope, kaynak belirtilir
2. .env.local.example güncellenir (Bölüm 4)
3. Kullanıcıya platform dashboard'una eklemesi için bildirilir
4. DEPENDENCIES.md'de ilgili dosya bağımlılığı güncellenir (hangi route/lib bu değişkeni kullanıyor)
```

---

## 6. KALİTE KONTROL — CONFIG SELF-CHECK

```
[ ] Yeni env değişkeni mi ekleniyor?      → Bölüm 2 tablosuna eklendi mi?
[ ] Client tarafında mı kullanılacak?      → NEXT_PUBLIC_ prefix gerçekten güvenli mi? (BSC-2)
[ ] Secret/API key mi?                     → Server-only işaretlendi mi, .example'da boş mu?
[ ] .env.local .gitignore'da mı?           → Repo'ya yanlışlıkla commit riski var mı?
```

---

*BOWLERA CONFIG_SCHEMA.md — v1.3 — Session 11 — 2026-08-07*
*Kaynak: INTEGRATIONS.md · ARCHITECTURE.md §4.1, §3, §2.7 · AGENT.md BSC-2 · SESSION_INDEX.md (Session 8-11 senkronu)*
*v1.3 (bu güncelleme): `TWILIO_ACCOUNT_SID`/`TWILIO_AUTH_TOKEN`/`TWILIO_VERIFY_SERVICE_SID`
zorunluluk durumu ✅ → ⬜ PARKLI (#32/#56) olarak düzeltildi — Session 8'de `/giris` (Twilio OTP)
arayüzden kaldırıldı, birincil akış `/kayit-ol`'a taşındı, bu dosya o değişikliği hiç
yansıtmamıştı (ARCHITECTURE.md v1.6 ile aynı senkron turunun 2. adımı). `AUTH_SECRET`
zorunluluk durumu KORUNDU ve gerekçesi netleştirildi — artık Twilio'ya değil `/kayit-ol`
akışına bağlı. §4 şablonu ve yorum satırları güncellendi. Yeni env değişkeni EKLENMEDİ —
`/kayit-ol` backend'inin ek bir secret gerektirip gerektirmediği doğrudan koddan
doğrulanmadı (confidence: MEDIUM, bkz. KARAR BİLDİRİMİ). Kod paylaşılırsa bu satır
tekrar gözden geçirilmeli.*
*v1.2: §2'ye `DATABASE_URL` eklendi (Neon Postgres, Vercel Marketplace entegrasyonu, Karar #20 —
DB kararının kısmi revizyonu: kullanıcı adresi/sadakat puanı artık kalıcı saklanıyor). §3'e Development
environment istisnası notu eklendi. §4 şablonuna `DATABASE_URL` eklendi.*
*v1.1: §2 — Telefon+OTP auth (Karar #17) için `TWILIO_VERIFY_SERVICE_SID` ve `AUTH_SECRET` eklendi.
`TWILIO_ACCOUNT_SID`/`TWILIO_AUTH_TOKEN` zorunlu statüsüne öne çekildi (auth + gelecekteki SMS
bildirimi aynı hesabı paylaşıyor, mükerrer değil). §4 şablonu güncellendi. Kaynak: INTEGRATIONS.md §5.*
