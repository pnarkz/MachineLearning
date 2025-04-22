
# Matris Manipülasyonu ve Özdeğer–Özvektör Hesaplamaları

Bu doküman, makine öğrenmesi ve sayısal lineer cebirde sıkça kullanılan matris işlemleri ve özdeğer–özvektör kavramlarının NumPy ile nasıl uygulandığını özetlemektedir.

---

## 1. Kavram Tanımları

### 1.1 Matris Manipülasyonu

Matrisler, veri ve model parametrelerini lineer cebirsel olarak ifade etmemizi sağlar. Aşağıda temel matris işlemleri ve NumPy karşılıkları özetlenmiştir:

| **İşlem**         | **Matematiksel Tanım**            | **NumPy Örneği**          | **Kullanım Alanı**                                            |
|-------------------|-----------------------------------|---------------------------|---------------------------------------------------------------|
| Toplama           | \((A+B)_{ij}=A_{ij}+B_{ij}\)      | `C = A + B`               | İki ağırlık güncellemesini birleştirmek                       |
| Skaler Çarpma     | \((\alpha A)_{ij}=\alpha A_{ij}\) | `B = 0.1 * A`             | Öğrenme oranı uygulanması                                     |
| Matris Çarpımı    | \((AB)_{ij}=\sum_k A_{ik}B_{kj}\) | `C = A @ B`               | İleri beslemeli katmanda ağırlık–veri çarpımı                 |
| Transpoz          | \((A^T)_{ij}=A_{ji}\)             | `A_T = A.T`               | Kovaryans matrisinin \((X^T X)\) oluşturulması               |
| Determinant       | \(\det(A)\)                       | `np.linalg.det(A)`        | Matrisin tersinin var olup olmadığını kontrol etmek          |
| Ters Matris       | \(A^{-1}A=I\)                     | `A_inv = np.linalg.inv(A)`| Normal denklem çözümünde \((X^T X)^{-1}X^T y\) hesaplaması    |
| İz (Trace)        | \(\mathrm{tr}(A)=\sum_iA_{ii}\)   | `np.trace(A)`             | Toplam varyansı ölçen PCA ara adımlarında                    |
| Rütbe (Rank)      | \(\mathrm{rank}(A)\)              | `np.linalg.matrix_rank(A)`| Veri matrisinin tam dereceli olup olmadığını test etmek      |

**Ek Konular**  
- **Blok Matrisler**:  
  \(\begin{bmatrix}A & B\\C & D\end{bmatrix}\) yapıları, büyük modelleri modüler yapılandırmak için.  
- **Zaman/Karmaşıklık**:  
  Matris çarpımı genellikle \(O(n^3)\) karmaşıklığa sahiptir; BLAS/MKL gibi kütüphaneler pratikte önemli hız artışı sunar.

---

### 1.2 Özdeğer (\(\lambda\)) ve Özvektör (\(v\))

Bir kare \(A\in\mathbb{R}^{n\times n}\) matrisi için  
\[
A\,v = \lambda\,v,\quad v \neq 0
\]  
eşitliğini sağlayan skaler \(\lambda\) **özdeğer**, \(v\) ise **özvektör**dür.

#### Özdekompozisyon
\[
A = V\,\Lambda\,V^{-1},\quad
V=[v_1,\dots,v_n],\;
\Lambda=\mathrm{diag}(\lambda_1,\dots,\lambda_n)
\]

#### Simetrik Matrislerde Spektral Teorem
Eğer \(A = A^T\) ise  
\[
A = Q\,\Lambda\,Q^T,\quad Q^{-1}=Q^T
\]  
Özvektörler ortonormaldir.

#### Çarpanlar
- **Cebirsel Çarpan**: Özdeğerin tekrar sayısı.  
- **Geometrik Çarpan**: O özdeğere karşılık gelen bağımsız özvektör sayısı.

---

## 2. NumPy `linalg.eig` Fonksiyonu 

```python
def eig(a):
    a, wrap = _makearray(a)
    _assertRank2(a)
    t, result_t = _umath_linalg.eig(a, _compute_uv=False)
    if not t.iscomplexobj():
        t = t.real
    if not result_t.iscomplexobj():
        result_t = result_t.real
    return t, result_t
```

**Kodun Açıklaması:**
- `eig` fonksiyonu, matrisin özdeğerlerini ve özvektörlerini hesaplamak için `_umath_linalg.eig` fonksiyonunu çağırır.
- `_makearray(a)`: Girdi olan matrisin doğru tipte bir array haline getirilmesini sağlar.
- `_assertRank2(a)`: Matrisin 2 boyutlu olduğundan emin olunur.
- `_compute_uv=False`: Yalnızca özdeğerler döndürülür, özvektörler hesaplanmaz.
- `result_t` ve `t`: Hesaplanan özdeğerler ve özvektörler.

---

## 3. Özdeğer ve Özvektör Hesaplama Yöntemlerinin Karşılaştırılması

### Yöntem 1: NumPy ile Doğrudan Hesaplama

```python
import numpy as np

A = np.array([
    [ 4, -2,  1],
    [-2,  4, -2],
    [ 1, -2,  3]
])

eigvals_numpy, eigvecs_numpy = np.linalg.eig(A)

print("NumPy ile Özdeğerler:", eigvals_numpy)
print("NumPy ile Özvektörler:\n", eigvecs_numpy)
```

### Sonuçların Karşılaştırılması

| Metod               | Özdeğerler                     | Özvektörler                      |
|---------------------|--------------------------------|----------------------------------|
| NumPy `linalg.eig`  | [7.1190, 2.5684, 1.3126]        | Matrisi kolon vektörleri olarak |
| Polinom + SVD       | [7.1190, 2.5684, 1.3126]        | ± işaret farkı dışında aynı yön |

### Neden Aynı?

Her iki yöntem de aynı matematiksel temele dayanır:

- **Karakteristik Denklem:**  
  \[
  \det(A - \lambda I) = 0
  \]  
  denkleminden özdeğerler elde edilir.

- **Özvektör Alt Uzayı:**  
  \[
  (A - \lambda I)x = 0
  \]  
  denkleminden özvektör doğrultusu bulunur. \(v\) ve \(-v\) farkı geçerli ve doğaldır.

---
