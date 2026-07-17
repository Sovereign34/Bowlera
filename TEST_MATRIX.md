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
| Adım geçiş guard'ı — URL manipülasyonuyla atlanamıyor | ⬜ | Oturum 3 |
| `isStepValid` her adımı doğru kapsıyor | ⬜ | Oturum 3 |
| `getTotals()` seçim yokken `0`/`"—"` dönüyor, `NaN` yok | ⬜ | Oturum 3 |
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

*BOWLERA TEST_MATRIX.md — v1.0 — Session 1 — 2026-07-17*
*Kaynak: ARCHITECTURE.md §2 · CUSTOMIZER_SPEC.md §8 · DESIGN_SYSTEM.md §7*
