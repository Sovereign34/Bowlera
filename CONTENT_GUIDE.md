# BOWLERA — CONTENT_GUIDE.md
> Bu belge marka sesi, örnek metin kalıpları, SEO ve JSON-LD şema kontratını tanımlar.
> İçerik/metin yazan her görev önce bu dosyayı okumak zorundadır.
> Kaynak: MASTER_PLAN.md §6 (Marka Sesi ve Örnek Metinler) + §7 (SEO ve Yerel Görünürlük)

---

## 1. MARKA SESİ

**Ton:** Enerjik, şeffaf, bilinçli, sofistike. Kentli hızlı yaşam temposuna saygılı ama
sağlık/lezzetten ödün vermeyen; süslü jargon yok, malzeme odaklı dürüst dil.

| Yapılır | Yapılmaz |
|---|---|
| "Doğrudan yerel çiftçimizden aldığımız taze avokadolarla hazırladık." | "Eşsiz lezzet patlaması yaratan mucizevi süper kase." |
| Somut, ölçülebilir iddia (kalori, kaynak, malzeme) | Abartı sıfat yığını ("muhteşem", "eşsiz", "mucizevi") |
| Kullanıcıya doğrudan hitap ("Kâseni sen tasarla") | Üçüncü şahıs pazarlama dili |

> AGENT.md Self-Check: Yeni metin üretiliyorsa bu tablo karşı kontrol edilir — abartı sıfat
> tespit edilirse metin reddedilir.

---

## 2. HERO BAŞLIK KALIPLARI

| Yaklaşım | Örnek | CTA |
|---|---|---|
| Dönüşüm odaklı | "Şehrin Ritmini Yakalayan Taze ve Sağlıklı Kaseler" | "Kâseni Yarat" |
| Zanaatkar odaklı | "Toprağın Doğallığı, Şeflerin Dokunuşuyla Kâsende" | "Hemen Sipariş Ver" |
| Kişiselleştirme odaklı | "Senin Kaselerin, Senin Kuralların" | "Kendi Kâseni Tasarla" |

**CTA kütüphanesi:** "Sağlığı Keşfet" · "Ekspres Sipariş" · "Sepete Ekle" · "Kâseni Onayla"

> Yeni CTA üretilirken bu kütüphaneye eklenir, tek seferlik/rastgele CTA metni üretilmez —
> tutarlılık için.

---

## 3. ÜRÜN AÇIKLAMA KALIBI

```
[Malzeme kaynağı vurgusu] + [duyusal/somut detay] + [beslenme notu opsiyonel]

Örnek: "Ege'nin taze zeytinyağıyla harmanlanmış kinoa tabanı, ızgara
somon ve közlenmiş biberle — 520 kcal, 35g protein."
```

**Alt-text üretim kuralı:** DESIGN_SYSTEM.md §5.1'deki dosya adlandırma standardından türetilir:
```
[kategori]-[ürün-adı-kebab-case].webp  →  alt="[ürün adı, boşluklu] — Bowlera"

Örnek: signature-teriyaki-tavuk-kase.webp → alt="Teriyaki Tavuk Kase — Bowlera"
```

---

## 4. SEO — ANAHTAR KELİMELER

> Kaynak: MASTER_PLAN §7

| Öncelik | Anahtar Kelimeler |
|---|---|
| Birincil | "sağlıklı kase yemek", "poke bowl istanbul", "kendi kaseni yarat" |
| İkincil | "kinoa salatası sipariş", "vegan kase alternatifleri", "avokadolu somon kase" |

**Yerel SEO:** Her şube için ayrı Google Business Profile; NAP (isim/adres/telefon) bilgileri
"Şubeler" sayfasıyla birebir eşleşmeli — tutarsızlık yerel arama sıralamasını düşürür.

---

## 5. JSON-LD ŞEMA ŞABLONU

> Her şube sayfasına gömülür. Kaynak: MASTER_PLAN §7 · veri kaynağı: `types/index.ts` BowlItem
> (ARCHITECTURE.md §3).

```json
{
  "@context": "http://schema.org",
  "@type": "Restaurant",
  "name": "Bowlera - [Şube Adı]",
  "servesCuisine": ["Healthy Bowls", "Poke Bowls", "Salads"],
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "[Cadde/Mahalle No]",
    "addressLocality": "[İlçe]",
    "addressRegion": "[İl]",
    "addressCountry": "TR"
  },
  "hasMenu": {
    "@type": "Menu",
    "hasMenuSection": [{
      "@type": "MenuSection",
      "name": "İmza Kaseler",
      "hasMenuItem": {
        "@type": "MenuItem",
        "name": "[BowlItem.name]",
        "offers": { "@type": "Offer", "price": "[BowlItem.price]", "priceCurrency": "TRY" },
        "nutrition": {
          "@type": "NutritionInformation",
          "calories": "[BowlItem.calories] kcal",
          "proteinContent": "[BowlItem.protein]g"
        }
      }
    }]
  }
}
```

> ⚠️ `BowlItem.calories`/`protein` alanı boşsa şema üretimi durur — CORE.md §9 Mutlak
> Yasaklar ile tutarlı (kalori zorunlu alan, `nutrition` bloğu asla eksik/placeholder olamaz).
> Üretim: `lib/seo/schema.ts` (CORE.md §4 Dosya Haritası).

---

## 6. KALİTE KONTROL — CONTENT SELF-CHECK

```
[ ] Abartı sıfat var mı?                → Bölüm 1 tablosuna aykırı mı?
[ ] Yeni CTA mi üretildi?               → Kütüphaneye eklendi mi? (§2)
[ ] Ürün açıklaması kalıba uyuyor mu?   → Kaynak+duyusal detay var mı? (§3)
[ ] Alt-text adlandırma standardına uygun mu? → DESIGN_SYSTEM §5.1 ile eşleşiyor mu?
[ ] JSON-LD calories/protein dolu mu?   → BowlItem'dan geliyor mu, hardcode değil mi? (§5)
```

---

*BOWLERA CONTENT_GUIDE.md — v1.0 — Session 1 — 2026-07-17*
*Kaynak: MASTER_PLAN.md §6, §7 · DESIGN_SYSTEM.md §5.1 · ARCHITECTURE.md §3*
