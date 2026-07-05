# Tehdit Tespit Akışı

> Bu şema, `docs/05_tehdit_modeli.md` içeriğindeki tehdit senaryolarının (T1-T6) ajan tarafından nasıl tespit edildiğini gösterir. Tespit edilen tehdit, DOC-02'deki eskalasyon akışına devredilir.

```mermaid
flowchart TD
    A[Talep / Ajan Yanıtı Üretilmeden Önce] --> B[Veri İzolasyon Kontrolü<br/>Başka kullanıcıya ait bilgi var mı?]
    B -->|Evet| T1[T1: Veri Sızıntısı Riski]
    B -->|Hayır| C[Kullanıcı-Konu Eşleştirme Kontrolü<br/>Aynı konu başka kanalda açık mı?]
    C -->|Evet| T3[T3: Çift Yanıt Riski]
    C -->|Hayır| D[Memnuniyet-Etiket Tutarlılık Kontrolü<br/>'Çözüldü' etiketi memnuniyetle çelişiyor mu?]
    D -->|Evet| T2[T2: Yanlış Otomasyon Riski]
    D -->|Hayır| E[Talimat Manipülasyonu Kontrolü<br/>Mesaj ajanı yönlendirmeye mi çalışıyor?]
    E -->|Evet| T4[T4: Prompt Injection Riski]
    E -->|Hayır| F[Kategori Hassasiyet Kontrolü<br/>Ödeme / kurs ilerleme verisi mi?]
    F -->|Evet| T5G[T5/T6: Hassas Veri İşlem Riski]
    F -->|Hayır| G[Tehdit Tespit Edilmedi]

    T1 --> H[DOC-02 Eskalasyon Akışına Yönlendir<br/>Seviye 3 - Hukuk]
    T2 --> I[DOC-02 Eskalasyon Akışına Yönlendir<br/>Seviye 2 - Operasyon]
    T3 --> J[DOC-02 Eskalasyon Akışına Yönlendir<br/>Seviye 1 - Destek Uzmanı]
    T4 --> K[DOC-02 Eskalasyon Akışına Yönlendir<br/>Seviye 4 - Güvenilirlik]
    T5G --> L[DOC-02 Eskalasyon Akışına Yönlendir<br/>Seviye 2/3]
    G --> M[Ajan Otomatik Yanıt Üretebilir]
```

## Kontrol - Senaryo Eşleşmesi

| Kontrol Adımı | İlgili Tehdit Senaryosu | Mevcut Kontrol Durumu |
|---|---|---|
| Veri İzolasyon Kontrolü | T1 | Tanımlı (DOC-02, DOC-03) |
| Kullanıcı-Konu Eşleştirme | T3 | Tanımlı (DOC-03) |
| Memnuniyet-Etiket Tutarlılığı | T2 | Tanımlı (DOC-02) |
| Talimat Manipülasyonu Kontrolü | T4 | **Tanımlı değil** – DOC-06'da öncelikli test |
| Kategori Hassasiyet Kontrolü | T5, T6 | Kısmen tanımlı (T5 için DOC-03, T6 için **tanımlı değil**) |