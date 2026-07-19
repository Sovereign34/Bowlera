# BOWLERA — INTEGRATIONS.md
> Bu belge Türkiye pazarına özgü üçüncü parti entegrasyonların kontratıdır.
> Bu entegrasyonlara dokunan her görev önce bu dosyayı okumak zorundadır.
> Kaynak: MASTER_PLAN.md §5.6 (Üçüncü Parti Entegrasyonlar) + AGENT.md BSC-7, BSC-8

---

## 0. FAZ DURUMU

> ⚠️ Bu dosya kontratı tanımlar ama entegrasyonların canlıya alınması **ayrı bir fazdır**
> (SESSION_INDEX.md → Açık Sorunlar #3). Gerçek API anahtarı ve iş ortaklığı olmadan hiçbir
> entegrasyon "tamamlandı" sayılmaz (CORE.md §9 Mutlak Yasaklar).

| Entegrasyon | Durum |
|---|---|
| Adisyo/SepetTakip (pazaryeri toplama) | ⬜ API anahtarı bekleniyor |
| WhatsApp sipariş köprüsü | ⬜ Şube telefon numaraları bekleniyor |
| Masaya QR menü | ⬜ Kod üretimi Oturum 5 sonrası |
| SMS/e-posta bildirimi (Twilio) | ⬜ Lansmandan sonraki faz, POS ile birlikte |
| Telefon + OTP kullanıcı girişi (Twilio Verify + Auth.js) | ⬜ Mimari onaylandı (Karar #17/#19), kod yazılmadı — Twilio Verify Service SID bekleniyor |

---

## 1. ADİSYO / SEPETTAKIP — PAZARYERİ TOPLAMA

**Amaç:** Yemeksepeti/Getir Yemek/Trendyol Yemek siparişlerini tek ekranda toplayıp
POS/adisyo yazıcısına aktarmak.

```ts
// app/api/orders/marketplace/route.ts
// Amaç:    Adisyo/SepetTakip webhook'unu karşılar, siparişi normalize eder
// Bağlı:   lib/integrations/marketplace.ts, risk: sipariş kaybı/gecikmesi
// Dokunma: CONFIG_SCHEMA.md → ADISYO_API_KEY / SEPETTAKIP_API_KEY

export async function POST(req: Request) {
  const signature = req.headers.get('x-webhook-signature')
  if (!isValidSignature(signature, await req.text())) {
    return new Response('Unauthorized', { status: 401 })   // BSC-3
  }
  // ... normalize + POS'a ilet
}
```

**Kural:** Bu çağrı **yalnızca `app/api/` Route Handler'ından** yapılır — client component'ten
asla (ARCHITECTURE.md §1 Kural 4).

### 1.1 Rate Limit (BSC-7)
```
Adisyo/SepetTakip API'sine giden istekler token-bucket rate limiter'dan geçer —
üçüncü parti sağlayıcının kotasını aşıp hesabın askıya alınmasını önlemek için.
```

### 1.2 Kopma Senaryosu (BSC-8)
```ts
try {
  await sendToMarketplace(order)
} catch (err) {
  logger.error({ event: 'MARKETPLACE_SYNC_FAILED', orderId: order.id })
  await queueForRetry(order)
  return { status: 'QUEUED', message: 'Siparişiniz alındı, onay birazdan gelecek' }
}
```
> FAILURE_PATTERNS.md'de "pazaryeri API kopması" senaryosuna referans verir.

---

## 2. WHATSAPP SİPARİŞ KÖPRÜSÜ

**Amaç:** Özelleştirilen kaseyi şablon mesaj olarak şubenin WhatsApp hattına yönlendirmek.

```ts
// lib/integrations/whatsapp.ts
// Amaç:    Sepeti wa.me linkine dönüştürür
// Bağlı:   CartDrawer "WhatsApp ile Sipariş Ver" butonu (ARCHITECTURE.md §2.6)
// Risk:    Encode hatası → şubeye eksik/bozuk sipariş mesajı gider

export function buildWhatsAppOrderLink(branchPhone: string, cart: CartItem[]): string {
  if (!branchPhone) throw new Error('Şube telefon numarası eksik')   // BSC-3
  const message = formatOrderMessage(cart)
  return `https://wa.me/${branchPhone}?text=${encodeURIComponent(message)}`
}
```

### 2.1 Mesaj Şablonu

```
Merhaba, Bowlera'dan sipariş vermek istiyorum 🥗

[Ürün adı] x[adet] — [özelleştirme varsa: taban, protein, toppings, sos]
Toplam: [fiyat] TL

Şube: [şube adı]
```

> Şablon değişirse CONTENT_GUIDE.md §1 marka sesine uygunluk kontrol edilir.

### 2.2 Edge Case'ler (AGENT.md §3)
```
1. wa.me linki oluşturulamaması        → hata mesajı + "Bizi arayın" fallback
2. Özel karakter encode hatası (emoji, Türkçe karakter) → encodeURIComponent testi zorunlu
3. Şube numarası eksim/hatalı format   → build zamanında değil, runtime'da doğrulanır (BSC-3)
```

---

## 3. MASAYA QR MENÜ

**Amaç:** QR kod → `/menu?table=14` parametresiyle sipariş doğrudan ilgili masaya düşer.

```ts
// app/menu/page.tsx — searchParams.table okunur
// Amaç:    Masa numarasını sipariş akışına taşır
// Risk:    table param kaybolursa sipariş hangi masaya ait belirsizleşir

const tableId = searchParams.table   // örn. "14"
// tableId, useCartStore'a sipariş meta verisi olarak eklenir (BSC-3: sayısal formata doğrulanır)
```

> QR kod üretimi/basımı kapsam dışıdır — yalnızca URL şeması ve state taşıma bu dosyanın
> sorumluluğu.

---

## 4. SİPARİŞ SONRASI BİLDİRİM (SMS / E-POSTA)

**Amaç:** Hazırlık süresi ve durum takibi için bildirim (ör. Twilio veya yerel SMS API).

> ⚠️ Lansmandan sonraki faz — POS entegrasyonuyla birlikte devreye alınmalı (MASTER_PLAN §5.6).
> Kontrat burada tanımlanır ama uygulama Oturum planına dahil değil (ROADMAP.md §2).

```ts
// lib/integrations/notify.ts (gelecek faz — iskelet)
// Amaç:    Sipariş durum değişikliğinde SMS/e-posta gönderir
// Risk:    Sağlayıcı kotası aşılırsa bildirim gitmez → BSC-7 rate limit zorunlu
```

---

## 5. TELEFON + OTP KULLANICI GİRİŞİ (AUTH)

**Amaç:** Şifresiz, telefon numarası + SMS OTP ile kullanıcı girişi. Guest checkout
korunur — bu akış zorunlu değil, kullanıcı isterse hesapsız sipariş vermeye devam eder.
Sadakat programı ileride bu kimliğe (telefon numarası) bağlanacak (Karar #17).

> ⚠️ Veritabanı kararı bilinçli olarak ERTELENDİ. Bu bölümdeki tasarım DB-agnostic'tir:
> Auth.js JWT stratejisiyle oturumun kendisi DB gerektirmez, ama kullanıcı profili/sadakat
> puanı DB seçilene kadar KALICI SAKLANAMAZ. Bu bilinçli bir MVP sınırıdır, hata değildir.

**Sağlayıcı seçimi:** Twilio Verify — CONFIG_SCHEMA.md'de zaten planlı olan
`TWILIO_ACCOUNT_SID`/`TWILIO_AUTH_TOKEN` bildirim (§4) ile paylaşılır, mükerrer
üçüncü parti eklenmez. Session yönetimi: Auth.js (NextAuth) Credentials provider + JWT.

### 5.1 OTP Gönderme

```ts
// app/api/auth/otp/send/route.ts
// Amaç:    Girilen telefon numarasına Twilio Verify ile OTP kodu gönderir
// Bağlı:   /giris sayfası telefon formu
// Risk:    Rate limit yoksa SMS bombalama / kota tükenmesi (BSC-7)
// Dokunma: CONFIG_SCHEMA.md → TWILIO_ACCOUNT_SID / TWILIO_AUTH_TOKEN / TWILIO_VERIFY_SERVICE_SID

export async function POST(req: Request) {
  const { phone } = await req.json()
  if (!isValidTurkishPhone(phone)) {
    return new Response('Geçersiz telefon numarası', { status: 400 })   // BSC-3
  }
  await verifyClient.verifications.create({ to: phone, channel: 'sms' })
  return Response.json({ status: 'SENT' })
}
```

### 5.2 OTP Doğrulama + Oturum Açma

```ts
// app/api/auth/otp/verify/route.ts
// Amaç:    Girilen kodu Twilio Verify'a doğrular, başarılıysa Auth.js session'ı tetikler
// Bağlı:   /giris sayfası kod formu → Auth.js Credentials provider
// Risk:    Doğrulama idempotent olmalı — aynı kod çift gönderimde çift oturum açmamalı

export async function POST(req: Request) {
  const { phone, code } = await req.json()
  const check = await verifyClient.verificationChecks.create({ to: phone, code })
  if (check.status !== 'approved') {
    return new Response('Kod hatalı veya süresi dolmuş', { status: 401 })
  }
  // Auth.js signIn('credentials', { phone }) → httpOnly JWT session cookie set edilir
}
```

### 5.3 Rate Limit (BSC-7)
```
/api/auth/otp/send çağrıları IP + telefon numarası bazlı token-bucket rate limiter'dan
geçer — SMS bombalama ve Twilio kotasının aşılmasını önlemek için (Adisyo/SepetTakip §1.1
ile aynı desen).
```

### 5.4 Edge Case'ler (AGENT.md §3)
```
1. Kod süresi doldu (Twilio varsayılan 10dk)     → "Yeni kod iste" akışı, eski kod geçersiz
2. Yanlış kod 3+ deneme                          → geçici kilitleme, Twilio Verify kendi
                                                    max-attempt kontrolünü de uygular
3. Aynı telefon numarasıyla ikinci kayıt denemesi → mevcut hesaba giriş yönlendirilir
                                                    ("1 numara = 1 hesap" — bilinen risk,
                                                    hesap kurtarma akışı Açık Sorun #30'da
                                                    ayrıca netleşecek)
4. DB yokken profil/sadakat verisi                → yalnızca oturum (JWT) kalıcı, profil
                                                    verisi bu fazda saklanmıyor — kullanıcıya
                                                    UI'da netleştirilmeli (yanıltıcı olmasın)
```

---

## 6. KALİTE KONTROL — INTEGRATIONS SELF-CHECK

```
[ ] Üçüncü parti çağrısı server-side mi?     → Route Handler içinde mi? (ARCHITECTURE §1 Kural 4)
[ ] Rate limit var mı?                        → BSC-7 uygulandı mı?
[ ] Kopma senaryosu ele alındı mı?            → BSC-8 fallback var mı?
[ ] API key client kodda mı?                  → CONFIG_SCHEMA.md env'den mi okunuyor? (BSC-2)
[ ] Gerçek anahtar/test olmadan "tamamlandı" mı deniyor? → CORE.md §9 ihlali mi?
[ ] Auth akışına dokunuluyor mu?              → DB henüz yok, profil/sadakat verisi kalıcı
                                                 saklanamıyor uyarısı UI'da netleştirildi mi? (§5.4)
```

---

*BOWLERA INTEGRATIONS.md — v1.1 — Session 4 — 2026-07-19*
*Kaynak: MASTER_PLAN.md §5.6 · AGENT.md BSC-7, BSC-8 · ARCHITECTURE.md §1, §2.6*
*v1.1: §0 faz tablosuna auth satırı eklendi. Yeni §5 — Telefon+OTP kullanıcı girişi
(Twilio Verify + Auth.js JWT, DB-agnostic tasarım, Karar #17 uyarınca) eklendi. Eski §5
(Kalite Kontrol) §6'ya kaydı, DB kısıtı self-check maddesi eklendi.*
