# python-proje2
Projenin Amacı
Bu projenin amacı, Münih şehrine ait günlük yağış ve kar yağışı verilerini işleyerek bu verilerdeki mevsimsel kalıpları, uzun vadeli trendleri ve aykırı hava olaylarını (aşırı yağışları) istatistiksel ve görsel yöntemlerle incelemektir.

1. Aşama: Veri Yükleme ve Hazırlık
Bu aşama, ham verilerin analiz edilmeye hazır, temiz ve standart bir zaman serisi formatına getirilmesini sağlar.

Veri Setinin Yüklenmesi: Belirtilen yoldaki (munich.csv) dosyası yüklendi. Dosyadaki veriler, yaygın kullanılan virgül (,) yerine noktalı virgül (;) ile ayrıldığı için, Pandas bu ayracı kullanarak veriyi doğru sütunlara ayırdı.

Sütun Tanımlaması: Analiz edilecek ana veri sütunları 'time' (tarih), 'precipitation_sum (mm)' (yağış) ve 'snowfall_sum (cm)' (kar yağışı) olarak tanımlandı.

Zaman Serisi Dönüşümü: Tarih bilgisi içeren 'time' sütunu, metin formatından zaman serisi analizleri için gerekli olan datetime (tarih-saat) formatına dönüştürüldü.

İndeksleme ve Temizleme: Dönüştürülen 'time' sütunu, veri tablosunun ana indeksi olarak belirlendi. Geçersiz veya eksik tarih bilgisine sahip tüm satırlar tablodan çıkarıldı.

Eksik Veri Doldurma (Imputation): Yağış ve kar yağışı sütunlarında boş (NaN) değerler olup olmadığı kontrol edildi. Bulunan eksik değerler, o sütunun medyan (ortanca) değeri kullanılarak dolduruldu. Bu işlem, eksik verilerin sonraki matematiksel hesaplamaları bozmasını engelledi.

2. Aşama: Keşifsel Veri Analizi (EDA)
Verinin genel yapısını ve matematiksel eğilimlerini ortaya çıkarmak için temel hesaplamalar yapıldı.

Betimleyici İstatistikler: Yağış ve kar yağışı verileri için ortalama, en yüksek, en düşük, standart sapma gibi özet istatistikler hesaplanarak verinin genel dağılımı hakkında bilgi edinildi.

Yıllık Trend Analizi:

Günlük yağış verileri, yıllara göre gruplandırılarak her yılın toplam yağış miktarı hesaplandı.

Bu yıllık toplamlar üzerinden NumPy kullanılarak doğrusal bir trend çizgisi hesaplandı. Elde edilen eğim değeri (slope), yıllık toplam yağışın incelenen dönemde genel olarak artış mı yoksa azalış mı gösterdiğini belirledi.

Mevsimsel Kalıp Analizi:

Tüm dönemdeki günlük veriler aylara göre gruplandırılarak her bir ayın (Ocak, Şubat, vb.) ortalama yağış miktarı hesaplandı. Bu, Münih'in mevsimsel yağış döngüsünü ortaya çıkardı.

3. Aşama: Veri Görselleştirme
Analiz bulguları, anlaşılırlığı artırmak için grafiklere dönüştürüldü.

Zaman Serisi Grafiği (Günlük Yağış ve Trend):

Tüm dönem boyunca günlük yağış miktarını gösteren bir çizgi grafik oluşturuldu.
<img width="1282" height="600" alt="yzt gorsel2" src="https://github.com/user-attachments/assets/53db8951-18fb-4f0e-b392-9ab885dd4c22" />

Grafiğin üzerine, günlük dalgalanmaları yumuşatarak uzun vadeli eğilimi daha belirgin hale getiren 365 günlük hareketli ortalama çizgisi eklendi.

Mevsimsel Kalıp Grafiği (Aylık Ortalama):

Aylık ortalama yağış miktarları bir sütun grafik (Bar Plot) ile gösterildi. Bu, hangi ayların ortalama olarak en yağışlı olduğunu kolayca karşılaştırmayı sağladı.

Aykırı Olay Tespiti (Box Plot):

Her bir yılın günlük yağış verilerinin dağılımını gösteren kutu grafikleri oluşturuldu.

Bu grafikler, verinin ortalama ve dağılımını gösterirken, özellikle aşırı yağışlı günlerin (aykırı değerler) hangi yıllarda daha yoğun olduğunu görsel olarak tespit etmeye yardımcı oldu. (Ancak bu grafikte verinin aşırı yayılmasını önlemek için aykırı değerler gösterilmedi.)

4. Aşama: Raporlama ve Özet Bulgular
Tüm analiz ve görselleştirme adımları özetlenerek nihai bir rapor oluşturuldu.

Aykırı Olayların Tanımlanması: İstatistiksel olarak nadir kabul edilen "aşırı yağış" eşiği (ortalama + 3 standart sapma) hesaplandı.

Sonuçların Raporlanması: Kod, elde edilen tüm bulguları aşağıdaki gibi özetledi:

İncelenen toplam zaman aralığı.

Yıllık toplam yağıştaki eğilim (artış/azalış) değeri.

En yağışlı ay ve bu aya ait ortalama yağış miktarı.

Dönemin kayda geçen en yüksek tek günlük yağış miktarı ve bu olayın tarihi.

Tanımlanan istatistiksel eşiği aşan aşırı yağışlı gün sayısı.
