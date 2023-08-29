# How to Remove Duplicates From a Python List

Pelajari cara menghapus duplikat dari sebuah List di Python.

Contoh

Menghapus duplikat apa pun dari Daftar:
```
mylist = ["a", "b", "a", "c", "c"]
mylist = list(dict.fromkeys(mylist))
print(mylist)
```
## Contoh Penjelasan
Pertama, kita memiliki sebuah Daftar yang berisi duplikat:

Daftar dengan Duplikat
```
mylist = ["a", "b", "a", "c", "c"]
mylist = list(dict.fromkeys(mylist))
print(mylist)
```
Buat kamus, dengan menggunakan item Daftar sebagai kunci. Hal ini akan secara otomatis menghapus semua duplikat karena kamus tidak boleh memiliki kunci duplikat.

Buat Kamus
```
mylist = ["a", "b", "a", "c", "c"]
mylist = list( dict.fromkeys(mylist) )
print(mylist)
```
Kemudian, ubah kembali kamus menjadi daftar:

Ubah Menjadi Daftar
```
mylist = ["a", "b", "a", "c", "c"]
mylist = list( dict.fromkeys(mylist) )
print(mylist)
```
Sekarang kita memiliki Daftar tanpa duplikat, dan memiliki urutan yang sama dengan Daftar asli.
Cetak Daftar untuk menunjukkan hasilnya

Cetak Daftar
```
mylist = ["a", "b", "a", "c", "c"]
mylist = list(dict.fromkeys(mylist))
print(mylist)
```
## Membuat Fungsi
Jika Anda ingin memiliki fungsi untuk mengirim daftar, dan mendapatkannya kembali tanpa duplikat, Anda dapat membuat fungsi dan menyisipkan kode dari contoh di atas.

Contoh
```
def my_function(x):
  return list(dict.fromkeys(x))

mylist = my_function(["a", "b", "a", "c", "c"])

print(mylist)
```
## Contoh Penjelasan

Membuat fungsi yang mengambil Daftar sebagai argumen.

Buat Fungsi
```
def my_function(x):
  return list(dict.fromkeys(x))

mylist = my_function(["a", "b", "a", "c", "c"])

print(mylist)
```
Buat kamus, dengan menggunakan item Daftar ini sebagai kunci.

Buat Kamus
```
def my_function(x):
  return list( dict.fromkeys(x) )

mylist = my_function(["a", "b", "a", "c", "c"])

print(mylist)
```
Mengonversi kamus menjadi daftar.

Ubah Menjadi Daftar
```
def my_function(x):
  return list( dict.fromkeys(x) )

mylist = my_function(["a", "b", "a", "c", "c"])

print(mylist)
```
Kembalikan daftar

Daftar Pengembalian
```
def my_function(x):
  return list(dict.fromkeys(x))

mylist = my_function(["a", "b", "a", "c", "c"])

print(mylist)
```
Panggil fungsi, dengan daftar sebagai parameter:

Panggil fungsi
```
def my_function(x):
  return list(dict.fromkeys(x))

mylist = my_function(["a", "b", "a", "c", "c"])

print(mylist)
```
Print the result:
```
def my_function(x):
  return list(dict.fromkeys(x))

mylist = my_function(["a", "b", "a", "c", "c"])

print(mylist)
```
