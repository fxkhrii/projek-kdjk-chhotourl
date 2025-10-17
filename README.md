
# Aplikasi Web "Chhoto URL"


## Pengenalan Chhoto URL

Chhoto URL merupakan aplikasi pemendek tautan (URL shortener) yang dikembangkan menggunakan bahasa pemrograman Rust dengan framework Actix Web. Nama “Chhoto” berasal dari bahasa Bengali yang berarti “kecil”, merepresentasikan filosofi aplikasi ini: berukuran kecil namun memiliki kemampuan yang efisien dan bermanfaat besar.

Aplikasi ini dirancang sebagai web app ringan dan mandiri yang berfungsi untuk mengonversi tautan panjang menjadi versi yang lebih singkat, mudah diingat, dan praktis untuk dibagikan. Melalui pendekatan arsitektur yang minimalis, Chhoto URL menawarkan solusi cepat dan aman tanpa ketergantungan pada layanan pihak ketiga.

Dengan performa tinggi serta kemudahan penggunaan melalui antarmuka web maupun Command Line Interface (CLI), Chhoto URL menjadi pilihan ideal untuk individu maupun organisasi yang membutuhkan sistem pemendek tautan sederhana, efisien, dan dapat diandalkan.

## Instalasi

- Prasyarat, apa saja yang harus diinstal sebelumnya.
- Langkah instalasi dalam CLI.


## Konfigurasi (opsional)

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

- Tampilan aplikasi web
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


## Pembahasan

- Pendapat anda tentang aplikasi web ini

**Kelebihan & Kekurangan**
Chhoto URL memiliki beberapa keunggulan utama. Pertama, aplikasinya sangat ringan dan efisien, karena dibangun dengan teknologi yang cepat dan hemat sumber daya. Aplikasi ini dapat dijalankan pada server dengan spesifikasi rendah, bahkan di komputer pribadi, tanpa mengurangi kinerjanya. Kedua, sistemnya mudah digunakan, baik melalui antarmuka web maupun melalui perintah terminal (CLI). Pengguna cukup memasukkan URL panjang untuk mendapatkan versi pendek secara otomatis. Ketiga, Chhoto URL dapat dijalankan di berbagai platform, seperti Fly.io, Render, atau DigitalOcean, sehingga fleksibel untuk kebutuhan pribadi maupun organisasi kecil.

Dari sisi teknis, Chhoto URL juga memiliki struktur kerja yang sederhana namun efektif. Saat pengguna meminta pembuatan tautan pendek, server memproses data dan menghasilkan URL baru yang mengarah ke alamat asli. Proses ini berlangsung cepat dan stabil karena menggunakan sistem pemrosesan permintaan secara paralel. Selain itu, pengguna memiliki kontrol penuh terhadap data yang tersimpan, karena seluruh sistem dapat dihosting sendiri tanpa ketergantungan pada layanan pihak ketiga.

Namun, Chhoto URL juga memiliki beberapa kekurangan. Sistem penyimpanan datanya masih menggunakan SQLite, yang kurang optimal untuk jumlah pengguna yang besar atau trafik tinggi. Aplikasi ini juga belum memiliki fitur pembagian beban (load balancing) atau cadangan server (backup system), sehingga jika server mengalami gangguan, layanan akan berhenti sepenuhnya. Dari sisi keamanan, Chhoto URL belum memiliki sistem enkripsi internal atau pengamanan tambahan, sehingga pengguna perlu menambahkan lapisan keamanan sendiri seperti SSL atau firewall eksternal. Selain itu, fitur analisis penggunaan masih terbatas; aplikasi hanya menampilkan jumlah kunjungan tanpa statistik lebih lanjut seperti lokasi pengguna atau waktu akses.

## Referensi

Cantumkan tiap sumber informasi yang anda pakai.
