# Aplikasi Web "Chhoto URL"


## Pengenalan Chhoto URL

Chhoto URL merupakan aplikasi pemendek tautan (URL shortener) yang dikembangkan menggunakan bahasa pemrograman Rust dengan framework Actix Web. Nama “Chhoto” berasal dari bahasa Bengali yang berarti “kecil”, merepresentasikan filosofi aplikasi ini: berukuran kecil namun memiliki kemampuan yang efisien dan bermanfaat besar.

Aplikasi ini dirancang sebagai web app ringan dan mandiri yang berfungsi untuk mengonversi tautan panjang menjadi versi yang lebih singkat, mudah diingat, dan praktis untuk dibagikan. Melalui pendekatan arsitektur yang minimalis, Chhoto URL menawarkan solusi cepat dan aman tanpa ketergantungan pada layanan pihak ketiga.

Dengan performa tinggi serta kemudahan penggunaan melalui antarmuka web maupun Command Line Interface (CLI), Chhoto URL menjadi pilihan ideal untuk individu maupun organisasi yang membutuhkan sistem pemendek tautan sederhana, efisien, dan dapat diandalkan.

## Instalasi

### Kebutuhan Sistem:

  - Sebuah Virtual Machine (misalnya VirtualBox dengan Kali Linux).
  - Docker dan Docker Compose terinstal di dalam VM.
  - Akun gratis di situs Ngrok.

### Proses Instalasi

Login ke dalam Virtual Machine Anda, buka terminal, lalu buat direktori proyek.

Pindah ke direktori home
```
 $ cd ~
```
Membuat folder bernama chhoto-url dan masuk ke dalamnya
```
 $ mkdir chhoto-url && cd chhoto-url
```
Buat file konfigurasi docker-compose.yml menggunakan editor teks.
```
 $ nano docker-compose.yml
```
Salin dan tempel seluruh konfigurasi berikut ke dalam editor. Ganti nilai PASSWORD dan API_KEY dengan nilai rahasia buatan Anda sendiri.
```
 version: '3.8'
 services:
   chhoto-url:
     image: sintan1729/chhoto-url:latest
     container_name: chhoto-url
     restart: unless-stopped
     ports:
       - "4567:4567"
     volumes:
       - ./data:/app/data
     environment:
       - SITE_URL=http://localhost:4567
       - PASSWORD=GANTI_DENGAN_PASSWORD_ANDA
       - API_KEY=GANTI_DENGAN_API_KEY_ANDA
```

Jalankan container Docker di latar belakang dan verifikasi bahwa container sudah berjalan.
```
 $ docker-compose up -d
 $ docker-compose ps
```
Pastikan status container adalah Up atau Running.

Unduh Ngrok. Kunjungi halaman download Ngrok, klik kanan pada tombol download Linux, lalu "Salin alamat tautan".

Pindah ke direktori home
```
 $ cd ~
```
Ganti "LINK_DARI_WEBSITE" dengan tautan yang Anda salin
```
 $ wget "LINK_DARI_WEBSITE"
```
Ekstrak file ke lokasi yang dapat diakses dari mana saja
```
 $ sudo tar xvz ngrok-v3-*.tgz -C /usr/local/bin
```
Hubungkan program ngrok dengan akun Anda. Dapatkan authtoken dari dashboard Ngrok.

Ganti <TOKEN_ANDA> dengan token dari dashboard
```
 $ ngrok config add-authtoken <TOKEN_ANDA>
```

Buka "terowongan" ke port 4567. Biarkan terminal ini tetap berjalan.
```
 $ ngrok http 4567
```

ngrok akan memberikan Anda sebuah URL publik di baris Forwarding. Salin URL HTTPS tersebut.

Buka terminal baru (jangan tutup terminal ngrok). Hentikan sementara container Docker untuk memperbarui konfigurasinya.
```
 $ cd ~/chhoto-url
 $ docker-compose down
```

Buka kembali file docker-compose.yml dan ubah nilai dari SITE_URL menjadi URL HTTPS yang Anda dapatkan dari ngrok.
```
 $ nano docker-compose.yml
```

