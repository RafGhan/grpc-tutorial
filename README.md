# TUTORIAL 9 ADPRO
#### Rafi Ghani Harditama (2206081364)
#### ADPRO A / VRO

## REFLECTION 

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

* RPC Unary adalah jenis RPC paling dasar yang mengirimkan satu permintaan dan menerima satu respons dari server. Metode ini cocok untuk operasi singkat dengan data kecil.

* RPC Server Streaming adalah jenis RPC yang mengirimkan satu permintaan dan menerima sekuens respons dari server. Metode ini cocok untuk mengambil sejumlah data yang besar. 

* RPC Bi-directional Streaming adalah jenis RPC yang mengirim dan menerima sekuens data secara independen.Metode ini cocok untuk komunikasi real-time dan interaktif.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

Dalam mengimplementasikan gRPC di Rust, penting untuk memperhatikan beberapa aspek keamanan, termasuk otentikasi, otorisasi, dan enkripsi data. 
Semua data yang ditransfer melalui gRPC harus melewati proses autentikasi dan otorisasi untuk memastikan keamanannya. Selain itu, enkripsi data menggunakan TLS atau SSL juga penting dalam menjaga keamanan saat mentransmisikan data antara klien dan server, memastikan integritas dan kerahasiaan data terjaga. Manajemen sertifikat juga diperlukan, termasuk pembaruan dan validasi sertifikat secara berkala. Pengujian keamanan secara rutin diperlukan untuk mengidentifikasi dan memperbaiki kerentanan potensial melalui pengujian penetrasi dan integrasi.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Dalam handling bidirectional streaming di Rust gRPC, terutama dalam skenario seperti aplikasi obrolan, beberapa tantangan yang muncul antara lain:

* mengelola concurrency antara klien dan server, di mana perlu dipastikan bahwa operasi yang berjalan secara bersamaan tidak saling mengganggu atau menyebabkan kesalahan.

* error handling, karena kesalahan dalam komunikasi dapat terjadi dan perlu ditangani dengan baik untuk mempertahankan keandalan aplikasi.

* manajemen koneksi, termasuk menangani koneksi yang mungkin putus atau tidak stabil, serta mengelola ulang koneksi dengan benar untuk mempertahankan komunikasi yang lancar

* flow control, mengatur aliran pesan dengan efisien, memastikan bahwa server dan klien dapat beroperasi dengan lancar tanpa mengalami tekanan berlebih.

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

Keuntungan:

* Integrasi yang efisien dengan tokio
* fleksibel dalam penanganan berbagai jenis stream
* streaming data secara asinkron

Kerugian:
* Ketergantungan pada Tokio
* Keterbatasan fitur dibandingkan dengan streaming libraries lainnya
* Menambah kompleksitas

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

* Pemisahan Layanan: Mengorganisir  kode ke dalam layanan terpisah berdasarkan fungsionalitasnya, seperti pemisahan antara definisi layanan `services.proto`, implementasi `grpc_server` dan `grpc_client`

* Menggunakan pola dependency injection dan objek trait untuk mengurangi ketergantungan antar komponen dan meningkatkan fleksibilitas.

* Reusable component dan utilitas sebaiknya dienkapsulasi ke dalam modul yang terpisah, memungkinkan akses dan penggunaan yang mudah di seluruh bagian kode yang berbeda.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Untuk memperbaiki implementasi MyPaymentService, kita dapat mengubah metode process_payment menjadi layanan streaming pada sisi server. Hal ini memungkinkan manajemen yang lebih efisien dari proses pembayaran yang kompleks. Dengan cara ini, pengiriman respons dapat dilakukan secara bertahap kepada klien saat proses pemrosesan pembayaran berlangsung, sehingga memungkinkan pertukaran informasi yang lebih komprehensif dan terperinci antara server dan klien.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?


Penggunaan gRPC sebagai protokol komunikasi mengubah pendekatan dalam desain dan pembangunan sistem terdistribusi. Dengan gRPC, kita tidak perlu lagi khawatir tentang akses modul melalui HTTP tradisional karena gRPC menyediakan mekanisme otomatis untuk memanggil metode yang dibutuhkan. Dengan menggunakan file proto sebagai kontrak bersama antara klien dan server, interaksi antara keduanya menjadi lebih mudah dan langsung. Hal ini memfasilitasi komunikasi antar berbagai teknologi dan platform, serta memperkuat kemampuan sistem yang berbeda untuk beroperasi dalam arsitektur yang kompleks.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

Kelebihan
* Kemampuan multiplexing yang memungkinkan pengiriman dan penerimaan beberapa permintaan dan respons secara bersamaan melalui satu koneksi TCP

* Kompresi header yang dapat mengurangi overhead dan meningkatkan kinerja

* Server push yang dapat mengirim respons tanpa diminta

Kekurangan
* Lebih kompleks jika dibandingkan dengan HTTP/1.1

* Belum sepenuhnya didukung oleh semua server dan klien, yang dapat menyebabkan masalah kompatibilitas.

* Memerlukan biaya overhead yang lebih besar

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

Model request-respons dari REST API memerlukan klien untuk mengirim permintaan dan kemudian menunggu respons dari server, menghasilkan pola komunikasi yang sinkron. Di sisi lain, gRPC memiliki kemampuan streaming dua arah yang memungkinkan klien dan server untuk mengirim dan menerima pesan secara simultan melalui satu koneksi, memungkinkan komunikasi real-time yang lebih responsif dan efisien. Dengan demikian, gRPC lebih cocok digunakan untuk aplikasi yang membutuhkan pertukaran data yang kontinu dan interaksi dengan latensi rendah.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

Penggunaan Protocol Buffers dalam gRPC memberikan kelebihan berupa validasi dan optimisasi data secara otomatis, mengurangi penggunaan bandwidth, serta meningkatkan kecepatan pemrosesan data. Ini sangat cocok untuk aplikasi dengan kebutuhan efisiensi tinggi. Di sisi lain, JSON dalam REST API menawarkan fleksibilitas dalam manipulasi data dinamis tanpa perlu mendefinisikan skema sebelumnya, meskipun dapat menyebabkan waktu pemrosesan yang lebih lama dan penggunaan sumber daya yang lebih besar. Dalam pemilihan antara keduanya, gRPC lebih cocok untuk situasi di mana performa tinggi dan ketatnya tipe data menjadi prioritas utama, sementara JSON lebih sesuai untuk kebutuhan yang menekankan fleksibilitas dan kemudahan pembacaan.
