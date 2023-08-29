# K-nearest neighbors (KNN)

KNN adalah algoritme machine learning (ML) yang sederhana dan terawasi yang dapat digunakan untuk tugas klasifikasi atau regresi - dan juga sering digunakan dalam imputasi nilai yang hilang. Hal ini didasarkan pada gagasan bahwa pengamatan yang paling dekat dengan titik data yang diberikan adalah pengamatan yang paling "mirip" dalam kumpulan data, dan oleh karena itu kita dapat mengklasifikasikan titik yang tidak terduga berdasarkan nilai dari titik terdekat yang ada. Dengan memilih K, pengguna dapat memilih jumlah pengamatan terdekat yang akan digunakan dalam algoritma.

Di sini, kami akan menunjukkan kepada Anda bagaimana mengimplementasikan algoritma KNN untuk klasifikasi, dan menunjukkan bagaimana nilai K yang berbeda mempengaruhi hasil.

## Bagaimana cara kerjanya?

K adalah jumlah tetangga terdekat yang digunakan. Untuk klasifikasi, suara mayoritas digunakan untuk menentukan ke kelas mana pengamatan baru harus masuk. Nilai K yang lebih besar sering kali lebih kuat terhadap pencilan dan menghasilkan batas keputusan yang lebih stabil daripada nilai yang sangat kecil (K = 3 akan lebih baik daripada K = 1, yang mungkin menghasilkan hasil yang tidak diinginkan.

### Contohnya
Mulailah dengan memvisualisasikan beberapa titik data:

```
import matplotlib.pyplot as plt

x = [4, 5, 10, 4, 3, 11, 14 , 8, 10, 12]
y = [21, 19, 24, 17, 16, 25, 24, 22, 21, 21]
classes = [0, 0, 1, 0, 0, 1, 1, 0, 1, 1]

plt.scatter(x, y, c=classes)
plt.show()
```
### Contohnya

![image](https://github.com/uin-fah/docs-python/assets/119867794/b8c2d5d8-aa3d-42b8-abb0-3c32cad79504)

Sekarang kita masukkan algoritma KNN dengan K = 1:

```
from sklearn.neighbors import KNeighborsClassifier

data = list(zip(x, y))
knn = KNeighborsClassifier(n_neighbors=1)

knn.fit(data, classes)
```
Dan menggunakannya untuk mengklasifikasikan titik data baru:

### Contohnya

```
new_x = 8
new_y = 21
new_point = [(new_x, new_y)]

prediction = knn.predict(new_point)

plt.scatter(x + [new_x], y + [new_y], c=classes + [prediction[0]])
plt.text(x=new_x-1.7, y=new_y-0.7, s=f"new point, class: {prediction[0]}")
plt.show()
```

### Hasilnya

![image](https://github.com/uin-fah/docs-python/assets/119867794/1a8f1625-4f32-465b-9e6b-c152bac21a81)

Sekarang kita melakukan hal yang sama, tetapi dengan nilai K yang lebih tinggi yang mengubah prediksi:

### Contohnya

```
knn = KNeighborsClassifier(n_neighbors=5)

knn.fit(data, classes)

prediction = knn.predict(new_point)

plt.scatter(x + [new_x], y + [new_y], c=classes + [prediction[0]])
plt.text(x=new_x-1.7, y=new_y-0.7, s=f"new point, class: {prediction[0]}")
plt.show()
```

### Hasilnya

![image](https://github.com/uin-fah/docs-python/assets/119867794/38d2c065-b305-4a2b-96f9-8ad3ca30e087)


## Contoh Penjelasan
Impor modul yang Anda butuhkan.

Anda dapat mempelajari tentang modul Matplotlib di [Tutorial Matplotlib](https://www.w3schools.com/python/matplotlib_intro.asp).

scikit-learn adalah library yang populer untuk pembelajaran mesin di Python.

```
import matplotlib.pyplot as plt
from sklearn.neighbors import KNeighborsClassifier
```

Membuat larik yang menyerupai variabel dalam kumpulan data. Kita memiliki dua fitur input (x dan y) dan kemudian kelas target (kelas). Fitur input yang telah diberi label dengan kelas target akan digunakan untuk memprediksi kelas data baru. Perhatikan bahwa meskipun kita hanya menggunakan dua fitur input di sini, metode ini akan bekerja dengan sejumlah variabel:

```
x = [4, 5, 10, 4, 3, 11, 14 , 8, 10, 12]
y = [21, 19, 24, 17, 16, 25, 24, 22, 21, 21]
classes = [0, 0, 1, 0, 0, 1, 1, 0, 1, 1]
```
Mengubah fitur input menjadi satu set titik:

```
data = list(zip(x, y))
print(data)
```

### Hasilnya

```
[(4, 21), (5, 19), (10, 24), (4, 17), (3, 16), (11, 25), (14, 24), (8, 22), (10, 21), (12, 21)]
```

Dengan menggunakan fitur input dan kelas target, kami mencocokkan model KNN pada model dengan menggunakan 1 tetangga terdekat:

```
knn = KNeighborsClassifier(n_neighbors=1)
knn.fit(data, classes)
```
Kemudian, kita dapat menggunakan objek KNN yang sama untuk memprediksi kelas titik data baru yang tidak terduga. Pertama, kita membuat fitur x dan y baru, lalu memanggil knn.predict() pada titik data baru untuk mendapatkan kelas 0 atau 1:

```
new_x = 8
new_y = 21
new_point = [(new_x, new_y)]
prediction = knn.predict(new_point)
print(prediction)
```

### Hasilnya
```
[0]
```

Ketika kita memplot semua data bersama dengan titik dan kelas yang baru, kita dapat melihat bahwa titik tersebut diberi label biru dengan kelas 1. Anotasi teks hanya untuk menyoroti lokasi titik baru:

```
plt.scatter(x + [new_x], y + [new_y], c=classes + [prediction[0]])
plt.text(x=new_x-1.7, y=new_y-0.7, s=f"new point, class: {prediction[0]}")
plt.show()
```

### Hasilnya 
![image](https://github.com/uin-fah/docs-python/assets/119867794/504f8eda-1faf-49a7-b7e0-5cf6aae36e23)

Namun, ketika kita mengubah jumlah tetangga menjadi 5, jumlah titik yang digunakan untuk mengklasifikasikan titik baru kita berubah. Akibatnya, klasifikasi titik baru juga berubah:

```
knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(data, classes)
prediction = knn.predict(new_point)
print(prediction)
```

### Hasilnya 

```
[1]
```

Ketika kita memplot kelas titik baru bersama dengan titik yang lama, kita mencatat bahwa warnanya telah berubah berdasarkan label kelas yang terkait:

```
plt.scatter(x + [new_x], y + [new_y], c=classes + [prediction[0]])
plt.text(x=new_x-1.7, y=new_y-0.7, s=f"new point, class: {prediction[0]}")
plt.show()
```

### Hasilnya 

![image](https://github.com/uin-fah/docs-python/assets/119867794/3e230d3d-b4ab-40e8-be92-41abec68f00a)

