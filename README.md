# Machine Learning Projesi

Bu proje, Makine Öğrenmesi dersi kapsamında oluşturulmuş **Naive Bayes** ve **Logistic Regression** modellerini içermektedir. Proje, iki farklı makine öğrenmesi algoritmasının performansını karşılaştırmak ve uygulamalı olarak öğrenmek amacıyla hazırlanmıştır.

---


---

## 📚 Projede Kullanılan Yöntemler

### **1. Naive Bayes**
Naive Bayes algoritması, olasılık tabanlı bir sınıflandırma yöntemidir. 
Aşağıdaki işlemler yapılmıştır:
- Veri ön işleme ve eksik değer analizi
- Model eğitimi ve test süreci
- Doğruluk (accuracy), doğruluk matrisleri ve sınıflandırma raporu
- Modelin performansını değerlendirme

#### **Naive Bayes Avantajları:**
- Hızlı ve verimli çalışır.
- Yüksek boyutlu verilerde başarılıdır.
- Küçük veri setlerinde bile iyi performans gösterir.

---

### **2. Logistic Regression**
Logistic Regression, ikili sınıflandırma problemleri için yaygın olarak kullanılan bir algoritmadır. 
Aşağıdaki işlemler yapılmıştır:
- Modelin Scikit-learn ile eğitilmesi
- Elle yapılan Logistic Regression modelinin oluşturulması
- Doğruluk (accuracy), eğitim ve tahmin sürelerinin karşılaştırılması
- Model performansının görselleştirilmesi (cost reduction grafiği ve karmaşıklık matrisi)

#### **Logistic Regression Avantajları:**
- Lineer olarak ayrılabilen verilerde yüksek performans gösterir.
- Model interpretasyonu kolaydır.
- Sınıflandırma olasılıklarını tahmin edebilir.

---


---

## 🚀 Model Karşılaştırma

| Model                     | Doğruluk | Eğitim Süresi | Tahmin Süresi |
|--------------------------|---------|---------------|---------------|
| Scikit-learn Logistic    | %85     | 0.05 saniye    | 0.01 saniye    |
| Bayes Logistic           | %83     | 2.5 saniye     | 0.02 saniye    |
| Naive Bayes              | %80     | 0.01 saniye    | 0.01 saniye    |

### 💡 **Sonuç ve Değerlendirme**
- **Scikit-learn Logistic Regression**, doğruluk ve hız açısından en iyi performansı göstermektedir.
- **Elle yapılan Logistic Regression**, modelin mantığını anlamak için önemli bir deneyim sağlamaktadır.
- **Naive Bayes**, hızlı ve verimli çalışmasına rağmen bazı veri kümelerinde doğruluk açısından zayıf kalabilir.
- Daha karmaşık veri kümelerinde logistic regression tercih edilmelidir.

---




