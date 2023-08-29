# How to Reverse a String in Python

## Pelajari cara membalikkan String di Python.

<p>Tidak ada fungsi bawaan untuk membalikkan String dalam Python.
Cara tercepat (dan termudah?) adalah dengan menggunakan irisan yang melangkah mundur, -1.</p>

Contoh

Membalikkan string "Halo Dunia":
```
txt = "Hello World"[::-1]
print(txt)
```
## Contoh Penjelasan
Kita memiliki sebuah string, "Hello World", yang ingin kita balikkan:

String untuk Membalikkan
```
txt = "Hello World" [::-1]
print(txt)
```

Membuat irisan yang dimulai dari akhir string, dan bergerak mundur.

Dalam contoh khusus ini, pernyataan irisan [::-1] berarti mulai dari akhir string dan berakhir di posisi 0, bergerak dengan langkah -1, negatif, yang berarti satu langkah mundur.

Potong Stringnya
```
txt = "Hello World" [::-1]
print(txt)
```

Sekarang kita memiliki txt string yang berbunyi "Hello World" secara terbalik.

Cetak String untuk mendemonstrasikan hasilnya

```
txt = "Hello World"[::-1]
print(txt)
```
## Membuat Fungsi
Jika Anda ingin memiliki fungsi untuk mengirim string dan mengembalikannya secara terbalik, Anda dapat membuat fungsi dan menyisipkan kode dari contoh di atas.

Contoh
```
def my_function(x):
  return x[::-1]

mytxt = my_function("I wonder how this text looks like backwards")

print(mytxt)
```
## Contoh Penjelasan

Membuat fungsi yang mengambil String sebagai argumen.

Buat Fungsi
```
def my_function(x):
  return x[::-1]

mytxt = my_function("I wonder how this text looks like backwards")

print(mytxt)
```

Potong String mulai dari ujung senar dan gerakkan ke belakang.

Potong Stringnya
```
def my_function(x):
  return x [::-1]

mytxt = my_function("I wonder how this text looks like backwards")

print(mytxt)
```

Mengembalikan String mundur

Kembalikan Stringnya
```
def my_function(x):
  return x[::-1]

mytxt = my_function("I wonder how this text looks like backwards")

print(mytxt )
```

Panggil fungsi, dengan string sebagai parameter:

Panggil Fungsinya
```
def my_function(x):
  return x[::-1]

mytxt = my_function("I wonder how this text looks like backwards")

print(mytxt)
```

Cetak Hasil
```
def my_function(x):
  return x[::-1]

mytxt = my_function("I wonder how this text looks like backwards")

print(mytxt)
```
