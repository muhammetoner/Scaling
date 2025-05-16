

#  Özellik Ölçekleme (Feature Scaling)

##  Özellik Ölçekleme Nedir?

Makine öğrenmesinde bazı algoritmalar verilerdeki **sayıların büyüklüğünden etkilenir**.  
Bu yüzden özelliklerin (değişkenlerin) aynı ölçek aralığında olması gerekir.  
Bu işleme **özellik ölçekleme** (feature scaling) denir.

---

##  Neden Gerekli?

Örnek:  
- `Yaş` değişkeni: 20–60  
- `Gelir` değişkeni: 10.000–100.000

Eğer bu veriler ölçeklenmezse, algoritma `gelir` değişkenine çok fazla önem verir.  
Bu da modeli **yanıltır**.

Özellik ölçekleme sayesinde her değişkenin modele katkısı **dengelenir**.

---

##  Nasıl Yapılır?

### 1. StandardScaler (Z-Score Standardizasyonu)

Verileri ortalama 0 ve standart sapma 1 olacak şekilde dönüştürür.

**Formül:**

```
z = (x - ortalama) / standart sapma
```

**Python Örneği:**

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

---

### 2. MinMaxScaler

Verileri 0 ile 1 arasına sıkıştırır.

**Formül:**

```
x_scaled = (x - min) / (max - min)
```

**Python Örneği:**

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
X_scaled = scaler.fit_transform(X)
```

---

### 3. RobustScaler

- Aykırı değerlere karşı dayanıklıdır  
- Ortalamadan değil **medyan** ve **IQR** (çeyrekler arası açıklık) kullanır

**Python Örneği:**

```python
from sklearn.preprocessing import RobustScaler

scaler = RobustScaler()
X_scaled = scaler.fit_transform(X)
```

---

### 4. MaxAbsScaler

Sadece **maksimum mutlak değere göre** ölçekler.  
Negatif değerli ve sparse (seyrek) veriler için idealdir.

**Python Örneği:**

```python
from sklearn.preprocessing import MaxAbsScaler

scaler = MaxAbsScaler()
X_scaled = scaler.fit_transform(X)
```

---

## Hangi Yöntemi Ne Zaman Kullanmalı?

| Durum | Uygun Yöntem |
|-------|---------------|
| Veride aykırı değer yoksa | StandardScaler, MinMaxScaler |
| Aykırı değer varsa | RobustScaler |
| Sparse veya negatif değerli veri | MaxAbsScaler |

---

## Hangi Algoritmalar İçin Gerekli?

| Algoritma | Ölçekleme Gerekli mi? |
|-----------|------------------------|
| K-Means   | Evet                |
| KNN       |  Evet                |
| SVM       |  Evet                |
| PCA       |  Evet                |
| Decision Tree |  Hayır           |
| Random Forest |  Hayır           |

---

##  Özet

- Özellik ölçekleme, algoritmaların doğru öğrenmesi için çok önemlidir.
- Farklı yöntemler farklı veri türleri için uygundur.
- Her zaman veriye özel yöntem seçilmelidir.

