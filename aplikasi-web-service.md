Aplikasi Web Service
====================

### Pendahuluan
<p style="text-align: justify">Sebelum kita bekerja dengan web service maka alangkah baiknya kita mengenal terlebih dahulu apa itu
web service. Pada bab pertama ini kita akan membahas hasl-hal fundamental yang perlu kita fahami
sebelum membangun aplikasi web service.</p>

### Definisi Web Service
<div style="text-align: justify;">
  Web service merupakan aplikasi yang didesain untuk mendukung interkoneksi & interaksi antar aplikasi
berbasis web yang terhubung melalui jaringan komputer. Web service diperlukan karena masing-masing
aplikasi bisa jadi memiliki format data yang berbeda, ditulis dengan bahasa pemrograman yang berbeda,
dan berjalan pada platform berbeda. Oleh karenanya diperlukan media yang standard untuk dapat saling
berkomunikasi, media inilah yang kemudian disebut sebagai web service.
<br><br>
Banyak orang menyebut web service dengan sebutan API, dan menganggap keduanya adalah barang
yang sama.
<br><br>
API singkatan dari application programming interface atau antarmuka pemrograman aplikasi merupakan
sekumpulan perintah atau fungsi yang dapat digunakan untuk berinteraksi dengan sistem tertentu. Pada
mulanya sistem yang dimaksud adalah sistem operasi (sehingga API merupakan fungsi-fungsi yang
dapat digunakan untuk berinteraksi dengan sistem operasi komputer), namun kemudian istilah ini
menjadi generic untuk sistem apapun.
<br><br>
Berdasarkan uraian tersebut dapat disimpulkan bahwa web service merupakan API untuk sistem aplikasi
berbasis web.

### RESTful Web Service

Salah satu standard dalam web service yang umum digunakan adalah REST. REST merupakan singkatan dari REpresentational State Transfer yaitu standard pertukaran resource dalam arsitektur web melalui protokol tertentu, umumnya HTTP. Resource bisa berupa data, dokumen, image, fungsi dsb.

REST pertama kali diperkenalkan oleh Roy Fielding pada tahun 2000 melalui disertasinya. Berikut beberapa konsep dari REST:

  - REST berbasis client-server. REST memisahkan antara bagian server yang bertugas menyediakan jalur untuk mengakses resource, dan bagian client melakukan akses resource dan kemudian menggunakannya. Pemisahan ini akan memberikan fleksibilitas baik dari sisi portabilitas dan skalabilitas sistem.
  - REST bersifat stateles. Setiap request dari client ke server bersifat independen, tidak boleh ada penyimpanan konteks atau state pada server atas suatu request. Sebuah state pada konsep REST hanya boleh disimpan pada client, sehingga ketika melakukan request ke server bisa menyertakan informasi state tersebut sehingga request tersebut dikenali oleh server.
  - Resource pada REST dapat dicache. Setiap resouce yang berasal dari respon REST server bisa diset sebagai resource yang bisa di-cache maupun tidak. Jika resource tersebut bisa di-cache maka client boleh menggunakan resource sebelumnya.
  - REST memiliki interface yang standard. REST menggunakan konsep URI (Uniform Resource Identifier) sebagai interface untuk dapat mengakses suatu resource pada REST server.
  - REST server bisa berperan sebagai layer perantara. Resource pada REST server tidak harus berasal dari server yang sama dengan REST server, bisa juga berasal dari server lain atau bahkan sistem lain, sehingga dalam hal ini REST server berperan sebagai jembatan perantara antara REST client dengan sistem lain.

Web service yang dibuat dengan konsep REST inilah yang kemudian dikenal sebagai RESTful Web Services.

### Method Web Service
Terdapat dua model interaksi pada RESTful, yaitu request (HTTP request) ketika meminta data kepada server, dan response (HTTP response) ketika menerima data dari server. Setiap model tersebut memiliki komponen-komponen penyusunnya.

