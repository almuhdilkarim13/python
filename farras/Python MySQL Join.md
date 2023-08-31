# Python MySQL Join

## Menggabungkan Dua Tabel atau Lebih
Anda dapat menggabungkan baris dari dua tabel atau lebih, berdasarkan kolom yang terkait di antara keduanya, dengan menggunakan pernyataan JOIN.

Anggaplah Anda memiliki tabel "pengguna" dan tabel "produk":

User
```
{ id: 1, name: 'John', fav: 154},
{ id: 2, name: 'Peter', fav: 154},
{ id: 3, name: 'Amy', fav: 155},
{ id: 4, name: 'Hannah', fav:},
{ id: 5, name: 'Michael', fav:}
```

Product
```
{ id: 154, name: 'Chocolate Heaven' },
{ id: 155, name: 'Tasty Lemons' },
{ id: 156, name: 'Vanilla Dreams' }
```

Kedua tabel ini dapat digabungkan dengan menggunakan field fav pengguna dan field id produk.

#### Contoh
Bergabunglah dengan pengguna dan produk untuk melihat nama produk favorit pengguna:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT \
  users.name AS user, \
  products.name AS favorite \
  FROM users \
  INNER JOIN products ON users.fav = products.id"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

## GABUNGAN KIRI
Pada contoh di atas, Hannah, dan Michael tidak termasuk dalam hasil, hal ini dikarenakan INNER JOIN hanya menampilkan record-record yang memiliki kecocokan.

Jika Anda ingin menampilkan semua pengguna, meskipun mereka tidak memiliki produk favorit, gunakan pernyataan LEFT JOIN:

#### Contoh
Pilih semua pengguna dan produk favorit mereka:

```
sql = "SELECT \
  users.name AS user, \
  products.name AS favorite \
  FROM users \
  LEFT JOIN products ON users.fav = products.id"
```

## GABUNG KANAN
Jika Anda ingin mengembalikan semua produk, dan pengguna yang memilikinya sebagai favorit mereka, meskipun tidak ada pengguna yang memilikinya sebagai favorit, gunakan pernyataan RIGHT JOIN:

#### Contoh
Pilih semua produk dan pengguna yang menjadikan produk tersebut sebagai favorit:

```
sql = "SELECT \
  users.name AS user, \
  products.name AS favorite \
  FROM users \
  RIGHT JOIN products ON users.fav = products.id"
```

