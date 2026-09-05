## Session: [numara belirtilmedi — devam eden sohbet] — 2026-09-05
## Açıklama:
`menu_items` tablosu Neon Postgres'e eklendi. Amaç: menünün statik `lib/menu-data.json`
dosyasından gerçek bir DB tablosuna taşınması, admin panelinin (planlanan) bu tablo
üzerinde CRUD yapabilmesi için ön koşul.

## Kaynak:
- lib/menu-data.json (gerçek üretim verisi, 9 kayıt — 8'i gerçek ürün, 1'i test verisi)
- ARCHITECTURE.md §3 (BowlItem tipi, kalori/protein zorunlu alan kuralı)
- DESIGN_SYSTEM.md §7.0 (alerjen, kalori/protein ile aynı zorunluluk statüsünde)
- CONFIG_SCHEMA.md (DATABASE_URL — Neon, Frankfurt, Vercel Marketplace entegrasyonu)

## Alınan kararlar (bu sohbette):
1. `tags` (diyet/kalori etiketi) DB seviyesinde kısıtlanmadı (CHECK constraint/enum YOK) —
   sadece admin panel form UI'ı 5 sabit seçenekle kısıtlayacak (yüksek protein, glutensiz,
   vegan, sıcak-tahıl, düşük kalori — gerçek veriden çıkarıldı, ekrandaki eski filtre
   UI'ının "Keto" seçeneği gerçek veride hiç kullanılmadığı için listeye ALINMADI, ayrı
   bir düzeltme gerektirir — bkz. Açık Sorun: Menü Filtre/Veri Etiket Uyuşmazlığı).
2. `build-your-own-kasem` kaydı (`price:999`, `calories:0`, açıkça "TEST VERİSİ" etiketli)
   `menu_items` tablosuna DAHİL EDİLMEDİ — gerçek bir ürün değil, customizer akışına giden
   bir giriş kartı olduğu değerlendirildi.
   ✅ **DOĞRULANDI (bu turda):** `grep -rn "build-your-own-kasem" --include="*.tsx"
   --include="*.ts" .` çıktısı paylaşıldı — bu id SADECE `components/home/Hero.tsx`'te
   (`href="/menu/customize/build-your-own-kasem"`, "Kâseni Yarat" CTA butonu) ve ona ait
   test dosyasında geçiyor. Hiçbir `MenuCard`/menü listeleme bileşeninde ürün olarak
   render edilmiyor. Karar (2) TEYİT EDİLDİ, revizyon gerekmedi.
3. `id` alanı `uuid` DEĞİL, `text` primary key olarak tutuldu — mevcut string id'ler
   ("sig-teriyaki-tavuk" gibi) korunuyor, başka bileşenlerde referans kırılması riski
   alınmadı.

## Kalan açık nokta:
- Gerçek `lib/db/schema.ts` dosyası bu turda paylaşıldı ve TAM DOSYA olarak `menuItems`
  eklenmiş hâliyle geri verildi — kullanıcı henüz repo'ya uygulamadı/onaylamadı.
- Migration (`001_menu_items.sql`) ve seed (`002_seed_menu_items.sql`) Neon'da henüz
  KOŞULMADI — koşulduktan sonra doğrulama sorguları çalıştırılıp sonuç bu dosyaya
  eklenmeli (CORE.md §7.4).

## Etkilenen dosyalar:
- lib/db/schema.ts (TAM DOSYA olarak güncellendi, kullanıcıya verildi — repo'ya henüz
  uygulanmadı)
- lib/db/migrations/001_menu_items.sql (YENİ, henüz koşulmadı)
- lib/db/migrations/002_seed_menu_items.sql (YENİ, henüz koşulmadı)
