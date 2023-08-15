# Categorical Data

## Categorical Data
Ketika data Anda memiliki kategori yang disajikan dalam bentuk string, maka akan sulit untuk menggunakannya untuk melatih model machine learning yang sering kali hanya menerima data numerik.

Alih-alih mengabaikan data kategorikal dan mengecualikan informasi tersebut dari model kami, Anda dapat mengubah data tersebut agar dapat digunakan dalam model Anda.

Lihatlah tabel di bawah ini, ini adalah kumpulan data yang sama dengan yang kita gunakan dalam bab regresi berganda.

#### Contohnya
```
import pandas as pd

cars = pd.read_csv('data.csv')
print(cars.to_string())
```
#### Hasilnya 
```
 Car       Model  Volume  Weight  CO2
  0       Toyoty        Aygo    1000     790   99
  1   Mitsubishi  Space Star    1200    1160   95
  2        Skoda      Citigo    1000     929   95
  3         Fiat         500     900     865   90
  4         Mini      Cooper    1500    1140  105
  5           VW         Up!    1000     929  105
  6        Skoda       Fabia    1400    1109   90
  7     Mercedes     A-Class    1500    1365   92
  8         Ford      Fiesta    1500    1112   98
  9         Audi          A1    1600    1150   99
  10     Hyundai         I20    1100     980   99
  11      Suzuki       Swift    1300     990  101
  12        Ford      Fiesta    1000    1112   99
  13       Honda       Civic    1600    1252   94
  14      Hundai         I30    1600    1326   97
  15        Opel       Astra    1600    1330   97
  16         BMW           1    1600    1365   99
  17       Mazda           3    2200    1280  104
  18       Skoda       Rapid    1600    1119  104
  19        Ford       Focus    2000    1328  105
  20        Ford      Mondeo    1600    1584   94
  21        Opel    Insignia    2000    1428   99
  22    Mercedes     C-Class    2100    1365   99
  23       Skoda     Octavia    1600    1415   99
  24       Volvo         S60    2000    1415   99
  25    Mercedes         CLA    1500    1465  102
  26        Audi          A4    2000    1490  104
  27        Audi          A6    2000    1725  114
  28       Volvo         V70    1600    1523  109
  29         BMW           5    2000    1705  114
  30    Mercedes     E-Class    2100    1605  115
  31       Volvo        XC70    2000    1746  117
  32        Ford       B-Max    1600    1235  104
  33         BMW         216    1600    1390  108
  34        Opel      Zafira    1600    1405  109
  35    Mercedes         SLK    2500    1395  120
```

Pada bab multiple regression, kami mencoba memprediksi CO2 yang diemisikan berdasarkan volume mesin dan berat mobil, namun kami tidak menyertakan informasi tentang merek dan model mobil.

Informasi mengenai merek mobil atau model mobil dapat membantu kami membuat prediksi yang lebih baik mengenai CO2 yang dihasilkan.

## One Hot Encoding 

Kita tidak dapat menggunakan kolom Mobil atau Model dalam data kita karena kolom tersebut bukan angka. Hubungan linear antara variabel kategorikal, Mobil atau Model, dan variabel numerik, CO2, tidak dapat ditentukan.

Untuk mengatasi masalah ini, kita harus memiliki representasi numerik dari variabel kategorikal. Salah satu cara untuk melakukannya adalah dengan memiliki kolom yang mewakili setiap kelompok dalam kategori.

Untuk setiap kolom, nilainya adalah 1 atau 0 di mana 1 mewakili penyertaan kelompok dan 0 mewakili pengecualian. Transformasi ini disebut dengan satu pengkodean panas.

Anda tidak perlu melakukan ini secara manual, modul Python Pandas memiliki fungsi yang disebut get_dummies() yang melakukan one hot encoding.

