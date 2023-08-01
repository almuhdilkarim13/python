# Polynomial Regression
Apabila seluruh titik data Anda tidak cocok dengan regresi linier (garis lurus yang melalui seluruh titik data), sebaiknya gunakan regresi polinomial. Regresi polinomial, mirip dengan regresi linier, memakai hubungan antara variabel x dan y untuk menemukan cara terbaik dalam menarik garis melalui titik-titik datanya. 

![Screenshot (68)](https://github.com/gitfah/docs-python/assets/119867794/a3f22e10-8580-43d2-9552-0ca79125e72e)

**Bagaimana Cara Kerjanya?**
Python punya metode untuk menentukan hubungan antara titik-titik data dan menggambar garis regresi polinomial. Kami dapat tunjukkan cara menggunakan teknik ini ketimbang menggunakan rumus matematika.

Pada contoh dibawah ini, kami telah mencatat 18 mobil yang akan melewati pintu tol tertentu.
Kami telah mencatat kecepatan mobil, dan waktu (jam) saat mobil tersebut melintas.
Sumbu x mewakili jam dalam sehari dan sumbu y mewakili kecepatan:
**Contoh** 
Mulailah dengan menggambar scatter plot: 
```Example
Start by drawing a scatter plot:

import matplotlib.pyplot as plt 

x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

plt.scatter(x, y)
plt.show()
```

**Hasilnya**
![Screenshot (66)](https://github.com/gitfah/docs-python/assets/119867794/4adad90b-3286-4744-ad4d-962a9444551c) 

Contoh :
Masukkan **numpy** dan **matplotlib** kemudian tarik garis Regresi Polinomial:
```import numpy
import matplotlib.pyplot as plt

x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

myline = numpy.linspace(1, 22, 100)

plt.scatter(x, y)
plt.plot(myline, mymodel(myline))
plt.show()
```

Hasilnya :
![img_polynomial_regression](https://github.com/gitfah/docs-python/assets/119867794/07009204-8250-4001-b6f7-76e3817430ed)

COntoh dan Penjelasan
pertama pilihlah ,odul yang anda butuhkan
anda dapat memahami tentang modul **Numpy** yang bisa diakses di [tutorial NumPy](https://www.w3schools.com/python/numpy/default.asp)
anda bisa mempelajari **SciPy** yang tersedia di [tutorial SciPy](https://www.w3schools.com/python/scipy_intro.asp)

```import numpy
import matplotlib.pyplot as plt
```
Buatlah susunan yang mewakili nilai sumbu x dan y:
```x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]
```

NumPy mempunyai metode yang dapat digunakan untuk membuat model polinomial:
```
mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))
```

Kemudian, menentukan bagaimana garis akan disajikan, kita mulai dari posisi 1, dan berakhir pada posisi 22:
```
myline = numpy.linspace(1, 22, 100)
```

Gambarlah  sebaran plot  aslinya:
```
plt.scatter(x,y)
```

 Gambarlah garis regresi polinomial:
```
plt.plot(myline, mymodel(myline))
```
plt.plot(myline, mymodel (myline)

Tampilan diagram
```
plt.show
```

**R-Squared**
Penting untuk mengetahui sebarapa besar hubungan antara sumbu x dan sumbu y. Jika tidak ada hubungan, regresi polinomial tidak dapat digunakan untuk memprediksi apa pun.
Hubungan tersebut diukur dengan nilai yang disebut r-kuadrat.
Nilai r-squared berkisar antara 0 hingga 1, nilai 0 berarti tidak ada hubungan, dan nilai 1 berarti 100% berhubungan.
Python dan modul Sklearn akan menghitung nilai ini untuk Anda, yang harus Anda lakukan adalah mengisinya dengan data x dan y:

Contoh
Bagaimana kecocokan data yang saya miliki dengan regresi polinomial?
```import numpy
from sklearn.metrics import r2_score
x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

print(r2_score(y, mymodel(x)))
```
**Note** Hasil 0,94 menunjukkan bahwa ada hubungan yang sangat baik, dan kita dapat menggunakan regresi polinomial dalam memprediksi kedepannya.

**Memperkirakan Nilai selanjutnya **
Memperkirakan Potensi Nilai di Waktu yang Akan Datang. 
Sekarang kita dapat menggunakan informasi yang telah kita kumpulkan untuk memprediksi nilai di kemudian hari. 
Contoh: Misalnya kita ingin memprediksi kecepatan sebuah mobil yang melewati jalan tol sekitaran jam 17:00:
Untuk melakukan hal tersebut, kita membutuhkan susunan mymodel yang sama dengan contoh di atas:

```
mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))
```
Contoh:
Predikasi kecepatan mobil yang lewat sekitar jam 17:00 
```
import numpy
from sklearn.metrics import r2_score

x = [1,2,3,5,6,7,8,9,10,12,13,14,15,16,18,19,21,22]
y = [100,90,80,60,60,55,60,65,70,70,75,76,78,79,90,99,99,100]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

speed = mymodel(17)
print(speed)
```
Contoh tersebut memprediksi kecepatan menjadi 88,87, dimana kecepatan tersebut juga dapat kita lihat pada diagram: 

![img_polynomial_prediction](https://github.com/uin-fah/docs-python/assets/119867794/dbcbb8e1-511e-477a-b361-0ac4d844196a)

**Tidak Cocok?**
Kurang Cocok?
Mari kita buat Contoh di mana regresi polinomial tidak akan menjadi metode terbaik untuk memperkirakan nilai di kemudian hari.
Contoh: Nilai-nilai ini untuk sumbu x dan y akan menghasilkan nilai yang kurang cocok untuk regresi polinomial
```
import numpy
import matplotlib.pyplot as plt

x = [89,43,36,36,95,10,66,34,38,20,26,29,48,64,6,5,36,66,72,40]
y = [21,46,3,35,67,95,53,72,58,10,26,34,90,33,38,20,56,2,47,15]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

myline = numpy.linspace(2, 95, 100)

plt.scatter(x, y)
plt.plot(myline, mymodel(myline))
plt.show()
```
Hasilnya: 
![img_polynomial_badfit](https://github.com/uin-fah/docs-python/assets/119867794/5ded7084-607f-4edf-a69c-dd83690907ae)

nilai r-kuadrat?
Contoh:
Mestinya Anda mendapatkan nilai r-kuadrat yang relatif rendah.
```
import numpy
from sklearn.metrics import r2_score

x = [89,43,36,36,95,10,66,34,38,20,26,29,48,64,6,5,36,66,72,40]
y = [21,46,3,35,67,95,53,72,58,10,26,34,90,33,38,20,56,2,47,15]

mymodel = numpy.poly1d(numpy.polyfit(x, y, 3))

print(r2_score(y, mymodel(x)))
```







