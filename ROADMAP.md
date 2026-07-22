# BOWLERA — ROADMAP.md
> 5 oturumluk inşa sırası, görev listesi ve kabul kriterleri.
> CORE.md §7.1 Adım 10 ve §7.3'te oturum/görev tamamlandığında bu dosya güncellenir.
> Kaynak: MASTER_PLAN.md §8 (Sonraki Adımlar)

---

## 1. OTURUM SIRASI VE KABUL KRİTERLERİ

### Oturum 0 — Ajan Altyapısı Kurulumu 🟡 Devam ediyor
| Görev | Kabul Kriteri | Durum |
|---|---|---|
| Çekirdek üçlü (CORE+AGENT+SESSION_INDEX) | Kullanıcı onayı | ✅ |
| ARCHITECTURE.md + DESIGN_SYSTEM.md + CUSTOMIZER_SPEC.md | Kullanıcı onayı, dosyalar arası çelişki yok | 🟡 Onay bekliyor (1 tutarsızlık düzeltilecek) |
| DEPENDENCIES.md + ROADMAP.md + TEST_MATRIX.md | Kullanıcı onayı | 🟡 Üretim aşamasında |
| CONFIG_SCHEMA.md + FAILURE_PATTERNS.md | Kullanıcı onayı | ⬜ Bekliyor |
| CONTENT_GUIDE.md + INTEGRATIONS.md | Kullanıcı onayı | ⬜ Bekliyor |

### Oturum 1 — Next.js Kurulumu
| Görev | Kabul Kriteri |
|---|---|
| Next.js (App Router) + Tailwind + TypeScript iskeleti | `npm run dev` hatasız çalışır |
| Font/renk sistemi (`tailwind.config.ts`) | DESIGN_SYSTEM.md §2, §3 token'larıyla birebir eşleşir |
| Header/Footer | Responsive, tüm sayfalarda render edilir |
| Ana Sayfa Hero | LCP < 2.5s (ARCHITECTURE §4.2) |

### Oturum 2 — Menü Sayfası
| Görev | Kabul Kriteri |
|---|---|
| `menu-data.json` (placeholder veri, TODO işaretli) | BowlItem şemasına uyar, `calories` her kayıtta dolu |
| MenuCard.tsx | Kalori her kartta görünür (zorunlu — atlanamaz) |
| Filtre paneli (alerjen + diyet/kalori) | Filtre sonucu boşsa "sonuç yok" state'i var |

### Oturum 3 — Zustand + Customizer (Masaüstü) 🟢 Tamamlandı — TEYİT EDİLDİ (2026-07-22)
> ⚠️ Bu bölüm v1.0'da "4 adım UI" diyordu. Oturum 2'deki Karar #1 (SESSION_INDEX.md)
> ile akış 5 adıma çıkarıldı ama bu değişiklik o sırada ROADMAP.md'ye işlenmemişti —
> burada düzeltiliyor.

