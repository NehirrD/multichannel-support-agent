# Eskalasyon Tetikleyicileri

## Doküman Bilgileri

| Alan | Değer |
|---|---|
| Doküman Adı | DOC-02 Eskalasyon Tetikleyicileri |
| Proje | Akademi Care – Çok Kanallı Destek Ajanı Çerçevesi |
| Hazırlayan | Nehir Doğan |
| Tarih | 05.07.2026 |

## 1. Amaç

Bu belgenin amacı, destek ajanının bir talebi kendi başına sonuçlandırabileceği durumlar ile mutlaka bir insana devretmesi gereken durumlar arasındaki sınırı somut kriterlerle tanımlamaktır. DOC-01'de tespit edilen iki olay (yanlış "çözüldü" etiketi ve ticket numarası sızıntısı), bu sınırın önceden tanımlanmamış olmasından kaynaklanmıştır; bu belge söz konusu boşluğu kapatır ve ajanın "ne zaman durup insana sorması gerektiğini" net kurallara bağlar.

## 2. Eskalasyon Nedir?

Bu proje kapsamında eskalasyon, ajanın bir talebi otomatik olarak sonuçlandırmak yerine, kararı bir insana (destek uzmanı, hukuk veya güvenilirlik ekibi) devretmesi anlamına gelir. Eskalasyon iki şekilde tetiklenebilir:

- **Proaktif eskalasyon:** Ajan, talebi işlerken önceden tanımlı bir riskli durumla karşılaşır ve kendiliğinden insana devreder.
- **Reaktif eskalasyon:** Ajanın verdiği bir kararın (örn. "çözüldü" etiketi) sonradan yanlış olduğu anlaşılır ve durum geriye dönük olarak insana taşınır.

DOC-01'deki 1. olay (yanlış "çözüldü" etiketi) reaktif eskalasyonun eksikliğine, 2. olay (ticket sızıntısı) proaktif eskalasyonun eksikliğine örnektir.

## 3. Tetikleyici Kategorileri

Ajanın bir talebi otomatik sonuçlandırmayıp insana devretmesi gereken durumlar beş ana kategoride toplanmıştır:

| Kategori | Örnek Durum | Neden Riskli |
|---|---|---|
| Çelişkili sinyaller | Kullanıcı düşük memnuniyet puanı verirken ajan talebi "çözüldü" olarak etiketlemek istiyor | Ajanın kendi başarısını dış doğrulama olmadan raporlaması yanlış metriklere yol açar |
| Veri gizliliği şüphesi | Yanıt içinde başka bir kullanıcıya ait ticket numarası, e-posta veya isim geçme ihtimali | Kişisel veri sızıntısı, hukuki sorumluluk |
| Çift yanıt riski | Aynı kullanıcı/konu hem Slack hem e-posta üzerinden talep açmış | Çelişkili veya tekrarlı yanıtlar kullanıcı güvenini zedeler |
| Düşük güven skoru | Ajanın sınıflandırma modeli talebi net bir kategoriye oturtamıyor (belirsiz/karma niyet) | Yanlış kategoriye göre üretilen yanıt hatalı olabilir |
| Hassas/hukuki içerik | İade talebi, yasal tehdit, şikayet, KVKK/veri talebi içeren mesajlar | Yanlış otomatik yanıt hukuki risk doğurabilir |

Bu kategorilerden herhangi biri tetiklendiğinde ajan, otomatik yanıt/etiketleme adımını durdurmalı ve talebi ilgili eskalasyon seviyesine yönlendirmelidir.

## 4. Eskalasyon Seviyeleri

| Seviye | Kim Devralır | Hangi Kategoriler İçin |
|---|---|---|
| Seviye 1 | Destek Uzmanı (Tier 1) | Düşük güven skoru, çift yanıt riski |
| Seviye 2 | Kıdemli Destek / Operasyon Sorumlusu | Çelişkili sinyaller (memnuniyet-etiket uyumsuzluğu) |
| Seviye 3 | Hukuk Ekibi | Veri gizliliği şüphesi, hassas/hukuki içerik |
| Seviye 4 | Güvenilirlik (Reliability) Ekibi | Sistemik/tekrarlayan hatalar (aynı tetikleyicinin kısa sürede birden çok kez tekrarlanması) |

Bir talep birden fazla kategoriyi aynı anda tetiklerse, en yüksek seviyeye (örn. Seviye 3 veya 4) yönlendirilir.

## 5. Karar Akışı

Ajanın karar süreci aşağıdaki sırayla işler (bkz. `diagrams/eskalasyon_akisi.drawio`):

1. Talep alınır ve kanal/içerik bilgisiyle birlikte sınıflandırılır.
2. Talep, Bölüm 3'teki beş tetikleyici kategoriye karşı kontrol edilir.
3. Tetikleyici yoksa, ajan otomatik yanıt üretir ve talebi normal akışta sonuçlandırabilir.
4. Tetikleyici varsa, talep ilgili eskalasyon seviyesine (Bölüm 4) yönlendirilir ve ajan **otomatik "çözüldü" etiketi koyamaz**.
5. Eskale edilen talep, insan onayı sonrası ya kapatılır ya da ajana revize talimatla geri döner.

## 6. Roller ve Sorumluluklar

| Rol | Sorumluluk |
|---|---|
| Destek Uzmanı (Tier 1) | Seviye 1 eskalasyonları değerlendirir, gerekirse Seviye 2'ye taşır |
| Kıdemli Destek / Operasyon Sorumlusu | Seviye 2 eskalasyonları çözer, memnuniyet-etiket uyumsuzluklarını doğrular |
| Hukuk Ekibi | Seviye 3 eskalasyonlarda veri gizliliği ve hukuki riski değerlendirir |
| Güvenilirlik Ekibi | Seviye 4'te sistemik hataları analiz eder, ajan kurallarında güncelleme önerir |
| Ajan (Sistem) | Tetikleyicileri tespit eder, otomatik karar vermeden ilgili seviyeye yönlendirir, kararı asla kendi kendine "çözüldü" olarak kapatmaz |

## 7. Varsayımlar

- Ajanın sınıflandırma modeli, güven skorunu (confidence score) her talep için üretebilmektedir.
- Kullanıcı memnuniyet puanı, talep kapanmadan veya kapandıktan hemen sonra sisteme ulaşabilmektedir.
- Eskalasyon seviyeleri arasındaki yönlendirme, mevcut destek altyapısında (ticket sistemi) teknik olarak mümkündür.
- Bu belgedeki seviye ve rol tanımları, gerçek bir kurumsal yapıyı birebir yansıtmak yerine senaryoya uygun örnek bir organizasyon varsaymaktadır.