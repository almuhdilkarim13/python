# Membuat Basis Data

Untuk membuat basis data di MongoDB, mulailah dengan membuat objek MongoClient, lalu tentukan URL koneksi dengan alamat ip yang benar dan nama basis data yang ingin Anda buat.

MongoDB akan membuat basis data jika belum ada, dan membuat koneksi ke basis data tersebut.

### Contoh
membuat database dengan mengetik "mydatabase"

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")

mydb = myclient["mydatabase"]
```

**Penting: Di MongoDB, basis data tidak akan dibuat hingga mendapatkan konten!**

MongoDB menunggu hingga Anda membuat koleksi (tabel), dengan setidaknya satu dokumen (record) sebelum benar-benar membuat basis data (dan koleksi). 


## Memeriksa apakah basis data sudah ada
Ingat: Di MongoDB, basis data tidak akan dibuat sampai basis data tersebut memiliki konten, jadi jika ini pertama kalinya Anda membuat basis data, Anda harus menyelesaikan dua bab berikutnya (membuat koleksi dan membuat dokumen) sebelum memeriksa apakah basis data sudah ada!

Anda dapat memeriksa keberadaan basis data dengan membuat daftar semua basis data di sistem Anda:


Mengembalikan daftar basis data sistem Anda:


```
print(myclient.list_database_names())
```

### Contoh
Periksa apakah "mydatabase" ada:

```
dblist = myclient.list_database_names()
if "mydatabase" in dblist:
  print("The database exists.")
```