... (bagian lain dari file tetap sama)
environment:
 - SITE_URL=[https://URL-ACAK-DARI-NGROK.ngrok-free.dev](https://URL-ACAK-DARI-NGROK.ngrok-free.dev)
 - PASSWORD=GANTI_DENGAN_PASSWORD_ANDA
 - API_KEY=GANTI_DENGAN_API_KEY_ANDA

Simpan file, lalu jalankan kembali container Docker dengan konfigurasi baru.
```
$ docker-compose up -d
```

## Konfigurasi (opsional)

Seluruh konfigurasi utama Chhoto URL diatur melalui environment variables di dalam file docker-compose.yml. Berikut adalah tiga variabel paling penting:

 - SITE_URL: Ini adalah alamat URL publik aplikasi Anda. Nilai ini wajib diisi dengan alamat yang diberikan oleh ngrok agar semua tautan pendek yang dihasilkan menjadi benar.
 - PASSWORD: Password yang Anda buat sendiri untuk login ke antarmuka web Chhoto URL.
 - API_KEY: Kunci rahasia yang Anda buat sendiri untuk otentikasi saat menggunakan API (misalnya, membuat tautan pendek via curl).

Setiap kali Anda mengubah nilai variabel ini, Anda harus menjalankan ulang container dengan docker-compose down dan docker-compose up -d agar perubahan diterapkan.

Setting server tambahan yang diperlukan untuk meningkatkan fungsi dan kinerja aplikasi, misalnya:
 - batas upload file
 - batas memori
 - dll

Plugin untuk fungsi tambahan
 - login dengan Google/Facebook
 - editor Markdown
 - dll


##  Maintenance (opsional)

Setting tambahan untuk maintenance secara periodik, misalnya:
- buat backup database tiap pekan
- hapus direktori sampah tiap hari
- dll


## Otomatisasi (opsional)

Skrip shell untuk otomatisasi instalasi, konfigurasi, dan maintenance.


## Cara Pemakaian

Setelah aplikasi berjalan dan dapat diakses melalui link ngrok:

 - Buka URL ngrok di browser. Anda mungkin akan melihat halaman peringatan dari ngrok. Klik "Visit Site" untuk melanjutkan.
 - Anda akan disambut oleh halaman login. Masukkan PASSWORD yang telah Anda atur di file docker-compose.yml.

Untuk Membuat Tautan Pendek:

 - Tempelkan URL panjang yang ingin Anda singkat di kolom "Long URL".
 - Anda bisa membiarkan "Short URL" kosong agar dibuat secara acak, atau mengisinya dengan teks kustom.
 - Klik "Go".

Tautan pendek baru Anda akan muncul di daftar di bawahnya. Anda dapat menyalinnya, melihat QR Code-nya, atau menghapusnya.

 - Tampilan aplikasi web
 - Fungsi-fungsi utama
 - Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


## Pembahasan

**Kelebihan Chhoto URL**

1. Efisiensi dalam Transmisi Data

Chhoto URL memperpendek panjang data yang dikirimkan dalam proses komunikasi HTTP, sehingga mempercepat waktu transmisi dan mengurangi overhead jaringan. Pemendekan URL secara langsung menurunkan ukuran payload pada lapisan aplikasi, yang berdampak pada efisiensi throughput jaringan, terutama pada koneksi dengan bandwidth terbatas.

2. Performa Tinggi dan Respons Cepat

Aplikasi ini dibangun menggunakan Rust dan framework Actix Web, yang memiliki keunggulan dalam penanganan I/O asinkron. Mekanisme tersebut memungkinkan server menangani banyak koneksi secara paralel tanpa penurunan kinerja. Dari sisi komunikasi data, ini meningkatkan efisiensi dalam pengiriman dan penerimaan paket pada lapisan transport.

3. Struktur Client–Server yang Jelas

Chhoto URL mengimplementasikan pola client–server secara eksplisit. Client mengirimkan permintaan HTTP untuk membuat atau mengakses URL pendek, dan server menanggapi dengan hasil atau melakukan redirect. Pola ini mencerminkan arsitektur komunikasi dua arah yang menjadi dasar interaksi jaringan modern berbasis TCP/IP.

4. Implementasi Protokol Standar Jaringan

Aplikasi ini beroperasi penuh di atas protokol HTTP/HTTPS, dengan penggunaan kode status seperti 301 (Permanent Redirect) dan 302 (Temporary Redirect). Hal tersebut menunjukkan penerapan standar komunikasi data pada lapisan aplikasi dan keterkaitannya dengan lapisan transport TCP. Setiap interaksi menunjukkan siklus permintaan dan respons yang sesuai dengan prinsip komunikasi berlapis OSI.

5. Portabilitas dan Fleksibilitas Jaringan

Chhoto URL dapat dijalankan di berbagai lingkungan jaringan—baik pada server lokal (intranet), cloud publik (Fly.io, Render, DigitalOcean), maupun jaringan privat dengan konfigurasi Docker. Portabilitas ini menunjukkan fleksibilitas arsitektur aplikasi dalam berbagai topologi jaringan, dari skala kecil hingga terdistribusi.

6. Transparansi Sistem dan Kemudahan Analisis Jaringan

Karena bersifat open-source, seluruh alur komunikasi dan manajemen data dapat dipelajari serta diaudit secara terbuka. Transparansi ini memungkinkan pengamatan terhadap bagaimana data dikirim, diterima, dan diproses pada berbagai lapisan jaringan, termasuk penanganan permintaan HTTP, pengalihan tautan, dan manajemen koneksi.

**Kekurangan Chhoto URL**

1. Skalabilitas Terbatas dalam Koneksi Jaringan

Chhoto URL menggunakan SQLite sebagai basis data lokal, yang hanya mampu menangani satu operasi tulis dalam satu waktu. Dalam konteks komunikasi jaringan, hal ini membatasi jumlah koneksi simultan dan throughput data, terutama saat banyak permintaan terjadi secara bersamaan.

2. Tidak Mendukung Distribusi Beban (Load Balancing)

Aplikasi tidak memiliki mekanisme pembagian beban trafik secara otomatis. Semua permintaan diarahkan ke satu instance server, menyebabkan potensi bottleneck pada lapisan aplikasi ketika beban jaringan meningkat. Hal ini membatasi efisiensi komunikasi data pada lingkungan multi-client.

3. Ketergantungan pada Keamanan Eksternal

Chhoto URL tidak menyediakan enkripsi internal maupun autentikasi tingkat jaringan. Keamanan komunikasi hanya bergantung pada lapisan eksternal, seperti penggunaan HTTPS melalui reverse proxy. Tanpa lapisan keamanan tambahan, komunikasi data rentan terhadap serangan sniffing atau injection pada jaringan terbuka.

4. Tidak Memiliki Pemantauan Trafik dan Performa Jaringan

Aplikasi ini tidak dilengkapi dengan fitur pemantauan (network monitoring) atau pengukuran performa seperti latency, packet loss, dan request time. Ketiadaan sistem pengawasan internal membatasi kemampuan untuk menganalisis efisiensi komunikasi data secara mendetail.

5. Dokumentasi Konfigurasi Jaringan Kurang Lengkap

Panduan resmi hanya berfokus pada instalasi aplikasi tanpa penjelasan detail mengenai integrasi dengan konfigurasi jaringan, seperti pengaturan port, NAT, atau firewall. Kondisi ini menyulitkan dalam pengelolaan konektivitas lintas jaringan atau penerapan sistem di lingkungan yang lebih kompleks.

6. Tidak Mendukung Redundansi dan Keandalan Tinggi

Chhoto URL belum memiliki mekanisme replikasi data atau sistem failover. Dalam konteks jaringan, hal ini berarti tidak ada jalur komunikasi cadangan jika terjadi kegagalan server utama. Akibatnya, ketahanan sistem terhadap gangguan jaringan tergolong rendah.

**Perbandingan Aplikasi Pemendek URL**

| Aspek | **Chhoto** | **Bitly** | **TinyURL** |
|:------|:------------|:-----------|:-------------|
| **Harga** | Gratis | Terbatas, langganan paling murah $10/bulan | Terbatas, langganan paling murah $10/bulan |
| **Skalabilitas** | Skalabilitas terbatas kecuali pengguna mengatur database & cache sendiri (Redis/PostgreSQL). | Dirancang untuk enterprise — dapat menangani jutaan request harian. | Tidak scalable untuk organisasi besar, hanya cocok personal. |
| **Dukungan Pengguna** | Komunitas GitHub & open issue, tanpa support resmi. | Dukungan pelanggan 24/7 untuk plan berbayar. | Dukungan minimal melalui FAQ. |
| **Kemudahan Instalasi & Pemeliharaan** | Mudah untuk developer: cukup git clone, npm install, dan deploy ke Railway/Vercel. | Tidak dapat diinstal lokal, hanya bisa pakai API atau dashboard web. | Tidak perlu instalasi. |


## Referensi

  * **[Chhoto URL - Repositori GitHub](https://www.google.com/search?q=https://github.com/sintan1729/chhoto-url)**
  * **[Ngrok - Situs Resmi & Dokumentasi](https://ngrok.com/)**
  * **[Docker - Situs Resmi](https://www.docker.com/)**

Cantumkan tiap sumber informasi yang anda pakai.
