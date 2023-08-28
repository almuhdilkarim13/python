# K-Means 
K-means adalah metode pembelajaran tanpa pengamatan untuk mengelompokkan titik-titik data. Algoritme ini secara iteratif membagi titik data ke dalam K cluster dengan meminimalkan varians di setiap cluster.

Di sini, kami akan menunjukkan kepada Anda cara memperkirakan nilai terbaik untuk K menggunakan metode siku, lalu menggunakan pengelompokan K-means untuk mengelompokkan titik-titik data ke dalam cluster.

## Bagaimana Cara Kerjanya
Pertama, setiap titik data secara acak ditempatkan ke salah satu dari K cluster. Kemudian, kami menghitung centroid (secara fungsional merupakan pusat) dari setiap klaster, dan menetapkan kembali setiap titik data ke klaster dengan centroid terdekat. Kami mengulangi proses ini hingga penetapan klaster untuk setiap titik data tidak lagi berubah.

Pengelompokan K-means mengharuskan kita untuk memilih K, jumlah cluster yang kita inginkan untuk mengelompokkan data. Metode siku memungkinkan kita untuk membuat grafik inersia (metrik berbasis jarak) dan memvisualisasikan titik di mana inersia mulai menurun secara linear. Titik ini disebut sebagai "eblow" dan merupakan perkiraan yang baik untuk nilai terbaik untuk K berdasarkan data kita.

### Contoh
```
import matplotlib.pyplot as plt

x = [4, 5, 10, 4, 3, 11, 14 , 6, 10, 12]
y = [21, 19, 24, 17, 16, 25, 24, 22, 21, 21]

plt.scatter(x, y)
plt.show()
```
### Hasilnya
![image](https://github.com/uin-fah/docs-python/assets/119867794/e3fc467b-7a8c-4339-b7c1-f5dcc8f93c07)

Sekarang, kita memanfaatkan metode siku untuk memvisualisasikan intertia untuk nilai K yang berbeda-beda:

### Contohnya
```
from sklearn.cluster import KMeans

data = list(zip(x, y))
inertias = []

for i in range(1,11):
    kmeans = KMeans(n_clusters=i)
    kmeans.fit(data)
    inertias.append(kmeans.inertia_)

plt.plot(range(1,11), inertias, marker='o')
plt.title('Elbow method')
plt.xlabel('Number of clusters')
plt.ylabel('Inertia')
plt.show()
```
### Hasilnya
![image](https://github.com/uin-fah/docs-python/assets/119867794/f9ac7101-d2d4-45d4-b584-54e4be2c49d0)

Metode siku menunjukkan bahwa 2 adalah nilai yang baik untuk K, jadi kita latih ulang dan memvisualisasikan hasilnya:

### Contohnya
```
kmeans = KMeans(n_clusters=2)
kmeans.fit(data)

plt.scatter(x, y, c=kmeans.labels_)
plt.show()
```

### Hasilnya
![image](https://github.com/uin-fah/docs-python/assets/119867794/17139b19-f916-461d-8921-ff6038276390)

## Penjelasan Hasil
Unduh modul yang anda butuhkan

```
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
```
Anda dapat mempelajari tentang modul Matplotlib di [Tutorial Matplotlib](https://www.w3schools.com/python/matplotlib_intro.asp).

scikit-learn adalah pustaka yang populer untuk pembelajaran mesin.
Membuat larik yang menyerupai dua variabel dalam sebuah kumpulan data. Perhatikan bahwa meskipun kita hanya menggunakan dua variabel di sini, metode ini dapat digunakan dengan sejumlah variabel:



```
x = [4, 5, 10, 4, 3, 11, 14 , 6, 10, 12]
y = [21, 19, 24, 17, 16, 25, 24, 22, 21, 21]
```

Ubah data menjadi sekumpulan poin:
```
data = list(zip(x, y))
print(data)
```

### Hasilnya
```
[(4, 21), (5, 19), (10, 24), (4, 17), (3, 16), (11, 25), (14, 24), (6, 22), (10, 21), (12, 21)]

```
Untuk menemukan nilai terbaik untuk K, kita perlu menjalankan K-means di seluruh data kita untuk berbagai nilai yang mungkin. Kita hanya memiliki 10 titik data, jadi jumlah maksimum cluster adalah 10. Jadi untuk setiap nilai K dalam rentang (1,11), kita melatih model K-means dan memplot intertia pada jumlah cluster tersebut:

```
inertias = []

for i in range(1,11):
    kmeans = KMeans(n_clusters=i)
    kmeans.fit(data)
    inertias.append(kmeans.inertia_)

plt.plot(range(1,11), inertias, marker='o')
plt.title('Elbow method')
plt.xlabel('Number of clusters')
plt.ylabel('Inertia')
plt.show()
```

Hasilnya : 


![image](https://github.com/uin-fah/docs-python/assets/119867794/4df7f5e9-f3fe-49e6-8337-3c70d2d78d65)

Kita dapat melihat bahwa "siku" pada grafik di atas (di mana interia menjadi lebih linier) berada pada K=2. Kita kemudian dapat menggunakan algoritma K-means sekali lagi dan memplotkan berbagai kelompok yang berbeda yang diberikan pada data:

```
kmeans = KMeans(n_clusters=2)
kmeans.fit(data)

plt.scatter(x, y, c=kmeans.labels_)
plt.show()
```

Hasilnya : 


![image](https://github.com/uin-fah/docs-python/assets/119867794/2dd03580-f645-4f1d-ac8a-5306c8f1ace3)




