# Tutorial for Advance Programming Course 2023/2024

**Nama** : **Restu Ahmad Ar Ridho** <br/>
**NPM** : **2206028951** <br/>
**Kelas** : **Advance Programming - A**

## Module 9 - High Level Networking

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

   - RPC unary adalah jenis RPC yang paling sederhana di mana klien mengirimkan satu permintaan ke server dan mendapatkan satu respons balik. RPC ini cocok untuk skenario permintaan dan respons sederhana seperti pada sistem autentikasi atau pengiriman _form_.

   - RPC streaming server adalah di mana klien mengirimkan satu permintaan ke server dan mendapatkan _stream_ beberapa respons kembali. Klien membaca dari _stream_ yang dikembalikan sampai tidak ada lagi pesan. Ini cocok untuk skenario di mana server perlu mengirim banyak data (seperti daftar besar atau file) ke klien.

   - RPC bi-directional streaming adalah dimana klien dan server mengirim serangkaian pesan menggunakan _stream_ _read-write_. Kedua _stream_ beroperasi secara independen, sehingga klien dan server dapat membaca dan menulis dalam urutan apa pun yang mereka suka. Ini cocok untuk skenario di mana klien dan server perlu mengirim banyak data satu sama lain secara independen seperti pada aplikasi obrolan.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?  
   Dalam implementasi gRPC di Rust, beberapa pertimbangan keamanan penting meliputi autentikasi, otorisasi, dan enkripsi data. Autentikasi dan otorisasi perlu dilakukan untuk setiap potongan data dalam gRPC untuk memastikan keamanan. Mekanisme autentikasi seperti sertifikat klien SSL/TLS atau sistem berbasis token harus diintegrasikan dan divalidasi dengan baik, sementara logika otorisasi perlu menegakkan kebijakan kontrol akses secara efektif. Selain itu, enkripsi data perlu diterapkan pada setiap potongan data yang dikirim baik oleh server maupun klien untuk menjaga privasi data. Enkripsi data, yang dipastikan melalui SSL/TLS, melindungi saluran komunikasi, dilengkapi dengan validasi input yang kuat untuk mencegah kerentanan umum. 

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?  
Mengelola _concurrency, error handling, message ordering, back-pressure, resource allocation, security, scalability, and latency_ merupakan pertimbangan penting dalam mengimplementasikan bidirectional streaming di gRPC. Memastikan komunikasi yang lancar antara klien dan server, menjaga integritas pesan, menangani kesalahan pada _concurrency_ seperti _race condition_, dan mengelola sumber daya secara efisien dengan tetap menjaga keamanan dan skalabilitas adalah hal yang terpenting. Selain itu, meminimalkan latensi dan mengoptimalkan kinerja jaringan berkontribusi pada pengalaman pengguna yang lancar, meskipun menghadirkan tantangan dalam pemantauan dan pengoptimalan.

4. What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?  
Menggunakan `tokio_stream::wrappers::ReceiverStream` menawarkan keuntungan seperti streaming asynchronus, integrasi dengan Tokio untuk meningkatkan kinerja, dan dukungan untuk penanganan _back-pressure handling_, mencegah kehabisan sumber daya. Namun, ini memperkenalkan kompleksitas dalam kode, terutama bagi mereka yang tidak terbiasa dengan model pemrograman asynchronus Rust, dan membutuhkan penanganan kesalahan yang lebih untuk memastikan komunikasi yang tepat. Selain itu, mengelola masa asinkronisasi dapat menjadi tantangan, yang berpotensi menyebabkan penghentian secara dini.

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?  
Untuk memastikan _extensibility_ dan _maintainability_ layanan gRPC yang efisien di Rust, manfaatkan _library_ yang ada untuk _reuse_ dan pemeliharaan kode, adopsi desain modular dengan menyusun kode ke dalam modul terpisah dengan tanggung jawab yang jelas, manfaatkan fitur untuk membuat _interface_ yang dapat digunakan kembali.

6. In the **MyPaymentService** implementation, what additional steps might be necessary to handle more complex payment processing logic?  
Untuk menangani logika pemrosesan pembayaran yang lebih kompleks, implementasi MyPaymentService dapat ditingkatkan dengan mengubah metode `process_payment` menjadi server streaming untuk mengirimkan respons secara bertahap kepada klien, memungkinkan pengiriman data yang lebih kompleks dengan lebih efisien.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?  
Adopsi gRPC sebagai protokol komunikasi memiliki dampak besar pada arsitektur dan desain sistem terdistribusi. Dengan gRPC, kebutuhan untuk memikirkan bagaimana modul dapat diakses melalui metode HTTP menjadi tidak relevan, karena gRPC secara otomatis menangani koneksi untuk memanggil metode yang diinginkan. Ini disebabkan oleh adanya kesepakatan yang sama antara klien dan server melalui file proto, sehingga klien dapat memanggil fungsi dari server seolah-olah mereka berinteraksi secara langsung. Hal ini mempermudah konektivitas dan operasi antar teknologi, platform, dan sistem terdistribusi, serta meningkatkan interoperabilitas antara berbagai teknologi dan platform yang digunakan dalam arsitektur sistem yang kompleks.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?  
HTTP/2 menawarkan keunggulan dibandingkan HTTP/1.1 dan HTTP/1.1 dengan WebSocket untuk REST API, termasuk multiplexing untuk permintaan yang bersamaan, server push untuk pengiriman sumber daya proaktif, kompresi header untuk mengurangi overhead, protokol biner untuk efisiensi, dan prioritas aliran untuk manajemen sumber daya yang lebih baik. Namun, hal ini juga menghadirkan kompleksitas dalam implementasi dan pemeliharaan, potensi overhead enkripsi, masalah kemacetan TCP, dan tantangan kompatibilitas browser. Sebagai perbandingan, WebSocket memungkinkan komunikasi dupleks penuh melalui koneksi TCP tunggal, cocok untuk interaksi waktu nyata, sementara HTTP/2 unggul dalam aplikasi web biasa dengan banyak permintaan dan respons kecil.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?  
REST API dikenal dengan kesederhanaannya, memanfaatkan metode HTTP standar dan tanpa _statelessness_ untuk kemudahan penggunaan. Namun, API ini tidak memiliki dukungan untuk komunikasi real-time, sering kali mengandalkan teknik seperti polling atau long-polling, yang dapat menimbulkan kerumitan dan latensi. Di sisi lain, gRPC menawarkan streaming dua arah, yang memungkinkan klien dan server mengirim data secara independen, sehingga cocok untuk skenario waktu nyata dan berpotensi meningkatkan _responsiveness_. Terlepas dari kerumitannya, kemampuan streaming dua arah gRPC dapat menawarkan kinerja yang lebih baik dan manfaat komunikasi waktu nyata dalam kasus penggunaan tertentu dibandingkan dengan REST API.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?  
gRPC dengan Protocol Buffer menawarkan kompatibilitas, kinerja yang lebih baik, dan _tools_ yang lebih baik karena pendekatan berbasis skema. Sebaliknya, JSON dalam muatan REST API memberikan fleksibilitas dan keterbacaan di berbagai bahasa dan platform, meskipun dengan potensi biaya tambahan. Pilihan di antara keduanya bergantung pada persyaratan tertentu, dengan gRPC lebih diuntungkan untuk skenario yang membutuhkan _strong typing_ dan kinerja yang kuat, sementara JSON dalam REST API sesuai dengan situasi yang memprioritaskan fleksibilitas dan keterbacaan.