Pelajari tentang Pandas di [Tutorial Pandas](https://www.w3schools.com/python/pandas/default.asp).

#### Contohnya 
One Hot Encode the Car column:

```
import pandas as pd

cars = pd.read_csv('data.csv')
ohe_cars = pd.get_dummies(cars[['Car']])

print(ohe_cars.to_string())
```
#### Hasilnya 
```
Car_Audi  Car_BMW  Car_Fiat  Car_Ford  Car_Honda  Car_Hundai  Car_Hyundai  Car_Mazda  Car_Mercedes  Car_Mini  Car_Mitsubishi  Car_Opel  Car_Skoda  Car_Suzuki  Car_Toyoty  Car_VW  Car_Volvo
  0          0        0         0         0          0           0            0          0             0         0               0         0          0           0           1       0          0
  1          0        0         0         0          0           0            0          0             0         0               1         0          0           0           0       0          0
  2          0        0         0         0          0           0            0          0             0         0               0         0          1           0           0       0          0
  3          0        0         1         0          0           0            0          0             0         0               0         0          0           0           0       0          0
  4          0        0         0         0          0           0            0          0             0         1               0         0          0           0           0       0          0
  5          0        0         0         0          0           0            0          0             0         0               0         0          0           0           0       1          0
  6          0        0         0         0          0           0            0          0             0         0               0         0          1           0           0       0          0
  7          0        0         0         0          0           0            0          0             1         0               0         0          0           0           0       0          0
  8          0        0         0         1          0           0            0          0             0         0               0         0          0           0           0       0          0
  9          1        0         0         0          0           0            0          0             0         0               0         0          0           0           0       0          0
  10         0        0         0         0          0           0            1          0             0         0               0         0          0           0           0       0          0
  11         0        0         0         0          0           0            0          0             0         0               0         0          0           1           0       0          0
  12         0        0         0         1          0           0            0          0             0         0               0         0          0           0           0       0          0
  13         0        0         0         0          1           0            0          0             0         0               0         0          0           0           0       0          0
  14         0        0         0         0          0           1            0          0             0         0               0         0          0           0           0       0          0
  15         0        0         0         0          0           0            0          0             0         0               0         1          0           0           0       0          0
  16         0        1         0         0          0           0            0          0             0         0               0         0          0           0           0       0          0
  17         0        0         0         0          0           0            0          1             0         0               0         0          0           0           0       0          0
  18         0        0         0         0          0           0            0          0             0         0               0         0          1           0           0       0          0
  19         0        0         0         1          0           0            0          0             0         0               0         0          0           0           0       0          0
  20         0        0         0         1          0           0            0          0             0         0               0         0          0           0           0       0          0
  21         0        0         0         0          0           0            0          0             0         0               0         1          0           0           0       0          0
  22         0        0         0         0          0           0            0          0             1         0               0         0          0           0           0       0          0
  23         0        0         0         0          0           0            0          0             0         0               0         0          1           0           0       0          0
  24         0        0         0         0          0           0            0          0             0         0               0         0          0           0           0       0          1
  25         0        0         0         0          0           0            0          0             1         0               0         0          0           0           0       0          0
  26         1        0         0         0          0           0            0          0             0         0               0         0          0           0           0       0          0
  27         1        0         0         0          0           0            0          0             0         0               0         0          0           0           0       0          0
  28         0        0         0         0          0           0            0          0             0         0               0         0          0           0           0       0          1
  29         0        1         0         0          0           0            0          0             0         0               0         0          0           0           0       0          0
  30         0        0         0         0          0           0            0          0             1         0               0         0          0           0           0       0          0
  31         0        0         0         0          0           0            0          0             0         0               0         0          0           0           0       0          1
  32         0        0         0         1          0           0            0          0             0         0               0         0          0           0           0       0          0
  33         0        1         0         0          0           0            0          0             0         0               0         0          0           0           0       0          0
  34         0        0         0         0          0           0            0          0             0         0               0         1          0           0           0       0          0
  35         0        0         0         0          0           0            0          0             1         0               0         0          0           0           0       0          0
```
### Hasil

Kolom dibuat untuk setiap merek mobil di kolom Mobil.

## Memprediksi emisi CO2

Kita dapat menggunakan informasi tambahan ini bersama dengan volume dan berat untuk memprediksi CO2

Untuk menggabungkan informasi tersebut, kita dapat menggunakan fungsi concat() dari pandas.

Pertama, kita perlu mengimpor beberapa modul.

Kita akan mulai dengan mengunduh Pandas.

```
Import Pandas
```
Pandas modul memudahkan kita untuk membaca file csv dan memanipulasi objek DataFrame:

```
cars = pandas.read_csv("data.csv")
```
Ini juga memungkinkan kita untuk membuat variable dummy:

```
ohe_cars = pandas.get_dummies(cars[['Car']])
```

Kemudian kita harus memilih variabel independen (X) dan menambahkan variabel dummy secara kolom.

Simpan juga variabel dependen dalam (y).

```
X = pandas.concat([cars[['Volume', 'Weight']], ohe_cars], axis=1)
y = cars['CO2']
```
Kita juga perlu mengimpor metode dari sklearn untuk membuat model linier

Mengetahui tentang [linear regression](https://www.w3schools.com/python/python_ml_linear_regression.asp).

```
from sklearn import linear_model
```
Sekarang kita dapat memasukkan data ke dalam linear regresi:

```
regr = linear_model.LinearRegression()
regr.fit(X,y)
```
Akhirnya, kami dapat memprediksi emisi CO2 berdasarkan berat, volume, dan pabrikan mobil.
```
##predict the CO2 emission of a Volvo where the weight is 2300kg, and the volume is 1300cm3:
predictedCO2 = regr.predict([[2300, 1300,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0]])
```

#### Contohnya 
```
import pandas
from sklearn import linear_model

cars = pandas.read_csv("data.csv")
ohe_cars = pandas.get_dummies(cars[['Car']])

X = pandas.concat([cars[['Volume', 'Weight']], ohe_cars], axis=1)
y = cars['CO2']

regr = linear_model.LinearRegression()
regr.fit(X,y)

##predict the CO2 emission of a Volvo where the weight is 2300kg, and the volume is 1300cm3:
predictedCO2 = regr.predict([[2300, 1300,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0]])

print(predictedCO2)
```

#### Hasilnya
```
 [122.45153299]
```
Kita sekarang memiliki koefisien untuk volume, berat, dan setiap merek mobil dalam kumpulan data

## Dummifiying

Tidak perlu membuat satu kolom untuk setiap grup dalam kategori Anda. Informasi dapat disimpan dengan menggunakan 1 kolom yang lebih sedikit dari jumlah grup yang Anda miliki.

Sebagai contoh, Anda memiliki kolom yang mewakili warna dan dalam kolom tersebut, Anda memiliki dua warna, merah dan biru.

#### Contohnya
```
import pandas as pd

colors = pd.DataFrame({'color': ['blue', 'red']})

print(colors)
```

#### Hasilnya
```
color
  0  blue
  1   red
```
Anda dapat membuat 1 kolom yang disebut merah di mana 1 mewakili merah dan 0 mewakili bukan merah, yang berarti berwarna biru.

Untuk melakukan ini, kita dapat menggunakan fungsi yang sama dengan yang kita gunakan untuk satu pengkodean panas, get_dummies, dan kemudian membuang salah satu kolom. Ada sebuah argumen, drop_first, yang memungkinkan kita untuk mengecualikan kolom pertama dari tabel yang dihasilkan.

#### Contohnya
```
import pandas as pd

colors = pd.DataFrame({'color': ['blue', 'red']})
dummies = pd.get_dummies(colors, drop_first=True)

print(dummies)
```

#### Hasilnya
```
 color_red
  0          0
  1          1
```
Bagaimana jika Anda memiliki lebih dari 2 kelompok? Bagaimana beberapa kelompok dapat diwakili oleh 1 kolom yang lebih sedikit?

Katakanlah kali ini kita memiliki tiga warna, merah, biru dan hijau. Ketika kita menggunakan get_dummies sambil menjatuhkan kolom pertama, kita akan mendapatkan tabel berikut.

#### Contohnya
```
import pandas as pd

colors = pd.DataFrame({'color': ['blue', 'red', 'green']})
dummies = pd.get_dummies(colors, drop_first=True)
dummies['color'] = colors['color']

print(dummies)
```

#### Hasilnya
```
color_green  color_red  color
  0            0          0   blue
  1            0          1    red
  2            1          0  green
```
