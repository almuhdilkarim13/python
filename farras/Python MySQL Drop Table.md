# Python MySQL Drop Table

## Menghapus Tabel
Anda dapat menghapus tabel yang sudah ada dengan menggunakan pernyataan "DROP TABLE":

#### Contoh 
Hapus tabel "pelanggan":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DROP TABLE customers"

mycursor.execute(sql)
```

## Hapus Hanya Jika Ada
Jika tabel yang ingin Anda hapus sudah terhapus, atau karena alasan lain tidak ada, Anda dapat menggunakan kata kunci IF EXISTS untuk menghindari kesalahan.

#### Contoh
Hapus tabel "pelanggan" jika sudah ada:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DROP TABLE IF EXISTS customers"

mycursor.execute(sql)
```
