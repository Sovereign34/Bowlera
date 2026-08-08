# Şema Değişikliği — `users.verificationStatus` + `users.contactAttempts`

**Tarih:** 2026-08-08
**İlgili Açık Sorun:** #62 (Personel Sipariş Paneli), #59 (kayıt sonrası oturum eksikliği)
**İlgili Karar:** ARCHITECTURE.md §2.7a, Açık Sorun #64 (revize — "3 başarısız deneme" eklendi)

## Gerekçe

Twilio/Netgsm SMS-OTP kararı bu görev kapsamında bilinçli olarak bir kenara bırakıldı
(kullanıcı: "sadece bu görev için, Twilio kararı ileride ayrıca konuşulur"). Yerine:
kayıt formu (`consent/route.ts`) artık OTP olmadan doğrudan bir Auth.js oturumu açıyor —
ama sipariş TAMAMLANMASI hâlâ personel tarafından telefon/WhatsApp ile MANUEL onaylanmalı
(§2.7a, #64 — bu karar DEĞİŞMEDİ, sadece genişledi). Bu iki alan, "oturum açık ama
sipariş için henüz onaylı değil" durumunu ve "personel kaç kez ulaşmayı denedi"
sayacını DB'de tutmak için ekleniyor.

## Diff (`lib/db/schema.ts`, `users` tablosu)

```diff
   role: text("role").notNull().default("customer"), // "customer" | "staff"
+  // 🆕 [2026-08-08] Gel Al ilk-sipariş manuel onay akışı (§2.7a, #64 revize).
+  // "pending": kayıt oldu ama personel telefon/WhatsApp ile erişimi henüz TEYİT ETMEDİ —
+  //   ilk sipariş bu durumda TAMAMLANAMAZ (checkout tarafında ayrıca kodlanacak, henüz yazılmadı).
+  // "confirmed": personel teyit etti — bu ve sonraki siparişler serbest.
+  // Not: mevcut `verifiedAt` alanı ARTIK "SMS doğrulaması" anlamına gelmiyor — sadece
+  // "hesap ne zaman açıldı" anlamında kalıyor (bkz. auth.ts yorum güncellemesi). Gerçek
+  // doğrulama durumunun TEK kaynağı bu alan.
+  verificationStatus: text("verification_status").notNull().default("pending"), // "pending" | "confirmed"
+  // 🆕 [2026-08-08] Personel panelinden "ulaşamadım" işaretlemesinde +1 artar. 3'e ulaşınca
+  // panel bu kaydı "şüpheli/muhtemelen sahte" diye öne çıkarır (manuel silme kararı hâlâ
+  // personelde — otomatik silme YOK, bkz. ARCHITECTURE.md §2.7a). Panelin kendisi + bu
+  // sayacı artıran endpoint HENÜZ YAZILMADI (#62'nin kalan kapsamı).
+  contactAttempts: integer("contact_attempts").notNull().default(0),
 })
```

## Migration SQL

```sql
ALTER TABLE users ADD COLUMN IF NOT EXISTS verification_status text NOT NULL DEFAULT 'pending';
ALTER TABLE users ADD COLUMN IF NOT EXISTS contact_attempts integer NOT NULL DEFAULT 0;
```

## Edge Case'ler

1. **Mevcut satırlar (0 satır, #32 kısıtı nedeniyle):** Risk yok — tablo hâlâ boş, `DEFAULT`
   değerleri gerçek regresyon riski taşımadan uygulanabilir.
2. **`role: "staff"` olan personel hesapları da `verificationStatus` alır mı?** Evet, ama
   personel hesapları elle DB'de açıldığı için (bkz. auth.ts yorum notu — bu dosyanın
   kapsamı dışında) pratikte anlamsız kalacak. Şimdilik ayrım YAPILMADI (basitlik), panel
   UI'ı sadece `role: "customer"` kayıtlarını listeler (bu da henüz yazılmadı).
3. **`contactAttempts` sıfırlanır mı?** Personel "teyit ettim" derse (`verificationStatus`
   → `confirmed`) sayaç SIFIRLANMALI mı yoksa kalır mı — bu, panel UI'ı yazılırken
   netleştirilmeli (henüz kodlanmadı, açık soru olarak SESSION_INDEX'e işlenecek).

## Kapsam DIŞI (bilinçli olarak bu turda yapılmadı)

- Checkout akışının (`app/siparis/page.tsx`) `verificationStatus === 'pending'` durumunda
  sipariş tamamlamayı engellemesi — bu ayrı bir kod turu (Kural #5).
- Personel panelinin kendisi (contactAttempts'i artıran UI/endpoint) — #62'nin kalan
  kapsamı, henüz hiç yazılmadı.
