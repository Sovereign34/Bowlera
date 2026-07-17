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

### Oturum 3 — Zustand + Customizer (Masaüstü)
| Görev | Kabul Kriteri |
|---|---|
| `useCustomizerStore.ts` | CUSTOMIZER_SPEC.md §3'teki tam kontrata uyar |
| 4 adım UI (masaüstü) | Adım geçiş guard'ı çalışır — URL manipülasyonuyla atlanamaz |
| SummaryPanel canlı hesaplama | Seçim yokken `"—"` gösterir, `NaN` üretmez |

### Oturum 4 — VisualPreview + Mobil + Sepet
| Görev | Kabul Kriteri |
|---|---|
| VisualPreview (katmanlı CSS/SVG) | Katman sırası: kase→taban→protein→topping→sos |
| Mobil sticky çekmece | Açık/kapalı durumları CUSTOMIZER_SPEC §6'ya uyar |
| `useCartStore.ts` + CartDrawer/CartBadge | Sepet tarayıcı kapansa da korunur (persist) |

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

*BOWLERA ROADMAP.md — v1.0 — Session 1 — 2026-07-17*
*Kaynak: MASTER_PLAN.md §8 · CORE.md §7.1, §7.3*
