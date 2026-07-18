# BOWLERA — TEST_MATRIX.md
> Modül bazlı test senaryoları ve durumu — CORE.md §7.1 Adım 3 ve §10 Sağlık Kontrolü'nün kaynağı.
> Session kapanışında dokunulan modül varsa güncellenir (CORE.md §7.1 Adım 3).
> Kaynak: ARCHITECTURE.md §2 · CUSTOMIZER_SPEC.md §8 · DESIGN_SYSTEM.md §7

---

## DURUM SEMBOLLERİ
`❓ Test edilmedi` · `✅ Geçti` · `❌ Başarısız` · `⬜ Henüz uygulanabilir değil (kod yok)`

---

## 1. VERİ / API KATMANI

| Test | Durum | Not |
|---|---|---|
| `/api/menu` boş veri döndüğünde graceful degradation | ⬜ | Oturum 2 |
| `BowlItem.calories` eksik kayıt reddediliyor mu | ⬜ | Oturum 2 |
| CMS geçişinde `/api/menu` response şekli sabit kalıyor mu | ⬜ | Büyüme fazı |

## 2. CUSTOMIZER

| Test | Durum | Not |
|---|---|---|
| `useCustomizerStore.ts` — adım/seçim state mantığı (9 test, npm test'te ✅) | ❓ | Oturum 3 — dosya seviyesinde 9/9 test geçti, ancak bu testlerin aşağıdaki satırlarla birebir eşleşmesi (isStepValid/guard/getTotals ayrımı) bu SESSION_INDEX güncellemesinde satır satır teyit edilmedi. Açık Sorun #11. |
| `lib/customizer-pricing.ts` — fiyat hesaplama (10 test, npm test'te ✅) | ❓ | Oturum 3 — aynı teyit notu geçerli |
| Adım geçiş guard'ı — URL manipülasyonuyla atlanamıyor | ⬜ | Oturum 3 — henüz UI (`page.tsx`) yok, guard test edilemez |
| `isStepValid` her adımı doğru kapsıyor | ❓ | Oturum 3 — store testlerine dahil olabilir, teyit gerekiyor |
| `getTotals()` seçim yokken `0`/`"—"` dönüyor, `NaN` yok | ❓ | Oturum 3 — pricing testlerine dahil olabilir, teyit gerekiyor |
| VisualPreview katman sırası doğru (kase→taban→protein→topping→sos) | ⬜ | Oturum 4 |
| Mobil sticky çekmece açık/kapalı geçişi | ⬜ | Oturum 4 |
| "Sepete Ekle" çift tıklama koruması (BSC-6) | ⬜ | Oturum 4 |

## 3. SEPET

| Test | Durum | Not |
|---|---|---|
| Tarayıcı kapanınca sepet korunuyor (persist) | ⬜ | Oturum 4 |
| `removeFromCart` doğru `cartId`'yi siliyor | ⬜ | Oturum 4 |

## 4. TASARIM / ERİŞİLEBİLİRLİK

| Test | Durum | Not |
|---|---|---|
| `prefers-reduced-motion` tüm animasyonlarda kontrol ediliyor | ⬜ | Oturum 1-5 arası, her animasyon eklendiğinde |
| Logo degrade yalnızca 4 izinli yerde kullanılıyor | ⬜ | Oturum 1-5 arası |
| Bronze rengi küçük gövde metninde kullanılmıyor | ⬜ | Oturum 1-5 arası |
| WCAG kontrast oranları (Bölüm 2 tablosu) korunuyor | ⬜ | Oturum 1 |

## 5. PERFORMANS (Core Web Vitals)

| Metrik | Hedef | Durum |
|---|---|---|
| LCP | < 2.5s | ⬜ |
| FID / INP | < 100ms | ⬜ |
| CLS | < 0.1 | ⬜ |
| Lighthouse | 90+ | ⬜ |

## 6. ÜÇÜNCÜ PARTİ ENTEGRASYON (Sonraki Faz)

| Test | Durum | Not |
|---|---|---|
| WhatsApp linki doğru encode ediliyor | ⬜ | INTEGRATIONS.md sonrası |
| Adisyo/SepetTakip API kopması → graceful degradation | ⬜ | INTEGRATIONS.md sonrası |

---

*BOWLERA TEST_MATRIX.md — v1.1 — Session 3 (kısmi) — 2026-07-18*
*Kaynak: ARCHITECTURE.md §2 · CUSTOMIZER_SPEC.md §8 · DESIGN_SYSTEM.md §7*
*Not: Bölüm 1, 3, 4, 5, 6 bu oturumda değişmedi — sadece Bölüm 2 (Customizer) güncellendi.*
