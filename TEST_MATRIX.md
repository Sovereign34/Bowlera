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
| `isStepValid` her adımı doğru kapsıyor (store seviyesi) | ✅ | Oturum 3 — `useCustomizerStore.test.ts` (9 test) içinde raporlandı |
| `getTotals()` seçim yokken `0`/`"—"` dönüyor, `NaN` yok (store seviyesi) | ✅ | Oturum 3 — `customizer-pricing.test.ts` (10 test) içinde raporlandı |
| Adım geçiş guard'ı — URL manipülasyonuyla atlanamıyor (UI seviyesi, `page.tsx`) | ❓ | Oturum 3 — dosya üretildiği bildirildi ama bu session'da hiç görülmedi/test edilmedi (bkz. SESSION_INDEX Açık Sorun #14) |
| SummaryPanel/SummaryTotals canlı render doğru | ❓ | Oturum 3 — üretildiği bildirildi, test/kod görülmedi |
| VisualPreview katman sırası doğru (kase→taban→protein→topping→sos) | ⬜ | Oturum 4 |
| Mobil sticky çekmece açık/kapalı geçişi | ⬜ | Oturum 4 |
| "Sepete Ekle" çift tıklama koruması (BSC-6) | ❓ | **Kapsam değişti: Oturum 4→3.** AddToCartButton.tsx bu oturumda üretildi (ROADMAP.md v1.1 ile güncellendi) ama test sonucu bu session'da görülmedi |

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

*BOWLERA TEST_MATRIX.md — v1.1 — Session 3 — 2026-07-18*
*Kaynak: ARCHITECTURE.md §2 · CUSTOMIZER_SPEC.md §8 · DESIGN_SYSTEM.md §7*
*Değişiklik: Store seviyesi customizer testleri ✅ işaretlendi (önceki session'da 19 test
raporlandı). UI seviyesi testler (page.tsx, SummaryPanel, AddToCartButton) ❓ olarak
işaretlendi — bu session'da içerik/test sonucu görülmedi. AddToCartButton'ın Oturum 4'ten
Oturum 3'e kapsam kayması not edildi.*
------
# TEST_MATRIX — Checkpoint 19 ekleme (2026-10-19)
> Mevcut TEST_MATRIX.md bu oturumda YÜKLENMEDİ; aşağıdaki satırlar dosyanın sonuna eklenecek.
> Durum sütunu: ✅ görüldü · 🟡 kod var, çalıştırılmadı · ⏳ donanım/canlı bekliyor.

| Alan | Test dosyası / senaryo | Durum |
|---|---|---|
| Zil sesleri | `lib/personel/alert-sounds.test.ts` (4) | 🟡 koşu sonucu görülmedi |
| Zil tekrarı | `lib/personel/alert-ringer.test.ts` (5) | 🟡 |
| Zil hook | `hooks/useNewEntryAlert.test.ts` (7) | 🟡 |
| Fiş sorguları | `lib/personel/print-jobs-queries.test.ts` (7) | 🟡 (SQL kuralları mock'la DOĞRULANAMAZ) |
| Yazıcı API | `app/api/personel/yazici/route.test.ts` (6) | 🟡 |
| Fiş şablonu | `lib/personel/ticket-format.test.ts` (7) | 🟡 |
| Tarayıcı yazdırma | `lib/personel/print-silent.test.ts` (3) | 🟡 |
| QZ köprüsü | `lib/personel/qz-printer.test.ts` (7) + `print-dispatch.test.ts` (3) | 🟡 |
| Yazıcı döngüsü | `hooks/usePrintStation.test.ts` (6) | 🟡 |
| Yazıcı paneli | `components/personel/YaziciPanel.test.tsx` (5) | 🟡 |
| Neon tabloları | `site_settings` + `print_jobs` var | ✅ (kullanıcı ekranı 15:03) |
| Canlı: zil | bekleyen kayıt/sipariş → sipariş ve kayıt melodisi ayrı, onayda susar | ⏳ |
| Canlı: QZ | QZ Tray kur → izin 'Remember' → 'Yazıcıları bul' → test fişi (80/58 mm) | ⏳ DONANIM |
| Canlı: fiş | tanınan müşteri siparişi → mutfak+kasa yazıcısı, yenilemede ÇİFT FİŞ YOK | ⏳ DONANIM |
| Canlı: fiş | ilk sipariş onaylanana kadar BASILMAZ | ⏳ |
| Canlı: Masaya | dine-in 'pending' + doğrulanmamış müşteri davranışı | ⏳ |
| Canlı: admin | 'Kendi kasem' listede yok, Hero 'Kâseni Oluştur' çalışıyor, DELETE 403 | ⏳ |
| Canlı: hero | admin'den görsel yükle → ana sayfada görünür, 'kaldır' → yer tutucu | ⏳ |

------
# TEST_MATRIX — Checkpoint 25 ekleme (2026-10-22)
> Durum sütunu: ✅ görüldü (kullanıcı ekranı) · 🟡 kod var, çalıştırılmadı/görülmedi · ⏳ canlı bekliyor · ❓ dosya görülmedi.

| Alan | Test dosyası / senaryo | Durum |
|---|---|---|
| Sipariş kapısı | `lib/verification/order-gate.test.ts` (7: 403+code, gerçek `PENDING_ACCOUNT_RESPONSE` uyumu, null/string gövde, `verifyHref` encode) | ✅ |
| Doğrulama kutusu | `components/order/PhoneVerifyPrompt.test.tsx` (2) | ✅ |
| Login sonrası yol | `lib/verification/post-login.test.ts` (7: callbackUrl, açık yönlendirme, personel/admin, oturum null, giriş sayfası döngüsü) | ✅ (`lib/verification` 4 dosya/25 PASS; satır ekranda görülmedi) |
| Doğrulama paketi | `vitest run lib/verification components/verification components/order components/registration hooks` | ✅ 11 dosya / 56 PASS |
| Tip + build | `tsc --noEmit` temiz; sahte `IMAGEKIT_*` env'li `npm run build` yeşil | ✅ (Codespaces `.env.local`'de `IMAGEKIT_*` yok → düz build düşer, Vercel etkilenmez) |
| Gel Al onayı | `lib/personel/gel-al-queries.test.ts`: `confirmPickupOrder` SADECE `orderHistory` günceller (1 UPDATE) + DB hatası reject | 🟡 5b sonrası koşu görülmedi |
| Gel Al route | `app/api/personel/gel-al/[id]/route.test.ts` (`confirmPickupOrder(id)` tek parametre) | ❓ dosya görülmedi |
| Masaya route | `app/api/personel/orders/[id]/route.test.ts` (`preparing` artık `users` yazmaz) | ❓ dosya görülmedi |
| Kayıt formu | `useRegistrationForm` login sonrası `/menu` bekleyen eski test | ❓ koşu/dosya görülmedi |
| Canlı: banner | menüde/sitede 'personel onayı bekliyor' banner'ı YOK | ✅ (kullanıcı ekranı) |
| Canlı: callbackUrl | sipariş kapısı 401 → giriş → `/siparis`'e dönüş → sipariş alındı | ✅ (kullanıcı beyanı) |
| Canlı: doğrulama kutusu | doğrulanmamış hesapla 'Siparişi Onayla' → 'Önce telefonunu doğrula' kutusu → `/dogrula?next=%2Fsiparis` → dönüş | ⏳ |
| Canlı: login yönlendirme | doğrulanmamış müşteri girişte `/dogrula`'ya düşer; personel/admin düşmez | ⏳ |
| Canlı: `/dogrula` `next` | `app/dogrula/page.tsx` `next` parametresini okuyor, doğrulayınca hedefe dönüyor | ⏳ (kod görülmedi) |
| Canlı: Masaya | 'preparing' müşteriyi artık `confirmed` YAPMAZ; sonra Gel Al → 403 + kutu | ⏳ |
| Canlı: Gel Al | 'Onayla' siparişi Hazırlanıyor'a alır, hesap durumu DEĞİŞMEZ | ⏳ |

------
# TEST_MATRIX — Checkpoint 26 ekleme (2026-10-22 15:45)
> Durum sütunu: ✅ görüldü · 🟡 kod var, koşulmadı · ⏳ canlı bekliyor · ❓ dosya görülmedi.

| Alan | Test dosyası / senaryo | Durum |
|---|---|---|
| Tip kontrolü | `rm -rf .next` sonrası `npx tsc --noEmit` (5c silmeleri + 5d sonrası) | ✅ temiz (ilk 6 hata eski `.next/types` önbelleğiydi) |
| Kayıt Onayları kaldırma | silinen dosyalara import kalmadı (`tsc` temiz); `git ls-files \| grep -i kayit` ile silme teyidi | 🟡 teyit görülmedi |
| Personel sayfası | `app/personel/page.tsx` 5 sekme (Masaya, Şifre Talepleri, Gel Al, Müşteriler, Ürünler) çalışıyor | ⏳ canlı |
| Admin etiketi | `app/admin/musteriler/[id]/page.tsx:76` doğrulanmamış hesapta 'Doğrulama: Teyitsiz' | ✅ kod (`grep`), ⏳ canlı |
| 5a/5b testleri | `vitest run lib/personel "app/api/personel" components/personel hooks` | 🟡 koşulmadı |
| Yazıcı | `YaziciPanel`/`usePrintStation`/`qz-printer` testleri dosyada var; sekme sayfaya BAĞLI DEĞİL | 🟡 / ⏳ donanım (#171, #176) |
| Güvenlik | `npm audit --omit=dev` 9 açık (3 orta, 6 yüksek); GitHub 39 uyarı | 🟡 high paket adları görülmedi (#144) |

