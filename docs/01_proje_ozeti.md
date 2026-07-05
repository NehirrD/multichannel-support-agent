# Proje Özeti

## Doküman Bilgileri

| Alan | Değer                                           |
|---|-------------------------------------------------|
| Doküman Adı | DOC-01 Proje Özeti                              |
| Proje | Akademi Care – Çok Kanallı Destek Ajanı Çerçevesi |
| Hazırlayan | Nehir Doğan                                     |
| Tarih | 05.07.2026                                      |

## 1. Amaç

Bu belgenin amacı, Akademi Care'in Slack topluluğu, e-posta ve web formu üzerinden yürüttüğü çok kanallı destek sürecinde görev alan otomatik yanıtlama ajanının mevcut çalışma biçimini tanımlamak, bu ajanın son dönemde neden olduğu iki olayın kök nedenini ortaya koymak ve ürün, hukuk ve güvenilirlik ekiplerinin talep ettiği çerçeve belgesinin (politika + eskalasyon + ölçüm) temelini oluşturmaktır.


## 2. Sistem Kapsamı

Akademi Care destek sistemi üç farklı kanaldan gelen kullanıcı taleplerini tek bir düzenleyici graf (orchestrator graph) üzerinde çalışan bir ajan aracılığıyla işlemektedir:

- **Slack Topluluğu** — kamuya açık, çok kullanıcılı bir kanal; mesajlar herkese görünür olabilir.
- **E-posta** — bire bir, yarı resmi iletişim kanalı.
- **Web Formu** — yapılandırılmış, kategori seçimi içeren talep kanalı.

Ajan, kanal fark etmeksizin gelen talebi okur, sınıflandırır, bir yanıt/aksiyon üretir ve gerektiğinde talebi "çözüldü" olarak etiketler. Aynı graf, farklı kanallardan gelen talepleri aynı bağlamda işlediği için kanallar arası veri karışması riski yapısal olarak mevcuttur.

## 3. Vaka Analizi

Geçtiğimiz hafta içinde, ajanın karar mekanizmasındaki zayıflıkları ortaya çıkaran iki olay yaşanmıştır:

| # | Olay | Gözlemlenen Sorun | Etki |
|---|---|---|---|
| 1 | Yanlış "çözüldü" etiketi | Müşteri düşük memnuniyet puanı verdiği halde ajan talebi "çözüldü" olarak işaretlemiştir | Metriklerin gerçek durumu yansıtmaması, memnuniyetsiz kullanıcının takipsiz kalması |
| 2 | Ticket numarası sızıntısı | Bir kullanıcıya, başka bir kullanıcıya ait özel/bağlantılı ticket numarası görünür hale gelmiştir | Kişisel veri ihlali riski, kullanıcı güveninde zedelenme, olası yasal sorumluluk |

Her iki olay da ajanın **kendi kararını doğrulama** ve **kanallar/kullanıcılar arası veri izolasyonu** konusunda yeterli kontrol mekanizmasına sahip olmadığını göstermektedir.

## 4. Problem Tanımı

Kök neden, ajanın hangi kararları otonom verebileceği ile hangi kararlarda insan onayına ihtiyaç duyduğu arasındaki sınırın net biçimde tanımlanmamış olmasıdır. Bunun sonucunda:

- Ajan, kendi başarısını (çözüm durumunu) dış bir doğrulama olmadan kendi kendine raporlayabilmektedir.
- Farklı kullanıcılara/kanallara ait bağlamlar, tek bir graf içinde yeterince izole edilmemektedir.
- Hatalı kararların ne sıklıkla oluştuğunu gösteren sistematik bir ölçüm/raporlama mekanizması bulunmamaktadır.

Bu problem, projenin geri kalan belgelerinde ele alınacak üç ana eksene karşılık gelmektedir: **politika** (hangi çıktı otomatik/hangisi onaylı), **eskalasyon** (ne zaman insana devredilir) ve **ölçüm** (bu süreç nasıl izlenir).

## 5. Beklentiler

| Paydaş | Beklentisi                                                                                     |
|---|------------------------------------------------------------------------------------------------|
| Ürün Ekibi | Kullanıcı deneyiminin kesintiye uğramadan, doğru şekilde otomatikleştirilmesi                  |
| Hukuk Ekibi | Kişisel veri sızıntısı riskinin ortadan kaldırılması, uyumluluk gerekliliklerinin karşılanması |
| Güvenilirlik (Reliability) Ekibi | Ajan kararlarının denetlenebilir, izlenebilir ve tekrarlanabilir olması                        |
| Destek/Operasyon Ekibi | Eskale edilen taleplerin net kriterlerle kendilerine ulaşması                                  |

## 6. Varsayımlar

- Sistem, kullanıcı talebini kanal fark etmeksizin aynı orkestrasyon grafında işlemektedir.
- "Özel bağlantılı ticket numarası" gibi tanımlayıcılar, kullanıcıya özgü hassas veri olarak kabul edilmektedir.
- Geçen haftaki iki olay, sistemin genelinde tekrarlanabilecek yapısal zayıflıkların örnekleri olarak ele alınmaktadır.
- Bu belgede yer alan senaryo örnek/varsayımsal niteliktedir, gerçek üretim verilerini temsil etmemektedir.