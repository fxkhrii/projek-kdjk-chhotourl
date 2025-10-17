# Aplikasi Web "Chhoto URL"


## Pengenalan Chhoto URL

Chhoto URL merupakan aplikasi pemendek tautan (URL shortener) yang dikembangkan menggunakan bahasa pemrograman Rust dengan framework Actix Web. Nama “Chhoto” berasal dari bahasa Bengali yang berarti “kecil”, merepresentasikan filosofi aplikasi ini: berukuran kecil namun memiliki kemampuan yang efisien dan bermanfaat besar.

Aplikasi ini dirancang sebagai web app ringan dan mandiri yang berfungsi untuk mengonversi tautan panjang menjadi versi yang lebih singkat, mudah diingat, dan praktis untuk dibagikan. Melalui pendekatan arsitektur yang minimalis, Chhoto URL menawarkan solusi cepat dan aman tanpa ketergantungan pada layanan pihak ketiga.

Dengan performa tinggi serta kemudahan penggunaan melalui antarmuka web maupun Command Line Interface (CLI), Chhoto URL menjadi pilihan ideal untuk individu maupun organisasi yang membutuhkan sistem pemendek tautan sederhana, efisien, dan dapat diandalkan.

## Instalasi

### Kebutuhan Sistem:

  *Sebuah Virtual Machine (misalnya VirtualBox dengan Kali Linux).
  - Docker dan Docker Compose terinstal di dalam VM.
  *Akun gratis di situs Ngrok.

### Proses Instalasi

Login ke dalam Virtual Machine Anda, buka terminal, lalu buat direktori proyek.

### Pindah ke direktori home
```
$ cd ~
```
### Membuat folder bernama chhoto-url dan masuk ke dalamnya
  $ mkdir chhoto-url && cd chhoto-url


Buat file konfigurasi docker-compose.yml menggunakan editor teks.

$ nano docker-compose.yml


Salin dan tempel seluruh konfigurasi berikut ke dalam editor. Ganti nilai PASSWORD dan API_KEY dengan nilai rahasia buatan Anda sendiri.

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


Jalankan container Docker di latar belakang dan verifikasi bahwa container sudah berjalan.

$ docker-compose up -d
$ docker-compose ps


Pastikan status container adalah Up atau Running.

Unduh Ngrok. Kunjungi halaman download Ngrok, klik kanan pada tombol download Linux, lalu "Salin alamat tautan".

# Pindah ke direktori home
$ cd ~
# Ganti "LINK_DARI_WEBSITE" dengan tautan yang Anda salin
$ wget "LINK_DARI_WEBSITE"
# Ekstrak file ke lokasi yang dapat diakses dari mana saja
$ sudo tar xvz ngrok-v3-*.tgz -C /usr/local/bin


Hubungkan program ngrok dengan akun Anda. Dapatkan authtoken dari dashboard Ngrok.

# Ganti <TOKEN_ANDA> dengan token dari dashboard
$ ngrok config add-authtoken <TOKEN_ANDA>


Buka "terowongan" ke port 4567. Biarkan terminal ini tetap berjalan.

$ ngrok http 4567


ngrok akan memberikan Anda sebuah URL publik di baris Forwarding. Salin URL HTTPS tersebut.

Buka terminal baru (jangan tutup terminal ngrok). Hentikan sementara container Docker untuk memperbarui konfigurasinya.

$ cd ~/chhoto-url
$ docker-compose down


Buka kembali file docker-compose.yml dan ubah nilai dari SITE_URL menjadi URL HTTPS yang Anda dapatkan dari ngrok.

$ nano docker-compose.yml


