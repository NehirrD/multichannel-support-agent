# 07 — Meta Loglama Alanları

## Amaç

Bu doküman, çok kanallı destek ajanının güvenlik, denetlenebilirlik ve performans analizini desteklemek amacıyla tutulması gereken temel meta log alanlarını tanımlar.

Meta loglar; olay incelemeleri, güvenlik analizleri, performans ölçümü ve hata ayıklama süreçlerinde kritik rol oynar. Hassas kullanıcı verileri doğrudan kaydedilmez; yalnızca güvenli ve anonimleştirilmiş bilgiler saklanır.

---

## Zorunlu Meta Log Alanları

| Alan | Açıklama | Neden Zorunlu? |
|------|----------|----------------|
| **channel_id** | Talebin geldiği kanal (Slack, Web Form, E-posta vb.) | Kanal bazlı analiz, olay takibi ve kanal davranışlarının karşılaştırılması için gereklidir. |
| **user_id_hash** | Kullanıcının anonimleştirilmiş kimliği | Aynı kullanıcıya ait olayların takip edilmesini sağlar. Kişisel veriyi ifşa etmeden denetlenebilirlik sunar. |
| **model_version** | Yanıtı üreten LLM sürümü | Hataların hangi model sürümünde oluştuğunu belirlemek ve model güncellemelerini değerlendirmek için gereklidir. |

---

## Destekleyici Meta Alanları

Aşağıdaki alanlar zorunlu olmamakla birlikte güvenlik ve operasyon açısından önerilmektedir.

| Alan | Amaç |
|------|------|
| prompt_change_id | Prompt değişikliklerinin hangi sürümde yapıldığını izlemek |
| tool_call_status | Araç çağrılarının başarılı veya başarısız olduğunu kaydetmek |
| escalation_status | Talebin insan desteğine yönlendirilip yönlendirilmediğini göstermek |
| risk_level | Düşük, Orta, Yüksek risk sınıflandırması |
| timestamp | Olayın gerçekleştiği tarih ve saat bilgisi |

---

## Red Team Tatbikatı ile İlişkisi

06 numaralı Red Team tatbikatında gerçekleştirilen API anahtarı isteme senaryosunda aşağıdaki alanlar kritik önem taşımaktadır.

### channel_id

- Talebin hangi kanaldan geldiğini belirler.
- Riskli davranışların kanal bazında analiz edilmesini sağlar.

### user_id_hash

- Aynı kullanıcının tekrar eden saldırı girişimlerini tespit etmeye yardımcı olur.
- Kişisel veri saklanmadan olay geçmişi oluşturulabilir.

### model_version

- Güvenlik ihlalinin hangi model sürümünde gerçekleştiği belirlenebilir.
- Model güncellemelerinin güvenlik üzerindeki etkisi ölçülebilir.

---

## Tehdit Modeli ile İlişkisi

| Tehdit | Kullanılan Meta Alan |
|--------|----------------------|
| Prompt Enjeksiyonu | model_version, prompt_change_id |
| Araç Yanlış Kullanımı | tool_call_status |
| Hallucination | model_version |
| Gizli Bilgi Sızdırma | channel_id, user_id_hash |

Bu meta alanları sayesinde güvenlik olayları daha hızlı tespit edilir ve kök neden analizi yapılabilir.

---

## Gizlilik İlkeleri

Meta loglarda aşağıdaki bilgiler **kesinlikle saklanmaz**:

- API anahtarları
- Şifreler
- Access Token'lar
- Kredi kartı bilgileri
- Kimlik numaraları
- Ham kişisel veriler

Bunun yerine yalnızca anonimleştirilmiş kimlikler ve sistem olay kayıtları tutulur.

---

## Meta Log Örneği

```json
{
  "timestamp": "2026-07-06T14:20:31Z",
  "channel_id": "slack",
  "user_id_hash": "4d72c19e...",
  "model_version": "GPT-5.5",
  "tool_call_status": "blocked",
  "risk_level": "High",
  "escalation_status": "Security Team"
}
```

---

## Sonuç

Belirlenen meta log alanları sayesinde sistem;

- Güvenlik olaylarını izleyebilir,
- Red Team senaryolarını analiz edebilir,
- Model performansını değerlendirebilir,
- Kanal bazlı raporlama yapabilir,
- Kişisel verileri koruyarak denetlenebilirlik sağlayabilir.

Bu yapı, hem güvenlik hem de operasyonel sürdürülebilirlik açısından güçlü ve ölçeklenebilir bir loglama altyapısı sunmaktadır.