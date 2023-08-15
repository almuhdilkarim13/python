# Grid Search

## Grid Search 
Sebagian besar model pembelajaran komputer berisi parameter yang dapat disesuaikan untuk memvariasikan bagaimana model tersebut belajar. Sebagai contoh, model regresi logistik, dari sklearn, memiliki parameter C yang mengontrol regularisasi, yang memengaruhi kompleksitas model.

Bagaimana kita memilih nilai terbaik untuk C? Nilai terbaik tergantung pada data yang digunakan untuk melatih model.

### Bagaimana Cara kerjanya
Salah satu metodenya adalah dengan mencoba nilai yang berbeda dan kemudian memilih nilai yang memberikan skor terbaik. Teknik ini dikenal sebagai pencarian kriteria. Jika kita harus memilih nilai untuk dua atau lebih parameter, kita akan mengevaluasi semua kombinasi dari kumpulan nilai sehingga membentuk kisi-kisi nilai.

Sebelum kita masuk ke dalam contoh, ada baiknya kita mengetahui apa yang dilakukan oleh parameter yang kita ubah. Nilai C yang lebih tinggi memberi tahu model, data pelatihan menyerupai informasi dunia nyata, memberikan bobot yang lebih besar pada data pelatihan. Sementara nilai C yang lebih rendah melakukan hal yang sebaliknya.

## Menggunakan Parameter Standar

Pertama, mari kita lihat hasil seperti apa yang dapat kita hasilkan tanpa grid search dengan hanya menggunakan parameter standar.

Untuk memulai, pertama-tama kita harus memuat dataset yang akan kita gunakan.

```
from sklearn import datasets
iris = datasets.load_iris()
```

Selanjutnya untuk membuat model, kita harus memiliki satu set variabel independen X dan variabel dependen y.

```
X = iris['data']
y = iris['target']
```

Sekarang kita akan memuat model logistik untuk mengklasifikasikan bunga iris.

```
from sklearn.linear_model import LogisticRegression
```

Membuat model, mengatur max_iter ke nilai yang lebih tinggi untuk memastikan bahwa model menemukan hasil.

Perlu diingat bahwa nilai standar untuk C dalam model regresi logistik adalah 1, kita akan membandingkannya nanti.

Pada contoh di bawah ini, kita melihat kumpulan data iris mata dan mencoba melatih model dengan berbagai nilai C dalam regresi logistik.

```
logit = LogisticRegression(max_iter = 10000)
```

Setelah kita membuat model, kita harus menyesuaikan model dengan data.

```
print(logit.fit(X,y))
```
Untuk mengevaluasi model, kami menjalankan metode skor.

#### Contoh

```
from sklearn import datasets
from sklearn.linear_model import LogisticRegression

iris = datasets.load_iris()

X = iris['data']
y = iris['target']

logit = LogisticRegression(max_iter = 10000)

print(logit.fit(X,y))

print(logit.score(X,y))
```

Dengan pengaturan standar C = 1, kami mencapai skor 0,973.

Mari kita lihat apakah kita dapat melakukan yang lebih baik dengan mengimplementasikan pencarian grid dengan nilai perbedaan 0,973.

### Menerapkan Grid Search

Kita akan mengikuti langkah yang sama seperti sebelumnya kecuali kali ini kita akan menetapkan rentang nilai untuk C.

Mengetahui nilai mana yang harus ditetapkan untuk parameter yang dicari akan membutuhkan kombinasi pengetahuan domain dan praktik.

Karena nilai default untuk C adalah 1, kita akan menetapkan rentang nilai di sekitarnya.

```
C = [0.25, 0.5, 0.75, 1, 1.25, 1.5, 1.75, 2]
```

Selanjutnya kita akan membuat perulangan for untuk mengubah nilai C dan mengevaluasi model dengan setiap perubahan.

Pertama, kita akan membuat sebuah daftar kosong untuk menyimpan nilai di dalamnya.

```
scores = []
```
Untuk mengubah nilai C, kita harus mengulangi rangkaian nilai dan memperbarui parameter setiap kali.

```
for choice in C:
  logit.set_params(C=choice)
  logit.fit(X, y)
  scores.append(logit.score(X, y))
```

Dengan skor yang tersimpan dalam daftar, kita dapat menilai apa pilihan C yang terbaik.

```
print(scores)
```
#### Contohnya
```
from sklearn import datasets
from sklearn.linear_model import LogisticRegression

iris = datasets.load_iris()

X = iris['data']
y = iris['target']

logit = LogisticRegression(max_iter = 10000)

C = [0.25, 0.5, 0.75, 1, 1.25, 1.5, 1.75, 2]

scores = []

for choice in C:
  logit.set_params(C=choice)
  logit.fit(X, y)
  scores.append(logit.score(X, y))

print(scores)
```

#### Penjelasan Hasil
Kita dapat melihat bahwa nilai C yang lebih rendah berkinerja lebih buruk daripada parameter dasar 1. Namun, ketika kami meningkatkan nilai C menjadi 1,75, model mengalami peningkatan akurasi.

Tampaknya meningkatkan C melebihi jumlah ini tidak membantu meningkatkan akurasi model.




