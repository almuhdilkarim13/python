# Python MySQL Delete From By

## Menghapus Catatan
Anda dapat menghapus record dari tabel yang sudah ada dengan menggunakan pernyataan "DELETE FROM":

#### Contoh 
Hapus catatan apa pun yang alamatnya adalah "Gunung 21":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "DELETE FROM customers WHERE address = 'Mountain 21'"

mycursor.execute(sql)

mydb.commit()

print(mycursor.rowcount, "record(s) deleted")
```

**Penting!**: Perhatikan pernyataan: mydb.commit(). Pernyataan ini diperlukan untuk membuat perubahan, jika tidak, tidak ada perubahan yang dibuat pada tabel.

## Mencegah Injeksi SQL
Merupakan praktik yang baik untuk melarikan diri dari nilai kueri apa pun, juga dalam pernyataan hapus.

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

sql = "DELETE FROM customers WHERE address = %s"
adr = ("Yellow Garden 2", )

mycursor.execute(sql, adr)

mydb.commit()

print(mycursor.rowcount, "record(s) deleted")
```
