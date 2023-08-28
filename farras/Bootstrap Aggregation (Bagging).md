# Bootstrap Aggregation (Bagging)

## Bagging
Metode seperti Decision Trees, dapat rentan terhadap overfitting pada set pelatihan yang dapat menyebabkan prediksi yang salah pada data baru.

Bootstrap Aggregation (bagging) adalah metode ensembling yang mencoba mengatasi overfitting untuk masalah klasifikasi atau regresi. Bagging bertujuan untuk meningkatkan akurasi dan kinerja algoritma machine learning. Hal ini dilakukan dengan mengambil subset acak dari dataset asli, dengan penggantian, dan mencocokkan pengklasifikasi (untuk klasifikasi) atau pengatur (untuk regresi) ke setiap subset. Prediksi untuk setiap subset kemudian digabungkan melalui suara mayoritas untuk klasifikasi atau rata-rata untuk regresi, sehingga meningkatkan akurasi prediksi.

## Mengevaluasi Klasifikasi Dasar
Untuk melihat bagaimana bagging dapat meningkatkan performa model, kita harus mulai dengan mengevaluasi performa pengklasifikasi dasar pada dataset. Jika Anda tidak mengetahui apa itu pohon keputusan, tinjau kembali pelajaran tentang pohon keputusan sebelum melangkah lebih jauh, karena bagging adalah kelanjutan dari konsep tersebut.

Kita akan mengidentifikasi berbagai kelas wine yang ditemukan dalam dataset wine Sklearn.

Mari kita mulai dengan mengimpor modul-modul yang diperlukan.

```
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
from sklearn.tree import DecisionTreeClassifier
```

Selanjutnya kita perlu memuat data dan menyimpannya ke dalam X (fitur input) dan y (target). Parameter as_frame diset sama dengan True sehingga kita tidak kehilangan nama fitur ketika memuat data. (versi sklearn yang lebih tua dari 0.23 harus melewatkan argumen as_frame karena tidak didukung)

```
data = datasets.load_wine(as_frame = True)

X = data.data
y = data.target
```

Untuk melakukan evaluasi model dengan benar pada data yang tidak terlihat, kita perlu membagi X dan y menjadi set data latih dan uji. Untuk informasi mengenai cara membagi data, lihat pelajaran Train/Test.

```
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state = 22)
```

Dengan data yang telah disiapkan, kita sekarang dapat membuat pengklasifikasi dasar dan menyesuaikannya dengan data pelatihan.

```
dtree = DecisionTreeClassifier(random_state = 22)
dtree.fit(X_train,y_train)
```

### Hasilnya

```
DecisionTreeClassifier(random_state=22)
```

Sekarang kita dapat memprediksi kelas wine yang tidak terlihat pada set uji coba dan mengevaluasi performa model.

```
y_pred = dtree.predict(X_test)

print("Train data accuracy:",accuracy_score(y_true = y_train, y_pred = dtree.predict(X_train)))
print("Test data accuracy:",accuracy_score(y_true = y_test, y_pred = y_pred))
```

Hasilnya

```
Train data accuracy: 1.0
Test data accuracy: 0.8222222222222222
```

### Contoh

Impor data yang diperlukan dan evaluasi kinerja pengklasifikasi dasar.

```
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
from sklearn.tree import DecisionTreeClassifier

data = datasets.load_wine(as_frame = True)

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state = 22)

dtree = DecisionTreeClassifier(random_state = 22)
dtree.fit(X_train,y_train)

y_pred = dtree.predict(X_test)

print("Train data accuracy:",accuracy_score(y_true = y_train, y_pred = dtree.predict(X_train)))
print("Test data accuracy:",accuracy_score(y_true = y_test, y_pred = y_pred))
```

Pengklasifikasi dasar berkinerja cukup baik pada dataset yang mencapai akurasi 82% pada dataset uji dengan parameter saat ini (Hasil yang berbeda dapat terjadi jika Anda tidak mengatur parameter random_state).

Sekarang kita memiliki akurasi dasar untuk dataset uji, kita dapat melihat bagaimana kinerja Bagging Classifier dari Decision Tree Classifier.

## Membuat Klasifikasi Bagging (Bagging Classifier)
Untuk bagging kita perlu mengatur parameter n_estimator, ini adalah jumlah pengklasifikasi dasar yang akan digabungkan oleh model kita.

Untuk dataset sampel ini, jumlah estimator relatif rendah, sering kali rentang yang dieksplorasi jauh lebih besar. Penyetelan hiperparameter biasanya dilakukan dengan pencarian grid, tetapi untuk saat ini kita akan menggunakan satu set nilai tertentu untuk jumlah penaksir.

Kita mulai dengan mengimpor model yang diperlukan.

```
from sklearn.ensemble import BaggingClassifier
```

Sekarang mari kita buat rentang nilai yang mewakili jumlah penaksir yang ingin kita gunakan dalam setiap ansambel.

```
estimator_range = [2,4,6,8,10,12,14,16]
```

Untuk melihat bagaimana kinerja Bagging Classifier dengan nilai n_estimator yang berbeda-beda, kita membutuhkan cara untuk mengulang-ulang rentang nilai dan menyimpan hasil dari setiap ensemble. Untuk melakukan hal ini, kita akan membuat perulangan for, menyimpan model dan nilai dalam daftar terpisah untuk visualisasi selanjutnya.

Catatan: Parameter standar untuk klasifikasi dasar di BaggingClassifier adalah DicisionTreeClassifier, oleh karena itu kita tidak perlu mengaturnya saat menginstansiasi model bagging.