Adapun komponen penyusun HTTP request adalah:
- Verb, HTTP method yang digunakan misalnya GET, POST, DELETE, PUT dll.
- URI/URL, endpoint untuk mengidentifikasikan lokasi dari sumber data pada server.
- HTTP version, menunjukkan versi dari HTTP yang digunakan, contoh HTTP v1.1.
- Request header, berisi meta data untuk HTTP request. Contoh, jenis client/browser, format yang didukung oleh client, format dari body pesan, pengaturan cache dll.
- Request body, konten dari resource.

Sedangkan komponen penyusun HTTP response adalah:
- Status/response code, mengindikasikan status server terhadap resource yang di-request. misal : 404, artinya resource tidak ditemukan dan 200 artinya OK.
- HTTP version, menunjukkan versi dari HTTP yang digunakan, contoh HTTP v1.1.
- Response header, berisi meta data untuk HTTP response. Contoh: jenis server, panjang konten, jenis konten, waktu response, dll
- Response body, konten dari dari resource yang diberikan.

### HTTP Response Code
Sebagaimana yang telah disebutkan sebelumnya bahwa setiap terjadi permintaan data ke server melalui protokol HTTP maka akan mengembalikan respon yang salah satunya adalah status atau kode respon. Kode ini mengindikasikan status server terhadap data yang diminta tersebut.
Secara umum kode respon tersebut dapat dikelompokkan menjadi lima kelompok.

| Kelompok Kode | Keterangan |
| ------------- | ---------- |
| 1xx | Informational response |
| 2xx | Success |
| 3xx | Redirection |
| 4xx | Client errors |
| 5xx | Server errors |

Berikut ini beberapa kode respon yang umum terjadi ketika kita bermain dengan web service.

| Code | Status | Keterangan |
| ---- | ------ | ---------- |
| 200 | OK | Request resource berhasil |
| 301 | Move Permanently | Redirect ke resource lain |
| 304 | Not Modified | Resource belum berubah |
| 400 | Bad Request | Terjadi kesalahan pada request client |
| 403 | Forbidden | Server menolah akses ke resource |
| 404 | Not Found | Resource tidak ditemukan |
| 405 | Method Not Allowed | Method salah |
| 500 | Server Error | Server Error |

### Konsep Stateless pada Web Service
Dalam arsitektur REST, seharusnya tidak boleh ada penyimpanan state atau session untuk mengidentifikasi suatu client pada suatu request, artinya setiap request dari client harus bersifat independen dan dianggap sebagai request baru. Hal ini disebut sebagai stateless.

Tujuan utama dari stateless adalah memudahkan kebutuhan akan peningkatan dalam hal concurrent access terhadap web service.

Salah satu contoh penggunaan state yang umum adalah untuk kebutuhan authorization atau pembatasan hak akses. Pertanyaan yang mungkin timbul adalah dengan tidak adanya state pada REST lalu bagaimana cara kita mengidentifikasi suatu request itu dilakukan oleh client yang mana? atau bagaimana cara kita memproteksi suatu endpoint agar hanya bisa diakses oleh client yang memang memiliki hak akses?.

Untuk mengatasi hal ini maka kemudian digunakan mekanisme tertentu untuk membedakan suatu request apakah berasal dari client yang sudah terdaftar atau belum. Mekanisme yang biasa digunakan adalah dengan menggunakan token.

Alurnya kurang lebih sebagai berikut:

Mula-mula client melakukan request data login, kemudian server melakukan pengecekan untuk memastikan data login tersebut valid. Jika data login valid maka server menggenerate dan mengembalikan suatu token dimana token tersebut untuk mengidentifikasi client yang telah login.

Pada request berikutnya, client dapat menyisipkan token tersebut sehingga server penerima dapat mengenali client yang melakukan request tersebut.

Pada perkembangan selanjutnya, token yang digenerate oleh server bukan dalam bentuk plain data, melainkan data yang sudah dienkripsi dengan metode hash tertentu.

Adapun format data yang dienkripsi biasanya berformat JSON yang memiliki standard tertentu, kemudian dikenal sebagai JSON Web Token atau JWT.

</div>