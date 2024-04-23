# Module 8 - Software Architectures #
a. what is amqp?<br>
Layaknya http, amqp termasuk salah satu protokol komunikasi. AMQP (Advanced Message Queuing Protocol) adalah application layer protocol yang digunakan untuk komunikasi antar aplikasi. <br>
b. what it means? guest:guest@localhost:5672 , what is the first guest, and what is the second guest, and what is localhost:5672 is for? <br>
guest pertama adalah username, sedangkan guest kedua adalah password. Kemudian, localhost:5672 menyatakan hostname yang merupakan komputer lokal untuk mengakses server dengan nomor port nya 5672.
 ## Simulating Slow Subscriber ##
![Simulating Slow Subscriber](img/RMQSleep.png)
Total number of queues pada laptop saya adalah 40 karena subscribers membutuhkan waktu untuk memproses message yang diterima secara sekuensial sehingga timbul antrean.
## Running Three Subscribers ##
![Running Three Subscribers](img/3Sub.png)
![Monitoring Three Subscribers](img/RMQ3Sub.png)
Screenshots di atas menunjukkan tiga subscribers yang dijalankan bersamaan. Dalam RabbitMQ terlihat bahwa spike dapat turun lebih cepat dibandingkan dengan hanya mengaktifkan 1 subscriber saja karena queue dapat diproses secara bersamaan <br>
Hal-hal yang bisa di-improve pada kode di publisher dan subscriber:
1. Link amqp://guest:guest@localhost:5672 jangan di-hard code pada kode, sebaiknya diletakkan di dalam environment variable untuk menjamin keamanan aplikasi.
2. Sebaiknya menggunakan error handling berupa `expect()` untuk error handling dibandingkan menggunakan `unwrap()`
3.  Sebaiknya tidak menggunakan `println()` untuk melihat output, tetapi menggunakan logging.