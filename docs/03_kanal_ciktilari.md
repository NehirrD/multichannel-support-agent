# Kanal Çıktıları

## Doküman Bilgileri

| Alan | Değer |
|---|---|
| Doküman Adı | DOC-03 Kanal Çıktıları |
| Proje | Akademi Care – Çok Kanallı Destek Ajanı Çerçevesi |
| Hazırlayan | Nehir Doğan |
| Tarih | 05.07.2026 |

## 1. Amaç

Bu belgenin amacı, DOC-02'de tanımlanan eskalasyon mantığını her destek kanalının (Slack, e-posta, web formu) kendine özgü yapısına göre somutlaştırmaktır. Aynı tetikleyici kategorisi, farklı kanallarda farklı risk seviyesi taşıyabilir; bu nedenle "ajan hangi kanalda neyi onaysız yapabilir" sorusu kanal bazında ayrı ayrı yanıtlanmıştır.

## 2. Kanal Özellikleri

| Kanal | Görünürlük | Format | Hız Beklentisi |
|---|---|---|---|
| Slack Topluluğu | Kamuya açık, çok kullanıcılı | Kısa, gayri resmi mesaj | Yüksek (dakikalar içinde yanıt beklenir) |
| E-posta | Bire bir, yarı resmi | Uzun, yapılandırılmış metin | Orta (saatler içinde yanıt beklenir) |
| Web Formu | Bire bir, yapılandırılmış | Kategori seçimli, sabit alanlar | Düşük-orta (form üzerinden takip edilir) |

Slack'in kamuya açık olması, burada üretilen her otomatik yanıtın **potansiyel olarak tüm topluluk tarafından görülebileceği** anlamına gelir; bu da veri gizliliği açısından en riskli kanalı Slack yapar.

## 3. Kanal Bazlı Otomatik Çıktılar

Ajanın insan onayı olmadan üretebileceği çıktılar, DOC-02'deki tetikleyici kategorilerinden hiçbiri tespit edilmediği sürece kanal bazında şu şekildedir:

| Kanal | Otomatik Üretilebilir Çıktı |
|---|---|
| Slack Topluluğu | Genel/sık sorulan soru (SSS) niteliğindeki, kişisel veri içermeyen yanıtlar |
| E-posta | Kullanıcının kendi hesap/kurs bilgisiyle sınırlı, tekil yanıtlar |
| Web Formu | Kategoriye önceden tanımlı, standart bilgilendirme yanıtları (örn. "talebiniz alındı, X iş günü içinde dönülecektir") |


## 4. Kanal Bazlı Onay Gereken Çıktılar

| Kanal | İnsan Onayı Gereken Durum |
|---|---|
| Slack Topluluğu | Herhangi bir kullanıcıya özel bilgi (ticket no, hesap detayı, ödeme bilgisi) içeren her yanıt |
| E-posta | Iade, üyelik iptali, hukuki içerikli veya şikayet niteliğindeki talepler |
| Web Formu | Ödeme/faturalandırma kategorisiyle işaretlenmiş talepler |

Bu tablo, DOC-02 Bölüm 3'teki "Veri gizliliği şüphesi" ve "Hassas/hukuki içerik" kategorilerinin kanal bazlı karşılığıdır.

## 5. Kanallar Arası Ortak Riskler

- **Çift yanıt riski:** Aynı kullanıcı aynı konuda hem Slack hem e-posta hem de web formu üzerinden talep açabilir. Ajan, farklı kanallardan gelen talepleri aynı kullanıcı/konu olarak eşleştiremezse her kanalda ayrı ve muhtemelen çelişkili yanıt üretir.
- **Kanal karışması:** Tek orkestrasyon grafı farklı kanallardaki bağlamları işlediği için, bir kanaldan gelen veri (örn. ticket numarası) yanlışlıkla başka bir kanaldaki yanıta sızabilir.
- **Tutarsız ton/format:** Slack'teki gayri resmi ton ile e-postadaki resmi ton karışırsa kurumsal izlenim zedelenebilir; bu doğrudan güvenlik riski olmasa da marka riski taşır.

## 6. Varsayımlar

- Her kanaldan gelen talep, aynı kullanıcı kimliğine (hesap/e-posta eşleşmesi üzerinden) bağlanabilmektedir.
- Slack'teki mesajların topluluk geneline açık olduğu, e-posta ve web formunun ise bire bir olduğu kabul edilmektedir.
- Kanal bazlı otomatik/onaylı çıktı ayrımı, mevcut destek altyapısının teknik olarak bu ayrımı uygulayabildiği varsayımına dayanmaktadır.
- Bu belgedeki örnekler senaryoya özgüdür, gerçek üretim kurallarını birebir yansıtmayabilir.