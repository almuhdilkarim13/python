# Python MySQL Order By

## Mengurutkan Hasil
Gunakan pernyataan ORDER BY untuk mengurutkan hasil dalam urutan naik atau turun.

Kata kunci ORDER BY mengurutkan hasil secara default. Untuk mengurutkan hasil dalam urutan menurun, gunakan kata kunci DESC.

#### Contoh 
Urutkan hasil menurut abjad berdasarkan nama: result:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers ORDER BY name"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```

## ORDER BY DESC
Gunakan kata kunci DESC untuk mengurutkan hasil dalam urutan menurun.

#### Contoh
Mengurutkan hasil secara terbalik menurut abjad nama:

```
import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="yourusername",
  password="yourpassword",
  database="mydatabase"
)

mycursor = mydb.cursor()

sql = "SELECT * FROM customers ORDER BY name DESC"

mycursor.execute(sql)

myresult = mycursor.fetchall()

for x in myresult:
  print(x)
```
