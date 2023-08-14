# Menghapus Dokumen Python MongoDB

**Menghapus Dokumen**

Untuk menghapus satu dokumen, kita menggunakan metode delete_one().

Parameter pertama dari metode delete_one() adalah sebuah objek kueri yang mendefinisikan dokumen mana yang akan dihapus.

**Contoh**

Hapus dokumen dengan alamat "Mountain 21":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Mountain 21" }

mycol.delete_one(myquery)
```

**Hapus Banyak Dokumen**

Untuk menghapus lebih dari satu dokumen, gunakan metode delete_many().

Parameter pertama dari metode delete_many() adalah sebuah objek kueri yang menentukan dokumen mana yang akan dihapus.


**Contoh**

Hapus semua dokumen yang alamatnya dimulai dengan huruf S:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": {"$regex": "^S"} }

x = mycol.delete_many(myquery)

print(x.deleted_count, " documents deleted.")
```


**Menghapus Semua Dokumen di dalam Koleksi**

Untuk menghapus semua dokumen dalam koleksi, berikan objek kueri kosong ke metode delete_many():

**Contoh**

Menghapus semua dokumen dalam koleksi "Costumers":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

x = mycol.delete_many({})

print(x.deleted_count, " documents deleted.")
```
