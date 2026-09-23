# BOWLERA — BSC_EXAMPLES.md
> AGENT.md'deki BSC (Bowlera Secure Code) tablosunun detaylı kod örnekleri.
> AGENT.md'de her BSC kuralı artık tek satır — buraya SADECE ihlal gerçekten
> tespit edildiğinde veya örneğe ihtiyaç duyulduğunda bakılır (CORE.md §3
> Tetikleyici Tablosu bu dosyayı "BSC ihlali düzeltme" görevine bağlar).
> Kural metninin kendisi (ne yapılır/yapılmaz) her zaman AGENT.md'de kalır —
> bu dosya SADECE kod örneklerini taşır, kuralın kendisini değil.

---

## BSC-1. XSS / GİRDİ SANİTİZASYONU

```tsx
// ❌
<div dangerouslySetInnerHTML={{ __html: userInput }} />

// ✅
<div>{userInput}</div>  // React otomatik escape eder
// Zorunlu HTML render gerekiyorsa:
import DOMPurify from 'isomorphic-dompurify'
<div dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(userInput) }} />
```

---

## BSC-2. GİZLİ VERİ YASAĞI

```ts
// ❌ — client component içinde
const res = await fetch(`https://api.adisyo.com/orders?key=abc123`)

// ✅ — server-side API Route
// app/api/orders/route.ts
const res = await fetch(`https://api.adisyo.com/orders`, {
  headers: { Authorization: `Bearer ${process.env.ADISYO_API_KEY}` }
})
```
**Ek:** `.env.local` önerilirse `.gitignore`'da olduğu doğrulanır.

---

## BSC-3. GİRDİ DOĞRULAMA ZORUNLULUĞU

```ts
// ❌
const { productId, quantity } = req.body
addToCart(productId, quantity)

// ✅
const { productId, quantity } = req.body
if (!productId || !menuData.find(i => i.id === productId)) {
  return res.status(400).json({ error: 'Geçersiz ürün' })
}
if (!Number.isInteger(quantity) || quantity <= 0 || quantity > MAX_ITEM_QTY) {
  return res.status(400).json({ error: 'Geçersiz miktar' })
}
addToCart(productId, quantity)
```

---

## BSC-4. HATA YÖNETİMİ STANDARDI

```ts
// ❌
} catch (e) {}
} catch (err) { return res.status(500).json({ error: err.message }) }

// ✅
} catch (err) {
  const message = err instanceof Error ? err.message : 'Bilinmeyen hata'
  logger.error({
    trace_id: req.headers.get('x-trace-id') ?? generateTraceId(),
    module: 'cart-api',
    action: 'addToCart',
    error: message,
    timestamp: new Date().toISOString()
  })
  return res.status(500).json({ error: 'Sepete eklenemedi, tekrar deneyin' })
}
```

---

## BSC-5. SAHTE VERİ YASAĞI (PRODUCTION)

```ts
// ❌
const calories = 450  // hardcode

// ✅
const calories = bowlItem.calories  // menu-data.json / CMS'den

// Test modunda:
// TEST_ONLY: const calories = 450
```

---

## BSC-6. RACE CONDITION KORUMASI (SEPET/CUSTOMIZER)

```ts
// ❌
addToCart(item)  // hızlı çift tıklamada iki kez eklenebilir

// ✅
const isAdding = useRef(false)
const handleAddToCart = () => {
  if (isAdding.current) return
  isAdding.current = true
  addToCart(item)
  setTimeout(() => { isAdding.current = false }, 500)
}
```

---

## BSC-7. ÜÇÜNCÜ PARTİ İSTEK KORUMASI

```ts
// ✅
const rateLimiter = new RateLimiter({ maxRequests: 60, windowMs: 60000 })
router.post('/api/orders/sync', rateLimitMiddleware, syncOrderHandler)
```

---

## BSC-8. ÜÇÜNCÜ PARTİ KOPMA — GRACEFUL DEGRADATION

```ts
// ✅
try {
  await sendToMarketplace(order)
} catch (err) {
  logger.error({ event: 'MARKETPLACE_SYNC_FAILED', orderId: order.id })
  await queueForRetry(order)  // sipariş kaybolmaz, kuyruğa alınır
  return { status: 'QUEUED', message: 'Siparişiniz alındı, onay birazdan gelecek' }
}
```

---

## BSC-9. SECRET DOSYASI COMMIT YASAĞI

```
// ❌ — repo kökünde bırakılıp `git add .` ile commit edilen dosya
service-account.json
.env.production
signing.key

// ✅ — .gitignore'da açıkça listelenir + commit öncesi otomatik tarama
*.env*
*.key
*.pem
service-account*.json
```
**Ek:** Böyle bir dosya yanlışlıkla commit edilirse, silmek yetmez — o secret
**iptal edilip yeniden üretilmelidir** (git geçmişinde kalır).

---

*BOWLERA BSC_EXAMPLES.md — v1.0 — 2026-09-22*
*Kaynak: AGENT.md BSC tablosundan ayrıştırıldı (token/context optimizasyonu,
kural metninin kendisi taşınmadı, sadece kod örnekleri).*