| Görev | Kabul Kriteri | Durum |
|---|---|---|
| `useCustomizerStore.ts` | CUSTOMIZER_SPEC.md §3'teki tam kontrata uyar | 🟢 Oturum 4'te dosya bizzat görüldü, satır satır CUSTOMIZER_SPEC.md §3 ile teyit edildi. Ayrıca Bitkisel Protein alt-varyant mekanizması (§3.4/§3.5, Karar #11) bu store'a eklendi. |
| **5 adım** UI (masaüstü) — Base→Main→Garden→Signature Flavor→Finish | Adım geçiş guard'ı çalışır — URL manipülasyonuyla atlanamaz | 🟢 `StepMain.tsx` görüldü, guard mantığı (`maxReachedStep`) store tarafında teyit edildi. |
| SummaryPanel canlı hesaplama | Seçim yokken `"—"` gösterir, `NaN` üretmez | 🟢 `lib/customizer-pricing.ts` görüldü ve düzeltildi (Bitkisel Protein variant-aware olmama bug'ı giderildi, Karar #11). `lib/customizer-summary-format.ts` de görülüp `MobileSummaryDrawer.tsx` ile konsolide edildi (Açık Sorun #43 kapandı). |
| "Sepete Ekle" (AddToCartButton) | Çift tıklama koruması (BSC-6) çalışır, geçersiz adımda disabled | 🟡 `AddToCartButton.tsx` bu sohbette hiç görülmedi — `MobileSummaryDrawer.tsx` içinde referans olarak geçiyor ama BSC-6 koruması bu oturumda doğrulanmadı. **NOT:** TEST_MATRIX.md senkron kontrolü hâlâ açık. |

### Oturum 4 — VisualPreview + Mobil + Sepet 🟡 Devam ediyor
| Görev | Kabul Kriteri | Durum |
|---|---|---|
| VisualPreview (katmanlı CSS/SVG) | Katman sırası: kase→taban→protein→topping→sos | 🟡 Bileşen bu sohbette görülmedi, sadece `MobileSummaryDrawer.tsx` içindeki referansı (className davranışı) incelendi (Açık Sorun #34) |
| Mobil sticky çekmece | Açık/kapalı durumları CUSTOMIZER_SPEC §6'ya uyar | 🟢 `MobileSummaryDrawer.tsx` görüldü, açık/kapalı davranışı §6 ile tutarlı; format hatası düzeltildi (Açık Sorun #43) |
| `useCartStore.ts` + CartDrawer/CartBadge | Sepet tarayıcı kapansa da korunur (persist) | 🟡 CartDrawer portal bug'ı (backdrop-blur containing-block) düzeltildiği raporlandı, ama `useCartStore.ts` bu sohbette hiç görülmedi — persist davranışı teyit edilmedi |

> 🆕 **Planlanmamış ek kapsam (v1.2 notu):** Oturum 4 sırasında, orijinal 5 oturumluk
> planda hiç yer almayan bir **Auth/Hesap alt sistemi** eklendi (Twilio Verify + Auth.js
> JWT, Neon Postgres, `/giris`, `/hesap`, adres/profil formu). Bu MASTER_PLAN.md v2.2'de
> sitemap'e işlendi ama ROADMAP'in oturum tablosunda kendi satırı yok — kabul kriterleri
> tanımsız kaldı. Bir sonraki güncellemede ya Oturum 4'e ek satır olarak ya da ayrı bir
> "Oturum 4.5" olarak eklenmesi önerilir. Kaynak: `SESSION_INDEX.md` Karar #17-23.

### 🛑 Kontrol Noktası — Kullanıcı Testi
| Görev | Kabul Kriteri |
|---|---|
| 5-10 kişilik test grubu | Adım netliği, mobil özet panel fark edilirliği, "Sepete Ekle" süresi ölçülür |
| Bulgular | Oturum 5 öncesi kritik UX sorunları giderilir |

### Oturum 5 — İçerik Sayfaları + SEO + Son Kontrol
| Görev | Kabul Kriteri |
|---|---|
| Hakkımızda, Şubeler, İletişim | CONTENT_GUIDE.md marka sesine uyar |
| JSON-LD şema (her şube) | CONTENT_GUIDE.md §JSON-LD şablonuna göre, Google Rich Results testinden geçer |
| Core Web Vitals son kontrol | LCP<2.5s, FID/INP<100ms, CLS<0.1, Lighthouse 90+ |

---

## 2. SONRAKİ FAZ (Lansman Sonrası — Kapsam Dışı)

| Alan | Not |
|---|---|
| Adisyo/SepetTakip, WhatsApp köprüsü, QR menü | Gerçek API anahtarı/iş ortaklığı gerektirir — INTEGRATIONS.md hazır olacak ama entegrasyon ayrı faz |
| SMS/e-posta bildirimi (Twilio) | POS entegrasyonuyla birlikte devreye alınır |
| Headless CMS geçişi (Sanity/Contentful) | `/api/menu` sözleşmesi bozulmadan yapılmalı (ARCHITECTURE §2.2) |
| Server-side gerçek ürün fotoğrafı kompozisyonu | VisualPreview'ın CSS/SVG yerine gerçek foto katmanına geçişi |

---

*BOWLERA ROADMAP.md — v1.2 — Session 4 — 2026-07-22*
*Kaynak: MASTER_PLAN.md §8 · CORE.md §7.1, §7.3*
*Değişiklik (v1.1): Oturum 3 satırı 4→5 adıma düzeltildi (Karar #1 ile senkron), AddToCartButton
kabul kriteri eklendi, tüm Oturum 3 satırlarına teyit durumu eklendi.*
*Değişiklik (v1.2): Oturum 3 satırları bu sohbette görülen dosyalarla (useCustomizerStore.ts,
customizer-pricing.ts, customizer-summary-format.ts) teyit edilip 🟢'ye güncellendi; sadece
AddToCartButton.tsx görülmediği için 🟡 kaldı. Oturum 4'e durum sütunu eklendi. Planlanmamış
Auth/Hesap alt sistemi (Karar #17-23) not olarak eklendi — kendi oturum satırı henüz yok,
takip gerekiyor. Kaynak: bu sohbette yapılan MASTER_PLAN/ROADMAP tutarlılık denetimi.*
