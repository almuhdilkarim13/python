# Python MongoDB Sort

**Sortir Hasil**

Gunakan metode sort() untuk mengurutkan hasil dalam urutan menaik atau menurun.

Metode sort() mengambil satu parameter untuk "nama bidang" dan satu parameter untuk "arah" (menaik adalah arah default).

**Contoh**

Urutkan hasilnya menurut abjad berdasarkan nama:
```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydoc = mycol.find().sort("name")

for x in mydoc:
  print(x)
```

**Urutkan Turun**

Gunakan nilai -1 sebagai parameter kedua untuk mengurutkan menurun.

`
sort("name", 1) #ascending
sort("name", -1) #descending
`

**Contoh**

Urutkan hasilnya secara terbalik menurut abjad nama:

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydoc = mycol.find().sort("name", -1)

for x in mydoc:
  print(x)
```
