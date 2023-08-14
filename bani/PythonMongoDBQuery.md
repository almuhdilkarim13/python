# Python MongoDB Query

Menyaring Hasil
Saat menemukan dokumen dalam koleksi, Anda dapat menyaring hasilnya dengan menggunakan objek kueri.

Argumen pertama dari metode find() adalah objek kueri, dan digunakan untuk membatasi pencarian.

**Contoh
Temukan dokumen dengan alamat "Park Lane 38":**

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": "Park Lane 38" }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)
```

**Kueri Tingkat Lanjut
Untuk membuat kueri lanjutan, Anda dapat menggunakan pengubah sebagai nilai dalam objek kueri.
Misalnya, untuk menemukan dokumen di mana bidang "alamat" dimulai dengan huruf "S" atau lebih tinggi (menurut abjad), gunakan pengubah greater than: {"$gt": "S"}:**

**Contoh
Temukan dokumen yang alamatnya dimulai dengan huruf "S" atau lebih tinggi:**

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$gt": "S" } }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)
```

**Menyaring Dengan Ekspresi Reguler
Anda juga dapat menggunakan ekspresi reguler sebagai pengubah.**

`
Ekspresi reguler hanya dapat digunakan untuk menanyakan string.
`

Untuk menemukan hanya dokumen yang bidang "alamat" dimulai dengan huruf "S", gunakan ekspresi reguler {"$regex": "^S"}:

**Contoh
Temukan dokumen yang alamatnya dimulai dengan huruf "S":**

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }

mydoc = mycol.find(myquery)

for x in mydoc:
  print(x)
```
