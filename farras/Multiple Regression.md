# Multiple Regression

Multiple reggresion mirip dengan [linear regression](https://www.w3schools.com/python/python_ml_linear_regression.asp). Tetapi, multiple regression terdiri banyak nilai bebas atau independent. Artinya multiple regression mencoba untuk memprediksi suatu nilai berdasarkan dua atau lebih variabel.

Perhatikan data dibawah ini yang berisikan informasi tentang mobil. 

| Car | Model | Volume | Weight | CO2 |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Toyota | Aygo | 1000 |	790 |	99 |
| Mitsubishi	| Space Star | 1200 | 1160	| 95 |
| Skoda |	Citigo | 1000 |	929 |	95 |	
| Fiat |	500	| 900 |	865 |	90 |
| Mini |	Cooper | 1500 |	1140 |	105 |	
| VW |	Up! | 1000 |	929 |	105 |
| Skoda |	Fabia |	1400 | 1109 |	90 |
| Mercedes |	A-Class |	1500 |	1365 |	92 |
| Ford |	Fiesta |	1500 |	1112 |	98 |
| Audi |	A1 |	1600 |	1150 |	99 |
| Hyundai |	I20 |	1100 |	980 |	99 |
| Suzuki |	Swift |	1300 |	990 |	101 |
|Ford |	Fiesta |	1000 |	1112 |	99 |
|Honda |	Civic |	1600 |	1252 |	94 |
| Hundai |	I30 |	1600 |	1326 |	97 |
|Opel |	Astra |	1600 |	1330 |	97 |
| BMW |	1 | 1600 | 1365 |	99 |
| Mazda | 3 |	2200	| 1280	| 104 |
| Skoda	| Rapid	| 1600	| 1119 |	104 |
| Ford |	Focus	| 2000 |	1328	| 105 |
| Ford |	Mondeo |	1600 |	1584 |	94 |
| Opel |	Insignia |	2000 |	1428 |	99 |
| Mercedes |	C-Class |	2100 |	1365 |	99 |
| Skoda |	Octavia |	1600 |	1415 |	99 |
| Volvo |	S60 |	2000 |	1415 |	99 |
| Mercedes |	CLA |	1500 |	1465 |	102 |
| Audi |	A4 |	2000 |	1490 |	104 |
| Audi |	A6 |	2000 |	1725 |	114 |
| Volvo |	V70 |	1600 |	1523 |	109 |
| BMW |	5 | 2000 |	1705 |	114 |
| Mercedes |	E-Class |	2100 |	1605 |	115 |
| Volvo |	XC70 |	2000 | 1746 |	117 | 
| Ford |	B-Max |	1600 |	1235 |	104 |
| BMW |	2 |	1600 |	1390 |	108 |
| Opel |	Zafira |	1600 |	1405 |	109 |
| Mercedes | SLK |	2500 |	1395 |	120 |

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

```
#predict the CO2 emission of a car where the weight is 2300kg, and the volume is 1300cm3:
predictedCO2 = regr.predict([[2300, 1300]])
```


**Contoh**
Perhatikan seluruh contoh:
```
import pandas
from sklearn import linear_model

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]
y = df['CO2']

regr = linear_model.LinearRegression()
regr.fit(X, y)

#predict the CO2 emission of a car where the weight is 2300kg, and the volume is 1300cm3:
predictedCO2 = regr.predict([[2300, 1300]])

print(predictedCO2)
```
```
Hasil :
**[107.2087328]**
```

## Koefisien
Koefisien adalah faktor yang menjelaskan relasi dengan variabel yang tidak diketahui.

Contoh: jika x adalah sebuah variabel, maka 2x adalah x dua kali. x adalah variabel yang tidak diketahui, dan angka 2 adalah koefisiennya.

Dalam hal ini, kita dapat mencari nilai koefisien dari berat terhadap CO2, dan volume terhadap CO2. Jawaban yang kita dapatkan memberi tahu kita apa yang akan terjadi jika kita menambah, atau mengurangi, salah satu nilai bebas.

**Contoh**
Menampilkan nilai koefisien objek regresi:
```
import pandas
from sklearn import linear_model

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]
y = df['CO2']

regr = linear_model.LinearRegression()
regr.fit(X, y)

print(regr.coef_)
```

```
Hasilnya:
**[0.00755095 0.00780526]**
```

## Penjelasan Hasil

Deretan hasil menunjukkan nilai koefisien berat dan volume.

Berat: 0,00755095
Volume: 0,00780526

Nilai-nilai ini menunjukkan bahwa jika berat bertambah 1kg, emisi CO2 meningkat sebesar 0,00755095g.

Dan jika ukuran mesin (Volume) bertambah 1 cm3, maka emisi CO2 bertambah 0,00780526 g. Saya pikir ini adalah tebakan yang masuk akal, tetapi mari coba kita uji! Kami telah memperkirakan bahwa jika mobil dengan mesin 1300cm3 memiliki berat 2300kg, maka emisi CO2 yang dihasilkan adalah sekitar 107g.

Bagaimana jika kita menambah bobotnya dengan 1000kg?

**Contoh**
Salin contoh sebelumnya, tetapi ubah bobotnya dari 2300 menjadi 3300:

```
import pandas
from sklearn import linear_model

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]
y = df['CO2']

regr = linear_model.LinearRegression()
regr.fit(X, y)

predictedCO2 = regr.predict([[3300, 1300]])

print(predictedCO2)
```

```
Hasil :
**[114.75968007]**
```
Kami telah memprediksi bahwa mobil dengan mesin 1,3 liter, dan berat 3300 kg, akan melepaskan sekitar 115 gram CO2 untuk setiap kilometer yang dikendarai. Hal ini menunjukkan bahwa koefisien 0,00755095 adalah benar:

107.2087328 + (1000 * 0.00755095) = 114.75968


