# BOWLERA — DEPENDENCIES.md
> Bu belge dosya/bileşen bağımlılık haritasıdır — "bu dosyayı değiştirirsem ne kırılır" sorusuna cevap verir.
> Session kapanışında bir değişiklik oldukça CORE.md §7.1 Adım 4 gereği güncellenir.
> Kaynak: ARCHITECTURE.md §2 (Modül Kontratları) + CORE.md §4 (Dosya Haritası)

---

## 1. DOSYA → DOSYA BAĞIMLILIĞI (Dokümantasyon Katmanı)

| Dosya | Kaynak Aldığı | Değişirse Etkilediği |
|---|---|---|
| MASTER_PLAN.md | — (kök referans, değiştirilmez) | Tüm dosyalar |
| CORE.md | MASTER_PLAN.md | AGENT.md, SESSION_INDEX.md tetikleyici tablosu |
| AGENT.md | CORE.md | Tüm kod üretim görevleri (Self-Check) |
| ARCHITECTURE.md | MASTER_PLAN §3, §5 | CUSTOMIZER_SPEC.md, DEPENDENCIES.md (bu dosya), DESIGN_SYSTEM.md §token kullanımı |
| DESIGN_SYSTEM.md | MASTER_PLAN §2, §4 | Tüm UI bileşenleri, CUSTOMIZER_SPEC.md §5 VisualPreview |
| CUSTOMIZER_SPEC.md | MASTER_PLAN §3.3, §5.2, §5.4 · ARCHITECTURE §2.4 | store/useCustomizerStore.ts, components/customizer/* |
| CONTENT_GUIDE.md | MASTER_PLAN §6, §7 | Tüm statik metin, SEO/JSON-LD üretimi |
| INTEGRATIONS.md | MASTER_PLAN §5.6 | lib/integrations/*, app/api/order/route.ts |
| CONFIG_SCHEMA.md | INTEGRATIONS.md, ARCHITECTURE §4.1 | .env.local, deploy platformu env ayarları |

> ⚠️ ARCHITECTURE.md §2.4'teki `CustomizerState` özeti ile CUSTOMIZER_SPEC.md §3.1'deki tam
> kontrat arasında isim tutarsızlığı var (`calculateTotals` vs `getTotals`) — düzeltme bekliyor,
> düzeltilene kadar **CUSTOMIZER_SPEC.md esas alınır** (tam kontrat o).

---

## 2. BİLEŞEN → STORE BAĞIMLILIĞI

```
useCartStore.ts
├── CartBadge.tsx           (cart.length okur)
├── CartDrawer.tsx          (cart okur, removeFromCart çağırır)
└── Customizer "Sepete Ekle" (addToCart çağırır — CUSTOMIZER_SPEC §7)

useCustomizerStore.ts
├── StepBase/Protein/Toppings/Sauce.tsx  (selections okur, select* çağırır)
├── SummaryPanel.tsx         (getTotals() okur — CANLI, her seçimde re-render)
├── VisualPreview.tsx        (selections okur, katman aktiflik hesaplar)
└── app/menu/customize/[id]/page.tsx  (currentStep okur, goToStep guard'ı uygular)
```

> Bir store'a yeni alan eklenirse: yukarıdaki bağımlı bileşenlerin **hepsi** kontrol edilmeli —
> CORE.md §7.4 (Veri Şeması Değişiklik Protokolü) devreye girer.

---

## 3. VERİ MODELİ BAĞIMLILIĞI

```
types/index.ts (BowlItem, CartItem, CustomizerSelection)
├── lib/menu-data.json           (BowlItem şemasına uymalı)
├── app/api/menu/route.ts        (BowlItem[] döner)
├── components/menu/MenuCard.tsx (BowlItem alır, calories ZORUNLU render eder)
├── store/useCartStore.ts        (CartItem[] tutar)
└── lib/seo/schema.ts            (BowlItem → JSON-LD MenuItem dönüşümü — CONTENT_GUIDE.md)
```

> `BowlItem.calories` alanı opsiyonel yapılırsa: MenuCard, CUSTOMIZER_SPEC §4, CONTENT_GUIDE
> §JSON-LD şeması hepsi kırılır — CORE.md §9 Mutlak Yasaklar'da açıkça engellenmiş.

---

## 4. ÜÇÜNCÜ PARTİ ENTEGRASYON BAĞIMLILIĞI

```
lib/integrations/whatsapp.ts    ← INTEGRATIONS.md §WhatsApp Köprüsü
lib/integrations/marketplace.ts ← INTEGRATIONS.md §Adisyo/SepetTakip (server-side ZORUNLU — ARCHITECTURE §1 Kural 4)
app/api/order/route.ts          ← CONFIG_SCHEMA.md'deki env değişkenlerine bağlı (API key)
```

> Bu üç dosyadan biri değişirse: FAILURE_PATTERNS.md'de ilgili "entegrasyon kopması" senaryosu
> gözden geçirilmeli.

---

## 5. KALİTE KONTROL — DEPENDENCIES SELF-CHECK

```
[ ] Yeni dosya/bileşen eklendi mi?        → İlgili bağımlılık satırı eklendi mi?
[ ] Store'a yeni alan eklendi mi?         → Bağımlı bileşenler listelendi mi? (§2)
[ ] BowlItem şeması değişti mi?           → §3'teki zincir kontrol edildi mi, CORE §7.4 tetiklendi mi?
[ ] Yeni üçüncü parti entegrasyon mu?     → §4'e satır eklendi mi?
```

---

*BOWLERA DEPENDENCIES.md — v1.0 — Session 1 — 2026-07-17*
*Kaynak: ARCHITECTURE.md §2 · CORE.md §4, §7.4*
