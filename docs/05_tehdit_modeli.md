# Tehdit Modeli

## Doküman Bilgileri

| Alan | Değer |
|---|---|
| Doküman Adı | DOC-05 Tehdit Modeli |
| Proje | Akademi Care – Çok Kanallı Destek Ajanı Çerçevesi |
| Hazırlayan | Nehir Doğan |
| Tarih | 05.07.2026 |

## 1. Amaç

Bu belgenin amacı, destek ajanının maruz kalabileceği riskleri sadece DOC-01'de gözlemlenen iki olayla sınırlı tutmayıp, benzer yapısal zayıflıklardan doğabilecek daha geniş bir tehdit kümesi olarak sistematik şekilde ortaya koymaktır. Burada tanımlanan senaryolar, DOC-06'daki red team tatbikatının test edeceği vakaların ve `diagrams
/tehdit_tespit_akisi.md` diyagramının temelini oluşturur.

## 2. Tehdit Modelleme Yaklaşımı

Tehditler, güvenlik alanında yaygın kullanılan STRIDE yaklaşımının bu projeye uyarlanmış, basitleştirilmiş bir versiyonuyla sınıflandırılmıştır. Her tehdit; **hangi varlığı**, **hangi mekanizmayla** etkilediği ve **hangi kanal(lar)da** ortaya çıkabileceği belirtilerek tanımlanmıştır. Amaç, akademik bir güvenlik analizi değil, ajanın gerçek karar noktalarında nerede yanlış gidebileceğini somut biçimde listelemektir.

## 3. Varlıklar (Assets)

| Varlık | Açıklama |
|---|---|
| Kullanıcı Kimlik/Hesap Bilgisi | Ad, e-posta, üyelik durumu |
| Ticket/Talep Verisi | Talep içeriği, ticket numarası, geçmiş yazışmalar |
| Ödeme/Faturalandırma Bilgisi | Abonelik, iade, ödeme durumu |
| Kurs İlerleme Verisi | Kullanıcının eğitim içeriğindeki ilerlemesi |
| Kurumsal İtibar | Marka güveni, kullanıcı memnuniyeti algısı |
| Ajanın Karar Bütünlüğü | Ajanın ürettiği etiket/kararın doğruluğu ve tutarlılığı |

## 4. Tehdit Senaryoları

| # | Senaryo | Etkilenen Varlık | İlgili Kanal(lar) | DOC-01 Bağlantısı |
|---|---|---|---|---|
| T1 | Başka kullanıcıya ait ticket/hesap bilgisinin yanıtta görünmesi | Ticket Verisi, Kimlik Bilgisi | Slack, E-posta | Vaka 2 (doğrudan) |
| T2 | Düşük memnuniyete rağmen "çözüldü" etiketi atanması | Ajanın Karar Bütünlüğü | Tüm kanallar | Vaka 1 (doğrudan) |
| T3 | Aynı konunun birden fazla kanaldan çelişkili şekilde yanıtlanması | Kurumsal İtibar | Slack + E-posta + Web Formu | Dolaylı |
| T4 | Kullanıcının ajana yanıltıcı/manipülatif talimat içeren mesaj göndererek (prompt injection) ajanı normalde vermeyeceği bir bilgiyi vermeye yönlendirmesi | Ticket Verisi, Kimlik Bilgisi | Slack, E-posta | Yeni – doğrudan gözlemlenmedi |
| T5 | Ödeme/iade talebinin otomatik olarak yanlış sonuçlandırılması | Ödeme Bilgisi | Web Formu | Yeni |
| T6 | Kurs ilerleme verisinin yanlış kullanıcıya atfedilmesi | Kurs İlerleme Verisi | Web Formu, E-posta | Yeni – potansiyel sistemik risk |


## 5. Etki x Olasılık Matrisi

| Senaryo | Etki | Olasılık | Risk Seviyesi |
|---|---|---|---|
| T1 | Yüksek | Orta (bir kez gözlemlendi) | Yüksek |
| T2 | Orta | Orta (bir kez gözlemlendi) | Orta-Yüksek |
| T3 | Orta | Orta | Orta |
| T4 | Yüksek | Düşük (henüz gözlemlenmedi) | Orta |
| T5 | Yüksek | Düşük | Orta |
| T6 | Düşük | Düşük | Düşük |

## 6. Mevcut Kontroller

| Senaryo | İlgili Mevcut Kontrol                                                         |
|---|-------------------------------------------------------------------------------|
| T1 | DOC-02 "Veri gizliliği şüphesi" tetikleyicisi → Seviye 3 (Hukuk) eskalasyonu  |
| T2 | DOC-02 "Çelişkili sinyaller" tetikleyicisi → Seviye 2 eskalasyonu             |
| T3 | DOC-03 Bölüm 5 "Çift yanıt riski" — kullanıcı/konu eşleştirmesi               |
| T4 | Henüz doğrudan bir kontrol tanımlı değil — DOC-06'da test edilir.             |
| T5 | DOC-03 Bölüm 4 — ödeme/faturalandırma kategorisinde onay zorunluluğu          |
| T6 | Henüz doğrudan bir kontrol tanımlı değil — izleme kapsamına alınması önerilir |


## 7. Varsayımlar

- Tehdit senaryoları, ajanın mevcut mimarisi (tek orkestrasyon grafı, üç kanal) değişmediği sürece geçerlidir.
- T4-T6 gibi henüz gözlemlenmemiş senaryolar, benzer sistemlerde bilinen risk kalıplarına dayanılarak varsayımsal olarak eklenmiştir.
- Risk seviyeleri göreceli bir önceliklendirme aracıdır, kesin/ölçülmüş olasılık değerlerine dayanmamaktadır.