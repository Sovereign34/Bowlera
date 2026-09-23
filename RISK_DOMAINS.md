# BOWLERA — RISK_DOMAINS.md
> Bu belge FAILURE_PATTERNS.md'den farklı bir şeyi tutar: **henüz yaşanmamış ama
> yaşanması muhtemel** hata sınıflarını. FAILURE_PATTERNS geçmişe bakar (oldu →
> kaydedildi), bu dosya geleceğe bakar (bu alana dokunuyorsan → şu kontrol zorunlu).
> Kaynak: AGENT.md BSC modülü + CONFIG_SCHEMA.md + CORE.md §3 Tetikleyici Tablosu

---

## NASIL KULLANILIR
Bir görev aşağıdaki alanlardan birine dokunuyorsa, CORE.md §3 Tetikleyici Tablosu
bu dosyaya yönlendirir. Buradaki kontroller "tamamlandı" işaretlenmeden önce
zorunludur — kod+test yeşil olması yeterli değildir (bkz. session_arşiv_2,
"DOKUZUNCU DERS").

Bu dosyadaki maddelerin BSC modülünden farkı: BSC kuralları *kodun içindeki*
davranışı düzenler (örn. secret'ı client'a yazma). Buradaki maddeler *sürecin*
kendisini düzenler — yani kuralın var olması yetmez, kuralın ihlalinin AI'ın
hatırlamasına değil otomatik bir kontrole bağlı olması gerekir.

Her madde için üç alan doldurulur:
- **Neden sessiz risk:** hata neden kullanıcı/geliştirici tarafından hemen fark edilmeyebilir
- **Zorunlu kontrol:** hangi araç/geçiş, AI'ın hatırlamasına değil otomatik çalışmasına dayanır
- **Son karar mercii:** AI mi, yoksa insan onayı mı gerekiyor

Bir olay burada tarif edilen risklerden biri olarak gerçekten yaşanırsa, o olay
FAILURE_PATTERNS.md'ye FP-N olarak taşınır — bu dosyadaki maddeler kendileri asla
"olay" olarak sayılmaz, yalnızca önleyici kontrol tanımıdır.

---

## 1. GİZLİ VERİ / SECRET DOSYASI

| Alan | Detay |
|---|---|
| Kapsam | `.env*`, servis hesabı JSON'ı, imzalama/sertifika dosyası, CMS/DB export'u içeren her değişiklik |
| Mevcut kural | CONFIG_SCHEMA.md §1: "Hiçbir API key/secret client bundle'a veya repo'ya commit edilmez (BSC-2)." Kural zaten yazılı. |
| Boşluk | Bu kuralın uygulanması tamamen AI'ın/geliştiricinin o an hatırlamasına dayanıyor — repo tarafında bunu otomatik engelleyen bir mekanizma yok |
| Neden sessiz risk | Yanlışlıkla commit edilen bir secret dosyası, uygulama sorunsuz çalışmaya devam ettiği için fark edilmeyebilir — sorun yalnızca repo geçmişi incelenirse görülür |
| Zorunlu kontrol | Commit öncesi otomatik secret-scanning (`gitleaks`/`trufflehog`) — CI adımı olarak, AI session'ından bağımsız |
| Son karar mercii | Araç bir eşleşme bulursa **insan onayı zorunlu** — AI "yanlış pozitif, sorun yok" diyerek kendi kendine kapatamaz |
| Bilinen örnek | — (Bowlera'da henüz yaşanmadı; ilk olay olduğunda FAILURE_PATTERNS.md'ye taşınır) |

## 2. FİYAT / ÖDEME MANTIĞI

