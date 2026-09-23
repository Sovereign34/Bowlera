# KOD_KALİTESİ_EXAMPLES.md
> AGENT.md'deki KOD KALİTESİ KURALLARI (1-7) tablosunun tam örnek/senaryo detayı.
> Kuralın kendisi (ne yapılır/yapılmaz + tespit mesajı) AGENT.md'de her session yüklü;
> buraya SADECE ihlal tespit edildiğinde veya somut örneğe ihtiyaç duyulduğunda bakılır.
> Token/context optimizasyonu amaçlı ayrıldı (2026-09-23) — bilgi kaybı yok.

---

## Kural 1 — Bileşen/Fonksiyon Boyutu Disiplini

**Örnek ihlal:** `CustomizerStep.tsx` 90 satır — state yönetimi, validasyon, animasyon,
render tek bileşende toplanmış.

**Örnek doğru bölünme:**
`useCustomizerStep()` hook + `StepValidation.ts` + `StepAnimation.tsx` + `StepRender.tsx`
— dört ayrı dosya, her biri tek iş yapıyor.

---

## Kural 2 — Niyet Yorumu Zorunluluğu

Her dosyanın en üstüne yazılan blok, tam format:

```ts
// [DOSYA ADI]
// Amaç:    [bu dosya ne iş yapar — tek cümle]
// Bağlı:   [hangi sayfaya / store'a / API route'a bağlı]
// Risk:    [bu dosya hatalı çalışırsa ne olur — örn: "sepet fiyatı yanlış hesaplanır" / "sipariş WhatsApp'a gitmez"]
// Dokunma: [bu dosya değiştirilmeden önce ne kontrol edilmeli]
```

`Risk:` alanı Bowlera'ya özgüdür — kullanıcı/sipariş deneyimine etkisi her zaman belirtilir.

---

## Kural 3 — Edge Case Önce, Kod Sonra

**Süreç:**
1. "Bu özellik nasıl kırılır?" → 3-5 senaryo listele
2. "Hangi edge case'ler var?" → sınır değerleri belirle
3. Kod yaz
4. Yazılan kodun edge case'leri kapattığını doğrula

Edge case sayısı 3-5 ile sınırlıdır — 2 yetersiz, 6+ analiz felcine yol açar.

**Bowlera kritik örnekler:**
- `useCartStore.ts` → edge case: aynı ürün iki kez eklenmesi, tarayıcı kapanıp açılması,
  stok/şube değişikliği
- `CustomizerStep.tsx` → edge case: adım atlanarak URL'den erişim, çift tıklama,
  malzeme tükenmesi
- `whatsapp.ts` → edge case: `wa.me` linki oluşturulamaması, özel karakter encode hatası,
  şube numarası eksik

---

## Kural 4 — Sahte Veri Yasağı

Geçici çözüm kabul edilir ama dosyaya `// TODO: PROD — gerçek değerle değiştir` notu
eklenir. Session kapanışında bu TODO'lar SESSION_INDEX.md'ye teknik borç olarak
kaydedilir. Bowlera özel: hardcode fiyat/kalori/şube adresi kesinlikle yasak — her
zaman `menu-data.json`/CMS'den.

---

## Kural 5 — Bağımlılık Disiplini

Her yeni import/bağımlılık için sorulan üç soru:
```
- Zaten mevcut mu? (duplicate önleme)
- Sadece bu dosyada mı kullanılacak? (gereksiz global önleme)
- Kaldırılırsa ne kırılır? (DEPENDENCIES.md güncellenmeli mi?)
```
Tek kullanımlık util için ayrı paket eklenmez — inline yazılır. Bundle boyutu önemlidir
(Core Web Vitals) — her yeni paket gerekçelendirilir, Framer Motion gibi ağır
kütüphaneler yalnızca orkestrasyon gerektiren yerlerde kullanılır.

---

## Kural 6 — Test Yazım Standardı

Test dosyası lokasyonu: `components/[katman]/[bileşen].test.tsx` veya
`store/[store].test.ts`. Test çerçevesi `package.json`'dan okunur — belirsizse
kullanıcıya sorulur (Vitest/Jest varsayılan). Bowlera kritik: `useCartStore` ve
customizer fiyat/kalori hesaplama testleri ZORUNLU — diğerleri geciktirilebilir.

---

## Kural 7 — Context Kaybı Koruması

Dosya adı, bileşen adı SESSION_INDEX ile tutarlı olmalı. 20 mesajda re-injection →
CORE.md Bölüm 11.
