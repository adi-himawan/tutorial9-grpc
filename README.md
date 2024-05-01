## Tutorial 9 Reflection

#### 1. What are the key differences between unary, server streaming, and bidirectional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
- Unary RPC adalah metode paling sederhana yang mengirimkan satu request dan mendapatkan satu response. RPC ini cocok untuk skenario yang melibatkan pengiriman request dan response sederhana, seperti sistem autentikasi. 
- Server streaming RPC mengirimkan satu request dan mendapatkan stream beberapa response. Client akan membaca stream hingga tidak ada lagi data yang dikirimkan. RPC ini cocok untuk skenario di mana server perlu mengirim banyak data, seperti harga real-time saham. 
- Bidirectional streaming RPC melibatkan pertukaran data antara client dan server menggunakan stream read-write. Kedua stream beroperasi secara independen. Oleh karena itu, RPC ini cocok untuk skenario di mana client dan server sama-sama perlu mengirimkan banyak data, seperti di aplikasi chatting.

#### 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
Untuk memastikan security, setiap data yang dikirimkan oleh gRPC harus dilakukan autentikasi dan otorisasi. Selain itu, dalam konteks data encryption, setiap data yang dikirimkan baik oleh client maupun server akan dienkripsi secara terpisah untuk menjaga privasi data.

#### 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
Dalam mengimplementasikan bidirectional streaming di Rust gRPC, beberapa tantangan yang umumnya harus dihadapi adalah terkait race condition serta sinkronisasi data. Selain itu, koneksi yang berlangsung lama juga dapat menimbulkan masalah lain seperti mempersulit load balancing hingga membebankan server.

#### 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
Menggunakan tokio_stream::wrappers::ReceiverStream memiliki kelebihan seperti asynchronous yang mempercepat pengolahan data hingga kemudahan dalam melakukan integrasi dengan modul tokio yang lain. Di sisi lain, kekurangan dari penggunaan tokio_stream::wrappers::ReceiverStream adalah kompleksitas kode yang semakin bertambah serta banyaknya autentikasi dan otorisasi yang diperlukan untuk setiap data.

#### 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
Penggunaan Rust gRPC nyatanya memberikan kemudahan dalam meningkatkan maintainability dan ekstensibility. Dengan proto, setiap perubahan atau penambahan fitur dapat dilakukan dengan lebih mudah karena adanya interface yang dapat diimplementasikan oleh setiap class dalam Rust.

#### 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
Dalam implementasi MyPaymentService, langkah tambahan yang sekiranya diperlukan untuk menangani logika pemrosesan pembayaran yang lebih kompleks adalah mengubah implementasi function ``process_payment`` menjadi server streaming. Implementasi ini diperlukan untuk mempercepat pengiriman data kompleks serta mengurangi overhead pembuatan koneksi antara client dan server.

#### 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
Adopsi gRPC sebagai protokol komunikasi memiliki dampak yang signifikan terhadap arsitektur dan desain sistem terdistribusi, khususnya dalam konteks interoperability dengan teknologi dan platform lain. Dengan gRPC, kita tidak perlu memikirkan cara suatu modul diakses dengan metode HTTP karena gRPC akan secara otomatis menghubungkan pemanggilan metode yang kita inginkan. Hal ini tentunya memudahkan konektivitas dan operasi antar teknologi serta platform.

#### 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
Sebagai protokol dasar dari gRPC, kelebihan HTTP/2 terletak pada kemampuannya untuk mengirimkan banyak request dan mendapatkan banyak response hanya dalam satu koneksi. Akan tetapi, mempertahankan koneksi seperti ini mengakibatkan kerugian karena memakan biaya overhead yang lebih tinggi baik dari segi kinerja maupun penggunaan memori. Akibatnya, pengiriman data kecil menggunakan HTTP/2 bisa saja memakan biaya yang lebih tinggi dibanding HTTP/1 atau HTTP/1.1.

#### 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
Request-response model dari REST API memiliki perbedaan yang cukup signifikan dengan bidirectional streaming dari gRPC. Pada REST API, setiap pengiriman request melibatkan pembuatan koneksi baru dari client ke server. Sebaliknya, pada gRPC, hanya diperlukan satu koneksi untuk setiap pengiriman request. Hal ini membuat gRPC lebih optimal untuk komunikasi yang bersifat real-time dibandingkan REST API.

#### 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
Dengan Protocol Buffer, pengguna harus mendefinisikan skema data secara eksplisit menggunakan proto. Hal ini menghasilkan kode yang lebih terstruktur serta validasi yang lebih ketat. Selain itu, serialisasi dan deserialisasi data juga terjadi secara otomatis sehingga setiap data yang dikirimkan tidak mungkin salah tipe dan langsung dapat digunakan.

Sementara itu, JSON dalam REST API tidak memerlukan pendefinisian skema data yang eksplisit. Meski memungkinkan struktur data yang lebih fleksibel, penggunaan JSON dalam REST API dapat menyebabkan validasi yang tidak ketat serta ketidakpastian tipe data. Akibatnya, ada kemungkinan data yang dikirimkan tidak dapat digunakan. 