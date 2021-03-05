Routing dasar
=================

Routing dasar mengacu pada bagaimana aplikasi kita merespon permintaan client ke titik tertentu yang merupakan URL (atau jalur) yang dijalankan dengan metode HTTP tertentu, seperti GET, POST, PUT, dan DELETE.

Setiap rute memiliki satu atau lebih fungsi penanganan yang mana akan dijalankan pada saat rute cocok.

Pada ExpressJs penanganan routing sederhana menggunakan format:
```
app.METHOD(ROUTE, CALLBACK)
```
Dimana :
- METHOD merupakan HTTP method yaitu get, post, put, dan delete.
- ROUTE merupakan definisi routernya dalam bentuk string.
- CALLBACK merupakan fungsi yang dijalankan ketika routing terpenuhi.

Sebelumnya kita telah menyinggung sedikit tentang routing dasar yakni pada kode :
```js
app.get('/', (req, res) => res.send('Hello World!'))
```

Dan jika dijabarkan akan menjadi seperti dibawah ini :
- app merupakan objek atau instance dari class Express 
```js
const express = require('express')
```
- get() merupakan method HTTP GET, sehingga untuk method lainnya kita bisa sesuaikan saja
post(), delete(), put(), dll.
- ```'/'``` merupakan definisi routenya atau dalam contoh ini merupakan route utama. Untuk membuat
routing lain misalnya about maka cukup dengan menuliskannya dengan ```'/user'```, demikian juga
untuk route bertingkat kita juga bisa tuliskan sebagai berikut: ```'/user/status'```
- ```(req, res) => res.send('Hello World!'))``` merupakan callback berbentuk fungsi closure/anonymous yang akan dieksekusi ketika routing ditemukan. Fungsi ini setidaknya memiliki
dua argumen yaitu req (request) dan res (response), dimana fungsi ini menjalankan perintah ```res.send()``` yang berarti mengirimkan suatu response ke client. Responsenya pada contoh ini berupa teks Hello World!

Setelah pada contoh diatas kita mencoba method ```get()```, lalu selannjutnya kita akan mencoba dengan method HTTP yang lain.

```js
const express = require('express')
const app = express()

app.get('/get', (req, res)=>{
    res.send("Ini adalah halaman GET")
})

app.post('/post', (req, res)=>{
    res.send("Ini adalah halaman POST")
})

app.put('/put', (req, res)=>{
    res.send("Ini adalah halaman PUT")
})

app.delete('/delete', (req, res)=>{
    res.send("Ini adalah halaman DELETE")
})

app.listen(3000, ()=>{
    console.log("Aplikasi berjalan di port http://localhost:3000")
})
```

Lalu kita coba jalan kan menggunakan postman, maka hasilnya akan seperti ini :
![](images/01.jpg)

Akan tetapi, jika kita mengakses routing namun methodnya tidak sesuai dengan yang didefinisikan maka akan muncul error Cannot GET [path route].
Misalnya mengakses route /post namun methodnya menggunakan GET.
![](images/02.jpg)

Namun jika kita menggunakan route yang sama dengan yang didefinisikan maka hasilnya akan seperti ini :
![](images/03.jpg)
