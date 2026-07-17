# BOWLERA — FAILURE_PATTERNS.md
> Bu belge projeye özgü bilinen/beklenen hata kalıplarını ve çözümlerini toplar.
> Bug fix görevlerinde CORE.md §3 Tetikleyici Tablosu bu dosyaya yönlendirir.
> Kaynak: AGENT.md BSC modülü + CUSTOMIZER_SPEC.md + INTEGRATIONS.md

---

## NASIL KULLANILIR
Yeni bir hata kalıbı keşfedildiğinde buraya eklenir (CORE.md §7.1 Adım 4). Aynı hata
tekrar yaşanmasın diye kalıp + kök neden + çözüm + önleme birlikte tutulur.

---

## 1. SEPET / STATE KALIPLARI

### FP-1 — Sepette Aynı Ürün İki Kez Eklenir
| Alan | Detay |
|---|---|
| Belirti | Kullanıcı "Sepete Ekle"ye hızlı çift tıklar, aynı ürün iki `cartId` ile sepete girer |
| Kök Neden | `addToCart` çağrısı race condition korumasız (BSC-6 ihlali) |
| Çözüm | `isAdding.current` ref lock — CUSTOMIZER_SPEC.md §7 |
| Önleme | Her "Sepete Ekle" butonu için lock deseni zorunlu (AGENT.md YASAK LİSTE) |

### FP-2 — Tarayıcı Kapanınca Sepet Kayboluyor
| Alan | Detay |
|---|---|
| Belirti | Kullanıcı siteye geri döndüğünde sepet boş |
| Kök Neden | `useCartStore` `persist` middleware'siz kuruldu veya `name` çakışması var |
| Çözüm | `persist({ name: 'bowlera-cart-storage' })` — ARCHITECTURE.md §2.3 |
| Önleme | TEST_MATRIX.md §3 "Tarayıcı kapanınca sepet korunuyor" testi her deploy öncesi çalıştırılır |

---

## 2. CUSTOMIZER KALIPLARI

### FP-3 — Adım Sırası URL ile Atlanıyor
| Alan | Detay |
|---|---|
| Belirti | `/menu/customize/[id]?step=4` direkt girilince eksik seçimle 4. adıma ulaşılıyor |
| Kök Neden | `goToStep` guard'ı yok, `maxReachedStep` kontrolü atlanmış |
| Çözüm | CUSTOMIZER_SPEC.md §3.2 guard deseni — `step > maxReachedStep + 1` ise no-op |
| Önleme | AGENT.md Self-Check: "Customizer adım sırası atlanabiliyor mu?" her PR'da sorulur |

### FP-4 — Kalori/Fiyat `NaN` Gösteriyor
| Alan | Detay |
|---|---|
| Belirti | Taban/protein/sos seçilmeden SummaryPanel'de `NaN` veya boş görünüyor |
| Kök Neden | `getTotals()` null seçim durumunu ele almıyor |
| Çözüm | Seçim `null` iken ilgili değer `0` döner, UI `"—"` gösterir — CUSTOMIZER_SPEC.md §4 |
| Önleme | BSC-3 girdi doğrulama prensibiyle tutarlı; test seti happy+edge+failure zorunlu (AGENT.md §6) |

### FP-5 — VisualPreview Yanlış Katman Gösteriyor
| Alan | Detay |
|---|---|
| Belirti | Kullanıcı somon seçtiğinde önizlemede tavuk katmanı görünüyor |
| Kök Neden | Yeni malzeme eklendi ama `public/images/layers/`'a karşılık gelen PNG/SVG eklenmedi veya z-index sırası bozuldu |
| Çözüm | CUSTOMIZER_SPEC.md §5.1 z-index sırası: kase→taban→protein→topping→sos |
| Önleme | Yeni malzeme eklenirken DEPENDENCIES.md §3 kontrol edilir, katman dosyası aynı PR'da eklenir |

---

## 3. ÜÇÜNCÜ PARTİ ENTEGRASYON KALIPLARI

### FP-6 — Pazaryeri (Adisyo/SepetTakip) API Kopması
| Alan | Detay |
|---|---|
| Belirti | Yemeksepeti/Getir siparişi POS'a düşmüyor, sessizce kayboluyor |
| Kök Neden | `try/catch` var ama hata yutuluyor, retry kuyruğu yok (BSC-8 ihlali) |
| Çözüm | INTEGRATIONS.md §1.2 — `queueForRetry` + kullanıcıya `QUEUED` durumu göster |
| Önleme | Sessiz catch bloğu AGENT.md YASAK LİSTE'de açıkça yasak |

### FP-7 — WhatsApp Linki Bozuk Mesaj Gönderiyor
| Alan | Detay |
|---|---|
| Belirti | Şubeye giden mesajda Türkçe karakterler/emoji bozuk görünüyor |
| Kök Neden | `encodeURIComponent` çağrısı atlanmış veya çift encode edilmiş |
| Çözüm | INTEGRATIONS.md §2 — tek katman `encodeURIComponent`, birim testle doğrulanır |
| Önleme | AGENT.md §3 Edge Case listesi: "özel karakter encode hatası" test setinde zorunlu |

### FP-8 — QR Masa Numarası Kayboluyor
| Alan | Detay |
|---|---|
| Belirti | QR ile giriş yapan kullanıcının siparişi hangi masaya ait belirsiz kalıyor |
| Kök Neden | `table` search param customizer/sepet akışı boyunca state'e taşınmamış |
| Çözüm | INTEGRATIONS.md §3 — `tableId` sepet meta verisine eklenir, BSC-3 ile sayısal doğrulanır |
| Önleme | Route değişikliklerinde DEPENDENCIES.md §4 kontrol edilir |

---

## 4. TASARIM / PERFORMANS KALIPLARI

### FP-9 — Animasyon Layout Shift Yaratıyor (CLS)
| Alan | Detay |
|---|---|
| Belirti | Lighthouse CLS skoru hedefin (< 0.1) üzerine çıkıyor |
| Kök Neden | Animasyon `width`/`height`/`top` gibi layout tetikleyen özellik kullanıyor |
| Çözüm | Yalnızca `transform`/`opacity` — DESIGN_SYSTEM.md §6.2 |
| Önleme | AGENT.md Self-Check her yeni animasyonda bu kuralı kontrol eder |

### FP-10 — Logo Degrade Yanlış Yerde Kullanılıyor
| Alan | Detay |
|---|---|
| Belirti | Site arka planında veya büyük yüzeyde mor-pembe-turuncu degrade görünüyor |
| Kök Neden | DESIGN_SYSTEM.md §2.1'deki 4 izinli yer dışına taşınmış |
| Çözüm | Yalnızca: aktif adım göstergesi, sepet rozeti, CTA hover kenarlığı, "Süper Gıda" etiketi |
| Önleme | AGENT.md SELF-CORRECTION tablosu bu ihlali otomatik yakalar |

---

## 5. KALİTE KONTROL — FAILURE_PATTERNS SELF-CHECK

```
[ ] Yeni hata mı keşfedildi?         → Buraya FP-N olarak eklendi mi?
[ ] Kök neden belirlendi mi?          → Sadece belirti değil, neden yazıldı mı?
[ ] Önleme kuralı var mı?             → Tekrar olmaması için hangi kontrol eklendi?
[ ] İlgili BSC/AGENT kuralına referans verildi mi?
```

---

*BOWLERA FAILURE_PATTERNS.md — v1.0 — Session 1 — 2026-07-17*
*Kaynak: AGENT.md (BSC modülü) · CUSTOMIZER_SPEC.md · INTEGRATIONS.md · DESIGN_SYSTEM.md §6.2*
