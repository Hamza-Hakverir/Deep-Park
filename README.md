Model Uygulama ve Test Süreci (Hamza Hakverir)

Bu çalışmada, otopark doluluk tespiti probleminin çözümünde modelin ezberlemesini (overfitting) minimize etmek ve genelleme başarısını artırmak amacıyla Dropout (Seyreltme) mekanizması ile güçlendirilmiş özgün bir CNN mimarisi geliştirilmiştir.

Veri ön işleme aşamasında, hesaplama maliyetini düşürmek ve işlem hızını artırmak adına tüm giriş görüntüleri 64x64 piksel boyutuna indirgenmiş ve PyTorch ImageFolder yapısı ile sisteme dahil edilmiştir. Veri seti, modelin öğrenme performansını objektif bir şekilde ölçebilmek ve yanlılığı önlemek amacıyla rastgele yöntemle %80 eğitim ve %20 test kümesi olarak ayrıştırılmıştır.

Tasarlanan model mimarisi, öznitelik çıkarımı için kademeli olarak artan filtre sayılarına (16 ve 32) sahip iki adet konvolüsyon katmanı üzerine kurgulanmıştır. Boyut azaltma ve önemli özellikleri belirginleştirme işlemi için Max Pooling katmanları tercih edilmiştir. Bu mimariyi diğer temel modellerden ayıran en kritik özellik, tam bağlı (Fully Connected) katmandan hemen önce eklenen ve eğitim sırasında nöronların %50'sini rastgele pasif hale getiren Dropout (0.5) katmanıdır. Bu katman sayesinde modelin eğitim verisine aşırı uyum sağlamasının (overfitting) önüne geçilmesi ve test verisinde daha kararlı sonuçlar vermesi hedeflenmiştir.

Eğitim sürecinde optimizasyon algoritması olarak Adam (Learning Rate=0.001) tercih edilmiş, sınıflandırma hatasının hesaplanmasında ise CrossEntropyLoss fonksiyonu kullanılmıştır. Model toplam 3 epoch boyunca eğitilmiş, her iterasyonda kayıp (loss) ve doğruluk (accuracy) değerleri anlık olarak izlenmiş, son aşamada ise modelin daha önce hiç görmediği test veri seti üzerinde nihai performans ölçümü gerçekleştirilmiştir.
