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
| `TWILIO_ACCOUNT_SID` | ⬜ (lansman sonrası) | Server-only | SMS bildirim servisi | INTEGRATIONS.md §4 |
| `TWILIO_AUTH_TOKEN` | ⬜ (lansman sonrası) | Server-only | SMS bildirim servisi | INTEGRATIONS.md §4 |
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

# Bildirim (lansman sonrası — INTEGRATIONS.md §4)
TWILIO_ACCOUNT_SID=
TWILIO_AUTH_TOKEN=

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

*BOWLERA CONFIG_SCHEMA.md — v1.0 — Session 1 — 2026-07-17*
*Kaynak: INTEGRATIONS.md · ARCHITECTURE.md §4.1 · AGENT.md BSC-2*
