Rangkuman Membangun Web Service Menggunakan Node.js
Anda berada di akhir dari modul Membangun Web Service Menggunakan Node.js. Mari kita uraikan materi yang sudah Anda pelajari untuk mempertajam pemahaman.



Membuat HTTP Server secara Native
Pengembangan back-end adalah hal prioritas untuk Node.js. Ia andal dalam membangun aplikasi back-end, salah satunya web server alias sebuah komputer yang dapat menangani dan menanggapi permintaan dari client. Node.js menyediakan core modules http untuk membangun web server.

HTTP module memiliki banyak member seperti objek, properti, atau method yang berguna untuk melakukan hal-hal terkait protokol HTTP. Salah satu member yang penting untuk kita ketahui sekarang adalah method http.createServer().

Sesuai namanya, method ini berfungsi untuk membuat HTTP server yang merupakan instance dari http.server. Method ini menerima satu parameter custom callback yang digunakan sebagai request listener. Di dalam request listener inilah logika untuk menangani dan menanggapi sebuah request dituliskan.

Request listener memiliki 2 parameter, yakni request dan response. Request merupakan objek yang menyimpan informasi terkait permintaan yang dikirimkan oleh client. Di dalam objek ini kita bisa melihat alamat yang diminta, data yang dikirim, ataupun HTTP metode yang digunakan oleh client.

Sementara itu, response merupakan objek yang digunakan untuk menanggapi permintaan. Melalui objek ini kita bisa menentukan data yang diberikan, format dokumen yang digunakan, kode status, atau informasi response lainnya.

Setiap instance dari http.server juga memiliki method listen(). Method inilah yang membuat http.server selalu standby untuk menangani permintaan yang masuk dari client. Setiap kali ada permintaan yang masuk, request listener akan tereksekusi.

Method listen() dapat menerima 4 parameter, berikut detailnya:

port (number): jalur yang digunakan untuk mengakses HTTP server.
hostname (string): nama domain yang digunakan oleh HTTP server.
backlog (number): maksimal koneksi yang dapat ditunda (pending) pada HTTP server.
listeningListener (function): callback yang akan terpanggil ketika HTTP server sedang bekerja (listening).

Namun, keempat parameter di atas bersifat opsional. Kita bisa memberikan nilai port saja atau kombinasi apa pun dari keempatnya. Hal itu tergantung terhadap kebutuhan Anda. Lazimnya, ketika memanggil method listen(), kita memberikan nilai port, hostname, dan listeningListener. 



Web Framework
Web Framework adalah sebuah kerangka yang dapat membantu mempermudah pengembangan web, termasuk dalam membuat web server. Dengan menggunakan framework, penulisan kode akan lebih terstruktur, mudah dipelihara, dan gampang dikembangkan.  

Web Framework menyediakan sekumpulan tools dan library yang dapat menyederhanakan hal-hal yang sering dilakukan dalam pengembangan web, seperti pembuatan server, routing, menangani permintaan, interaksi dengan database, otorisasi, hingga meningkatkan ketahanan web dari serangan luar.



Web Framework di Node.js
Di kelas ini kita menggunakan Hapi framework. Framework seperti Hapi menyediakan environment yang lengkap untuk mengembangkan web server yang kompleks. Bila menggunakan Hapi, kita tak perlu tools lain untuk menerapkan layer authentication, tokenize, cors, dan lain sebagainya. 

Kelemahan Hapi adalah abstraksinya yang terlalu jauh dari Node.js native. Kita perlu belajar secara dalam untuk menguasai framework ini.

Penggunaan framework menjadi pilihan personal. Salah satu faktornya adalah kasus yang hendak Anda hadapi. Bila Anda ingin membangun web server yang kompleks tanpa membutuhkan effort yang besar, Hapi adalah pilihan yang tepat.

Kita akan membangun web server dengan arsitektur REST yang kompleks ke depannya. Agar Anda selalu “Hapi” ketika mengikuti alur belajar, kita akan gunakan framework Hapi dalam membangun web server.

Ketahuilah bahwa Hapi memiliki environment yang cukup luas. Kelas ini tidak akan mengajarkan secara dalam tentang API yang ada di Hapi, melainkan hanya fitur-fitur yang menjadi dasar pembuatan REST API. Jadi, bila Anda ingin mendalami terkait framework Hapi, sempatkan waktu untuk eksplorasi di dokumentasi Hapi yang disediakan ya. 



