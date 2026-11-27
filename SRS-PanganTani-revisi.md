# Spesifikasi Kebutuhan Perangkat Lunak
## PanganTani

Versi 0.1 — Draf untuk validasi pemangku kepentingan\
Disusun oleh Tim Perancangan PanganTani (identitas penyusun belum ditetapkan)\
Organisasi belum ditetapkan\
19 November 2026

## Daftar Isi

- [1. Pendahuluan](#1-pendahuluan)
- [2. Gambaran Umum Produk](#2-gambaran-umum-produk)
- [3. Persyaratan](#3-persyaratan)
- [4. Verifikasi](#4-verifikasi)
- [5. Lampiran](#5-lampiran)

## Riwayat Revisi

| Nama | Tanggal | Perubahan | Versi |
|---|---|---|---|
| Tim Perancangan PanganTani | 19 November 2026 | Konsolidasi 30 FR, subfitur, NFR dan diagram dari pembahasan | 0.1 |

## 1. Pendahuluan

### 1.1 Tujuan Dokumen

Dokumen Spesifikasi Kebutuhan Perangkat Lunak (*Software Requirements Specification* atau SRS) ini menjadi acuan utama dalam pengembangan dan pengujian situs web PanganTani. Untuk membangun pemahaman yang sama di antara pemilik produk, pengembang, penguji, petani, dan perwakilan pembeli, dokumen ini menjelaskan ruang lingkup produk, perilaku yang harus disediakan sistem, serta kriteria verifikasinya. Seluruh persyaratan di dalamnya masih berstatus draf sampai memperoleh validasi dari para pemangku kepentingan.

### 1.2 Ruang Lingkup Produk

PanganTani berfokus pada penyaluran hasil panen surplus dari petani kepada pembeli lokal. Melalui katalog, petani dapat menawarkan hasil panen berlebih atau komoditas yang secara tampilan tidak memenuhi standar ritel kepada usaha kuliner, dapur umum, dan panti sosial. Selanjutnya, pembeli dapat mencari penawaran terdekat, melihat harga yang berlaku, memesan produk, serta menentukan jadwal pengambilan. Untuk mendukung proses tersebut, sistem juga menyediakan fasilitas pengaduan dan pelaporan distribusi.

Pada tahap awal, PanganTani menerapkan transaksi jual beli dengan mekanisme pengambilan mandiri. Pembeli melakukan pembayaran melalui transfer, lalu administrator memverifikasinya secara manual sebelum petani menyiapkan pesanan. Dengan demikian, donasi, integrasi layanan kurir, sensor kesegaran, dan pembayaran otomatis belum termasuk dalam ruang lingkup rancangan awal.

### 1.3 Definisi, Akronim, dan Singkatan

| Istilah | Definisi |
|---|---|
| Batas pemesanan | Waktu terakhir sistem menerima pesanan baru untuk penawaran. |
| FR | Functional Requirement, perilaku yang wajib disediakan sistem. |
| NFR | Non-Functional Requirement, kualitas dan batas operasional yang diuji. |
| Pangan tersalurkan | Berat yang dikonfirmasi diterima pada transaksi selesai. |
| Pangan terselamatkan | Pangan surplus berisiko terbuang yang benar-benar tersalurkan, mengikuti definisi dan bukti risiko yang disepakati. |
| Penawaran | Satu kelompok hasil panen milik petani dengan stok, kondisi, harga, dan jadwal tertentu. |
| Reservasi | Penahanan stok sementara untuk pesanan. |
| SDG | Sustainable Development Goal. |
| Tenggat pembayaran | Waktu terakhir pembeli mengirim pembayaran dan bukti untuk ditinjau. |

### 1.4 Referensi

Daftar rujukan ini bersifat informatif dan mendukung perumusan masalah, penyusunan persyaratan, serta perbandingan alur sistem. Tim perancangan menggunakan sumber tersebut sebagai bahan pertimbangan dalam merumuskan aturan bisnis. Pengguna tetap perlu memvalidasi kesesuaian aturan tersebut dengan proses yang akan dijalankan.

| ID | Pemilik, judul, versi/tahun | Penggunaan dan lokasi |
|---|---|---|
| R-01 | ISO/IEC/IEEE, Requirements Engineering, 29148:2018 | Struktur dan penelusuran kebutuhan. https://www.iso.org/standard/72089.html |
| R-02 | Bappenas, Kajian Food Loss and Waste di Indonesia, 2021 | Landasan masalah. https://lcdi-indonesia.id/wp-content/uploads/2021/06/Report-Kajian-FLW-FINAL-4.pdf |
| R-03 | Badan Pangan Nasional, Stop Boros Pangan, situs berjalan | Pembanding distribusi dan pelaporan. https://sbp.badanpangan.go.id/ |
| R-04 | Too Good To Go, How does the app work, situs berjalan | Pembanding pencarian, reservasi dan pengambilan. https://www.toogoodtogo.com/en-us/how-does-the-app-work |
| R-05 | Robert Evan Sanders, Dynamic Pricing and Organic Waste Bans, Marketing Science, 2024 (terbit daring pada 2023) | Dasar eksplorasi harga dinamis. https://doi.org/10.1287/mksc.2020.0214 |
| R-06 | FLW Protocol, FLW Accounting and Reporting Standard, 2016, Appendix E | Pencatatan berat pangan terselamatkan. https://flwprotocol.org/wp-content/uploads/2017/05/FLW_Standard_final_2016.pdf |
| R-07 | W3C, WCAG 2.2, Recommendation | Acuan aksesibilitas untuk pengujian proyek. https://www.w3.org/TR/WCAG22/ |
| R-08 | OWASP, ASVS 5.0.0 | Acuan kontrol autentikasi dan otorisasi. https://asvs.owasp.org/ |
| R-09 | WooCommerce, dokumentasi inventori dan transfer, situs berjalan | Pembanding reservasi dan verifikasi manual. https://woocommerce.com/document/configuring-woocommerce-settings/products/ dan https://woocommerce.com/document/bacs/ |
| R-10 | EPA Irlandia, proyek kalkulator karbon FoodCloud, situs berjalan | Pertimbangan kategori, transportasi dan skenario alternatif. https://www.epa.ie/our-services/research/epa-funded-research/epa-funded-projects/research-data-table-dev/calculation-of-the-carbon-footprint-of-the-activities-of-foodcloud-improve-impact-reporting.php |

### 1.5 Ikhtisar Dokumen

Dokumen ini menyajikan persyaratan PanganTani dari gambaran produk hingga rencana pengujian. Bagian 2 menjelaskan konteks penggunaan dan batasan produk. Bagian 3 merinci persyaratan serta aturan bisnis. Bagian 4 menjelaskan cara penguji memverifikasi persyaratan tersebut. Bagian 5 menghubungkan persyaratan dengan diagram dan mencatat keputusan yang masih terbuka.

Setiap subfitur memiliki ID unik dan mengikuti prioritas persyaratan induknya. Dalam persyaratan fungsional, kata “dapat” menyatakan kemampuan yang wajib disediakan oleh sistem.

## 2. Gambaran Umum Produk

### 2.1 Perspektif Produk

PanganTani dirancang sebagai situs web responsif baru dengan pengelolaan data terpusat. Sistem dapat menggunakan layanan eksternal untuk menampilkan peta dan mengirim tautan pemulihan akun. Pembayaran berlangsung melalui bank di luar situs web. Administrator memeriksa penerimaan dana, kemudian sistem mencatat hasil pemeriksaan tersebut.

### 2.2 Fungsi Produk

Rangkaian fungsi PanganTani mengikuti proses penyaluran hasil panen dari penerbitan penawaran hingga penerimaan barang. Pengguna mengelola akun dan lokasi, sedangkan petani mengajukan verifikasi sebelum menerbitkan penawaran. Setiap penawaran memuat informasi kelompok panen, stok, kondisi, dan jadwal pengambilan. Petani juga dapat menetapkan perubahan harga berdasarkan waktu.

Pembeli menggunakan katalog untuk mencari produk dan menyaring penawaran berdasarkan radius. Setelah pembeli membuat pesanan, sistem menahan stok selama proses pembayaran dan administrator memeriksa bukti transfer secara manual. Petani menyiapkan pesanan yang telah dibayar, lalu pembeli mengambil produk dan mengonfirmasi penerimaan. Pengguna dapat mengajukan pembatalan atau pengaduan sesuai status transaksi.

Fungsi pendukung memudahkan pengguna menemukan, mengelola, dan melaporkan penyaluran pangan. Sistem menyediakan notifikasi, favorit, dan papan kebutuhan pangan. Petani dapat menyalin penawaran lama ke draf baru. Hasil penyaluran dicatat dalam laporan yang mendukung estimasi emisi karbon dan ekspor data.

### 2.3 Batasan Produk

PanganTani menggunakan bahasa dan satuan yang sesuai dengan wilayah operasional awal. Antarmuka menggunakan bahasa Indonesia, harga ditampilkan dalam rupiah (IDR), dan berat dinyatakan dalam kilogram. Sistem menyimpan informasi waktu secara konsisten dan menampilkannya dalam zona waktu Asia/Jakarta.

Informasi masa simpan bersumber dari keterangan petani dan batas pemesanan. Informasi ini membantu pengguna menentukan waktu pemesanan serta pengambilan. Rancangan awal tidak menggunakan sensor untuk menilai kesegaran atau menjamin kelayakan pangan. Kerangka kerja perangkat lunak, penyedia peta, dan layanan hos masih perlu ditentukan.

### 2.4 Karakteristik Pengguna

Akses pada PanganTani mengikuti peran dan kepemilikan data. Pengunjung dapat melihat katalog tanpa akun, sedangkan pengguna terdaftar dapat mengakses fungsi yang berkaitan dengan akun dan perannya. Petani mengelola penawaran serta pesanan, pembeli melakukan transaksi, dan administrator menangani verifikasi serta pengawasan operasional.

| Aktor | Akses dan kebutuhan |
|---|---|
| Pengunjung | Pengunjung dapat membuka katalog dan detail publik, menyesuaikan tampilan, serta membagikan penawaran tanpa masuk. |
| Pengguna terdaftar | Pengguna terdaftar dapat memakai fungsi umum sesuai hak akses atas akun dan data. |
| Petani | Petani mengelola penawaran dan pesanannya. Penerbitan penawaran memerlukan verifikasi. Petani membutuhkan formulir sederhana yang dapat digunakan melalui ponsel. |
| Pembeli | Usaha kuliner, dapur umum, dan panti sosial dapat berperan sebagai pembeli. Pembeli mengelola pesanan, favorit, dan permintaan pangan miliknya. |
| Administrator | Administrator menggunakan akun internal untuk melakukan verifikasi, moderasi, penyelesaian masalah, dan pelaporan. Setiap keputusan dapat diaudit. |

### 2.5 Asumsi dan Ketergantungan

Rancangan awal menetapkan satu penawaran dari satu petani untuk setiap pesanan. Pembeli memesan dalam kilogram dengan ketelitian hingga tiga angka di belakang koma. Harga dinyatakan dalam rupiah per kilogram. Dukungan untuk produk yang dijual per ikat atau per buah memerlukan kesepakatan tentang konversi berat.

Proses pembayaran bergantung pada konfirmasi penerimaan transfer. Dalam draf ini, pembeli mentransfer dana langsung ke rekening petani yang tercatat pada pesanan. Administrator memerlukan cara untuk mengonfirmasi penerimaan dana. Jika terjadi pengembalian dana, transaksi dilakukan di luar aplikasi dan buktinya dicatat dalam sistem. Pilihan operasional ini perlu dikonfirmasi sebelum sistem digunakan di lingkungan produksi.

Operasi PanganTani bergantung pada koneksi internet dan ketepatan data pengguna. Pengguna menyediakan informasi kondisi produk, lokasi, dan penerimaan barang. Jika layanan peta gagal, pengguna tetap dapat melihat penawaran dalam bentuk daftar. Peluncuran estimasi emisi karbon bergantung pada ketersediaan faktor emisi dan metode perhitungan yang sesuai dengan konteks lokal.

### 2.6 Pembagian Prioritas Persyaratan

Urutan pengembangan yang diusulkan dimulai dari persyaratan berprioritas Inti. Fitur berprioritas Pembeda ditargetkan setelah alur inti lulus pengujian. Fitur Pelengkap dan Pembeda lanjutan dijadwalkan pada iterasi berikutnya sesuai kapasitas pengembangan. Bagian 3.2 mencatat prioritas setiap persyaratan fungsional.

## 3. Persyaratan

### 3.1 Antarmuka Eksternal

#### 3.1.1 Antarmuka Pengguna

Antarmuka PanganTani mendukung penelusuran produk, pengelolaan akun, dan pelaksanaan transaksi. Pengunjung menggunakan halaman katalog dan detail produk. Pengguna terdaftar juga dapat mengakses halaman akun, konfirmasi pesanan, riwayat, notifikasi, dan papan kebutuhan sesuai perannya. Petani serta administrator menggunakan dasbor masing-masing.

Antarmuka memberi umpan balik setelah pengguna memasukkan data atau melakukan tindakan. Setiap formulir menampilkan pesan validasi pada kolom terkait. Setelah pengguna melakukan pemesanan atau pembayaran, sistem menampilkan status berhasil, gagal, atau masih diproses. Pengguna dapat memeriksa hasil tindakan sebelum mencoba kembali.

#### 3.1.2 Antarmuka Perangkat Keras

PanganTani dapat digunakan melalui peramban pada komputer dan ponsel. Pengguna dapat memakai geolokasi perangkat jika memberikan izin, serta memilih foto dari penyimpanan perangkat saat mengunggah berkas. Rancangan awal berjalan tanpa integrasi sensor fisik.

#### 3.1.3 Antarmuka Perangkat Lunak

Pertukaran data antara peramban dan sistem di lingkungan produksi menggunakan HTTPS. Sistem memvalidasi lintang dan bujur pada data lokasi. Tautan untuk mengatur ulang kata sandi dikirim melalui kanal kontak akun yang telah terverifikasi. Spesifikasi antarmuka pemrograman aplikasi (API) dan kontrak integrasi dirinci setelah penyedia layanan peta dan surel dipilih.

Sistem memeriksa jenis dan isi berkas yang diunggah pada server. Foto dan bukti pembayaran dapat diunggah dalam format JPEG atau PNG. Batas ukuran yang diusulkan adalah 5 MB per berkas.

Laporan diekspor dalam format CSV dengan pengodean UTF-8. Berkas memuat tanggal, ID transaksi, komoditas, wilayah, berat dalam kilogram, dan status. Sistem menetralkan isi sel yang dapat dijalankan sebagai rumus oleh aplikasi lembar kerja.

### 3.2 Fungsi

Persyaratan fungsional PanganTani dikelompokkan berdasarkan peran pengguna agar tanggung jawab dan batas akses setiap aktor dapat dipahami dengan jelas. Diagram _use case_ memetakan fungsi yang digunakan oleh masing-masing aktor, sedangkan diagram aktivitas memperlihatkan urutan tindakan dan percabangan dalam proses penyaluran pangan. Rincian visualnya tersedia pada [diagram use case](use-case.md) dan [diagram aktivitas](activity-diagram.md).

#### Ruang Lingkup Umum

Fungsi umum mendukung pengguna saat mengakses dan menjelajahi PanganTani. Pengunjung dapat melihat katalog dan membagikan penawaran. Pengguna yang telah masuk dapat mengelola profil dan membuka pemberitahuan sesuai hak aksesnya. Pengaturan tampilan membantu pengguna menyesuaikan kontras dan ukuran teks.

**FR-UM-01 — Registrasi dan akses akun** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-UM-01.1 | Pengguna dapat mendaftar sebagai petani atau pembeli dengan nama, kontak dan kata sandi. |
| FR-UM-01.2 | Pengguna dapat masuk, keluar dan mengakses halaman sesuai peran. |
| FR-UM-01.3 | Pengguna dapat meminta tautan reset kata sandi sekali pakai dengan masa berlaku. |
| FR-UM-01.4 | Sistem memeriksa peran dan kepemilikan data pada setiap tindakan terlindungi. |

**FR-UM-02 — Pengaturan profil** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-UM-02.1 | Pengguna dapat mengubah nama, kontak dan informasi usaha atau organisasi. |
| FR-UM-02.2 | Pengguna dapat menambah dan mengubah alamat. |
| FR-UM-02.3 | Pengguna dapat memilih titik lokasi melalui perangkat atau secara manual. |

**FR-UM-03 — Katalog dan detail produk** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-UM-03.1 | Pengunjung dapat melihat penawaran aktif. |
| FR-UM-03.2 | Pengunjung dapat melihat foto, kondisi, tanggal panen, harga, stok dan batas pemesanan. |
| FR-UM-03.3 | Sistem menampilkan area pengambilan kepada pengunjung. Alamat lengkap hanya ditampilkan kepada pihak yang berhak mengakses transaksi terkait. |

**FR-UM-04 — Preferensi aksesibilitas** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-UM-04.1 | Pengguna dapat menyalakan dan mematikan mode kontras tinggi. |
| FR-UM-04.2 | Pengguna dapat memperbesar teks serta memulihkan ukuran awal. |
| FR-UM-04.3 | Sistem menyimpan dan memulihkan preferensi tampilan saat kunjungan berikutnya. |

**FR-UM-05 — Pusat notifikasi** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-UM-05.1 | Pengguna dapat melihat notifikasi pesanan, perubahan status dan tenggat yang relevan. |
| FR-UM-05.2 | Pengguna dapat menandai notifikasi sebagai terbaca. |
| FR-UM-05.3 | Pengguna dapat membuka produk atau pesanan dari tautan pada notifikasi sesuai hak aksesnya. |

**FR-UM-06 — Bagikan penawaran** · Pelengkap

| ID | Persyaratan subfitur |
|---|---|
| FR-UM-06.1 | Pengunjung dapat menyalin tautan produk. |
| FR-UM-06.2 | Halaman yang dibuka melalui tautan penawaran tetap menampilkan status terakhir meskipun produk sudah habis atau penawarannya ditutup. |
| FR-UM-06.3 | Halaman menampilkan penawaran aktif sejenis jika tersedia. |

#### Ruang Lingkup Petani

Fungsi petani mendukung pengelolaan panen dari pengajuan verifikasi hingga penyaluran. Setelah lolos verifikasi, petani dapat menerbitkan penawaran, mengatur stok dan harga, serta menentukan jadwal pengambilan. Setelah pesanan diproses, petani dapat memantau hasilnya melalui riwayat dan ringkasan penyaluran.

**FR-PT-01 — Pengajuan verifikasi** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-01.1 | Petani dapat mengirim data dan bukti pengajuan. |
| FR-PT-01.2 | Petani dapat melihat apakah pengajuannya sedang ditinjau, perlu diperbaiki, disetujui, atau ditolak, beserta alasan yang tercatat. |
| FR-PT-01.3 | Petani dapat memperbaiki dan mengirim ulang pengajuan. |

**FR-PT-02 — Pengelolaan hasil panen** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-02.1 | Petani dapat menyimpan draf berisi komoditas, foto, alasan surplus, kondisi, tanggal panen, berat, harga dan batas pemesanan. |
| FR-PT-02.2 | Petani terverifikasi dapat meninjau dan menerbitkan penawaran yang lengkap. |
| FR-PT-02.3 | Petani dapat mengedit penawaran tanpa mengubah rincian pesanan yang telah dibuat. |
| FR-PT-02.4 | Petani dapat menutup penawaran untuk menghentikan pesanan baru. |

**FR-PT-03 — Stok dan kondisi** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-03.1 | Petani dapat melihat jumlah stok yang tersedia, sedang direservasi, dan telah terjual. |
| FR-PT-03.2 | Petani dapat mengoreksi jumlah stok yang tersedia. Jika stok menjadi kurang untuk memenuhi pesanan aktif, sistem membuka proses penanganan transaksi. |
| FR-PT-03.3 | Petani dapat mencatat perubahan kondisi dan menutup penawaran lebih awal. |

**FR-PT-04 — Jadwal pengambilan** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-04.1 | Petani dapat menambah tanggal dan rentang jam pengambilan. |
| FR-PT-04.2 | Petani dapat mengubah jadwal pengambilan yang tersedia bagi pesanan baru. |
| FR-PT-04.3 | Petani dapat mengusulkan jadwal baru untuk pesanan aktif. Sistem menerapkan perubahan setelah pembeli menyetujuinya. |

**FR-PT-05 — Pemrosesan pesanan** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-05.1 | Petani dapat melihat daftar pesanan berdasarkan status. |
| FR-PT-05.2 | Petani dapat melihat jumlah, jadwal, dan status pembayaran pada pesanan miliknya. |
| FR-PT-05.3 | Petani dapat menandai pesanan yang telah dibayar sebagai siap diambil. Sistem kemudian mengirim pemberitahuan kepada pembeli. |
| FR-PT-05.4 | Petani dapat melihat konfirmasi penerimaan atau masalah transaksi. |

**FR-PT-06 — Harga dinamis** · Pembeda

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-06.1 | Petani dapat mengatur harga awal, minimum dan jadwal perubahan. |
| FR-PT-06.2 | Petani dapat melihat pratinjau harga per tahap. |
| FR-PT-06.3 | Sistem menerapkan harga sesuai waktu untuk pesanan baru dan menyimpan harga pesanan aktif. |

**FR-PT-07 — Ringkasan penyaluran** · Pembeda

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-07.1 | Petani dapat memfilter riwayat menurut periode dan status. |
| FR-PT-07.2 | Petani dapat melihat berat yang diterima pada transaksi selesai. |
| FR-PT-07.3 | Petani dapat melihat jumlah stok yang belum tersalurkan pada setiap penawaran. |

**FR-PT-08 — Salin penawaran** · Pelengkap

| ID | Persyaratan subfitur |
|---|---|
| FR-PT-08.1 | Petani dapat menyalin informasi dasar penawaran menjadi draf baru. |
| FR-PT-08.2 | Sistem meminta petani mengisi tanggal panen, kondisi, stok, dan batas pemesanan baru sebelum menerbitkan penawaran. |
| FR-PT-08.3 | Petani dapat meninjau dan menerbitkan draf hasil salinan setelah validasi. |

#### Ruang Lingkup Pembeli

Fungsi pembeli mendukung pencarian produk dan penyelesaian pesanan. Pembeli dapat mencari penawaran dalam radius tertentu, memilih jadwal pengambilan, mengirim bukti pembayaran, dan mencatat berat produk yang diterima. Favorit, pengingat, dan papan kebutuhan pangan membantu pembeli mencari penawaran yang sesuai.

**FR-PB-01 — Pencarian dan filter** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-01.1 | Pembeli dapat mencari komoditas berdasarkan nama. |
| FR-PB-01.2 | Pembeli dapat menyaring hasil pencarian berdasarkan kategori, harga, stok, dan jadwal. |
| FR-PB-01.3 | Jika pencarian tidak menghasilkan penawaran, sistem menampilkan pemberitahuan dan menyediakan pilihan untuk menghapus filter. |

**FR-PB-02 — Pencarian radius** · Pembeda

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-02.1 | Pembeli dapat menggunakan lokasi perangkat atau menentukan titik acuan secara manual. |
| FR-PB-02.2 | Pembeli dapat memilih radius pencarian dan mengurutkan penawaran berdasarkan jarak terdekat. |
| FR-PB-02.3 | Pembeli dapat melihat hasil yang sama pada daftar dan peta dengan label jarak garis lurus. |

**FR-PB-03 — Pemesanan dan reservasi** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-03.1 | Pembeli dapat memilih jumlah dan jadwal serta melihat total biaya. |
| FR-PB-03.2 | Sistem memeriksa stok, jadwal, batas pemesanan, dan harga sebelum membuat pesanan. Jika harga berubah, pembeli harus menyetujui harga terbaru. |
| FR-PB-03.3 | Sistem membuat pesanan dan reservasi stok dalam satu operasi yang berhasil atau gagal secara keseluruhan. Sistem menolak jumlah pesanan yang melebihi stok tersedia. |
| FR-PB-03.4 | Sistem membatalkan pesanan yang mencapai tenggat sesuai BR-04 dan melepaskan reservasi stok tepat satu kali. |

**FR-PB-04 — Pembayaran** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-04.1 | Pembeli dapat melihat tagihan, instruksi dan tenggat pembayaran. |
| FR-PB-04.2 | Pembeli dapat mengirim bukti pembayaran untuk pesanan miliknya. |
| FR-PB-04.3 | Pembeli dapat melihat hasil verifikasi dan alasan penolakan. |

**FR-PB-05 — Penerimaan dan riwayat** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-05.1 | Pembeli dapat melihat riwayat dan detail pesanan miliknya. |
| FR-PB-05.2 | Pembeli dapat melihat lokasi, petunjuk, dan jadwal pengambilan. Jika petani mengusulkan jadwal baru, pembeli dapat menerima atau menolaknya. |
| FR-PB-05.3 | Pembeli dapat mencatat berat produk yang diterima. Jika terdapat selisih berat, sistem membuka proses penanganan sebelum transaksi diselesaikan. |

**FR-PB-06 — Pembatalan dan pengaduan** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-06.1 | Pembeli dapat meminta pembatalan sesuai BR-06 dan melihat konfirmasi. |
| FR-PB-06.2 | Pembeli dapat mengirim pengaduan terkait pesanan dengan uraian dan bukti opsional. |
| FR-PB-06.3 | Pembeli dapat melihat tanggapan admin, hasil penyelesaian dan status pengembalian dana. |

**FR-PB-07 — Penawaran segera ditutup** · Pembeda

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-07.1 | Pembeli dapat melihat penawaran aktif yang mendekati batas pemesanan sesuai ambang waktu yang ditetapkan. |
| FR-PB-07.2 | Sistem menampilkan sisa waktu dan jadwal pengambilan. |
| FR-PB-07.3 | Sistem menghentikan pemesanan baru saat batas tercapai meskipun halaman belum dimuat ulang. |

**FR-PB-08 — Favorit dan pengingat** · Pelengkap

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-08.1 | Pembeli dapat menyimpan komoditas favorit dan mengikuti petani. |
| FR-PB-08.2 | Pembeli dapat menentukan radius serta mengaktifkan atau menonaktifkan pengingat. |
| FR-PB-08.3 | Sistem mengirim satu notifikasi untuk setiap penawaran baru yang cocok bagi pengguna yang sama. |

**FR-PB-09 — Papan kebutuhan pangan** · Pembeda lanjutan

| ID | Persyaratan subfitur |
|---|---|
| FR-PB-09.1 | Pembeli dapat menerbitkan permintaan yang memuat jenis komoditas, jumlah, area, dan tanggal kebutuhan. |
| FR-PB-09.2 | Petani dapat menanggapi permintaan aktif dengan jumlah, harga dan jadwal yang terkait penawaran miliknya. |
| FR-PB-09.3 | Pembeli dapat memilih tanggapan dan melanjutkan ke tahap konfirmasi pesanan. Sistem memeriksa stok dan harga yang berlaku. |
| FR-PB-09.4 | Pembeli dapat menandai kebutuhan sebagai terpenuhi atau menutup permintaan. Sistem menutup permintaan yang melewati batas waktu. |

#### Ruang Lingkup Administrator

Fungsi administrator mendukung pemeriksaan transaksi dan pelaporan distribusi. Administrator meninjau pengajuan petani dan bukti pembayaran, menindaklanjuti pengaduan, serta menyelesaikan masalah transaksi. Dasbor dan ekspor menyediakan data untuk meninjau hasil penyaluran.

**FR-AD-01 — Verifikasi petani** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-AD-01.1 | Administrator dapat memfilter antrean pengajuan menurut status. |
| FR-AD-01.2 | Administrator dapat memeriksa data dan bukti pengajuan. |
| FR-AD-01.3 | Administrator dapat menyetujui pengajuan, meminta perbaikan, atau menolak pengajuan dengan alasan. Sistem mencatat keputusan dan memberitahukan hasilnya kepada pemohon. |

**FR-AD-02 — Verifikasi pembayaran** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-AD-02.1 | Administrator dapat melihat antrean bukti pembayaran. |
| FR-AD-02.2 | Administrator dapat mencocokkan bukti dengan tagihan dan penerimaan dana. |
| FR-AD-02.3 | Administrator dapat menyetujui atau menolak bukti pembayaran dengan menyertakan alasan. Pengulangan keputusan yang sama tidak menggandakan perubahan stok atau status. |

**FR-AD-03 — Moderasi dan pengaduan** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-AD-03.1 | Administrator dapat memfilter laporan berdasarkan jenis dan status. |
| FR-AD-03.2 | Administrator dapat meminta klarifikasi kepada pihak terkait. |
| FR-AD-03.3 | Administrator dapat menonaktifkan penawaran dengan alasan tanpa menghapus pesanan aktif. |
| FR-AD-03.4 | Administrator dapat menutup laporan setelah mencatat hasil penanganan. Sistem memberitahukan hasilnya kepada pihak terkait. |

**FR-AD-04 — Transaksi bermasalah** · Inti

| ID | Persyaratan subfitur |
|---|---|
| FR-AD-04.1 | Administrator dapat melihat riwayat status, pembayaran, jadwal dan bukti transaksi. |
| FR-AD-04.2 | Administrator dapat menangani selisih berat, kegagalan serah terima, atau pembatalan. Administrator mencatat keputusan penyelesaiannya. |
| FR-AD-04.3 | Administrator dapat mencatat nominal, bukti dan status pengembalian dana. |

**FR-AD-05 — Dasbor distribusi** · Pembeda

| ID | Persyaratan subfitur |
|---|---|
| FR-AD-05.1 | Sistem menjumlahkan berat yang diterima dan memasukkan setiap transaksi selesai tepat satu kali ke dalam perhitungan. |
| FR-AD-05.2 | Administrator dapat menyaring laporan berdasarkan periode, wilayah, dan komoditas. |
| FR-AD-05.3 | Administrator dapat melihat transaksi yang diperhitungkan dalam setiap total. |

**FR-AD-06 — Estimasi karbon** · Pembeda lanjutan

| ID | Persyaratan subfitur |
|---|---|
| FR-AD-06.1 | Administrator dapat menyimpan faktor emisi, satuan, kategori, sumber dan versi. |
| FR-AD-06.2 | Sistem menghitung estimasi untuk data yang memenuhi metode perhitungan dan memiliki faktor emisi yang sesuai. |
| FR-AD-06.3 | Dasbor menampilkan metode, asumsi, versi faktor dan data yang belum dapat dihitung. |

**FR-AD-07 — Ekspor laporan** · Pelengkap

| ID | Persyaratan subfitur |
|---|---|
| FR-AD-07.1 | Administrator dapat memilih cakupan dan filter laporan. |
| FR-AD-07.2 | Administrator dapat mengunduh laporan berformat CSV yang isinya sesuai dengan filter aktif. |
| FR-AD-07.3 | CSV memuat periode, satuan berat dan waktu pembuatan. |

#### Aturan bisnis dan status

Aturan bisnis menentukan kapan sistem menerima pesanan, menahan stok, dan mencatat hasil penyaluran. Setelah pembeli membuat pesanan, status transaksi berubah menurut hasil pemeriksaan pembayaran dan serah terima. Jika transaksi perlu dibatalkan atau terjadi selisih berat, sistem mengikuti aturan penanganan sebelum mengubah stok atau laporan.

| ID | Aturan bisnis dalam draf |
|---|---|
| BR-01 | Stok tersedia dihitung dengan mengurangi stok yang dapat dijual dengan jumlah yang sedang direservasi. Jika permintaan dikirim kembali dengan ID yang sama, sistem mengembalikan pesanan yang sama. Stok tidak boleh bernilai negatif. |
| BR-02 | Sistem menghitung dan menyimpan harga akhir bersama rincian produk ketika pembeli mengonfirmasi pesanan. Total diperoleh dari berat dalam kilogram dikalikan dengan harga per kilogram, lalu dibulatkan ke rupiah terdekat. Pengambilan mandiri pada rancangan awal tidak dikenai biaya. |
| BR-03 | Sistem menggunakan waktu server untuk menentukan perubahan harga dan batas pemesanan. Jadwal pengambilan harus memungkinkan pesanan dipenuhi. Penyaringan berdasarkan radius menggunakan jarak garis lurus. |
| BR-04 | Tenggat pembayaran awal diusulkan selama 30 menit dan tidak boleh melewati batas pemesanan maupun awal jadwal pengambilan. Jika bukti diterima sebelum tenggat, pembayaran masuk ke status menunggu verifikasi dan stok tetap ditahan. Pesanan yang masih menunggu pembayaran tanpa bukti kedaluwarsa secara otomatis. Pembeli dapat memperbaiki bukti yang ditolak sebelum tenggat. Setelah tenggat, administrator menangani kasus dan memeriksa apakah dana telah diterima sebelum membatalkan pesanan. |
| BR-05 | Administrator hanya menandai pesanan sebagai terbayar setelah mengonfirmasi penerimaan dana. Jika jadwal pengambilan terlewati saat pembayaran masih dalam antrean, sistem menandai pesanan untuk ditangani tanpa mengubah statusnya secara otomatis menjadi terbayar atau selesai. |
| BR-06 | Sistem dapat langsung membatalkan pesanan atas permintaan pembeli jika pesanan masih menunggu pembayaran tanpa bukti. Setelah bukti dikirim atau pembayaran disetujui, administrator menangani permintaan pembatalan dan pengembalian dana jika diperlukan. Sistem melepaskan reservasi tepat satu kali. Stok hanya kembali ditampilkan apabila penawaran masih aktif dan petani menyatakan produk masih layak ditawarkan. |
| BR-07 | Penutupan penawaran menghentikan penerimaan pesanan baru dan mempertahankan catatan pesanan aktif. Jika perubahan kondisi produk mengganggu pemenuhan pesanan aktif, sistem membuka proses penanganan dan memberi tahu pembeli. |
| BR-08 | Perubahan jadwal pesanan aktif memerlukan persetujuan pembeli. Jika pembeli menolak jadwal baru, jadwal lama tetap berlaku. Jika jadwal lama tidak dapat dipenuhi, administrator menangani kasus tersebut. |
| BR-09 | Sistem menyelesaikan pesanan setelah pembeli mengonfirmasi bahwa berat yang diterima sesuai dengan pesanan. Jika terdapat selisih, administrator menangani kasus dan mencatat berat akhir, alasan, serta kesepakatan sebelum menyelesaikan transaksi. Sistem tidak menyelesaikan pesanan secara otomatis selama pembeli belum memberikan konfirmasi. |
| BR-10 | Dasbor menghitung berat akhir yang diterima tepat satu kali untuk setiap transaksi selesai. Jika terjadi koreksi, sistem menyimpan jejak audit dan memperbarui total tanpa menggandakan catatan. |
| BR-11 | Rancangan awal menggunakan istilah pangan tersalurkan. Istilah pangan terselamatkan hanya dapat digunakan setelah definisi risiko pangan terbuang dan bukti yang diperlukan disepakati. Estimasi karbon harus dapat ditelusuri melalui faktor emisi, satuan, sumber, versi, dan asumsi. Sistem menandai data tanpa faktor sebagai belum dihitung. |
| BR-12 | Reservasi stok dilakukan melalui proses pemesanan. Setelah pembeli memilih tanggapan pada papan kebutuhan, sistem membuka konfirmasi pesanan dan menjalankan validasi yang sama dengan pemesanan dari katalog. |

| Entitas | Status utama | Pengendali perpindahan |
|---|---|---|
| Verifikasi petani | Ditinjau → perlu perbaikan/disetujui/ditolak | Petani mengirim pengajuan, lalu administrator memutuskan hasil verifikasi. |
| Penawaran | Draf → aktif → habis/ditutup/kedaluwarsa | Petani, admin dan waktu server. |
| Pesanan | Menunggu pembayaran → menunggu verifikasi → diproses → siap diambil → selesai | Pembeli, admin dan petani sesuai peran. |
| Pesanan alternatif | Menunggu pembayaran → dibatalkan, atau transaksi aktif → bermasalah → selesai/dibatalkan | Tenggat, pembeli sesuai BR-06, atau admin. |
| Pembayaran | Belum dibayar → ditinjau → disetujui/ditolak | Admin mengonfirmasi penerimaan dana. |
| Pengembalian dana | Tidak diperlukan/diajukan/diproses/selesai | Admin mencatat tindakan di luar sistem dan buktinya. |

### 3.3 Kualitas Layanan

Bagian ini menetapkan target kualitas yang diusulkan sebagai kriteria penerimaan sistem. Penilaian mencakup kinerja, keamanan, keandalan, ketersediaan, observabilitas, kebergunaan, aksesibilitas, dan kompatibilitas. Agar hasilnya dapat ditelusuri dan dibandingkan, setiap pengukuran harus mencantumkan lingkungan pengujian serta himpunan data yang digunakan.

#### 3.3.1 Kinerja

- **NFR-01** — Sistem harus merespons sekurang-kurangnya 95% permintaan pencarian dan detail produk dalam waktu maksimal 2 detik. Pengukuran dilakukan dengan 100 pengguna aktif bersamaan dan menggunakan himpunan data uji yang diusulkan sebanyak 10.000 penawaran. Lingkungan uji dicatat, sedangkan waktu transfer gambar dan layanan pihak ketiga diukur secara terpisah.
- **NFR-10** — Sistem harus menampilkan perubahan stok, harga, dan status pada sesi lain dalam waktu maksimal 30 detik pada koneksi normal. Saat pesanan dikonfirmasi, server selalu memeriksa data terkini.

#### 3.3.2 Keamanan

- **NFR-05** — Sistem produksi harus menggunakan HTTPS dan melindungi akun serta sesi pengguna. Sistem menggunakan fungsi hash yang sesuai untuk kata sandi serta memeriksa unggahan dan otorisasi pada server. Pengujian harus menunjukkan bahwa sistem menolak akses lintas peran atau akun yang tidak berwenang.
- **NFR-06** — Sistem membatasi akses ke kontak, alamat lengkap, dan bukti transaksi kepada pemilik data, pihak transaksi yang membutuhkan informasi tersebut, serta administrator yang berwenang. Akses langsung melalui tautan berkas tetap memerlukan pemeriksaan hak akses.

#### 3.3.3 Keandalan

- **NFR-07** — Sistem harus menjaga agar stok tidak bernilai negatif ketika dua pembeli memesan secara bersamaan. Pengulangan permintaan, konfirmasi, atau pelepasan reservasi tidak boleh menggandakan transaksi maupun pencatatan dampaknya.
- **NFR-13** — Pengguna harus tetap dapat membuka katalog dalam bentuk daftar jika peta gagal dimuat. Jika koneksi terputus setelah pemesanan, pengguna harus dapat memeriksa hasilnya tanpa membuat pesanan duplikat.

#### 3.3.4 Ketersediaan

- **NFR-08** — Target ketersediaan layanan produksi adalah 99,5% per bulan. Ketersediaan dihitung dengan membagi jumlah menit layanan beroperasi dengan jumlah menit pemantauan. Periode pemeliharaan dicatat secara terpisah dalam laporan.
- **NFR-09** — Cadangan dibuat setiap hari dengan target kehilangan data maksimal 24 jam dan waktu pemulihan maksimal 4 jam. Prosedur pemulihan harus diuji sebelum peluncuran.

#### 3.3.5 Observabilitas

- **NFR-12** — Sistem harus mencatat perubahan stok, harga, pembayaran, status, dan keputusan administrator agar dapat diaudit. Catatan memuat pelaku, waktu, objek, nilai sebelum dan sesudah perubahan, serta alasan jika relevan. Kata sandi dan token pengaturan ulang tidak boleh tercatat dalam log. Aturan harga, reservasi, dan perhitungan dampak harus diuji secara otomatis.

#### 3.3.6 Kebergunaan, Aksesibilitas, dan Kompatibilitas

- **NFR-02** — Pengguna harus dapat menggunakan dasbor dan menyelesaikan alur dari katalog hingga pemesanan pada lebar layar 360–1440 piksel tanpa menggulir halaman secara horizontal.
- **NFR-03** — Sekurang-kurangnya 4 dari 5 peserta yang mewakili masing-masing kelompok petani dan pembeli harus dapat menyelesaikan tugas utama tanpa bantuan setelah pengarahan singkat. Penguji mencatat keberhasilan dan hambatan yang dialami peserta.
- **NFR-04** — Pengguna harus dapat menyelesaikan alur utama menggunakan papan ketik, melihat penanda fokus, dan membaca label formulir. Status harus dapat dikenali tanpa mengandalkan warna saja. Pembesaran teks hingga 200% harus mempertahankan seluruh fungsi pada alur utama. Rasio kontras sekurang-kurangnya 4,5:1 untuk teks biasa dan 3:1 untuk teks besar.
- **NFR-11** — Alur utama harus diuji pada dua versi mayor terbaru Chrome, Firefox, Edge, dan Safari saat peluncuran. Penguji mencatat nomor versi yang digunakan dalam laporan uji.

### 3.4 Kepatuhan

Rancangan PanganTani mengacu pada standar rekayasa kebutuhan dan kriteria pengujian aksesibilitas terpilih. Dokumen ini menggunakan R-01 untuk menyusun persyaratan dan mengacu pada kriteria aksesibilitas terpilih dari R-07 untuk pengujian. Sertifikasi dan kepatuhan hukum secara menyeluruh belum dinyatakan. Kebijakan privasi, retensi data, syarat transaksi, dan kewajiban operator perlu dikaji sesuai model operasional sebelum peluncuran produksi.

Informasi tentang kondisi pangan harus disajikan secara akurat. Sistem menampilkan informasi tersebut kepada pengguna serta menyediakan fungsi untuk menutup penawaran dan mengajukan pengaduan.

### 3.5 Desain dan Implementasi

#### 3.5.1 Installation

PanganTani dapat diakses melalui peramban tanpa memasang aplikasi tambahan. Dokumentasi implementasi mencakup lingkungan server, basis data, pengaturan yang bersifat rahasia, dan layanan pendukung.

#### 3.5.2 Build and Delivery

Setiap rilis PanganTani harus dapat ditelusuri melalui nomor versi, catatan perubahan, dan hasil pengujian persyaratan fungsional yang terkait. Konfigurasi rahasia produksi disimpan di luar repositori. Sebelum perubahan skema data diterapkan, perpindahan skema dan prosedur pemulihannya diuji.

#### 3.5.3 Distribution

PanganTani menggunakan layanan terpusat yang dapat diakses melalui peramban. Penetapan lokasi hos dan kebutuhan replikasi data harus mempertimbangkan target ketersediaan dan pemulihan pada NFR-08 dan NFR-09. Kedua keputusan tersebut masih terbuka.

#### 3.5.4 Maintainability

Perubahan pada aturan bisnis harus disertai pengujian regresi. Pengujian memeriksa bahwa perubahan aturan harga, stok, atau perhitungan dampak menghasilkan perilaku yang sesuai. Jika perubahan memengaruhi perilaku yang dilihat pengguna, SRS juga harus diperbarui.

#### 3.5.5 Reusability

Aturan pemesanan dan pelaporan digunakan secara konsisten di seluruh fitur terkait. Pemesanan dari katalog maupun papan kebutuhan mengikuti aturan validasi, reservasi, dan harga yang sama. Dasbor petani, dasbor administrator, dan hasil ekspor menggunakan definisi berat pangan tersalurkan yang sama.

#### 3.5.6 Portability

Dukungan lintas lingkungan mengikuti persyaratan kompatibilitas pada NFR-11. Konfigurasi lingkungan dipisahkan dari data bisnis. Penyedia peta dan layanan hos masih dapat dipilih pada tahap implementasi.

#### 3.5.7 Cost

Perkiraan biaya operasional bergantung pada volume penggunaan dalam uji coba. Setelah volume tersebut ditetapkan, biaya hos, peta, penyimpanan, dan pengiriman surel dapat dihitung. Anggaran dan batas biaya layanan masih perlu ditentukan.

#### 3.5.8 Deadline

Kesiapan rilis inti ditentukan oleh hasil pengujian dan validasi prosedur pembayaran. Seluruh persyaratan berprioritas Inti dan persyaratan nonfungsional yang relevan harus lulus pengujian. Keputusan tentang prosedur pembayaran juga harus divalidasi. Tanggal peluncuran masih perlu ditetapkan.

#### 3.5.9 Proof of Concept

Uji konsep dirancang untuk menunjukkan bahwa satu transaksi dapat berlangsung dari penerbitan penawaran hingga pencatatan pada dasbor. Petani terverifikasi menerbitkan penawaran, lalu dua pembeli mencoba memesan stok yang sama. Setelah sistem mencatat reservasi, administrator memverifikasi pembayaran dan pembeli mengonfirmasi serah terima. Dasbor harus mencatat penyaluran tersebut tepat satu kali. Uji konsep juga mencakup skenario bukti pembayaran tertunda, penolakan, dan pembatalan.

#### 3.5.10 Change Management

Setiap perubahan persyaratan dicatat agar dampaknya dapat ditelusuri. Catatan memuat ID, alasan perubahan, serta dampaknya terhadap persyaratan fungsional, persyaratan nonfungsional, diagram, dan kriteria uji. Persyaratan yang dihapus tetap tercatat dengan ID yang sama dan diberi status dihentikan. Perubahan lingkup menjadi bagian dari versi acuan berikutnya setelah pemilik produk menyetujuinya.

### 3.6 AI/ML

#### 3.6.1 Model Specification

Perhitungan pada rancangan awal mengikuti aturan yang telah ditetapkan. Sistem menentukan harga berdasarkan waktu, menghitung jarak, dan memperkirakan emisi berdasarkan faktor yang terdokumentasi. Model pembelajaran mesin berada di luar kebutuhan rancangan awal.

#### 3.6.2 Data Management

Pengelolaan data transaksi dan lokasi mengikuti hak akses pengguna. Rancangan awal menetapkan data tersebut untuk kebutuhan operasional sistem. Himpunan data untuk pelatihan model belum ditetapkan.

#### 3.6.3 Guardrails

Server memeriksa harga minimum, stok, dan waktu agar transaksi mengikuti aturan yang berlaku. Pada pelaporan emisi, sistem hanya menghitung estimasi jika faktor emisi yang sah tersedia. Data yang tidak memiliki faktor tersebut ditandai belum dihitung.

#### 3.6.4 Ethics

Sistem menampilkan informasi yang mendasari keputusan pengguna. Pengguna dapat melihat alasan perubahan harga, jenis jarak yang dipakai, kondisi produk, dan asumsi perhitungan dampak. Setelah pesanan dibuat, harga yang disepakati tetap tercatat pada transaksi.

#### 3.6.5 Human-in-the-Loop

Pemeriksaan kondisi produk dan keputusan transaksi melibatkan pengguna sesuai perannya. Petani memperbarui informasi kondisi produk, sedangkan administrator memverifikasi akun dan pembayaran serta menyelesaikan pengaduan. Pembeli mengonfirmasi barang yang diterima setelah serah terima.

#### 3.6.6 Model Lifecycle and Operations

Siklus pelatihan model berada di luar lingkup rancangan awal. Jika kecerdasan buatan atau pembelajaran mesin ditambahkan, spesifikasi tersendiri harus menetapkan tujuan, himpunan data, cara evaluasi, dan mekanisme pengawasan model.

## 4. Verification

Verifikasi bertujuan memastikan bahwa setiap persyaratan memiliki metode dan bukti pengujian yang dapat ditelusuri. Oleh karena itu, pengujian terhadap persyaratan induk harus mencakup seluruh subfitur, jalur keberhasilan, masukan tidak valid, serta penolakan akses apabila relevan. Pada versi dokumen ini, seluruh persyaratan masih berstatus **Belum diuji**, sedangkan bukti pengujian akan dilengkapi setelah implementasi tersedia.

| Requirement ID | Verification Method | Test/Artifact Link | Status | Evidence |
|---|---|---|---|---|
| FR-UM-01.1–4 | Uji fungsional registrasi dan akses akun, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-UM-01, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-UM-02.1–3 | Uji fungsional pengaturan profil, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-UM-02, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-UM-03.1–3 | Uji fungsional katalog dan detail produk, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-UM-03, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-UM-04.1–3 | Uji fungsional preferensi aksesibilitas, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-UM-04, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-UM-05.1–3 | Uji fungsional pusat notifikasi, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-UM-05, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-UM-06.1–3 | Uji fungsional berbagi penawaran, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-UM-06, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-01.1–3 | Uji fungsional pengajuan verifikasi, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-01, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-02.1–4 | Uji fungsional pengelolaan hasil panen, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-02, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-03.1–3 | Uji fungsional stok dan kondisi, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-03, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-04.1–3 | Uji fungsional jadwal pengambilan, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-04, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-05.1–4 | Uji fungsional pemrosesan pesanan, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-05, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-06.1–3 | Uji fungsional harga dinamis, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-06, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-07.1–3 | Uji fungsional ringkasan penyaluran, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-07, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PT-08.1–3 | Uji fungsional penyalinan penawaran, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PT-08, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-01.1–3 | Uji fungsional pencarian dan filter, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-01, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-02.1–3 | Uji fungsional pencarian radius, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-02, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-03.1–4 | Uji fungsional pemesanan dan reservasi, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-03, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-04.1–3 | Uji fungsional pembayaran, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-04, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-05.1–3 | Uji fungsional penerimaan dan riwayat, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-05, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-06.1–3 | Uji fungsional pembatalan dan pengaduan, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-06, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-07.1–3 | Uji fungsional penawaran segera ditutup, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-07, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-08.1–3 | Uji fungsional favorit dan pengingat, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-08, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-PB-09.1–4 | Uji fungsional papan kebutuhan pangan, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-PB-09, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-AD-01.1–3 | Uji fungsional verifikasi petani, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-AD-01, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-AD-02.1–3 | Uji fungsional verifikasi pembayaran, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-AD-02, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-AD-03.1–4 | Uji fungsional moderasi dan pengaduan, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-AD-03, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-AD-04.1–3 | Uji fungsional transaksi bermasalah, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-AD-04, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-AD-05.1–3 | Uji fungsional dasbor distribusi, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-AD-05, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-AD-06.1–3 | Uji fungsional estimasi karbon, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-AD-06, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| FR-AD-07.1–3 | Uji fungsional ekspor laporan, seluruh subfitur, data sah dan tidak sah, serta hak akses | TC-AD-07, [use case](use-case.md) | Belum diuji | Rekaman hasil belum tersedia |
| NFR-01 | Uji beban dan persentil latensi | Q-01 | Belum diuji | Belum tersedia |
| NFR-02 | Uji pada berbagai lebar layar | Q-02 | Belum diuji | Belum tersedia |
| NFR-03 | Uji tugas dengan pengguna | Q-03 | Belum diuji | Belum tersedia |
| NFR-04 | Uji papan ketik, pembesaran teks, dan kontras | Q-04 | Belum diuji | Belum tersedia |
| NFR-05 | Uji kontrol keamanan | Q-05 | Belum diuji | Belum tersedia |
| NFR-06 | Uji akses lintas akun dan berkas | Q-06 | Belum diuji | Belum tersedia |
| NFR-07 | Uji konkurensi dan pengulangan | Q-07 | Belum diuji | Belum tersedia |
| NFR-08 | Pemantauan ketersediaan bulanan | Q-08 | Belum diuji | Belum tersedia |
| NFR-09 | Simulasi pemulihan cadangan | Q-09 | Belum diuji | Belum tersedia |
| NFR-10 | Uji dua sesi dan ukur jeda | Q-10 | Belum diuji | Belum tersedia |
| NFR-11 | Matriks peramban | Q-11 | Belum diuji | Belum tersedia |
| NFR-12 | Inspeksi audit dan regresi | Q-12 | Belum diuji | Belum tersedia |
| NFR-13 | Simulasi kegagalan peta dan jaringan | Q-13 | Belum diuji | Belum tersedia |

Skenario berikut digunakan untuk menguji kondisi yang dapat memengaruhi stok, pembayaran, hak akses, dan ketepatan laporan.

1. Jika dua pembeli masing-masing memesan 7 kg pada saat yang sama ketika stok tersedia 10 kg, sistem menerima satu reservasi dan menyisakan 3 kg.
2. Jika sistem menerima bukti sebelum tenggat dan administrator baru memeriksanya setelah tenggat, sistem tetap menahan stok agar tidak terjual kembali.
3. Jika pesanan tanpa bukti mencapai tenggat dan tindakan pelepasan stok dijalankan dua kali, sistem hanya menambah ketersediaan stok sekali.
4. Jika harga berubah sebelum konfirmasi pesanan, pembeli harus menyetujui harga terbaru. Sistem tetap menggunakan harga yang tercatat pada pesanan yang telah dibuat.
5. Jika pembeli menerima 8 kg dari pesanan 10 kg, selisih tersebut ditangani sebelum transaksi diselesaikan. Setelah transaksi selesai, sistem menambahkan 8 kg ke dasbor satu kali dan mencatat pengembalian dana jika telah diputuskan.
6. Jika pengguna mengganti ID pada permintaan dengan ID pesanan atau berkas milik akun lain, server menolak akses.
7. Jika koneksi terputus setelah pesanan tersimpan, pemeriksaan ulang menampilkan pesanan yang sama.

## 5. Lampiran

### 5.1 Diagram dan keterlacakan

Keterlacakan persyaratan menunjukkan hubungan antara fungsi, aktor, alur, dan sumber kebutuhan. Sebanyak 18 persyaratan awal dikembangkan menjadi 30 persyaratan induk dengan kode UM, PT, PB, dan AD. Diagram use case memetakan persyaratan induk ke aktor, sedangkan diagram aktivitas menggambarkan urutan dan percabangan proses utama. Lihat [diagram use case](use-case.md) dan [diagram aktivitas](activity-diagram.md).

| Kelompok FR | Landasan | Validasi yang diperlukan |
|---|---|---|
| UM-01–02, PB-03–06, AD-02–04 | R-08–09 dan alur pengguna | Kontak, pembayaran, pembatalan dan kewenangan admin. |
| UM-03, PT-02–05, PB-01–02, PB-07 | R-02–04 dan kebutuhan distribusi lokal | Detail komoditas, radius dan jadwal pengambilan. |
| PT-06 | R-05, rancangan aturan waktu | Harga minimum dan jadwal penurunan bersama petani. |
| PT-07, AD-05–06 | R-06, R-10 | Definisi pangan terselamatkan dan metode karbon. |
| UM-04 | R-07 | Uji petani dan pembeli dengan kebutuhan aksesibilitas. |
| PT-01, AD-01 | Rancangan tata kelola proyek | Bukti verifikasi dan pihak yang berwenang. |
| UM-05–06, PT-08, PB-08–09, AD-07 | Usulan kenyamanan dari pembahasan | Prioritas, penerimaan pengguna dan biaya operasional. |

### 5.2 Keputusan terbuka

Keputusan yang masih terbuka berkaitan dengan lingkup uji coba, proses pembayaran, dan pilihan layanan pendukung. Setiap keputusan dicatat bersama dampaknya agar dapat ditinjau sebelum rancangan digunakan sebagai acuan produksi.

| ID | Hal yang perlu diputuskan | Dampak |
|---|---|---|
| TBD-01 | Identitas penyusun, organisasi, pemilik produk dan tanggal rilis | Administrasi dokumen dan persetujuan versi acuan. |
| TBD-02 | Wilayah uji coba dan kapasitas aktual | Radius, beban, biaya dan jadwal. |
| TBD-03 | Dokumen verifikasi petani | Formulir dan akses data sensitif. |
| TBD-04 | Rekening tujuan, akses konfirmasi dana, waktu layanan administrator, dan pengembalian dana | Validasi asumsi pembayaran manual sebelum produksi. |
| TBD-05 | Tenggat pembayaran, ambang segera ditutup, batas unggahan dan retensi | Angka draf belum menjadi keputusan operasional final. |
| TBD-06 | Definisi risiko pangan terbuang dan faktor emisi lokal | Aktivasi klaim penyelamatan pangan dan estimasi karbon. |
| TBD-07 | Kerangka kerja, layanan hos, peta, kanal surel, dan anggaran | Integrasi serta biaya. |

Parameter dalam draf ini dapat digunakan untuk membuat prototipe. Persetujuan para pemangku kepentingan dan hasil pengujian masih diperlukan sebelum parameter tersebut ditetapkan sebagai acuan implementasi.
