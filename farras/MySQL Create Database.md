# MySQL Create Database


## Membuat Basis Data
Untuk membuat database di MySQL, gunakan pernyataan "CREATE DATABASE":


#### Contoh 

create a database named "mydatabase":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword"
)

mycursor = mydb.cursor()

mycursor.execute("CREATE DATABASE mydatabase")
```

Jika kode di atas dieksekusi tanpa kesalahan, Anda telah berhasil membuat database.

## Mengecek Keberadaan Basis Data
Anda dapat memeriksa apakah database sudah ada dengan membuat daftar semua database dalam sistem Anda dengan menggunakan pernyataan "SHOW DATABASES":

#### Contoh

Return a list of your system's databases:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword"
)

mycursor = mydb.cursor()

mycursor.execute("SHOW DATABASES")

for x in mycursor:
  print(x)
```

Atau Anda dapat mencoba mengakses database saat membuat koneksi:

#### Contoh

Try connecting to the database "mydatabase":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)
```