# ... (bagian lain dari file tetap sama)
environment:
  - SITE_URL=[https://URL-ACAK-DARI-NGROK.ngrok-free.dev](https://URL-ACAK-DARI-NGROK.ngrok-free.dev)
  - PASSWORD=GANTI_DENGAN_PASSWORD_ANDA
  - API_KEY=GANTI_DENGAN_API_KEY_ANDA


Simpan file, lalu jalankan kembali container Docker dengan konfigurasi baru.

$ docker-compose up -d


## Konfigurasi (opsional)

Seluruh konfigurasi utama Chhoto URL diatur melalui environment variables di dalam file docker-compose.yml. Berikut adalah tiga variabel paling penting:

SITE_URL: Ini adalah alamat URL publik aplikasi Anda. Nilai ini wajib diisi dengan alamat yang diberikan oleh ngrok agar semua tautan pendek yang dihasilkan menjadi benar.

PASSWORD: Password yang Anda buat sendiri untuk login ke antarmuka web Chhoto URL.

API_KEY: Kunci rahasia yang Anda buat sendiri untuk otentikasi saat menggunakan API (misalnya, membuat tautan pendek via curl).

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

Buka URL ngrok di browser. Anda mungkin akan melihat halaman peringatan dari ngrok. Klik "Visit Site" untuk melanjutkan.

Anda akan disambut oleh halaman login. Masukkan PASSWORD yang telah Anda atur di file docker-compose.yml.

Untuk Membuat Tautan Pendek:

Tempelkan URL panjang yang ingin Anda singkat di kolom "Long URL".

Anda bisa membiarkan "Short URL" kosong agar dibuat secara acak, atau mengisinya dengan teks kustom.

Klik "Go".

Tautan pendek baru Anda akan muncul di daftar di bawahnya. Anda dapat menyalinnya, melihat QR Code-nya, atau menghapusnya.

- Tampilan aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


## Pembahasan

Metode deployment menggunakan Docker di VM lokal yang di-ekspos melalui ngrok memiliki beberapa kelebihan dan kekurangan yang penting untuk dipahami.

Kelebihan
Gratis & Cepat: Tidak memerlukan biaya sewa VPS dan prosesnya sangat cepat untuk membuat aplikasi lokal menjadi publik.

Tidak Perlu Kartu Kredit: Tidak seperti layanan VPS, ngrok tidak memerlukan verifikasi kartu kredit untuk paket gratisnya.

Sangat Baik untuk Demo & Tugas: Metode ini sempurna untuk mempresentasikan proyek atau tugas tanpa perlu setup server yang rumit.

Kekurangan
Tidak Online 24/7: Aplikasi hanya dapat diakses selama komputer utama, VirtualBox, container Docker, dan terminal ngrok semuanya berjalan. Jika salah satu mati, link akan ikut mati.

URL Dinamis: Pada paket gratis ngrok, URL publik akan berubah setiap kali Anda menghentikan dan menjalankan kembali program ngrok.

Bergantung pada Koneksi Lokal: Kecepatan dan stabilitas aplikasi bergantung sepenuhnya pada kecepatan dan stabilitas koneksi internet di rumah Anda.

- Pendapat anda tentang aplikasi web ini

**Kelebihan & Kekurangan**

Chhoto URL memiliki beberapa keunggulan utama. Pertama, aplikasinya sangat ringan dan efisien, karena dibangun dengan teknologi yang cepat dan hemat sumber daya. Aplikasi ini dapat dijalankan pada server dengan spesifikasi rendah, bahkan di komputer pribadi, tanpa mengurangi kinerjanya. Kedua, sistemnya mudah digunakan, baik melalui antarmuka web maupun melalui perintah terminal (CLI). Pengguna cukup memasukkan URL panjang untuk mendapatkan versi pendek secara otomatis. Ketiga, Chhoto URL dapat dijalankan di berbagai platform, seperti Fly.io, Render, atau DigitalOcean, sehingga fleksibel untuk kebutuhan pribadi maupun organisasi kecil.

Dari sisi teknis, Chhoto URL juga memiliki struktur kerja yang sederhana namun efektif. Saat pengguna meminta pembuatan tautan pendek, server memproses data dan menghasilkan URL baru yang mengarah ke alamat asli. Proses ini berlangsung cepat dan stabil karena menggunakan sistem pemrosesan permintaan secara paralel. Selain itu, pengguna memiliki kontrol penuh terhadap data yang tersimpan, karena seluruh sistem dapat dihosting sendiri tanpa ketergantungan pada layanan pihak ketiga.

Namun, Chhoto URL juga memiliki beberapa kekurangan. Sistem penyimpanan datanya masih menggunakan SQLite, yang kurang optimal untuk jumlah pengguna yang besar atau trafik tinggi. Aplikasi ini juga belum memiliki fitur pembagian beban (load balancing) atau cadangan server (backup system), sehingga jika server mengalami gangguan, layanan akan berhenti sepenuhnya. Dari sisi keamanan, Chhoto URL belum memiliki sistem enkripsi internal atau pengamanan tambahan, sehingga pengguna perlu menambahkan lapisan keamanan sendiri seperti SSL atau firewall eksternal. Selain itu, fitur analisis penggunaan masih terbatas; aplikasi hanya menampilkan jumlah kunjungan tanpa statistik lebih lanjut seperti lokasi pengguna atau waktu akses.

## Referensi

  * **[Chhoto URL - Repositori GitHub](https://www.google.com/search?q=https://github.com/sintan1729/chhoto-url)**
  * **[Ngrok - Situs Resmi & Dokumentasi](https://ngrok.com/)**
  * **[Docker - Situs Resmi](https://www.docker.com/)**

Cantumkan tiap sumber informasi yang anda pakai.
