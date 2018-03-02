# MongoDB Tutorials

## Membuat Database Baru
Membuat database baru dengan nama **analogue**, atau _return_ database jika database yang dimaksud sudah ada:
> use _analogue_

## Mengecek Database Terseleksi
> db

## Melihat Daftar Seluruh Database
> show dbs

_Untuk database yang baru saja dibuat tidak akan tampil dalam daftar, sebelum minimal sebuah dokumen ada di dalamnya_.

## Menghapus Database
Menghapus database terpilih
> db._dropDatabase()_


---
## Membuat Collection Dalam Database
> db._createCollection( name, options )_

_* **options** adalah pengaturan konfigurasi dari collection yang dibuat_. Lebih jelas tentang _options_ ini lihat di [Tutorial Points](https://www.tutorialspoint.com/mongodb/mongodb_create_collection.htm).

### Tanpa options
> db._createCollection( "**item**" )_

Membuat collection dengan nama **item**.

### Dengan options
> db._createCollection( "**admin**", { **capped:true, autoIndexId:true, size:6142800, max:10000** } )_

Lebih detail tentang options lihat di [Tutorial Points](https://www.tutorialspoint.com/mongodb/mongodb_create_collection.htm).

### Cara lain membuat collection, dengan sekaligus menginsertkan document
> _db.**user**.insert({"name":"Indra Arianggi"})_

Membuat collection baru dengan nama **user**, sekaligus menginsertkan sebuah document (data) ke dalamnya.

## Melihat Daftar Seluruh Collection Dalam Sebuah Database
> show collections

## Menghapus Collections
> _db.**admin**.drop()_

Menghapus collection dengan nama **admin**.


---
## Tipe Data Dalam MongoDB
- String
- Integer
- Boolean
- Double
- Min/Max Keys
- Arrays
- Timestamp
- Object
- Null
- Symbol
- Date
- Object ID
- Binary Data
- Code
- Regular Expression

Penjelasan lebih detail lihat [Tutorial Points](https://www.tutorialspoint.com/mongodb/mongodb_datatype.htm).


---
## Memasukkan Document Ke Dalam Collection
Dapat menggunakan method **insert()** atau **save()**.

> db.**item._insert({_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_name: 'Minolta Capios 75',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_detail: 'Pocket analog camera with epic result',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_price: 500000,_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_stock: 2_**
>
> **_})_**

Memasukkan beberapa document sekaligus:
> db.**item.insert(_[_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_{_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_name: 'Minolta Capios 75',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_detail: 'Pocket analog camera with epic result',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_type: 'camera',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_price: 500000,_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_stock: 2_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_},_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_{_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_name: 'Canonet QL17 GIII',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_detail: 'Classic Retro Analog Camera',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_type: 'camera',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_price: 750000,_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_stock: 1_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_},_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_{_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_name: 'Kodak Color Plus 200',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_detail: 'Awesome film',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_type: 'film',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_price: 50000,_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_stock: 100_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_}_**
>
> **_]_)**

_Penggunaan method **save()** sama dengan method **insert()**._


---
## Query Document
Menampilkan seluruh document dalam collection **item**.
> db.item.**_find()_**

Menampilkan hanya _satu_ document.
> db.item.**_findOne()_**

Menampilkan hasil pencarian dengan format terstruktur.
> db.item.find().**_pretty()_**

### Query Document dengan Kondisi Tertentu (Document yang Spesifik)
#### Sama dengan (=)
> db.item.find( **_{ "type":"film" }_** )

Mencari document dengan nilai field **type** sama dengan **film**.

#### Kurang dari (<)
> db.item.find({ 'price':**_{$lt:500000}_** })

Mencari document dalam collection item, dengan nilai field **price** kurang dari **500000**.

#### Kurang dari sama dengan (<=)
> db.item.find({ 'price':**_{$lte:500000}_** })

Mencari document dalam collection item, dengan nilai field **price** kurang dari sama dengan **500000**.

#### Lebih dari (>)
> db.item.find({ 'price':**_{$gt:500000}_** })

Mencari document dalam collection item, dengan nilai field **price** lebih dari **500000**.

#### Lebih dari sama dengan (>=)
> db.item.find({ 'price':**_{$gte:500000}_** })

Mencari document dalam collection item, dengan nilai field **price** lebih dari sama dengan **500000**.

#### Tidak sama dengan (!=)
> db.item.find({ 'price':**_{$ne:500000}_** })

Mencari document dalam collection item, dengan nilai field **price** tidak sama dengan **500000**.

### Kondisi AND dan OR
Mencari document dimana nilai type = camera **AND** price <= 500000
> db.item.find({ **_'type':'camera', 'price':{$lte:500000}_** })

Mencari document dimana nilai type = camera **OR** price <= 500000
> db.item.find({ **_$or:[{'type':'camera'},{'price':{$lte:500000}}]_** })

Mencari document dimana nilai type = camera **AND** price = 500000 **OR** price = 100000
> db.item.find( {
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_'type':'camera',_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_$or:[_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_{'price':500000}, {'price':100000}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_]_**
>
> } )


---
## Update Document
Update dapat menggunakan method **update()** dan **save()**.

Method **update()** akan _mengupdate_ sebuah nilai field dalam document, sedangkan method **save()** akan _mengganti_ document dengan yang baru.
> db.item.**_update(_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_{name: "Agva Vista 200"},_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_{_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_$set: {price:55000}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_}_**
>
> **_)_**

Parameter pertama adalah kriteria untuk mencari document yang akan diupdate, dan parameter kedua adalah field dan nilai baru.
Kriteria lebih dari satu, dan nilai yang diset lebih dari satu:
> db.item.update(
>
> &nbsp;&nbsp;&nbsp;&nbsp;**{**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_name: "Kodak Color Plus 200",_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_type: "film"_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**},**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**{**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_$set: {_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_price:45000,_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_stock:50_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**}**
>
> )

Cara diatas secara default hanya akan mengupdate satu document, untuk mengupdate multiple document perlu menset parameter **multi** menjadi **true**.
> db.item.update(
>
> &nbsp;&nbsp;&nbsp;&nbsp;{type: "film"},
>
> &nbsp;&nbsp;&nbsp;&nbsp;{
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$set: {price:55000}
>
> &nbsp;&nbsp;&nbsp;&nbsp;},
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_{multi:true}_**
>
> )


---
## Menghapus Document
Menggunakan method **remove()**, yang mempunya 2 parameter optional.
- deletion criteria: kriteria document yang akan dihapus.
- justOne: jika diset true atau 1, maka hanya akan menghapus sebuah dokumen (yang pertama).

Jika kriteria document yang akan dihapus tidak diset maka method **remove()** akan menghapus seleruh document dalam collection.
> db.item.**_remove( {type:"film"} )_**

Dengan lebih dari satu kriteria:
> db.item.remove( { **_type:"film", stock:50_** } )

Dengan menset parameter _justOne_, hanya akan menghapus sebuah document:
> db.item.remove({type:"camera"}, **_1_**)

Hapus seluruh document:
> db.item.remove( **_{}_** )


---
## Projection
Menampilkan field tertentu saja.

Hanya _menampilkan_ nilai dari **field name** dari seuruh document dalam collection **item**:
> db.item.find( {}, **_{name:1, _id:0}_** )

_Tidak menampilkan_ **field price** dan **stock**:
> db.item.find( {}, **_{price:0, stock:0}_** )

Dalam query document, untuk **_menampilkan_** field tertentu (tidak semua), field yang ingin ditampilkan diberi nilai **_1_**.

Sedangkan jika **_tidak ingin menampilkan_** field tertentu, field tersebut diberi nilai **_0_**.

Field **_id** secara default selalu ditampilkan, sehingga jika tidak ingin menampilkannya beri nilai 0 pada saat melakukan query document.


---
## Limiting Records
Membatasi jumlah document yang ditampilkan, menggunakan method **limit()**.

Hanya menampilkan 3 record dari hasil query document:
> db.item.find().**_limit(3)_**

Method **skip()** digunakan untuk melewatkan sejumlah record dan lanjut ke record setelahnya.

Melewatkan 2 record awal:
> db.item.find().**_skip(2)_**


---
## Sorting Records
Mengurutkan record atau document hasil pencarian, menggunakan method **sort()**.
Nilai untuk mengurutkannya adalah:
- Ascending => **1**
- Descending => **-1**

Mengurutkan secara **ascending** berdasarkan nilai **field name**:
> db.item.find().**_sort( {name:1} )_**

Mengurutkan secara **descending** berdasarkan nilai **field name**:
> db.item.find().sort({ name: **_-1_** })


---
## Indexing
Pengindeksan mendukung query yang efisien. Tanpa indexing MongoDB akan menscan setiap document dari collection untuk menemukan document yang sesuai dengan query.

Membuat index menggunakan method **ensureIndex()**.

Membuat index dari collection item dengan field **name** secara **ascending (1)**.
> db.item.**_ensureIndex( {"name":1} )_**

Nama field yang dibuat untuk index haruslah yang mengandung nilai yang unik, sebagai contoh field **user_id** dalam sebuah collection **user**.

Method **ensureIndex()** juga menerima beberapa options konfigurasi, dapat dilihat di [Tutorial Points](https://www.tutorialspoint.com/mongodb/mongodb_indexing.htm).

### Melihat daftar index dalam sebauh collection
Menampilkan daftar index dari collection **item**:
> db.item.**_getIndexes()_**

### Menghapus sebuah index
> db.item.**_dropIndex({"name":1})_**


---
## Aggregations
Mengelompokkan document-document setelah diproses berdasarkan kategori tertentu. Operasi aggregations dilakukan menggunakan method **aggregate()**.

Misalnya, mengelompokkan document-document dalam collection item berdasarkan **type** item, dan menghitung jumlah item dalam setiap **type**:
> db.item.**_aggregate([_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_{_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_$group: {_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_ _id: "$type",_** 
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_total: {$sum:1}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_}_**
>
> **_])_**

Operasi diatas jika dijabarkan dengan kata-kata menjadi: _kelompokkan document-document dalam collection **item** berdasarkan nilai **field type**, dan hitung **jumlah** document yang nilai field **type-nya sama**_.

Operasi yang dapat dilakukan dalam aggregations selain penjumlahan (**$sum**), dapat dilihat di [Tutorial Points](https://www.tutorialspoint.com/mongodb/mongodb_aggregation.htm).

Contoh lain:
#### Nilai Maximum
Mencari harga (_price_) termahal:
> db.item.aggregate([
>
> &nbsp;&nbsp;&nbsp;&nbsp;{
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$group: {
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_id: "", 
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_max_price: {$max: "$price"}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
>
> &nbsp;&nbsp;&nbsp;&nbsp;}
>
> ])

#### Nilai Minimum
Mencari harga (_price_) termurah:
> db.item.aggregate([
>
> &nbsp;&nbsp;&nbsp;&nbsp;{
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$group: {
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_id: "", 
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_min_price: {$min: "$price"}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
>
> &nbsp;&nbsp;&nbsp;&nbsp;}
>
> ])


---
## Pipeline Concept
Menjalankan operasi secara berurutan. Hasil output dari sebuah operasi akan menjadi inputan bagi operasi selanjutnya, dan seterusnya hingga operasi terakhir.
Lebih detail lihat di [Tutorial Points](https://www.tutorialspoint.com/mongodb/mongodb_aggregation.htm).


---
## Replication
Replication adalah proses sinkronisasi data pada beberapa server. Replication menyediakan redundansi data dan meningkatkan ketersediaan data pada server database yang berbeda. Replication bertujuan untuk melindungi database dari kehilangan pada sebuah server. Dengan beberapa salinan data, kita dapat memanfaatkannya untuk tujuan yang berbeda-beda, misalnya satu untuk disaster recovery, dan yang lain untuk reporting atau backup.

Lebih detail lihat [Tutorial Points](https://www.tutorialspoint.com/mongodb/mongodb_replication.htm).


---
## Deployment
Lebih detail lihat [Tutorials Point](https://www.tutorialspoint.com/mongodb/mongodb_deployment.htm).

---
## Relationships
Relasi di MongoDB mewakili bagaimana berbagai dokumen saling terkait secara logis.

Sebuha relasi bisa berupa 1:1, 1:N, N:1, atau N:N.

Relasi dalam MongoDB bisa dibuat dengan pendekatan Embedded (tertanam) atau Referenced (referensi).

Contoh, user bisa memiliki _lebih dari_ satu alamat, maka hubungan antara tabel **user** dan **alamat** adalah **1:N**.

Document user:
> {
>
> &nbsp;&nbsp;&nbsp;&nbsp;"_id":ObjectId("52ffc33cd85242f436000001"),
>
> &nbsp;&nbsp;&nbsp;&nbsp;"name": "Tom Hanks",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"contact": "987654321",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"dob": "01-01-1991"
>
> }

Document alamat:
> {
>
> &nbsp;&nbsp;&nbsp;&nbsp;"_id":ObjectId("52ffc4a5d85242602e000000"),
>
> &nbsp;&nbsp;&nbsp;&nbsp;"building": "22 A, Indiana Apt",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"pincode": 123456,
>
> &nbsp;&nbsp;&nbsp;&nbsp;"city": "Los Angeles",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"state": "California"
>
> }

Maka model data dalam MongoDB menjadi:

### Dengan pendekatan embedded
> {
>
> &nbsp;&nbsp;&nbsp;&nbsp;"_id":ObjectId("52ffc33cd85242f436000001"),
>
> &nbsp;&nbsp;&nbsp;&nbsp;"contact": "987654321",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"dob": "01-01-1991",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"name": "Tom Benzamin",
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_"address": [_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_{_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"building": "22 A, Indiana Apt",_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"pincode": 123456,_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"city": "Los Angeles",_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"state": "California"_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_},_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_{_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"building": "170 A, Acropolis Apt",_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"pincode": 456789,_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"city": "Chicago",_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_"state": "Illinois"_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_}_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_]_**
>
> }

Kelebihan dari model **embedded** adalah data mudah diambil. Namun kekurangannya, jika data yang ter-embed (_alamat_) semakin banyak/besar akan mempengaruhi operasi read/write.

### Dengan pendekatan referenced
> {
>
> &nbsp;&nbsp;&nbsp;&nbsp;"_id":ObjectId("52ffc33cd85242f436000001"),
>
> &nbsp;&nbsp;&nbsp;&nbsp;"contact": "987654321",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"dob": "01-01-1991",
>
> &nbsp;&nbsp;&nbsp;&nbsp;"name": "Tom Benzamin",
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_"address_ids": [_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_ObjectId("52ffc4a5d85242602e000000"),_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**_ObjectId("52ffc4a5d85242602e000001")_**
>
> &nbsp;&nbsp;&nbsp;&nbsp;**_]_**
>
> }

Menggunakan pendekatan **referenced** hanya **id** dari document alamat yang disimpan (_di-embed_) ke dalam document user.

Sehingga nantinya untuk melihat alamat user memerlukan dua operasi:
> var result = db.users.findOne({"name":"Tom Benzamin"},{"address_ids":1})
>
> var addresses = db.address.find({"_id":{"$in":result["address_ids"]}})


---
## Database References
MongoDB menyediakan **DBRef** untuk melakukan referensi document. **DBRef** digunakan jika document yang ingin direfensikan memiliki banyak jenis.

Berkaitan dengan pembahasan sebelumnya, misal document **alamat** memiliki banyak jenis, antaranya **alamat rumah**, **alamat kantor**, dan sebagainya.

DBRef memiliki 3 field:
- $ref => nama collection dari document referensi.
- $id => id dari document referensi.
- $db (opsional) => nama database dimana document referensi berada.


---
## Covered Queries
Adalah query yang:
- semua field kriteria dalam query adalah bagian dari index
- semua field yang ingin ditampilkan adlah bagian dari index yang sama

Akan mempercepat pencarian, karena pencarian hanya akan dilakukan pada index, tidak sampai melihat ke dalam document.


---
## Analizing Query
Untuk mengetahui seberapa efektif desain database dan index yang dibuat.

Menggunakan method **explain()** dan **hint()**.


---
### _Mencari_ Sekaligus _Update_ Document
Menggunakan method **findAndModiry()**:
> **_db.item.findAndModify( {_**
> &nbsp;&nbsp;&nbsp;&nbsp;**_query:{name: "Nikon FM2", stock:{$gt:0}},_**
> &nbsp;&nbsp;&nbsp;&nbsp;**_update: { $inc: {stock:-1} }_**
> **_} )_**

Lebih detail lihat [Tutorials Point](https://www.tutorialspoint.com/mongodb/mongodb_atomic_operations.htm).


---
## Advance Indexing
### Indexing Array Fields
Membuat index pada array, secara otomatis akan membuat index-index terpisah untuk masing-masing nilai dalam array.

### Indexing Sub-Document Fields
Membuat index untuk field sub-document, dengan cara membuat index berdasarkan field-field yang ada dalam sub-document tersebut.

Pada saat melakukan query berdasarkan nilai sub-document, PERHATIKAN urutan field dalam sub-document tersebut. Urutan pencarian dalam fungsi query harus sama dengan urutan field dalam sub-document.


---
## Regular Expression
MongoDB menyediakan fungsionalitas dari regular expression untuk pencocokan string menggunakan operator **$regex**.
> db.item.find( _{ name: **{$regex:"Minolta"}** }_ )

### Regular expression dengan case insensitive
Mencari dengan regular expression secara insensitive, menggunakan parameter **$options** dengan nilai **$i**.
> db.item.find({name: {$regex:"_capios_", **_$options:"$i"_** }})


## GridFS
GridFS adalah spesifikasi MongoDB untuk menyimpan file besar seperti gambar, audio, video, dan sebagainya. GridFS mempunyai kemampuan untuk menyimpan file, bahkan yang lebih besar dari batas ukuran document 16MB.

GridFS membagi sebuah file ke dalam potongan-potongan dan menyimpan setiap potongan data ke dalam document yang terpisah.

GridFS secara default menggunakan dua collection, **fs.files** dan **fs.chunks**, untuk menyimpan metadata file dan potongan-potongan data.

Untuk menambahkan file ke dalam GridFS, lihat [Tutotials Point](https://www.tutorialspoint.com/mongodb/mongodb_gridfs.htm).

