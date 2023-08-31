# Python MySQL Update Table

## Memperbarui Tabel
Anda dapat memperbarui catatan yang ada dalam tabel dengan menggunakan pernyataan "UPDATE":

#### Contoh 
Timpa kolom alamat dari "Lembah 345" menjadi "Ngarai 123":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "UPDATE customers SET address = 'Canyon 123' WHERE address = 'Valley 345'"

mycursor.execute(sql)

mydb.commit()

print(mycursor.rowcount, "record(s) affected")
```

**Penting!**: Perhatikan pernyataan: mydb.commit(). Pernyataan ini diperlukan untuk membuat perubahan, jika tidak, tidak ada perubahan yang dibuat pada tabel.

## Mencegah Injeksi SQL
Merupakan praktik yang baik untuk melarikan diri dari nilai kueri apa pun, juga dalam pernyataan pembaruan.

Hal ini untuk mencegah injeksi SQL, yang merupakan teknik peretasan web yang umum digunakan untuk menghancurkan atau menyalahgunakan basis data Anda.

Modul mysql.connector menggunakan placeholder %s untuk meloloskan nilai dalam pernyataan hapus:

#### Contoh
Melepaskan nilai dengan menggunakan metode placeholder %s:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "UPDATE customers SET address = %s WHERE address = %s"
val = ("Valley 345", "Canyon 123")

mycursor.execute(sql, val)

mydb.commit()

print(mycursor.rowcount, "record(s) affected")
```
