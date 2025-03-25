# Logistic Regression Karşılaştırması

## 1. Problem Tanımı
Bu proje, lojistik regresyon yöntemi kullanarak ikili sınıflandırma problemini çözmeyi amaçlamaktadır. 
Bu proje kapsamında hem Scikit-learn kütüphanesi kullanılarak hem de manuel olarak oluşturulmuş bir lojistik regresyon modeli ile karşılaştırma yapılmıştır.
İki modelin de doğruluk (accuracy), eğitim süresi ve tahmin süresi gibi metrikleri analiz edilmiştir.

---

## 2. Logistic Regression Nedir?
Lojistik regresyon, bir bağımlı değişkenin (genellikle ikili) bir veya daha fazla bağımsız değişkene dayalı olarak tahmin edilmesi için kullanılan bir sınıflandırma algoritmasıdır. 
Matematiksel olarak, lojistik regresyon şu formüle dayanır:

### **Sigmoid Fonksiyonu**
Sigmoid fonksiyonu, lojistik regresyonun temel fonksiyonudur ve aşağıdaki gibi tanımlanır:

\[
\sigma(z) = \frac{1}{1 + e^{-z}}
\]

Bu fonksiyonun çıktısı 0 ile 1 arasında bir değer alır. Bu sayede sınıflandırma yapılırken bir olasılık değeri elde edilir.

---

## 3. Kullanılan Yöntemler ve Fonksiyonlar

### a) Scikit-learn Logistic Regression
Scikit-learn kütüphanesi ile lojistik regresyon modelini hızlı ve optimize bir şekilde oluşturduk.
Aşağıdaki adımları uyguladık:
1. Model Eğitimi: `LogisticRegression()` sınıfı kullanıldı.
2. Model Tahmini: `predict()` fonksiyonu ile çıktı alındı.
3. Model Değerlendirme: `confusion_matrix` ve `classification_report` fonksiyonları ile performans metrikleri elde edildi.

---

### b) Bayes Logistic Regression
Bayes lojistik regresyon modeli oluşturulurken aşağıdaki fonksiyonlar kullanıldı:

#### **1. Sigmoid Fonksiyonu**
Sigmoid fonksiyonu, model çıktısının olasılık değeri olarak yorumlanabilmesi için kullanılır.


#### def sigmoid(z):
    return 1 / (1 + np.exp(-z))

# Veri Seti
Kullanılan veri seti: Heart Disease Dataset

Veri kaynağı: Kaggle

Toplam örnek sayısı: 1025

Özellik sayısı: 13

Eksik veri: Bulunmamaktadır

Hedef değişken: target (0: Sağlıklı, 1: Hasta)

# Sonuçlar ve Karşılaştırma
| Model                    | Doğruluk | Eğitim Süresi | Tahmin Süresi |
|--------------------------|---------|---------------|---------------|
| Scikit-learn Logistic    | %85     | 0.05 saniye    | 0.01 saniye    |
| Bayes Logistic           | %83     | 2.5 saniye     | 0.02 saniye    |

### Yorum ve Değerlendirme
- **Scikit-learn modeli**, hem doğruluk hem de eğitim süresi açısından daha iyi performans göstermektedir.
- **Bayes lojistik regresyon modeli**, algoritmanın çalışma mantığını anlamak açısından faydalıdır, ancak hız ve doğruluk açısından Scikit-learn modeline göre daha zayıf kalmaktadır.
- Daha büyük veri setlerinde ve daha karmaşık özelliklerle çalışıldığında Scikit-learn'ün sağladığı performans avantajı daha belirgin hale gelmektedir.
- Lojistik regresyon modelleri, sınıflandırma problemlerinde hız ve doğruluğu dengeleyerek etkili sonuçlar verebilmektedir.