```
models = []
scores = []

for n_estimators in estimator_range:

    # Create bagging classifier
    clf = BaggingClassifier(n_estimators = n_estimators, random_state = 22)

    # Fit the model
    clf.fit(X_train, y_train)

    # Append the model and score to their respective list
    models.append(clf)
    scores.append(accuracy_score(y_true = y_test, y_pred = clf.predict(X_test)))
```

Dengan model dan skor yang tersimpan, kita sekarang dapat memvisualisasikan peningkatan kinerja model.

```
import matplotlib.pyplot as plt

# Generate the plot of scores against number of estimators
plt.figure(figsize=(9,6))
plt.plot(estimator_range, scores)

# Adjust labels and font (to make visable)
plt.xlabel("n_estimators", fontsize = 18)
plt.ylabel("score", fontsize = 18)
plt.tick_params(labelsize = 16)

# Visualize plot
plt.show()
```

![image](https://github.com/uin-fah/docs-python/assets/119867794/cabccfb7-828e-45a3-8d54-dc33e5992b57)


### Contoh 
Impor data yang diperlukan dan evaluasi kinerja BaggingClassifier.

```
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
from sklearn.ensemble import BaggingClassifier

data = datasets.load_wine(as_frame = True)

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state = 22)

estimator_range = [2,4,6,8,10,12,14,16]

models = []
scores = []

for n_estimators in estimator_range:

    # Create bagging classifier
    clf = BaggingClassifier(n_estimators = n_estimators, random_state = 22)

    # Fit the model
    clf.fit(X_train, y_train)

    # Append the model and score to their respective list
    models.append(clf)
    scores.append(accuracy_score(y_true = y_test, y_pred = clf.predict(X_test)))

# Generate the plot of scores against number of estimators
plt.figure(figsize=(9,6))
plt.plot(estimator_range, scores)

# Adjust labels and font (to make visable)
plt.xlabel("n_estimators", fontsize = 18)
plt.ylabel("score", fontsize = 18)
plt.tick_params(labelsize = 16)

# Visualize plot
plt.show()
```

### Hasilnya

![image](https://github.com/uin-fah/docs-python/assets/119867794/89b9429e-d625-475e-90e1-4a1d586d0f76)

## Penjelasan Hasil
Dengan melakukan iterasi melalui nilai yang berbeda untuk jumlah penaksir, kita dapat melihat peningkatan performa model dari 82,2% menjadi 95,5%. Setelah 14 penaksir, akurasi mulai menurun, sekali lagi jika Anda menetapkan random_state yang berbeda, nilai yang Anda lihat akan bervariasi. Itulah mengapa praktik terbaiknya adalah menggunakan validasi silang untuk memastikan hasil yang stabil.

Dalam kasus ini, kami melihat peningkatan akurasi sebesar 13,3% dalam hal mengidentifikasi jenis wine.

## Bentuk Evaluasi Lainnya
Karena bootstrapping memilih subset pengamatan secara acak untuk membuat pengklasifikasi, ada beberapa pengamatan yang tidak diikutsertakan dalam proses seleksi. Pengamatan yang "tidak masuk" ini kemudian dapat digunakan untuk mengevaluasi model, sama halnya dengan set pengujian. Perlu diingat, bahwa estimasi out-of-bag dapat melebih-lebihkan kesalahan dalam masalah klasifikasi biner dan hanya boleh digunakan sebagai pelengkap untuk metrik lainnya.

Kita telah melihat pada latihan terakhir bahwa 12 estimator menghasilkan akurasi tertinggi, jadi kita akan menggunakannya untuk membuat model kita. Kali ini kita akan mengatur parameter oob_score menjadi true untuk mengevaluasi model dengan nilai di luar kantong.

### Contoh 

Buat model tanpa bag-metric

```
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.ensemble import BaggingClassifier

data = datasets.load_wine(as_frame = True)

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state = 22)

oob_model = BaggingClassifier(n_estimators = 12, oob_score = True,random_state = 22)

oob_model.fit(X_train, y_train)

print(oob_model.oob_score_)
```
Karena sampel yang digunakan dalam OOB dan set pengujian berbeda, dan datasetnya relatif kecil, maka ada perbedaan dalam akurasinya. Jarang sekali keduanya akan sama persis, sekali lagi OOB harus digunakan sebagai cara cepat untuk memperkirakan kesalahan, tetapi bukan satu-satunya metrik evaluasi.

## Menghasilkan Pohon Keputusan dari Pengklasifikasi Bagging
Seperti yang telah dilihat dalam pelajaran Pohon Keputusan, adalah mungkin untuk membuat grafik pohon keputusan dari model yang telah dibuat. Kita juga dapat melihat pohon keputusan individual yang masuk ke dalam pengklasifikasi agregat. Hal ini membantu kita untuk mendapatkan pemahaman yang lebih intuitif tentang bagaimana model bagging sampai pada prediksinya.

Catatan: Ini hanya berfungsi pada dataset yang lebih kecil, di mana pohon-pohonnya relatif dangkal dan sempit sehingga mudah divisualisasikan.

Kita perlu mengimpor fungsi plot_tree dari sklearn.tree. Pohon-pohon yang berbeda dapat dibuat grafiknya dengan mengubah estimator yang ingin Anda visualisasikan.

### Contoh
Menghasilkan Pohon Keputusan dari Klasifikasi Bagging


```
from sklearn import datasets
from sklearn.model_selection import train_test_split
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import plot_tree

X = data.data
y = data.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25, random_state = 22)

clf = BaggingClassifier(n_estimators = 12, oob_score = True,random_state = 22)

clf.fit(X_train, y_train)

plt.figure(figsize=(30, 20))

plot_tree(clf.estimators_[0], feature_names = X.columns)
```

### Hasilnya

![image](https://github.com/uin-fah/docs-python/assets/119867794/706d9966-2642-4bc1-805c-612775e93931)
