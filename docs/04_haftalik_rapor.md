# Haftalık Rapor

## Doküman Bilgileri

| Alan | Değer |
|---|---|
| Doküman Adı | DOC-04 Haftalık Rapor |
| Proje | Akademi Care – Çok Kanallı Destek Ajanı Çerçevesi |
| Hazırlayan | Nehir Doğan |
| Tarih | 05.07.2026 |

## 1. Amaç

Bu belgenin amacı, DOC-02 ve DOC-03'te tanımlanan politika ve eskalasyon kurallarının pratikte gerçekten işleyip işlemediğini düzenli olarak ölçmektir. DOC-01'de tespit edilen iki olayın (yanlış "çözüldü" etiketi, ticket sızıntısı) bir daha fark edilmeden tekrarlanmaması için, bu tür sapmaların haftalık olarak sistematik biçimde görünür kılınması hedeflenmektedir.

## 2. Rapor Kapsamı ve Periyodu

- Rapor, **haftalık** olarak (Pazartesi–Pazar) hazırlanır ve bir sonraki haftanın ilk iş gününde paylaşılır.
- Kapsam, üç kanaldan (Slack, e-posta, web formu) gelen tüm taleplerin ajan tarafından işlendiği süreci kapsar.
- Rapor, hem ajanın otomatik kararlarını hem de insana devredilen (eskale edilen) kararları içerir.

## 3. İzlenecek Metrikler

| Metrik | Tanım |
|---|---|
| Yanlış "Çözüldü" Oranı | Ajanın "çözüldü" etiketlediği taleplerden, düşük memnuniyet puanı alanların oranı |
| Veri Gizliliği İnsident Sayısı | Bir kullanıcıya başka bir kullanıcıya ait bilgi görünme şüphesiyle açılan vaka sayısı |
| Çift Yanıt Oranı | Aynı kullanıcı/konu için birden fazla kanaldan ayrı yanıt üretilen talep oranı |
| Kanal Bazlı Eskalasyon Oranı | Toplam talep içinde eskale edilen taleplerin oranı, kanal ve seviye (1-4) kırılımında |
| Ortalama İnsan Onay Süresi | Bir talebin eskale edildiği andan insan onayı/kararı alana kadar geçen ortalama süre |

## 4. Metrik Hesaplama Yöntemi

- **Yanlış "Çözüldü" Oranı** = ("çözüldü" etiketli ve memnuniyet puanı eşik altında olan talep sayısı) / (toplam "çözüldü" etiketli talep sayısı)
- **Veri Gizliliği İnsident Sayısı** = ilgili hafta içinde Seviye 3 (Hukuk) eskalasyonuna düşen ve gizlilik şüphesi kategorisiyle etiketlenen vaka sayısının toplamı
- **Çift Yanıt Oranı** = (birden fazla kanaldan eşleşen talep sayısı) / (toplam benzersiz kullanıcı-konu sayısı)
- **Kanal Bazlı Eskalasyon Oranı** = (kanal başına eskale edilen talep sayısı) / (o kanaldan gelen toplam talep sayısı), seviye kırılımıyla birlikte raporlanır
- **Ortalama İnsan Onay Süresi** = toplam (onay zamanı − eskalasyon zamanı) / eskale edilen talep sayısı

## 5. Eşik Değerler ve Alarm Koşulları

| Metrik | Eşik | Alarm Koşulu |
|---|---|---|
| Yanlış "Çözüldü" Oranı | %2 | Eşik aşılırsa Güvenilirlik Ekibine bildirim gider |
| Veri Gizliliği İnsident Sayısı | 0 | Herhangi bir insident oluşması doğrudan Hukuk Ekibine bildirim gerektirir |
| Çift Yanıt Oranı | %5 | Eşik aşılırsa kanal eşleştirme mantığı gözden geçirilir |
| Ortalama İnsan Onay Süresi | 4 saat | Eşik aşılırsa operasyon kapasitesi değerlendirilir |


## 6. Rapor Sahipliği ve Dağıtımı

| Rol | Sorumluluk |
|---|---|
| Güvenilirlik Ekibi | Raporu hazırlar, eşik aşımlarını tespit eder |
| Ürün Ekibi | Kullanıcı deneyimine yönelik metrikleri (çift yanıt, onay süresi) değerlendirir |
| Hukuk Ekibi | Veri gizliliği insidentlerini inceler |
| Destek/Operasyon Ekibi | Eskalasyon oranı ve onay sürelerine göre kapasite planlar |

Rapor, ilgili tüm paydaşlara e-posta ile dağıtılır; eşik aşımı olan metrikler ayrıca ilgili ekibe doğrudan bildirim olarak iletilir.

## 7. Varsayımlar

- Memnuniyet puanı, talebin kapanmasından sonraki 48 saat içinde büyük ölçüde toplanabilmektedir.
- Eskalasyon zamanı ve onay zamanı, sistemde otomatik olarak zaman damgasıyla loglanmaktadır.
- Bu belgedeki eşik değerleri örnek/varsayımsal niteliktedir, gerçek üretim ortamında ekiplerle birlikte kalibre edilmesi gerekir.