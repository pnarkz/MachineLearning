# ForwardAndBackwardPropagation

Bu depo, ileri ve geri yayılım algoritmalarını sıfırdan (vanilla) yazdığınız bir sinir ağı modelini adım adım çalıştıran bir Jupyter Notebook içerir.

## İçerik

* **ForwardAndBackwardPropagation.ipynb**:

  * Veri yükleme ve ön işleme
  * İleri yayılım (forward propagation)
  * Geri yayılım (backpropagation)
  * Eğitim döngüsü (batch-based gradient descent)
  * Eğitim kaybı ve doğruluk eğrilerinin görselleştirilmesi
  * Test verisi üzerinde doğruluk, sınıflandırma raporu ve karışıklık matrisi

## Başlarken

1. Repoyu klonlayın:

   ```bash
   git clone https://github.com/<kullanici_adiniz>/ForwardAndBackwardPropagation.git
   cd ForwardAndBackwardPropagation
   ```

2. Gerekli Python paketlerini yükleyin:

   ```bash
   pip install numpy pandas matplotlib seaborn scikit-learn jupyter
   ```

3. Jupyter Notebook'u başlatın:

   ```bash
   jupyter notebook ForwardAndBackwardPropagation.ipynb
   ```

## Notebook Kullanımı

* `file_path` değişkenine veri dosyanızın tam yolunu girin. Örnek:

  ```python
  file_path = r"C:\Users\<KULLANICI>\data\iris.csv"  # Windows
  # veya
  file_path = "/home/<kullanici>/data/iris.csv"       # Linux/Mac
  ```

* Hücreleri sırasıyla çalıştırarak modelinizi eğitin ve sonuçları inceleyin.

## Çıktılar ve Analiz

* **Eğitim Kaybı Eğrisi**: Modelin her epoch sonunda ne kadar kayıp yaşadığını gösterir.
* **Doğruluk Eğrisi**: Doğrulama veri seti üzerindeki doğruluğu izler.
* **Classification Report**: Precision, recall ve F1-score değerleri.
* **Confusion Matrix**: Gerçek ve tahmin edilen sınıfların karşılaştırması.

Notebook içindeki açıklamalar ve grafikler üzerinden model performansınızı analiz edebilirsiniz.


---


