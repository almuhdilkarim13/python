# AUC - ROC Curve

Dalam klasifikasi, ada banyak metrik evaluasi yang berbeda. Yang paling populer adalah akurasi, yang mengukur seberapa sering model tersebut benar. Ini adalah metrik yang bagus karena mudah dipahami dan mendapatkan tebakan yang paling benar sering kali diinginkan. Ada beberapa kasus di mana Anda dapat mempertimbangkan untuk menggunakan metrik evaluasi lain.

Metrik umum lainnya adalah AUC, area di bawah kurva karakteristik operasi penerima (ROC). Kurva karakteristik operasi penerima memplot tingkat true positive (TP) versus false positive (FP) pada ambang batas klasifikasi yang berbeda. Ambang batas adalah batas probabilitas yang berbeda yang memisahkan dua kelas dalam klasifikasi biner. Kurva ini menggunakan probabilitas untuk memberi tahu kita seberapa baik sebuah model memisahkan kelas.

## Data Tidak Seimbang
Misalkan kita memiliki kumpulan data yang tidak seimbang di mana mayoritas data kita memiliki satu nilai. Kita dapat memperoleh akurasi yang tinggi untuk model dengan memprediksi kelas mayoritas.

### Contoh

```
import numpy as np
from sklearn.metrics import accuracy_score, confusion_matrix, roc_auc_score, roc_curve

n = 10000
ratio = .95
n_0 = int((1-ratio) * n)
n_1 = int(ratio * n)

y = np.array([0] * n_0 + [1] * n_1)
# below are the probabilities obtained from a hypothetical model that always predicts the majority class
# probability of predicting class 1 is going to be 100%
y_proba = np.array([1]*n)
y_pred = y_proba > .5

print(f'accuracy score: {accuracy_score(y, y_pred)}')
cf_mat = confusion_matrix(y, y_pred)
print('Confusion matrix')
print(cf_mat)
print(f'class 0 accuracy: {cf_mat[0][0]/n_0}')
print(f'class 1 accuracy: {cf_mat[1][1]/n_1}')
```

Meskipun kami mendapatkan akurasi yang sangat tinggi, model tidak memberikan informasi tentang data sehingga tidak berguna. Kami secara akurat memprediksi kelas 1 100% dari waktu ke waktu, sementara secara tidak akurat memprediksi kelas 0 0% dari waktu ke waktu. Dengan mengorbankan akurasi, mungkin akan lebih baik untuk memiliki model yang dapat memisahkan kedua kelas tersebut.

### Contoh 

```
# below are the probabilities obtained from a hypothetical model that doesn't always predict the mode
y_proba_2 = np.array(
    np.random.uniform(0, .7, n_0).tolist() +
    np.random.uniform(.3, 1, n_1).tolist()
)
y_pred_2 = y_proba_2 > .5

print(f'accuracy score: {accuracy_score(y, y_pred_2)}')
cf_mat = confusion_matrix(y, y_pred_2)
print('Confusion matrix')
print(cf_mat)
print(f'class 0 accuracy: {cf_mat[0][0]/n_0}')
print(f'class 1 accuracy: {cf_mat[1][1]/n_1}')
```

Untuk set prediksi kedua, kami tidak memiliki nilai akurasi setinggi yang pertama, tetapi akurasi untuk setiap kelas lebih seimbang. Dengan menggunakan akurasi sebagai metrik evaluasi, kami akan menilai model pertama lebih tinggi daripada model kedua meskipun model tersebut tidak memberi tahu kami apa pun tentang data.

Dalam kasus seperti ini, menggunakan metrik evaluasi lain seperti AUC akan lebih disukai.

```
import matplotlib.pyplot as plt

def plot_roc_curve(true_y, y_prob):
    """
    plots the roc curve based of the probabilities
    """

    fpr, tpr, thresholds = roc_curve(true_y, y_prob)
    plt.plot(fpr, tpr)
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
```

### Contoh

Model 1 :

```
plot_roc_curve(y, y_proba)
print(f'model 1 AUC score: {roc_auc_score(y, y_proba)}')
```
### Hasilnya

![image](https://github.com/uin-fah/docs-python/assets/119867794/3cd7c9a3-c6cc-4a67-b225-923d9320c81c)

### Contoh
Model 2 :

```
plot_roc_curve(y, y_proba_2)
print(f'model 2 AUC score: {roc_auc_score(y, y_proba_2)}')
```

### Hasilnya 
![image](https://github.com/uin-fah/docs-python/assets/119867794/e939432d-8361-4dc3-8b2e-841db4128dfe)

Nilai AUC sekitar 0,5 berarti model tidak dapat membuat perbedaan antara dua kelas dan kurva akan terlihat seperti garis dengan kemiringan 1. Nilai AUC yang lebih dekat ke 1 berarti model memiliki kemampuan untuk memisahkan dua kelas dan kurva akan lebih dekat ke sudut kiri atas grafik.

## Probabilitas
Karena AUC adalah metrik yang menggunakan probabilitas dari prediksi kelas, kita dapat lebih percaya diri dengan model yang memiliki skor AUC yang lebih tinggi daripada model yang memiliki skor yang lebih rendah meskipun memiliki akurasi yang sama.

Pada data di bawah ini, kita memiliki dua set probabilitas dari model hipotetis. Yang pertama memiliki probabilitas yang tidak terlalu "percaya diri" saat memprediksi dua kelas (probabilitasnya mendekati 0,5). Yang kedua memiliki probabilitas yang lebih "percaya diri" saat memprediksi dua kelas (probabilitasnya mendekati nilai ekstrem 0 atau 1).

### Contohnya

```
import numpy as np

n = 10000
y = np.array([0] * n + [1] * n)
#
y_prob_1 = np.array(
    np.random.uniform(.25, .5, n//2).tolist() +
    np.random.uniform(.3, .7, n).tolist() +
    np.random.uniform(.5, .75, n//2).tolist()
)
y_prob_2 = np.array(
    np.random.uniform(0, .4, n//2).tolist() +
    np.random.uniform(.3, .7, n).tolist() +
    np.random.uniform(.6, 1, n//2).tolist()
)

print(f'model 1 accuracy score: {accuracy_score(y, y_prob_1>.5)}')
print(f'model 2 accuracy score: {accuracy_score(y, y_prob_2>.5)}')

print(f'model 1 AUC score: {roc_auc_score(y, y_prob_1)}')
print(f'model 2 AUC score: {roc_auc_score(y, y_prob_2)}')
```

### Contohnya

Plot model 1 :
```
plot_roc_curve(y, y_prob_1)
```

### Hasilnya

![image](https://github.com/uin-fah/docs-python/assets/119867794/8d6c815c-7dd3-45c0-af34-7f4d83586f18)

### Contohnya 
Plot model 2 :

```
fpr, tpr, thresholds = roc_curve(y, y_prob_2)
plt.plot(fpr, tpr)
```

### Hasilnya 

![image](https://github.com/uin-fah/docs-python/assets/119867794/e835d50f-1a4a-4318-908d-458c334749d1)



Meskipun akurasi untuk kedua model ini serupa, model dengan nilai AUC yang lebih tinggi akan lebih dapat diandalkan karena memperhitungkan probabilitas yang diprediksi. Hal ini akan memberikan akurasi yang lebih tinggi ketika memprediksi data di masa depan.

