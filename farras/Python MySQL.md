# Python MySQL

Python dapat digunakan dalam aplikasi basis data.

Salah satu database yang paling populer adalah MySQL.

## Database MySQL
Untuk dapat bereksperimen dengan contoh kode dalam tutorial ini, Anda harus menginstal MySQL di komputer Anda.

Anda dapat mengunduh database MySQL di [Downloads](https://www.mysql.com/downloads/).

## Menginstal Driver MySQL
Python membutuhkan driver MySQL untuk mengakses database MySQL.

Pada tutorial ini kita akan menggunakan driver "MySQL Connector".

Kami menyarankan Anda untuk menggunakan PIP untuk menginstal "MySQL Connector".

PIP kemungkinan besar sudah terinstal di lingkungan Python Anda.

Arahkan baris perintah Anda ke lokasi PIP, dan ketik yang berikut ini:


```
Download and install "MySQL Connector":

C:\Users\Your Name\AppData\Local\Programs\Python\Python36-32\Scripts>python -m pip install mysql-connector-python
```

## Menguji Konektor MySQL
Untuk menguji apakah instalasi berhasil, atau jika Anda telah menginstal "MySQL Connector", buatlah halaman Python dengan konten berikut ini:


demo_mysql_test.py:
```
import mysql.connector
```

Jika kode di atas dijalankan tanpa kesalahan, "MySQL Connector" telah terinstal dan siap digunakan.


## Membuat Koneksi
Mulailah dengan membuat koneksi ke database.

Gunakan nama pengguna dan kata sandi dari basis data MySQL Anda:

demo_mysql_connection.py:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword"
)

print(mydb)
```

