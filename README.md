# YÖKAK Paydaş Görüş Analiz Yardımcısı

YÖKAK taslak ölçüt setine gelen **paydaş görüşlerini** (Excel) konsolide edip
**indikatör düzeyinde** değerlendirmeyi sağlayan tek dosyalık web uygulaması.

Kurulum gerektirmez: [`index.html`](index.html) dosyasını bir tarayıcıda açmanız yeterli.

## Özellikler

- **İç ve dış paydaş** görüşlerini ayrı ayrı yükleme (sürükle-bırak). Her Excel dosyası
  tek bir paydaşın görüşünü içerir; **dosya adı paydaş etiketi** olarak kullanılır.
- **Değerlendirme ekranı:** sol ağaç navigasyonu (Ana ölçüt → Alt ölçüt → İndikatör),
  her indikatör için ayrı sayfa:
  - Mevcut (taslak) ifade ve beklenen kanıt örnekleri
  - **Paydaş görüşleri göstergesi:** karar dağılım çubuğu + hangi paydaşın hangi
    kararı verdiği (iç/dış etiketli), görüş kartları alt alta
  - **LLM değişiklik önerisi** (Anthropic Claude ile sentez → nihai ifadeye uygula)
  - **Nihai karar** paneli (değerlendiricinin kararı + gözden geçirilmiş ifade + not)
- **Genel gösterge:** KPI'lar, karar türü dağılımı, **Paydaş × Karar Türü matrisi**,
  Kabul dışı görüş içeren "dikkat gerektiren indikatörler" listesi.
- Veriler ve kararlar tarayıcıda (`localStorage`) saklanır.

## Karar türleri

Kabul · Revize · Birleştir · Ayrıştır · Çıkar · Eksik Alan

## Beklenen Excel yapısı

Sayfa **"Değerlendirme Ölçütleri"**, 7 sütun (hiyerarşik, forward-fill):

| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| Ana ölçüt | Alt ölçüt | Alt ölçüte ilişkin indikatör | Beklenen kanıt örnekleri | Karar | Gerekçe | Önerilen İfade |

- **A (Ana ölçüt)** ve **B (Alt ölçüt) + D (Kanıt)** yalnızca blok başında dolu; uygulama
  aşağıya doğru otomatik doldurur (forward-fill).
- **C (İndikatör)** her satırda bulunur; asıl değerlendirme birimidir.
- İndikatör kodu `altÖlçütKodu/sıra` biçiminde üretilir (ör. `2.4/2`).

## LLM kullanımı

LLM önerisi için uygulamadaki **Ayarlar**'dan bir Anthropic API anahtarı girilir.
Anahtar yalnızca tarayıcıda (`localStorage`) saklanır, hiçbir sunucuya gönderilmez;
çağrılar doğrudan `api.anthropic.com` adresine yapılır. Model seçilebilir
(varsayılan: Claude Sonnet 5).

## Fontlar (kurumsal yazı tipleri)

Uygulama **Camber** (birincil) ve **DIN Pro** (veri/etiket) kurumsal yazı tiplerini
kullanır. Bu fontlar ticari lisanslı olduğundan **repoya dahil edilmez**; yerelde
`fonts/` klasöründe bulunmaları beklenir:

```
fonts/CamberW04-Light.ttf   CamberW04-Regular.ttf   CamberW04-Medium.ttf   CamberW04-Bold.ttf
fonts/DINPro-Regular.otf    DINPro-Medium.otf       DINPro-Bold.otf
```

Fontlar yoksa uygulama otomatik olarak sistem yazı tipine (Segoe UI / system-ui) düşer;
işlevsellik etkilenmez, yalnızca tipografi değişir.

## Teknoloji

- Vanilla JavaScript, tek `index.html`
- [SheetJS](https://sheetjs.com) (Excel okuma, CDN)
- YÖKAK Design System renk/tipografi kuralları

## Tasarım

Üç PANTONE mavi (`#2b5597`, `#006eb7`, `#5eb3e4`), mavi gradient, Camber/DIN Pro
(sistem yazı tipi yedeği), hairline gri kenarlıklar, kurumsal ve resmi ton.
