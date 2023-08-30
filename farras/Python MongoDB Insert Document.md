# Python MongoDB Insert Document

## Menyisipkan ke dalam Koleksi
Untuk menyisipkan catatan, atau dokumen sebagaimana disebut di MongoDB, ke dalam koleksi, kita menggunakan metode `insert_one()`

Parameter pertama dari metode `insert_one()` adalah sebuah kamus yang berisi nama dan nilai dari setiap field di dalam dokumen yang ingin Anda sisipkan.

### Contoh 
Dapatkan Server Python Anda sendiri
Sisipkan catatan dalam koleksi "customer":

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mydict = { "name": "John", "address": "Highway 37" }

x = mycol.insert_one(mydict)
```

Mengembalikan Bidang _id
Metode `insert_one()` mengembalikan objek InsertOneResult, yang memiliki properti, `inserted_id`, yang menyimpan id dokumen yang disisipkan.

### Contoh 

```
mydict = { "name": "Peter", "address": "Lowstreet 27" }

x = mycol.insert_one(mydict)

print(x.inserted_id)
```

Jika Anda tidak menentukan bidang `_id`, maka MongoDB akan menambahkannya untuk Anda dan memberikan id unik untuk setiap dokumen.

Pada contoh di atas, tidak ada bidang `_id` yang ditentukan, sehingga MongoDB menetapkan id unik untuk catatan (dokumen).


## Menyisipkan Beberapa Dokumen
Untuk menyisipkan banyak dokumen ke dalam koleksi di MongoDB, kita menggunakan metode `insert_many()`.

Parameter pertama dari metode `insert_many()` adalah sebuah daftar yang berisi kamus dengan data yang ingin Anda masukkan:

### Contoh 

```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mylist = [
  { "name": "Amy", "address": "Apple st 652"},
  { "name": "Hannah", "address": "Mountain 21"},
  { "name": "Michael", "address": "Valley 345"},
  { "name": "Sandy", "address": "Ocean blvd 2"},
  { "name": "Betty", "address": "Green Grass 1"},
  { "name": "Richard", "address": "Sky st 331"},
  { "name": "Susan", "address": "One way 98"},
  { "name": "Vicky", "address": "Yellow Garden 2"},
  { "name": "Ben", "address": "Park Lane 38"},
  { "name": "William", "address": "Central st 954"},
  { "name": "Chuck", "address": "Main Road 989"},
  { "name": "Viola", "address": "Sideway 1633"}
]

x = mycol.insert_many(mylist)

#print list of the _id values of the inserted documents:
print(x.inserted_ids)
```

Metode `insert_many()` mengembalikan objek InsertManyResult, yang memiliki properti, `inserted_ids`, yang menyimpan id dokumen yang disisipkan.


## Menyisipkan Beberapa Dokumen, dengan ID Tertentu
Jika Anda tidak ingin MongoDB memberikan id unik untuk dokumen Anda, Anda dapat menentukan bidang _id ketika Anda menyisipkan dokumen.

Ingatlah bahwa nilainya harus unik. Dua dokumen tidak dapat memiliki _id yang sama.

### Contoh 
```
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]
mycol = mydb["customers"]

mylist = [
  { "_id": 1, "name": "John", "address": "Highway 37"},
  { "_id": 2, "name": "Peter", "address": "Lowstreet 27"},
  { "_id": 3, "name": "Amy", "address": "Apple st 652"},
  { "_id": 4, "name": "Hannah", "address": "Mountain 21"},
  { "_id": 5, "name": "Michael", "address": "Valley 345"},
  { "_id": 6, "name": "Sandy", "address": "Ocean blvd 2"},
  { "_id": 7, "name": "Betty", "address": "Green Grass 1"},
  { "_id": 8, "name": "Richard", "address": "Sky st 331"},
  { "_id": 9, "name": "Susan", "address": "One way 98"},
  { "_id": 10, "name": "Vicky", "address": "Yellow Garden 2"},
  { "_id": 11, "name": "Ben", "address": "Park Lane 38"},
  { "_id": 12, "name": "William", "address": "Central st 954"},
  { "_id": 13, "name": "Chuck", "address": "Main Road 989"},
  { "_id": 14, "name": "Viola", "address": "Sideway 1633"}
]

x = mycol.insert_many(mylist)

#print list of the _id values of the inserted documents:
print(x.inserted_ids)
```

