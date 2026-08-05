## Session 6 — 2026-08-05 — Netgsm Blokajı, WhatsApp OTP Fallback Kararı ve Uygulaması

### Bağlam
- Kullanıcı Netgsm SMS başlık başvurusunda esnaf odası kaydı (9000 TL) veya marka tescili (uzun süre)
  isteniyor diye blokaja girdiğini bildirdi. Twilio'nun TR SMS kısıtından (#32) sonra ikinci bir
  sağlayıcı engeliyle karşılaşıldı.
- Araştırma: SMS başlık onayında hiyerarşi netleştirildi — vergi levhasında ticari ünvan (Bowlera)
  yazıyorsa esnaf odası/marka tescili GEREKMİYOR; yoksa işyeri açma ruhsatı (zaten restoran açılışı
  için alınacak) da yeterli olabiliyor. Esnaf odası/marka tescili sadece bu ikisi de yoksa gerekiyor.
- Kullanıcı, işyeri açma ruhsatı aşamasında Bowlera adını kullanabileceğini teyit etti.

### Karar (kullanıcı onayı ile) — Hibrit OTP Kanalı
- WhatsApp OTP birincil kanal, SMS ikincil/fallback kanal olarak kullanılacak.
- **Kritik bulgu:** Twilio Verify Service zaten `channel: "whatsapp"` parametresini destekliyor —
  ayrı bir Meta/WhatsApp Cloud API entegrasyonu GEREKMİYOR, mevcut Twilio hesabı üzerinden yürütülebilir.
- `verify/route.ts` DEĞİŞMEDİ — Twilio doğrulama kanaldan bağımsız çalışıyor (sadece kod/telefon).

### Kod Üretimi
- `lib/auth/send-otp.ts` (yeni) — `sendOtpWithFallback()`: WhatsApp→SMS sırasıyla dener, ikisi de
  başarısız olursa son hatayı fırlatır.
- `app/api/auth/otp/send/route.ts` (güncellendi) — yeni fallback modülünü çağırıyor, response'a
  hangi kanaldan gönderildiği (`channel`) eklendi.
- `lib/auth/send-otp.test.ts` (yeni) — happy path (WhatsApp başarılı), edge case (WhatsApp düşer,
  SMS'e geçer), failure path (ikisi de başarısız, hata fırlatılır). **Kullanıcı tarafından henüz
  koşulmadı — bir sonraki turda `npx vitest run` ile doğrulanmalı.**
- Kalite Skoru: 5/5. Güvenlik Skoru: 8/8.

### Açık Kalan / Yeni Açılan
- **#56 (yeni, 🟡):** Twilio hesabında WhatsApp Business Sender'ın onaylı/aktif olup olmadığı
  bilinmiyor — bu, Meta Business doğrulaması gerektiren AYRI bir ön koşul (esnaf odası/patent
  süreciyle ilgisi yok). Onaylanmadan `whatsapp` denemesi başarısız olur ama kod SMS'e otomatik
  düşer — sistem kırılmaz, sadece WhatsApp avantajı devreye girmez. Netleştirilmeli.
- **#32 kısmen etkilendi, KAPANMADI:** Twilio TR SMS kısıtı hâlâ geçerli olabilir (bu turda ayrıca
  test edilmedi) — ama WhatsApp kanalı bu kısıtın dışında kalabilir, bu da #32'yi fiilen aşabilir.
  Kesinleşmesi için canlı test gerekiyor (#56 çözüldükten sonra).
- Netgsm/esnaf odası konusu bu turda KAPANMADI — sadece paralel bir çözüm (WhatsApp) devreye alındı;
  vergi levhası/işyeri ruhsatı yoluyla Netgsm'in de ayrıca çözülmesi hâlâ mümkün ve istenirse yapılabilir.
- `/giris` sayfası telefon formu, gönderim sonrası hangi kanaldan gittiğini kullanıcıya göstermeli
  ("WhatsApp'tan gönderildi" / "SMS ile gönderildi") — frontend tarafı henüz üretilmedi.

### Sembol Özeti
📁 (3 dosya: 2 yeni + 1 güncelleme) · 🔧 (1 mimari karar — hibrit OTP kanalı) · 🆕 (#56)
