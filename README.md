# Dokumentasi Subscriber - MODUL 9

## Pertanyaan Refleksi

### 1. Apa itu AMQP?
**AMQP (Advanced Message Queuing Protocol)** adalah protokol standar terbuka untuk *message-oriented middleware*. Protokol ini memungkinkan aplikasi yang berbeda (bahkan dengan bahasa pemrograman berbeda) untuk saling berkirim pesan secara asinkron, aman, dan efisien melalui sebuah perantara yang disebut *message broker*.

### 2. Apa maksud dari `guest:guest@localhost:5672`?
Ini adalah *connection string* yang digunakan untuk terhubung ke layanan **RabbitMQ**. Berikut adalah rincian komponennya:

* **`guest` (pertama)**: *Username* default untuk autentikasi ke RabbitMQ.
* **`guest` (kedua)**: *Password* default untuk user tersebut.
* **`localhost`**: Alamat server (*host*) tempat RabbitMQ berjalan (dalam hal ini, di komputer lokal melalui Docker).
* **`5672`**: Port standar yang digunakan oleh protokol AMQP untuk komunikasi data.

### Running at least three subscribers
**Apa yang terjadi pada *console* subscriber ketika ada lebih dari satu subscriber yang berjalan bersamaan?**
Ketika menjalankan tiga program *subscriber* secara bersamaan dan *publisher* mengirimkan pesan, pesan-pesan tersebut tidak diterima oleh satu *subscriber* saja, melainkan didistribusikan secara bergantian kepada ketiga *subscriber* yang aktif. 

RabbitMQ menggunakan metode **Round-Robin** untuk membagikan antrean pesan. Misalnya, pesan ke-1 diproses oleh Subscriber A, pesan ke-2 oleh Subscriber B, pesan ke-3 oleh Subscriber C, lalu pesan ke-4 kembali diproses oleh Subscriber A, dan seterusnya. Ini menunjukkan bagaimana *message broker* sangat berguna untuk melakukan *load balancing* (pembagian beban kerja) agar tidak ada satu *worker* yang kelebihan beban sementara yang lain menganggur.