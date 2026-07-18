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

useCustomizerStore.ts  ✅ Oturum 3'te üretildi (aşağıdaki tüketiciler henüz yok)
├── lib/customizer-pricing.ts  ✅ Oturum 3 — store'un fiyat hesaplama mantığı buradan besleniyor
├── lib/customizer-data.ts     ✅ Oturum 3 — statik adım/malzeme verisi buradan besleniyor
├── StepBase/Protein/Toppings/Sauce.tsx  ⬜ Henüz yok (selections okur, select* çağırır)
├── SummaryPanel.tsx         ⬜ Henüz yok (getTotals() okur — CANLI, her seçimde re-render)
├── VisualPreview.tsx        ⬜ Henüz yok (selections okur, katman aktiflik hesaplar)
└── app/menu/customize/[id]/page.tsx  ⬜ Henüz yok (currentStep okur, goToStep guard'ı uygular)
```

> ⚠️ Adım isimleri: yukarıdaki liste `StepBase/Protein/Toppings/Sauce.tsx` şeklinde
> 4 adımı yansıtıyor — Oturum 2'de alınan 5 adım kararına (Base/Main/Garden/
> Signature Flavor/Finish) göre güncel değil. Açık Sorun #10 kapsamında,
> `useCustomizerStore.ts` gerçekten üretildiğinde bu liste 5 adıma göre
> düzeltilmeli — bu oturumda henüz düzeltilmedi (store içeriği satır satır
> incelenmedi, Açık Sorun #11).

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

> ⚠️ Oturum 3'te `store/useCustomizerStore.ts` üretildi — bu store'un `CustomizerSelection`
> tipini `types/index.ts`'ten mi aldığı, yoksa kendi içinde mi tanımladığı bu oturumda teyit
> edilmedi (Açık Sorun #12). Teyit edilene kadar bu diyagramda `types/index.ts` satırına
> `CustomizerSelection` bağımlılığı **varsayımsal** olarak işaretli kalıyor.

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

*BOWLERA DEPENDENCIES.md — v1.1 — Session 3 (kısmi) — 2026-07-18*
*Kaynak: ARCHITECTURE.md §2 · CORE.md §4, §7.4*
