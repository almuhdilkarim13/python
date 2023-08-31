# Python MySQL Limit

## Membatasi Hasil
Anda dapat membatasi jumlah catatan yang dikembalikan dari kueri, dengan menggunakan pernyataan "LIMIT":

#### Contoh 
Pilih 5 record pertama dalam tabel "pelanggan":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT * FROM customers LIMIT 5")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

## Mulai dari Posisi Lain
Jika Anda ingin mengembalikan lima rekaman, mulai dari rekaman ketiga, Anda dapat menggunakan kata kunci "OFFSET":

#### Contoh
Mulai dari posisi 3, dan kembalikan 5 catatan:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT * FROM customers LIMIT 5 OFFSET 2")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
