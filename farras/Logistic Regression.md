# Logistic Regression
## Logistic Regression

Logistic regression bertujuan untuk memecahkan masalah klasifikasi. Hal ini dilakukan dengan memprediksi hasil kategori, tidak seperti regresi linier yang memprediksi hasil yang berkelanjutan.

Dalam kasus yang paling sederhana, terdapat dua hasil, yang disebut binomial, contohnya adalah memprediksi apakah suatu tumor ganas atau jinak. Kasus lain memiliki lebih dari dua hasil untuk diklasifikasikan, dalam hal ini disebut multinomial. Contoh umum untuk regresi logistik multinomial adalah memprediksi kelas bunga iris di antara 3 spesies yang berbeda.

Di sini kita akan menggunakan regresi logistik dasar untuk memprediksi variabel binomial. Ini berarti hanya ada dua kemungkinan hasil.

### Bagaimana caranya ?

Dalam Python kita memiliki modul yang akan melakukan pekerjaan untuk kita. Mulailah dengan mengunduh modul numPy.

```
import numpy

```
Menyimpan variabel independen dalam X.

Menyimpan variabel dependen dalam y.

Di bawah ini adalah contoh dataset:

```
#X represents the size of a tumor in centimeters.
X = numpy.array([3.78, 2.44, 2.09, 0.14, 1.72, 1.65, 4.92, 4.37, 4.96, 4.52, 3.69, 5.88]).reshape(-1,1)

#Note: X has to be reshaped into a column from a row for the LogisticRegression() function to work.
#y represents whether or not the tumor is cancerous (0 for "No", 1 for "Yes").
y = numpy.array([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1])
```

Kita akan menggunakan metode dari sklearn, jadi kita harus mengunduh modul tersebut :

```
from sklearn import linear_model
```
Dari modul sklearn kita akan menggunakan metode LogisticRegression() untuk membuat objek regresi logistik.
                                      
Objek ini memiliki metode yang disebut fit() yang mengambil nilai independen dan dependen sebagai parameter dan mengisi objek regresi dengan data yang menggambarkan hubungan tersebut:
                                            
```
logr = linear_model.LogisticRegression()
logr.fit(X,y)
```
Sekarang kita memiliki objek logistic regression yang sudah siap untuk menentukan apakah suatu tumor adalah kanker berdasarkan ukuran tumor:

```
#predict if tumor is cancerous where the size is 3.46mm:
predicted = logr.predict(numpy.array([3.46]).reshape(-1,1))
```

#### Contoh 
Perhatikan contoh berikut 

```
import numpy
from sklearn import linear_model

#Reshaped for Logistic function.
X = numpy.array([3.78, 2.44, 2.09, 0.14, 1.72, 1.65, 4.92, 4.37, 4.96, 4.52, 3.69, 5.88]).reshape(-1,1)
y = numpy.array([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1])

logr = linear_model.LogisticRegression()
logr.fit(X,y)

#predict if tumor is cancerous where the size is 3.46mm:
predicted = logr.predict(numpy.array([3.46]).reshape(-1,1))
print(predicted)
```
#### Hasilnya 
**[0]**

Kami telah memprediksi bahwa tumor dengan ukuran 3,46 mm tidak akan menjadi kanker.

## Koefisien
Dalam logistic regression, koefisiennya adalah perubahan yang diharapkan dalam log-odds untuk mendapatkan hasil per unit perubahan dalam X.

Ini bukan pengertian yang paling intuitif, jadi mari kita gunakan untuk menciptakan sesuatu yang lebih masuk akal, peluang.

#### Contoh : 
perhatikan contoh berikut : 
```
import numpy
from sklearn import linear_model

#Reshaped for Logistic function.
X = numpy.array([3.78, 2.44, 2.09, 0.14, 1.72, 1.65, 4.92, 4.37, 4.96, 4.52, 3.69, 5.88]).reshape(-1,1)
y = numpy.array([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1])

logr = linear_model.LogisticRegression()
logr.fit(X,y)

log_odds = logr.coef_
odds = numpy.exp(log_odds)

print(odds)
```
#### Hasilnya 
**[4.03541657]**

Hal ini menunjukkan bahwa ketika ukuran tumor bertambah 1mm, kemungkinan tumor tersebut menjadi tumor kanker meningkat 4x lipat.

## Peluang (Probability)

Nilai koefisien dan nilai intercept dapat digunakan untuk menemukan probabilitas bahwa setiap tumor adalah kanker.

Buat sebuah fungsi yang menggunakan nilai koefisien dan intersep model untuk mengembalikan nilai baru. Nilai baru ini mewakili probabilitas bahwa pengamatan yang diberikan adalah tumor:

```
def logit2prob(logr,x):
  log_odds = logr.coef_ * x + logr.intercept_
  odds = numpy.exp(log_odds)
  probability = odds / (1 + odds)
  return(probability)
```
## Penjelasan Function

Untuk menemukan log-odds untuk setiap pengukuran, pertama kita harus membuat rumus yang mirip dengan rumus regresi linier, dengan mengambil koefisien dan intercept.

```
log_odds = logr.coef_ * x + logr.intercept_
```
Untuk mengubah log-odds menjadi odds, kita harus mengeksponensial log-odds.

```
odds = numpy.exp(log_odds)
```

Setelah kita memiliki peluang, kita dapat mengubahnya menjadi probabilitas dengan membaginya dengan 1 ditambah peluang.

```
probability = odds / (1 + odds)
```

Sekarang mari kita gunakan fungsi ini dengan apa yang telah kita pelajari untuk mengetahui probabilitas bahwa setiap tumor adalah kanker.

#### Contohnya
Perhatikan contoh dibawah ini 

```
import numpy
from sklearn import linear_model

X = numpy.array([3.78, 2.44, 2.09, 0.14, 1.72, 1.65, 4.92, 4.37, 4.96, 4.52, 3.69, 5.88]).reshape(-1,1)
y = numpy.array([0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1])

logr = linear_model.LogisticRegression()
logr.fit(X,y)

def logit2prob(logr, X):
  log_odds = logr.coef_ * X + logr.intercept_
  odds = numpy.exp(log_odds)
  probability = odds / (1 + odds)
  return(probability)

print(logit2prob(logr, X))
```

#### Hasilnya
```
[[0.60749955]
   [0.19268876]
   [0.12775886]
   [0.00955221]
   [0.08038616]
   [0.07345637]
   [0.88362743]
   [0.77901378]
   [0.88924409]
   [0.81293497]
   [0.57719129]
   [0.96664243]]
```

#### Penjelasan Hasil : 
3,78 0,61 Kemungkinan tumor dengan ukuran 3,78 cm bersifat kanker adalah 61%.

2.44 0.19 Kemungkinan tumor dengan ukuran 2.44 cm bersifat kanker adalah 19%.

2.09 0.13 Probabilitas bahwa tumor dengan ukuran 2.09cm adalah kanker adalah 13%.





