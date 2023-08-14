# Python MongoDB Update

**Perbarui Koleksi**

Anda dapat memperbarui catatan, atau dokumen, sebagaimana yang disebut di MongoDB, dengan menggunakan metode update_one().

Parameter pertama dari metode update_one() adalah objek kueri yang mendefinisikan dokumen mana yang akan diperbarui.

`
Catatan: Jika kueri menemukan lebih dari satu rekaman, hanya rekaman pertama yang diperbarui.
`

Parameter kedua adalah objek yang mendefinisikan nilai baru dokumen.


**Contoh**

Ubah alamat dari "Valley 345" ke "Canyon 123":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Valley 345" }
newvalues = { "$set": { "address": "Canyon 123" } }

mycol.update_one(myquery, newvalues)

#print "customers" after the update:
for x in mycol.find():
  print(x)
```

**Memperbarui banyak**

Untuk memperbarui semua dokumen yang memenuhi kriteria kueri, gunakan metode update_many().

**Contoh**

Perbarui semua dokumen yang alamatnya dimulai dengan huruf "S":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }
newvalues = { "$set": { "name": "Minnie" } }

x = mycol.update_many(myquery, newvalues)

print(x.modified_count, "documents updated.")
```

