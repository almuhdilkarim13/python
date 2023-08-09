# Multiple Regression

Multiple reggresion mirip dengan [linear regression](https://www.w3schools.com/python/python_ml_linear_regression.asp). Tetapi, multiple regression terdiri banyak nilai bebas atau independent. Artinya multiple regression mencoba untuk memprediksi suatu nilai berdasarkan dua atau lebih variabel.

Perhatikan data dibawah ini yang berisikan informasi tentang mobil. 

| Car | Model |
| ----------- | ----------- |
| Header | Title |
| Paragraph | Text |

Kita dapat memprediksi emisi CO2 dari sebuah mobil berdasarkan besaran mesinnya. Dengan multuple regression kita bisa menambahkan lebih banyak variabel, seperti berat mobil, untuk membuat prediksi yang lebih akurat.

Bagaimana Cara Penggunaannya?
Dalam Python kami memiliki sejumlah modul untuk melakukan tugas tersebut. Silakan mulai dengan mengunduh Pandas module.

```
import pandas
```

pelajari tentang pandas modul [disini](https://www.w3schools.com/python/pandas/default.asp). Pandas modul membuat kita bisa mendapatkan file csv dan mengembalikan objek DataFrame.

File ini dimaksudkan untuk tujuan testing saja, Anda dapat mengunduhnya [di sini](https://www.w3schools.com/python/data.csv) 

```
df = pandas.read_csv("data.csv")
```
Kemudian buatlah daftar nilai bebas dan namakan variabel ini X, kemudian Masukkan nilai-nilai dependen ke dalam sebuah variabel bernama y.

```
X = df[['Weight', 'Volume']]
y = df['CO2']
```

**Tips** Merupakan hal yang lumrah untuk memberi nama daftar nilai independen dengan X kapital, dan daftar nilai dependen dengan huruf y kecil.

Kita akan menggunakan beberapa metode dari sklearn modul, jadi kita harus mengunduh modul tersebut :

```
from sklearn import linear_model
```
Dari sklearn modul kita akan menggunakan metode LinearRegression() untuk membuat objek regresi linear.

Objek ini memiliki metode yang disebut fit() yang mengambil nilai bebas dan terikat sebagai parameter dan mengisi objek regresi dengan data yang menggambarkan hubungan tersebut: 
```
regr = linear_model.LinearRegression()
regr.fit(X, y)
```
Sekarang kita memiliki objek regresi yang siap untuk memprediksi nilai CO2 berdasarkan berat dan volume mobil: 