Membuat HTTP Server Menggunakan Hapi
Untuk membuat HTTP server menggunakan Hapi, kita tidak lagi menggunakan core module http secara langsung. Kita akan membuat server melalui modul pihak ketiga @hapi/hapi. Untuk menggunakan modul tersebut, kita perlu memasang terlebih dahulu melalui NPM.

HTTP server sendiri dibuat melalui method Hapi.server(). Method ini menerima satu parameter, yakni ServerOptions. ServerOptions merupakan objek yang menampung konfigurasi dari server yang hendak dibuat, salah satunya kita bisa menetapkan properti port dan host.

Proses menjalankan server (server.start()) dilakukan secara asynchronous. Karena itu, kita perlu menjalankannya di dalam fungsi async dan memanggil server.start() menggunakan await.

Setelah server berhasil berjalan, Anda bisa melihat alamat lengkap dan port di mana server dijalankan melalui properti server.info.uri.



ESLint
ESLint adalah tools yang dapat membantu atau membimbing Anda untuk selalu menuliskan kode JavaScript dengan gaya yang konsisten. Seperti yang Anda tahu, JavaScript tidak memiliki aturan yang baku untuk gaya penulisan kode, bahkan penggunaan semicolon. Karena itu, terkadang kita jadi tidak konsisten dalam menuliskannya.

ESLint dapat mengevaluasi kode yang dituliskan berdasarkan aturan yang Anda terapkan. Anda bisa menuliskan aturannya secara mandiri atau menggunakan gaya penulisan yang sudah ada seperti AirBnb JavaScript Code Style, Google JavaScript Code Style, dan StandardJS Code Style. Kami sarankan Anda untuk mengikuti salah satu code style yang ada. Mengapa begitu? Jawabannya karena code style tersebut sudah banyak digunakan oleh JavaScript Developer di luar sana.



Same-Origin Policy
Server dapat menampung sebuah website, aplikasi, gambar, video, dan masih banyak lagi. Ketika server menampung website, mungkin beberapa data gambar, video, stylesheet biasanya diambil dari alamat server lain atau origin yang berbeda. Contohnya, stylesheet yang diambil dari Bootstrap CDN ataupun gambar yang diperoleh dari server Unsplash. Hal ini wajar dan biasa dilakukan.

Namun, apakah Anda tahu bahwa tidak semua data bisa diambil dari origin yang berbeda? Contohnya, data JSON yang didapatkan melalui teknik XMLHTTPRequest atau fetch. Jika website meminta sesuatu menggunakan teknik tersebut dari luar origin-nya, permintaan tersebut akan ditolak. Itu disebabkan oleh kebijakan same-origin. Kasus ini terjadi pada aplikasi client dan web server yang kita buat.

Origin terdiri dari tiga hal: protokol, host, dan port number.

Selama aplikasi client mengakses data dari origin yang sama, hal itu dapat dilakukan. Namun, bila ada salah satu saja yang berbeda (misal port 8001), permintaan itu akan ditolak.

Lantas, apa solusi agar keduanya dapat berinteraksi? Tenang, untungnya ada mekanisme yang dapat membuat mereka saling berinteraksi. Mekanisme tersebut disebut Cross-Origin Resource Sharing (CORS).



Mengonsumsi dan Menggabungkan Data di Node.js
Tahukah Anda? Banyak aplikasi yang kita gunakan di belakang layar sebenarnya tidak hanya berasal dari satu layanan, melainkan berasal dari berbagai layanan yang saling berkomunikasi. Aplikasi yang kita gunakan di belakang layar mengonsumsi data yang berasal dari berbagai sumber, kemudian datanya digabungkan sesuai dengan kebutuhan.

Bagaimana cara satu layanan menemukan dan berkomunikasi dengan layanan lainnya? 

Supaya layanan bisa saling berkomunikasi, kita harus menemukan IP address, DNS, atau Port yang ada di server terlebih dahulu. Setelah itu, barulah ia dapat berkomunikasi antar layanan menggunakan protokol HTTP, RPC, dan AMQP.

Node.js memiliki kemampuan untuk mengonsumsi dan menggabungkan data dengan melakukan permintaan HTTP. Anda bisa mengonsumsi data dari suatu layanan REST API dan kemudian menggabungkan data tersebut sebelum dikembalikan sebagai response. 



Dengan ringkasan tersebut, diharapkan Anda dapat memahami semua materi yang telah disampaikan. Jika belum, Anda bisa ulas kembali materi yang diberikan pada modul ini. Untuk Anda yang sudah merasa mantap, yuk lanjut ke modul berikutnya!

