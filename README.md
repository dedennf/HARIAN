# Hub Pribadi

Aplikasi pribadi untuk kuliah, riset, dan keuangan. Berjalan sebagai PWA (web app yang bisa dipasang di HP), tidak bergantung pada Claude, dan seluruh datamu tersimpan di perangkat sendiri.

## Isi folder

| File | Fungsi |
|---|---|
| index.html, app.css, app.js | Aplikasi |
| manifest.webmanifest, sw.js | Agar bisa dipasang di HP dan dibuka tanpa internet |
| icon.svg, icon-192.png, icon-512.png, icon-180.png | Ikon aplikasi |

Tidak ada langkah build dan tidak ada library luar. Semua file statis.

## Cara menjalankan

**Mencoba di laptop.** Buka terminal di folder ini, jalankan `python3 -m http.server 8000`, lalu buka http://localhost:8000. Membuka index.html langsung dengan klik ganda juga bisa, tapi mode offline dan pemasangan di HP tidak aktif.

**Dipakai sehari-hari (disarankan).** Taruh folder ini di hosting statis gratis supaya bisa dibuka dari HP lewat HTTPS. Pilihannya:
- Netlify: buka app.netlify.com/drop lalu seret folder ini.
- Cloudflare Pages atau GitHub Pages: unggah isi folder ke repositori lalu aktifkan Pages.

Yang diunggah hanya kode aplikasi. Datamu tidak ikut karena tersimpan di browser masing-masing perangkat. Orang yang membuka tautannya hanya melihat aplikasi kosong miliknya sendiri.

**Pasang di HP.** Android (Chrome): menu titik tiga, lalu Instal aplikasi. iPhone (Safari): tombol Bagikan, lalu Tambah ke Layar Utama. Setelah terpasang, aplikasi bisa dibuka tanpa internet.

## Cara memakai

Kolom di bagian atas setiap halaman adalah asisten. Ketik perintah biasa, lihat pratinjau, lalu tekan Simpan. Tidak ada yang tersimpan sebelum kamu menekan Simpan.

| Ketik | Hasil |
|---|---|
| kopi 15rb dana | Pengeluaran Rp 15.000, kategori Makan & minum, akun Dana |
| tarik tunai 200rb dari bri admin 2500 | Transfer BRI ke Tunai, plus pengeluaran biaya admin |
| topup dana 100rb dari bca | Transfer BCA ke Dana |
| gaji magang 1,5jt masuk bca | Pemasukan Rp 1.500.000 |
| kemarin bensin 25rb tunai | Pengeluaran bertanggal kemarin |
| tugas laporan srg deadline Jumat | Tugas baru di mata kuliah SRG |
| tugas laporan srg deadline Jumat kerjakan Rabu jam 19 | Tugas dengan tenggat Jumat dan rencana mengerjakan Rabu pukul 19.00 |
| uas 2 desember | Ujian dengan tenggat 2 Desember |
| ide: uji metode yang sama di kawah lain | Masuk ke Ide riset lanjutan |
| butuh izin masuk kawasan | Masuk ke Kebutuhan riset |
| berapa pengeluaran makan bulan ini | Dijawab dari datamu |
| saldo, saldo dana, tugas minggu ini | Dijawab dari datamu |

Agar perintah dikenali dengan baik:
- Tambahkan akunmu dulu di Keuangan, tab Akun. Nama akun harus muncul di perintah. Nama lain (misalnya gopay untuk Dana) diisi di form akun.
- Singkatan mata kuliah (misalnya srg) diisi di form mata kuliah.
- Kata kunci kategori bisa ditambah di Keuangan, tab Kategori.

Perintah biasa diproses langsung di perangkatmu, tanpa internet dan tanpa AI.

## Jadwal kuliah, tugas, dan kalender

- Saat menambah mata kuliah, formulir jadwal kelas terbuka otomatis. Jadwal berulang tiap minggu dan langsung tampil di kalender serta di Beranda pada hari kuliahnya.
- Kalender hanya menampilkan kelas milik **semester aktif**. Kalau kamu menambah mata kuliah semester lain dan semester aktif belum punya mata kuliah, semester aktif otomatis pindah. Kalau tidak, kalender menampilkan pemberitahuan beserta tombol untuk mengaktifkan semester itu.
- Rentang tanggal semester (diatur di Kuliah, tab Jadwal) membatasi kapan kelas tampil. Kelas otomatis dijeda selama hari libur yang kamu catat.
- Setiap tugas punya dua tanggal: **tenggat** (deadline) dan **dikerjakan pada** (beserta jam mulai dan selesai, opsional). Keduanya muncul di kalender dengan warna berbeda. Penanda pengerjaan hilang otomatis begitu tugas ditandai selesai.

