# Python Mongo DB
## MongoDB
MongoDB menyimpan data dalam dokumen seperti JSON, yang membuat basis data ini sangat fleksibel dan dapat diskalakan.

Untuk dapat bereksperimen dengan contoh kode dalam tutorial ini, Anda memerlukan akses ke database MongoDB.

Anda dapat mengunduh database MongoDB gratis di [mongodb](https://www.mongodb.com/)

Atau segera mulai dengan layanan cloud MongoDB di [mongodb](https://www.mongodb.com/atlas/database)

## PyMongo
Python membutuhkan driver MongoDB untuk mengakses basis data MongoDB.

Dalam tutorial ini kita akan menggunakan driver MongoDB "PyMongo".

Kami menyarankan Anda untuk menggunakan PIP untuk menginstal "PyMongo".

PIP kemungkinan besar sudah terinstal di lingkungan Python Anda.

Arahkan baris perintah Anda ke lokasi PIP, dan ketik yang berikut ini:

```
Download and install "PyMongo":

C:\Users\Your Name\AppData\Local\Programs\Python\Python36-32\Scripts>python -m pip install pymongo
```

## Menguji PyMongo
Untuk menguji apakah instalasi berhasil, atau jika Anda sudah menginstal "pymongo", buat halaman Python dengan konten berikut:

```
import pymongo
```
