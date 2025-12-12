# 🚀 Power BI ile "The Look" E-Ticaret Veri Analizi ve İş İçgörüleri

![Uploading Ekran görüntüsü 2025-12-13 001059.png…]()


Bu proje, kurgusal bir giyim e-ticaret perakendecisi olan **"The Look"** şirketinin kapsamlı operasyonel verilerini analiz etmek ve bu verilerden iş kararlarını yönlendirecek uygulanabilir içgörüler çıkarmak amacıyla **Microsoft Power BI** kullanılarak geliştirilmiştir.

## 🎯 Proje Özeti ve Amacı

Analiz, şirketin satış performansı, müşteri davranışları ve envanter verimliliği üzerine odaklanmaktadır.

| Kriter | Detay |
| :--- | :--- |
| **Analiz Alanı** | E-Ticaret, Satış, Lojistik, Müşteri İlişkileri |
| **Kullanılan Araçlar** | Power BI Desktop, DAX, BigQuery (Veri Kaynağı) |
| **Veri Seti** | The Look E-ticaret Veri Seti (Google BigQuery Public Data) |
| **Temel Amaç** | Satış ve envanter KPI'larını görselleştirmek, performans düşüş/artış nedenlerini belirlemek. |

---

## 📂 Veri Seti ve Model Yapısı

Projede kullanılan veri seti, siparişler, envanter, kullanıcılar, ürünler ve olaylar gibi temel e-ticaret süreçlerini kapsayan 7 ana tablodan oluşmaktadır.

### 🗄️ Veri Modeli İlişkileri

Verilerin etkin analizi için Power BI'da bir Yıldız Şeması (Star Schema) yapısına uygun ilişkiler kurulmuştur.

| Tablo Adı | İçerik | Anahtar Alanlar (Örnek) |
| :--- | :--- | :--- |
| `siparişler` | Müşteri sipariş kayıtları | `sipariş_id`, `kullanıcı_id` |
| `sipariş_öğeleri` | Sipariş edilen ürünler ve durumları | `sipariş_id`, `envanter_öğesi_id` |
| `envanter_öğeleri` | Stok ve satışa ait maliyet/durum bilgileri | `ürün_id`, `maliyet`, `ürün_kategorisi` |
| `ürünler` | Ürün ana bilgileri | `id`, `kategori`, `marka`, `perakende_fiyatı` |
| `kullanıcılar` | Müşteri demografik bilgileri | `id`, `yaş`, `ülke` |
| `olaylar` | Web sitesi etkileşimleri | `kullanıcı_id`, `oturum_id` |

*(Not: Projenizin tam veri modelini (ERD) bu bölüme bir görsel olarak eklemeniz (örneğin `erd_diagram.png`) dökümantasyonunuzu daha etkili hale getirecektir.)*

---

## 📈 Anahtar Performans Göstergeleri (KPI'lar)

Analiz panosunda kritik iş sorularını yanıtlamak için DAX (Data Analysis Expressions) dili kullanılarak hesaplanan temel metrikler ve sonuçları:

| KPI | Hesaplama Amacı | Örnek DAX Formülü (Özet) | Sonuç (Panodan) |
| :--- | :--- | :--- | :--- |
| **Toplam Satış Geliri** | Toplam hasılat | `SUM('order_items'[sale_price])` | **$10.83 M** |
| **Sipariş Sayısı** | Tamamlanan toplam sipariş adedi | `DISTINCTCOUNT('orders'[order_id])` | **182 K** |
| **Ortalama Sipariş Tutarı (AOV)** | Müşteri başına ortalama işlem değeri | `[Total Sales] / [Order Count]` | **$86.62** |
| **İade Oranı (%)** | İade/İptal edilen ürünlerin yüzdesi | `COUNTROWS(iade_edilenler) / COUNTROWS(tüm_öğeler)` | **10.01 %** |
| **Ortalama Teslim Süresi** | Siparişten teslimata ortalama geçen gün | `AVERAGE('orders'[delivery_date] - 'orders'[created_at])` | **2.51 gün** |

---

## 📊 Dashboard Görselleştirmeleri ve Temel İçgörüler

Power BI panosu, kullanıcıların tarih, bölge ve ürün kategorisine göre dinamik olarak filtreleme yapabileceği etkileşimli grafikler içermektedir.

### 1. Gelir Trendleri
* **İçgörü:** Yıllık gelir performansı 2023'te zirve yapmıştır. 2024 verileri (kısmi yıl) bir düşüş eğilimi göstererek, ilgili dönem için pazarlama ve stok stratejilerinin gözden geçirilmesi gerektiğini işaret etmektedir.
* **Aylık Trend:** Yıllar itibarıyla genel bir satış artışı eğilimi gözlenirken, özellikle Eylül'den itibaren başlayan mevsimsel yükselişler net bir şekilde görülmektedir.

### 2. Ürün ve Envanter Verimliliği
* **Adet Bazında En Popüler Kategori:** **"Intimates" (İç Giyim)** kategorisi en yüksek adetli satışa sahiptir (13K).
* **Gelir Bazında En Yüksek Katkı:** **Jeans ($1.75M)** ve **Outerwear & Coats ($1.3M)** kategorileri, adet bazında ilk sırada olmamalarına rağmen yüksek ortalama fiyatları sayesinde en büyük gelir katkısını sağlamaktadır.

### 3. Müşteri ve Lojistik Performansı
* **İptal Oranı (%14.86) ve İade Oranı (%10.01):** Bu oranlar, e-ticaret için kabul edilebilir sınırlar içinde olmakla birlikte, maliyetleri düşürmek amacıyla bu oranlara neden olan temel faktörlerin (ürün kalitesi, beden tutarsızlığı, lojistik gecikmeleri) araştırılması gerekmektedir.

---

## 💡 Uygulanabilir İş Önerileri (Aksiyon Planı)

Elde edilen analiz sonuçlarına dayanarak, The Look şirketine aşağıdaki aksiyon odaklı öneriler sunulmuştur:

1.  **Yüksek Değerli Ürün Stok Yönetimi:** Yüksek gelir getiren **Jeans** ve **Outerwear & Coats** gibi ürünlerde stok tükenmesini önlemek için talep tahminleme modelleri (Time Series Forecasting) kullanılmalıdır.
2.  **İade/İptal Azaltma Stratejisi:** İade oranı yüksek olan spesifik ürün alt kategorileri belirlenerek, bu ürünler için ürün sayfalarında daha detaylı beden rehberleri ve 3D görseller sunulmalıdır.
3.  **Lojistik Optimizasyonu:** Ortalama teslim süresi **2.51 gün** seviyesindedir. Müşteri memnuniyetini artırmak ve operasyonel maliyetleri düşürmek için siparişin coğrafi konumu ile en yakın dağıtım merkezi arasındaki rotalar analiz edilerek dağıtım verimliliği artırılmalıdır.

---