## Menyambungkan Gemini (opsional)

Dipakai hanya untuk kalimat bebas yang tidak dikenali pengurai biasa, misalnya "tadi jajan nasi goreng empat puluh lima ribu".

1. Buat kunci API di Google AI Studio.
2. Buka Pengaturan, tab Asisten, isi kunci dan nama model, lalu tekan Uji koneksi.

Yang perlu kamu tahu:
- Yang dikirim ke Google hanya kalimat perintahmu serta daftar nama akun, kategori, dan mata kuliah. Saldo, riwayat transaksi, tugas, dan data lain tidak pernah dikirim.
- Pada tier gratis, Google menyatakan konten yang dikirim dapat dipakai untuk meningkatkan produk mereka.
- Kuota tier gratis berubah-ubah dan angkanya hanya terlihat di Google AI Studio. Kalau kuota habis, aplikasi menampilkan pesan dan perintah biasa tetap jalan.
- Nama model bisa berubah. Nilai bawaan adalah gemini-flash-latest. Kalau muncul pesan model tidak ditemukan, cek nama model terbaru di AI Studio lalu ubah di Pengaturan.
- Kunci API tersimpan di perangkat dan bisa terbaca oleh siapa pun yang memegang perangkatmu. Jangan isi di perangkat milik orang lain, dan jangan menulis kunci ke dalam kode yang diunggah.

## Data dan cadangan

- Data tersimpan di browser (IndexedDB), terpisah untuk tiap perangkat dan tiap alamat web. HP dan laptop tidak saling sinkron.
- Menghapus data situs atau data browser berarti data hilang. Unduh cadangan secara rutin dari Pengaturan, tab Data dan cadangan. Beranda akan mengingatkan kalau sudah lebih dari 14 hari.
- Memindahkan data antar perangkat: unduh cadangan JSON di satu perangkat, lalu pulihkan di perangkat lain.
- Transaksi juga bisa diunduh sebagai CSV untuk dibuka di Excel.
- Kunci API Gemini tidak ikut tersimpan di file cadangan.
- Jangan menulis nomor rekening, nomor kartu, PIN, atau kata sandi di aplikasi ini. Tidak ada kolom untuk itu, dan sebaiknya tidak dimasukkan ke kolom catatan juga.

## Fitur

**Kuliah:** mata kuliah per semester dengan filter semester, tugas dan ujian (dengan sub-tugas), materi, jadwal mingguan dengan hari libur, statistik.
**Riset:** progres dan target, kebutuhan riset, ide riset lanjutan, literatur (koleksi, tag, status verifikasi DOI, keputusan pakai atau tidak), log bimbingan.
**Keuangan:** akun, transaksi (masuk, keluar, transfer dengan biaya admin), kategori bawaan dan buatan sendiri, investasi, anggaran dengan batas harian, target tabungan, biaya sejati, utang dan piutang, tagihan berulang, pencocokan saldo, ringkasan dan grafik.
**Kalender gabungan:** tampilan hari, minggu, dan bulan untuk jadwal kuliah, tugas, ujian, milestone riset, bimbingan, dan tagihan.

## Yang belum ada

- Sinkron otomatis antar perangkat.
- Notifikasi. Pengingat hanya tampil di Beranda saat aplikasi dibuka.
- Harga investasi otomatis. Nilai sekarang diperbarui manual.
- Terhubung otomatis ke bank atau dompet digital.

## Catatan pengujian

Sudah diuji otomatis di Chromium (tampilan desktop dan HP): seluruh tab, pembuatan dan penghapusan data, perhitungan saldo dan transfer, pengurai perintah, cadangan dan pemulihan, mode offline, serta jalur Gemini dengan respons tiruan. Belum diuji di perangkat iPhone dan Android sungguhan, dan belum diuji dengan kunci Gemini asli. Kalau menemukan sesuatu yang janggal di perangkatmu, kabari supaya diperbaiki.

Literatur: tombol Salin daftar pustaka memakai format sederhana dan hanya memuat entri yang sudah terverifikasi dan berkeputusan Pakai. Cek ulang hasilnya dengan gaya sitasi yang dipakai kampusmu sebelum dimasukkan ke skripsi.
