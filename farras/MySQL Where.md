# MySQL Where

## Memilih Dengan Filter
Saat memilih catatan dari tabel, Anda dapat memfilter pilihan dengan menggunakan pernyataan "WHERE":

#### Contoh

Select record(s) where the address is "Park Lane 38": result:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers WHERE address ='Park Lane 38'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```


## Karakter Karakter Liar
Anda juga dapat memilih catatan yang dimulai, termasuk, atau diakhiri dengan huruf atau frasa tertentu.

Gunakan tanda % untuk mewakili karakter wildcard:

#### Contoh

Select records where the address contains the word "way":

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers WHERE address LIKE '%way%'"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

## Mencegah Injeksi SQL
Ketika nilai kueri disediakan oleh pengguna, Anda harus menghindari nilai tersebut.

Ini untuk mencegah injeksi SQL, yang merupakan teknik peretasan web yang umum untuk menghancurkan atau menyalahgunakan basis data Anda.

Modul mysql.connector memiliki metode untuk meloloskan nilai kueri:

#### Contoh

Escape query values by using the placholder %s method:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers WHERE address = %s"
adr = ("Yellow Garden 2", )

mycursor.execute(sql, adr)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
