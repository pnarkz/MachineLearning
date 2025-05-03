##  Model Karşılaştırması ve Yöntem Açıklaması

Bu projede aynı “Hours → Scores” veri seti üzerinde iki farklı yaklaşım denendi:

**Model 1: Manuel Least Squares (Analitik OLS)**  
- **Yöntem:** En küçük kareler (Ordinary Least Squares) formüllerini doğrudan uygular.  
  - Eğim (\(m\)) ve kesim (\(c\)) aşağıdaki kapalı formüllerle hesaplandı:
    \[
      m = \frac{\sum (x_i - \bar x)(y_i - \bar y)}{\sum (x_i - \bar x)^2}
      \quad,\quad
      c = \bar y - m\,\bar x
    \]
- **Avantajı:** Basit ve kesin çözüm verir, iterasyonsuzdur, küçük veri setleri için hızlıdır.  
- **Dezavantajı:** Çok sayıda veya yüksek boyutlu özellik olduğunda kapalı formül hesaplaması **\(O(n^3)\)** matris tersine çevriminden dolayı maliyetli olabilir.  

**Model 2: scikit-learn LinearRegression**  
- **Yöntem:** scikit-learn kütüphanesinin LinearRegression sınıfı, tek değişkenli durumda en küçük kareler denklemlerini alt planda yine **analitik (normal equation)** yöntemiyle çözer.  
- **Neden scikit-learn?**  
  - **Kullanım Kolaylığı:** Tek satırda model oluşturma, eğitim ve tahmin imkânı.  
  - **Performans:** BLAS/LAPACK gibi optimize matris kütüphanelerini kullanarak analitik hesaplamayı hızlandırır.  
  - **Güvenilirlik:** Dünyaca kabul görmüş, geniş testlerden geçmiş bir kütüphane; üretime hemen hazır.  
  - **Esneklik:** İleride çoklu değişken (multivariate) veya regularizasyon (Ridge, Lasso) eklemek istediğinizde aynı API’yi kullanabilirsiniz.  

| Yöntem                            | Eğim (m) | Kesim (c) | MSE     |
|-----------------------------------|----------|-----------|---------|
| Manuel Least Squares (OLS)        | 1.8942   | 36.6781   | 11.583  |
| scikit-learn `LinearRegression`   | 1.8942   | 36.6781   | 11.583  |
| Fark (Δ MSE)                      | —        | —         |  0.000  |

### Açıklama ve Sonuç  
- Her iki yöntem de aslında **aynı matematiksel temele** dayanıyor: “ortalama kare hatayı” minimize eden analitik kapalı formül.  
- scikit-learn, bu kapalı formülü kendi içinde optimize edilmiş matris işlemleriyle (normal denklemler) hesapladığı için sonuçlar _tamamen_ aynı çıktı.  
- Bu basit tek öz nitelikli (univariate) problemde her iki yöntemin performansı eşit; ancak pratikte scikit-learn’ün sunduğu kullanım kolaylığı ve geniş ekosistemi projeyi daha sürdürülebilir kılar.  

