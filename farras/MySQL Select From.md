# MySQL Select From

## Memilih dari sebuah tabel
Untuk memilih dari tabel di MySQL, gunakan pernyataan "SELECT":

#### Contoh

Select all records from the "customers" table, and display the result:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT * FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

`**Catatan**: Kami menggunakan metode fetchall(), yang mengambil semua baris dari pernyataan yang terakhir dieksekusi.`

## Memilih Kolom
Untuk memilih hanya beberapa kolom dalam tabel, gunakan pernyataan "SELECT" yang diikuti dengan nama kolom:

#### Contoh

Select only the name and address columns:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

mycursor.execute("SELECT name, address FROM customers")

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
