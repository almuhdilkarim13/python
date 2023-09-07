# MySQL Create Table

## Membuat Tabel
Untuk membuat tabel di MySQL, gunakan pernyataan "CREATE TABLE".

Pastikan Anda menentukan nama database saat membuat koneksi

#### Contoh
Create a table named "customers":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("CREATE TABLE customers (name VARCHAR(255), address VARCHAR(255))")
```

Jika kode di atas dijalankan tanpa kesalahan, Anda sekarang telah berhasil membuat tabel.

## Mengecek Keberadaan Tabel
Anda dapat memeriksa apakah sebuah tabel sudah ada dengan membuat daftar semua tabel dalam database Anda dengan pernyataan "SHOW TABLES":

#### Contoh

Return a list of your system's databases:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SHOW TABLES")

for x in mycursor:
  print(x)
```

## Kunci Utama
Saat membuat tabel, Anda juga harus membuat kolom dengan kunci unik untuk setiap record.

Hal ini dapat dilakukan dengan mendefinisikan KUNCI UTAMA.

Kami menggunakan pernyataan "INT AUTO_INCREMENT PRIMARY KEY" yang akan menyisipkan nomor unik untuk setiap record. Dimulai dari 1, dan bertambah satu untuk setiap record.

#### Contoh

Create primary key when creating the table:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("CREATE TABLE customers (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255), address VARCHAR(255))")
```

Jika tabel tersebut sudah ada, gunakan kata kunci ALTER TABLE:

#### Contoh

Create primary key on an existing table:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("ALTER TABLE customers ADD COLUMN id INT AUTO_INCREMENT PRIMARY KEY")
```
