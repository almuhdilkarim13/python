# Cross Validation

Ketika menyesuaikan model, kami bertujuan untuk meningkatkan kinerja model secara keseluruhan pada data yang tidak terlihat. Penyetelan hiperparameter dapat menghasilkan kinerja yang jauh lebih baik pada set pengujian. Namun, mengoptimalkan parameter pada set pengujian dapat menyebabkan kebocoran informasi yang menyebabkan model berkinerja lebih buruk pada data yang tidak terlihat. Untuk mengoreksi hal ini, kita dapat melakukan validasi silang.

Untuk lebih memahami CV, kita akan melakukan metode yang berbeda pada dataset iris. Pertama-tama, mari kita muat dan pisahkan datanya.

```
from sklearn import datasets

X, y = datasets.load_iris(return_X_y=True)
```

## K-Fold

Data pelatihan yang digunakan dalam model dibagi menjadi k set yang lebih kecil, yang akan digunakan untuk memvalidasi model. Model kemudian dilatih pada k-1 lipatan set pelatihan. Fold yang tersisa kemudian digunakan sebagai set validasi untuk mengevaluasi model.

Karena kita akan mencoba mengklasifikasikan spesies bunga iris yang berbeda, kita perlu mengimpor model pengklasifikasi, untuk latihan ini kita akan menggunakan DecisionTreeClassifier. Kita juga perlu mengimpor modul CV dari sklearn

```
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import KFold, cross_val_score
```

Dengan data yang dimuat, kita sekarang dapat membuat dan menyesuaikan model untuk evaluasi.

```
clf = DecisionTreeClassifier(random_state=42)
```

Sekarang mari kita mengevaluasi model kita dan melihat bagaimana kinerjanya pada setiap k-lipatan.

```
k_folds = KFold(n_splits = 5)

scores = cross_val_score(clf, X, y, cv = k_folds)
```

Ini juga merupakan praktik yang baik untuk melihat bagaimana kinerja CV secara keseluruhan dengan rata-rata skor untuk semua lipatan.


### Contoh
jalankan K-fold CV 
```
from sklearn import datasets
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import KFold, cross_val_score

X, y = datasets.load_iris(return_X_y=True)

clf = DecisionTreeClassifier(random_state=42)

k_folds = KFold(n_splits = 5)

scores = cross_val_score(clf, X, y, cv = k_folds)

print("Cross Validation Scores: ", scores)
print("Average CV Score: ", scores.mean())
print("Number of CV Scores used in Average: ", len(scores))
```

## Stratifikasi K-Fold

Dalam kasus di mana kelas-kelas tidak seimbang, kita membutuhkan cara untuk memperhitungkan ketidakseimbangan dalam set pelatihan dan validasi. Untuk melakukannya, kita dapat membuat stratifikasi kelas target, yang berarti bahwa kedua set akan memiliki proporsi yang sama dari semua kelas.

### Contohnya
```
from sklearn import datasets
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import StratifiedKFold, cross_val_score

X, y = datasets.load_iris(return_X_y=True)

clf = DecisionTreeClassifier(random_state=42)

sk_folds = StratifiedKFold(n_splits = 5)

scores = cross_val_score(clf, X, y, cv = sk_folds)

print("Cross Validation Scores: ", scores)
print("Average CV Score: ", scores.mean())
print("Number of CV Scores used in Average: ", len(scores))
```

Meskipun jumlah lipatannya sama, rata-rata CV meningkat dari k-fold dasar ketika memastikan adanya kelas bertingkat.

## Lepaskan-Satu-Keluar (LOO)

Alih-alih memilih jumlah pemisahan dalam set data pelatihan seperti k-fold LeaveOneOut, gunakan 1 pengamatan untuk memvalidasi dan n-1 pengamatan untuk melatih. Metode ini adalah teknik yang melelahkan.

### Contohnya

Jalankan LOO CV

```
from sklearn import datasets
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import LeaveOneOut, cross_val_score

X, y = datasets.load_iris(return_X_y=True)

clf = DecisionTreeClassifier(random_state=42)

loo = LeaveOneOut()

scores = cross_val_score(clf, X, y, cv = loo)

print("Cross Validation Scores: ", scores)
print("Average CV Score: ", scores.mean())
print("Number of CV Scores used in Average: ", len(scores))
```

Kita dapat mengamati bahwa jumlah skor validasi silang yang dilakukan sama dengan jumlah pengamatan dalam dataset. Dalam hal ini ada 150 pengamatan dalam dataset iris.

Skor CV rata-rata adalah 94%.

## Leave-P-Out (LPO)
Leave-P-Out adalah perbedaan yang sederhana dari ide Leave-One-Out, di mana kita dapat memilih jumlah p yang akan digunakan dalam set validasi kita.

### Contohnya
Jalankan LPO CV

```
from sklearn import datasets
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import LeavePOut, cross_val_score

X, y = datasets.load_iris(return_X_y=True)

clf = DecisionTreeClassifier(random_state=42)

lpo = LeavePOut(p=2)

scores = cross_val_score(clf, X, y, cv = lpo)

print("Cross Validation Scores: ", scores)
print("Average CV Score: ", scores.mean())
print("Number of CV Scores used in Average: ", len(scores))
```

Seperti yang bisa kita lihat, ini adalah metode yang lengkap, lebih banyak skor yang dihitung daripada Leave-One-Out, bahkan dengan p = 2, namun metode ini menghasilkan skor CV rata-rata yang kurang lebih sama.

## Pembagian Acak (Shuffle Split)

Tidak seperti KFold, ShuffleSplit membuang sebagian data, tidak untuk digunakan dalam set pelatihan atau validasi. Untuk melakukannya, kita harus menentukan ukuran train dan test, serta jumlah split.

### Contohnya 

Jalankan Shuffle Split CV

```
from sklearn import datasets
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import ShuffleSplit, cross_val_score

X, y = datasets.load_iris(return_X_y=True)

clf = DecisionTreeClassifier(random_state=42)

ss = ShuffleSplit(train_size=0.6, test_size=0.3, n_splits = 5)

scores = cross_val_score(clf, X, y, cv = ss)

print("Cross Validation Scores: ", scores)
print("Average CV Score: ", scores.mean())
print("Number of CV Scores used in Average: ", len(scores))
```

## Catatan Akhir

Ini hanyalah beberapa metode CV yang dapat diterapkan pada model. Masih banyak lagi kelas validasi silang, dengan sebagian besar model memiliki kelasnya sendiri. Lihat sklearns cross validation untuk opsi CV lainnya.


