# Eskalasyon Akışı

> Bu şema, `docs/02_eskalasyon_tetikleyicileri.md` (Bölüm 5 – Karar Akışı) içeriğinin görsel karşılığıdır.

```mermaid
flowchart TD
    A[Talep Alınır<br/>Slack / E-posta / Web Formu] --> B[Sınıflandırma ve<br/>Güven Skoru Hesaplama]
    B --> C{Tetikleyici Kategorisi<br/>Var mı?}
    C -->|Hayır| D[Otomatik Yanıt Üretilir]
    D --> E[Talep Kapatılır - Ajan<br/>'Çözüldü' Etiketi]
    C -->|Evet| F[İlgili Eskalasyon<br/>Seviyesine Yönlendirilir]
    F --> G[İnsan Değerlendirmesi / Onayı]
    G --> H{Onaylandı mı?}
    H -->|Evet| I[Talep Kapatılır - İnsan]
    H -->|Hayır / Revize| B
```

## Tetikleyici Kategorileri

- Çelişkili sinyaller
- Veri gizliliği şüphesi
- Çift yanıt riski
- Düşük güven skoru
- Hassas/hukuki içerik

## Eskalasyon Seviyeleri

| Seviye | Sorumlu |
|---|---|
| Seviye 1 | Destek Uzmanı (Tier 1) |
| Seviye 2 | Kıdemli Destek / Operasyon Sorumlusu |
| Seviye 3 | Hukuk Ekibi |
| Seviye 4 | Güvenilirlik (Reliability) Ekibi |