| Alan | Detay |
|---|---|
| Kapsam | Sepet/customizer canlı fiyat hesabı (CUSTOMIZER_SPEC.md, SANDWICH_SPEC.md), varsa ödeme entegrasyonu |
| Mevcut kural | YASAK LİSTE: "Math.random() / hardcode fiyat / hardcode kalori production'da kullan" zaten yasak |
| Boşluk | Bu dosyaların hiçbirinde (ARCHITECTURE.md, INTEGRATIONS.md) uçtan uca bir ödeme/tahsilat akışı tarif edilmiyor — yalnızca fiyat *hesabı* BSC kapsamında. Canlı kod tabanında bir ödeme entegrasyonu varsa, bu doküman setine henüz işlenmemiş demektir (TEST_MATRIX.md'nin kod tabanının gerisinde kalma deseninin bir tekrarı olabilir) |
| Neden sessiz risk | Yanlış bir hesaplama "çalışıyormuş" gibi görünür; testler örnek senaryoları geçse de sınır durumlarını (0 adet, maksimum malzeme, indirim üst üste binmesi) kaçırabilir |
| Zorunlu kontrol | Örnek-tabanlı test yetmez — invariant testi ("sepet toplamı, satır kalemlerinin toplamını hiçbir kombinasyonda aşamaz/altında kalamaz" gibi) |
| Son karar mercii | AI taslak/hesap mantığını yazabilir, **gerçek bir ödeme/tahsilat entegrasyonu varsa** bunun ilk canlıya çıkışı insan onayı olmadan yapılamaz |
| Bilinen örnek | — |

## 3. EŞZAMANLILIK (CONCURRENCY)

| Alan | Detay |
|---|---|
| Kapsam | Sepet/customizer state'ine eşzamanlı erişim (BSC-6 kapsamı) + ileride eklenecek her yeni paylaşılan state |
| Mevcut kural | BSC-6 (Race Condition Koruması) zaten var, FP-1 (sepette çift ürün) bunun kayıtlı örneği |
| Boşluk | BSC-6, mevcut sepet/customizer state'i için yazıldı — yeni bir paylaşılan state (örn. stok sayacı, kampanya kodu kullanım limiti) eklendiğinde bu korumanın otomatik uygulanacağının garantisi yok |
| Neden sessiz risk | Testlerde adım adım/tek kullanıcı simülasyonunda hata üretmez; yalnızca gerçek eşzamanlı yükte (iki sekme, hızlı çift tık) ortaya çıkar |
| Zorunlu kontrol | Yeni bir paylaşılan state eklenince SELF-CHECK'e (Sepet & Customizer Katmanı) otomatik olarak "bu state race condition'a açık mı" sorusu uygulanır — bu zaten var, buradaki ek şart: yeni state türleri de bu listeye eklenmeli |
| Son karar mercii | AI uygulayabilir; yeni bir paylaşılan state türü eklendiğinde insan gözden geçirmesi önerilir |
| Bilinen örnek | FP-1 |

## 4. DÜZENLEMEYE TABİ VERİ (KVKK)

| Alan | Detay |
|---|---|
| Kapsam | `consentRegistrations` tablosu (rıza esaslı kayıt, Session 8), `users`, `order_history` — DATABASE_URL üzerinden erişilen kişisel veri |
| Mevcut kural | AUTH_SECRET ile oturum bütünlüğü sağlanıyor (CONFIG_SCHEMA.md); ayrıca BSC-2/BSC-3 genel güvenlik kapsıyor |
| Boşluk | KVKK kapsamındaki verinin *işlenmesi* (saklama süresi, silme talebi, veri minimizasyonu) için ayrı bir kontrol dosyası/checklist yok — bu bir kod kalitesi sorunu değil, uyumluluk sorunu |
| Neden sessiz risk | Uygunsuzluk, bir denetim/kullanıcı şikayeti gelene kadar hiçbir teknik belirti vermez — uygulama sorunsuz çalışmaya devam eder |
| Zorunlu kontrol | AI, KVKK kapsamına giren bir değişiklik yaptığında bunu SELF-CHECK'te açıkça işaretler ("bu değişiklik consentRegistrations/users tablosunu etkiliyor") |
| Son karar mercii | **Her zaman insan/hukuki danışman** — AI burada yalnızca "bu alana bakılmalı" diye işaretler, uygunluk onayı veremez |
| Bilinen örnek | — |

---

## GENEL KURAL
Bu dosyadaki hiçbir madde AI'ın kendi kendine "kontrol ettim, temiz" diyerek
kapatabileceği bir madde değildir. AI'ın rolü işaretlemek; insanın rolü
onaylamaktır. Bu ayrım ihlal edilirse (AI kendi kontrolünü kendi onaylarsa), bu
durum SELF-CORRECTION'a yeni bir satır olarak eklenir (bkz. AGENT.md).

---

*BOWLERA RISK_DOMAINS.md — v1.0 — 2026-09-22*
*Kaynak: AGENT.md BSC modülü · CONFIG_SCHEMA.md · CORE.md §3*
