# Membuat Koleksi
Untuk membuat koleksi di MongoDB, gunakan objek database dan tentukan nama koleksi yang ingin Anda buat.

MongoDB akan membuat koleksi jika koleksi tersebut belum ada.

### Contoh
Mendapatkan Server Python Anda sendiri
Buat koleksi bernama "customer" :

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]

mycol = mydb["customers"]
```

**Penting: Di MongoDB, koleksi tidak akan dibuat hingga koleksi tersebut memiliki konten!**

MongoDB menunggu hingga Anda memasukkan dokumen sebelum benar-benar membuat koleksi.


## Memeriksa apakah koleksi sudah ada
**Ingat**: Di MongoDB, koleksi tidak akan dibuat hingga koleksi tersebut memiliki konten, jadi jika ini adalah kali pertama Anda membuat koleksi, Anda harus menyelesaikan bab berikutnya (membuat dokumen) sebelum memeriksa apakah koleksi tersebut sudah ada!

Anda dapat memeriksa apakah koleksi sudah ada di basis data dengan membuat daftar semua koleksi:

```
print(mydb.list_collection_names())
```

Atau Anda dapat memeriksa koleksi tertentu berdasarkan nama:

### Contoh
Memeriksa apakah koleksi "customer" ada:

```
collist = mydb.list_collection_names()
if "customers" in collist:
  print("The collection exists.")
```
