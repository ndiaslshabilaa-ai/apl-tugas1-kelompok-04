# U3. Taktik Arsitektur

Bagian ini mendokumentasikan taktik arsitektur (*architectural tactics*) yang diterapkan untuk merespons ketiga skenario atribut kualitas pada subsistem Layanan Tugas Akhir (*Assignment & Assessment*). Setiap taktik dirancang untuk mencapai sasaran kualitas tertentu dengan tetap memperhitungkan kompromi (*trade-off*) yang diterima.

---

## 1. Taktik untuk Skenario 1: Performance Efficiency (Manajemen Lonjakan Trafik)
* **Taktik yang Diterapkan:** 
  * *Manage Demand* (Menerapkan Antrean / *Message Queue Broker*).
  * *Defer Response* (Pemrosesan Latar Belakang / *Background Worker*).
* **Cara Kerja:**
  Ketika ribuan mahasiswa secara serentak menekan tombol pendaftaran sidang pada jam pembukaan kuota, sistem tidak memproses seluruh transaksi secara langsung ke basis data utama (*synchronous*). Permintaan masuk (*request*) akan ditampung terlebih dahulu ke dalam antrean terpusat menggunakan *Message Broker* (seperti RabbitMQ atau Redis Queue). Selanjutnya, *Background Worker* akan mengambil dan memproses antrean tersebut secara bertahap dan terstruktur tanpa membebani *web server*.
* **Harga yang Dibayar (Trade-off):**
  * Kompleksitas infrastruktur meningkat karena memerlukan penambahan komponen server/layanan *message broker*.
  * Mahasiswa mengalami sedikit penundaan instan (*latency*) karena mendapatkan konfirmasi antrean terlebih dahulu alih-alih respons langsung seketika (*instant response*).

---

## 2. Taktik untuk Skenario 2: Security & Integrity (Proteksi Dokumen Draf Skripsi)
* **Taktik yang Diterapkan:** 
  * *Authenticate Actor* & *Authorize Access* (Autentikasi Berbasis Token / JWT dan *Role-Based Access Control*).
* **Cara Kerja:**
  Setiap permintaan unduh atau akses terhadap berkas draf skripsi dan rekam nilai sidang wajib menyertakan token akses terenkripsi (*JSON Web Token / JWT*). Modul otorisasi akan memvalidasi identitas serta peran pengguna (*student, lecturer, admin*). Jika pengguna mencoba mengakses berkas di luar hak aksesnya melalui manipulasi URL (*direct object reference*), sistem akan secara otomatis menolak permintaan tersebut dan mencatatnya ke dalam log audit keamanan.
* **Harga yang Dibayar (Trade-off):**
  * Terjadi tambahan beban komputasi server (*overhead*) untuk proses verifikasi kriptografi dan dekripsi token pada setiap permintaan data.
  * Proses pengelolaan masa kedaluwarsa token (*token expiration*) memerlukan penanganan logika manajemen sesi yang lebih ketat di sisi klien dan server.

---

## 3. Taktik untuk Skenario 3: Maintainability (Kemudahan Pemeliharaan Aturan Akademik)
* **Taktik yang Diterapkan:** 
  * *Split Module / Encapsulation* (Pemisahan Lapisan Logika Bisnis).
* **Cara Kerja:**
  Aturan validasi syarat SKS kelulusan dipisahkan secara tegas dari antarmuka pengguna (*UI*) dan struktur basis data dokumen. Logika bisnis ini dikemas ke dalam modul layanan terisolasi (*service layer*), sehingga ketika ada perubahan kebijakan akademik dari fakultas, pengembang hanya perlu memperbarui kode di dalam modul aturan tersebut tanpa menyentuh bagian tampilan atau penyimpanan data.
* **Harga yang Dibayar (Trade-off):**
  * Jumlah berkas kode program (*codebase*) dan struktur direktori proyek menjadi lebih banyak dan terfragmentasi.
  * Membutuhkan dokumentasi antarmuka internal yang disiplin agar komunikasi antar-modul tetap terkelola dengan baik.
