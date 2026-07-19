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
| `TWILIO_ACCOUNT_SID` | ✅ (auth için öne çekildi) | Server-only | Twilio hesap kimliği — OTP (§5) + gelecekte SMS bildirimi (§4) ortak kullanır | INTEGRATIONS.md §4, §5 |
| `TWILIO_AUTH_TOKEN` | ✅ (auth için öne çekildi) | Server-only | Twilio hesap secret'ı — OTP (§5) + gelecekte SMS bildirimi (§4) ortak kullanır | INTEGRATIONS.md §4, §5 |
| `TWILIO_VERIFY_SERVICE_SID` | ✅ | Server-only | Twilio Verify servis kimliği — telefon+OTP kullanıcı girişi | INTEGRATIONS.md §5 |
| `AUTH_SECRET` | ✅ | Server-only | Auth.js (NextAuth) JWT imzalama secret'ı — oturum bütünlüğü | INTEGRATIONS.md §5 |
| `CMS_API_TOKEN` | ⬜ (büyüme fazı) | Server-only | Sanity/Contentful erişim anahtarı | ARCHITECTURE.md §2.2 |
| `CMS_PROJECT_ID` | ⬜ (büyüme fazı) | Server-only | Sanity/Contentful proje kimliği | ARCHITECTURE.md §2.2 |

> `NEXT_PUBLIC_` prefix'i **yalnızca** client'a güvenle açılabilecek değerler için kullanılır —
> hiçbir API key bu prefix'i almaz (BSC-2).

---

## 3. ORTAM BAZLI KAPSAM

| Ortam | Kullanım |
|---|---|
| Development (`.env.local`) | Lokal test, gerçek anahtarlar yerine test/sandbox anahtarları önerilir |
| Preview (PR deploy) | Sadece `NEXT_PUBLIC_SITE_URL` ve sandbox anahtarları — üretim anahtarı asla |
| Production | Tüm zorunlu değişkenler platform dashboard'unda, gerçek anahtarlarla |

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

# Telefon + OTP Kullanıcı Girişi (INTEGRATIONS.md §5)
# NOT: TWILIO_ACCOUNT_SID/TWILIO_AUTH_TOKEN artık burada da zorunlu —
# aşağıdaki §4 bildirim kullanımıyla AYNI Twilio hesabı paylaşılır, mükerrer değil.
TWILIO_ACCOUNT_SID=
TWILIO_AUTH_TOKEN=
TWILIO_VERIFY_SERVICE_SID=
AUTH_SECRET=

# Bildirim (lansman sonrası — INTEGRATIONS.md §4)
# TWILIO_ACCOUNT_SID / TWILIO_AUTH_TOKEN yukarıda tanımlı, tekrar eklenmez

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

*BOWLERA CONFIG_SCHEMA.md — v1.1 — Session 4 — 2026-07-19*
*Kaynak: INTEGRATIONS.md · ARCHITECTURE.md §4.1 · AGENT.md BSC-2*
*v1.1: §2 — Telefon+OTP auth (Karar #17) için `TWILIO_VERIFY_SERVICE_SID` ve `AUTH_SECRET` eklendi.
`TWILIO_ACCOUNT_SID`/`TWILIO_AUTH_TOKEN` zorunlu statüsüne öne çekildi (auth + gelecekteki SMS
bildirimi aynı hesabı paylaşıyor, mükerrer değil). §4 şablonu güncellendi. Kaynak: INTEGRATIONS.md §5.*
