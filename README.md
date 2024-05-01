# Reflection
1. 
* Unary RPCs: Adalah jenis komunikasi protokol yang memungkinan interaksi antara client dan server. Client mengirimkan a single request, lalu server mengirimkan a single response. Tipe ini cocok digunakan untku autentikasi.
* Server streaming: Adalah jenis komunikasi protokol yang memungkinan interaksi antara client dan server. Client mengirimkan a single request, lalu server akan mengirimkan response stream satu-satu kecil-kecil. Tipe ini cocok digunakan untuk real-time update saham, cuaca, berita, dan lainnya.
* Bidirectional streaming RPC: Tipe protokol komunikasi yang memungkian client dan server mengirimkan beberapa pesan-pesan kecil berkali-kali. Tipe jenis ini berguna untuk kolaboratif edit, multiplayer games, dan lain-lain.


2. 
* Autentikasi: Implementasikan mekanisme autentikasi yang aman seperti JSON Web Token (JWT), OAuth, atau kunci API untuk memverifikasi identitas klien yang terhubung ke layanan gRPC.
* Otorisasi: Implementasikan kontrol akses berbasis peran (RBAC) atau mekanisme otorisasi lainnya untuk memastikan klien hanya dapat mengakses sumber daya dan operasi yang diizinkan.
* Enkripsi Data: Gunakan Transport Layer Security (TLS) untuk mengenkripsi data saat transit antara klien dan server. gRPC mendukung TLS secara bawaan.
* Validasi Input: Validasi dan sanitasi semua input data dari klien untuk mencegah serangan injeksi, buffer overflow, atau kerentanan lainnya.


3. 
* Menangani Backpressure: Dalam skenario seperti aplikasi chat, di mana klien dan server mengirim aliran pesan secara konstan, sangat penting untuk menangani backpressure dengan benar untuk menghindari overload pada penerima atau konsumsi sumber daya yang berlebihan.
* Memelihara State: Bidirectional streaming sering kali memerlukan pemeliharaan state di sisi klien dan server, yang dapat menambah kompleksitas dan potensi kondisi ras jika tidak ditangani dengan benar.
* Pembatalan dan Penanganan Kesalahan: Menangani pembatalan atau kesalahan dalam aliran bidirectional dengan baik dapat menjadi tantangan, karena baik klien maupun server harus menyadari state dan merespons dengan tepat.
* Pengurutan dan Penghilangan Duplikasi: Dalam beberapa aplikasi, mungkin diperlukan untuk memastikan bahwa pesan diterima dalam urutan yang benar atau untuk menghilangkan duplikasi pesan yang diterima beberapa kali.


4. 
* Keuntungan:

Menyediakan cara yang mudah untuk mengonversi penerima asinkron (misalnya, mpsc::Receiver) menjadi Stream untuk digunakan dengan async/await dan API berbasis stream lainnya.

Memungkinkan integrasi saluran asinkron yang ada atau primitif perpindahan pesan lainnya ke dalam ekosistem tokio.

* Kerugian:

Memperkenalkan lapisan abstraksi tambahan dan overhead potensial dibandingkan dengan menggunakan primitif perpindahan pesan yang mendasarinya secara langsung.

Mungkin memiliki batasan atau kekurangan spesifik terkait implementasi perpindahan pesan yang mendasarinya, seperti penanganan backpressure atau jaminan pengurutan.


5. 
* Memisahkan definisi layanan dan implementasinya ke dalam modul terpisah.
* Menggunakan trait untuk mendefinisikan antarmuka layanan dan memungkinkan implementasi yang berbeda.
* Memanfaatkan fitur seperti cargo workspaces untuk mengatur proyek menjadi beberapa package yang dapat digunakan kembali.

6. 
Langkah-langkah yang mungkin dilakukan adalah:
* Validasi dan sanitasi input untuk memastikan integritas data.
* Integrasi dengan gateway pembayaran atau sistem pihak ketiga.
* Penanganan kasus khusus seperti pembayaran gagal atau pengembalian dana.

7. 
* gRPC menggunakan Protocol Buffers sebagai format data, yang dapat digunakan di berbagai bahasa pemrograman dan platform.
* gRPC menggunakan HTTP/2 yang memungkinkan multiplexing dan kompresi header untuk meningkatkan efisiensi jaringan.
* Skema berbasis Protocol Buffers memungkinkan evolusi layanan yang lebih mudah tanpa mempengaruhi klien yang ada.

8. 
* Multiplexing: Beberapa permintaan dapat dikirimkan secara bersamaan melalui satu koneksi.
* Kompresi header: Mengurangi overhead jaringan dengan mengompresi header permintaan dan respons.
* Aliran data dua arah: Memungkinkan komunikasi dua arah yang efisien antara klien dan server.
Kerugiannya adalah dukungan browser yang terbatas untuk HTTP/2 dan overhead tambahan dalam hal kompleksitas protokol.

9. 
Model permintaan-respons REST API bersifat sinkron dan berorientasi pada sumber daya, sedangkan kemampuan streaming dua arah gRPC memungkinkan komunikasi real-time yang lebih responsif dan efisien. Streaming dua arah memungkinkan pembaruan langsung dan pengiriman data secara inkremental tanpa harus melakukan polling terus-menerus.

10. 
Pendekatan berbasis skema gRPC menggunakan Protocol Buffers memberikan keuntungan seperti validasi skema yang ketat, serialisasi yang efisien, dan dukungan untuk evolusi skema. Namun, sifatnya yang kurang fleksibel dibandingkan dengan JSON dalam payload REST API dapat menjadi tantangan dalam skenario di mana struktur data yang dinamis diperlukan atau ketika berintegrasi dengan sistem eksternal yang mengharapkan JSON.