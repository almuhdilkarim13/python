# Scale 

## Skala Fitur

Ketika data Anda memiliki nilai yang berlainan, dan unit pengukuran yang berbeda, mungkin sulit untuk membandingkannya. Apa artinya kilogram dibandingkan dengan meter? Atau ketinggian dibandingkan dengan waktu?
Jawaban untuk masalah ini adalah penskalaan. Kita dapat menskalakan data menjadi nilai baru yang lebih mudah untuk dibandingkan.
Lihatlah tabel di bawah ini, ini adalah kumpulan data yang sama dengan yang kita gunakan pada bab regresi berganda, namun kali ini kolom volume berisi nilai dalam liter, bukan cm3 (1,0, bukan 1000).

**TABELL**

Mungkin sulit untuk membandingkan volume 1.0 dengan berat 790, tetapi jika kita mengukur keduanya ke dalam nilai yang sebanding, kita dapat dengan mudah melihat seberapa besar satu nilai dibandingkan dengan nilai lainnya.

Ada beberapa metode yang berbeda untuk mengukur data, dalam tutorial ini kita akan menggunakan metode yang disebut standardisasi.

Metode standardisasi menggunakan rumus ini:

`
z = (x - u) / s
`
Dimana **z** adalah nilai baru, **x** adalah nilai asli, **u** adalah rata-rata dan **s** adalah deviasi standar.

Jika mengambil kolom bobot dari kumpulan data di atas, nilai pertama adalah 790, dan nilai yang akan diskalakan adalah:

`
(790 - 1292.23) / 238.74 = -2.1
`

Jika Anda mengambil kolom volume dari kumpulan data di atas, nilai pertama adalah 1,0, dan nilai skalanya adalah:

`
(1.0 - 1.61) / 0.38 = -1.59
`

#### Contoh
Skala semua nilai di kolom Berat dan Volume:

```
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler
scale = StandardScaler()

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]

scaledX = scale.fit_transform(X)

print(scaledX)
```

#### Hasilnya 
Note that the first two values are -2.1 and -1.59, which corresponds to our calculations:

```
[[-2.10389253 -1.59336644]
 [-0.55407235 -1.07190106]
 [-1.52166278 -1.59336644]
 [-1.78973979 -1.85409913]
 [-0.63784641 -0.28970299]
 [-1.52166278 -1.59336644]
 [-0.76769621 -0.55043568]
 [ 0.3046118  -0.28970299]
 [-0.7551301  -0.28970299]
 [-0.59595938 -0.0289703 ]
 [-1.30803892 -1.33263375]
 [-1.26615189 -0.81116837]
 [-0.7551301  -1.59336644]
 [-0.16871166 -0.0289703 ]
 [ 0.14125238 -0.0289703 ]
 [ 0.15800719 -0.0289703 ]
 [ 0.3046118  -0.0289703 ]
 [-0.05142797  1.53542584]
 [-0.72580918 -0.0289703 ]
 [ 0.14962979  1.01396046]
 [ 1.2219378  -0.0289703 ]
 [ 0.5685001   1.01396046]
 [ 0.3046118   1.27469315]
 [ 0.51404696 -0.0289703 ]
 [ 0.51404696  1.01396046]
 [ 0.72348212 -0.28970299]
 [ 0.8281997   1.01396046]
 [ 1.81254495  1.01396046]
 [ 0.96642691 -0.0289703 ]
 [ 1.72877089  1.01396046]
 [ 1.30990057  1.27469315]
 [ 1.90050772  1.01396046]
 [-0.23991961 -0.0289703 ]
 [ 0.40932938 -0.0289703 ]
 [ 0.47215993 -0.0289703 ]
 [ 0.4302729   2.31762392]]
```

## Memprediksi Nilai CO2

Tugas pada bab Multiple Regression adalah memprediksi emisi CO2 dari sebuah mobil ketika Anda hanya mengetahui berat dan volumenya.

Ketika kumpulan data diskalakan, Anda harus menggunakan skala ketika memprediksi nilai:

#### Contoh
Memprediksi emisi CO2 dari mobil 1,3 liter dengan berat 2.300 kilogram:

```
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler
scale = StandardScaler()

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]
y = df['CO2']

scaledX = scale.fit_transform(X)

regr = linear_model.LinearRegression()
regr.fit(scaledX, y)

scaled = scale.transform([[2300, 1.3]])

predictedCO2 = regr.predict([scaled[0]])
print(predictedCO2)
```

#### Hasilnya 
`
[107.2087328]
`




