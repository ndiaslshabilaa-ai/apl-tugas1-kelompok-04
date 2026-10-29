# B3. Tiga Struktur Desain

<!-- Penanggung jawab: [Artika Milad Arhidayah] -->

Berikut adalah penjabaran tiga struktur desain arsitektur untuk Layanan Tugas Akhir (subsistem *Assignment & Assessment*) yang konsisten dengan diagram perancangan sistem kelompok:

## 1. Struktur Modul (Module Structure)
Struktur modul menunjukkan bagaimana kode sumber perangkat lunak dibagi ke dalam unit-unit fungsional dan relasi hubungan "menggunakan" antarmodul berdasarkan lapisan (*layered architecture*):

* **Lapisan Tampilan (Presentation Layer):** Modul *Halaman Pengajuan Judul*, Modul *Halaman Logbook Bimbingan*, dan Modul *Form Penilaian Sidang*.
* **Lapisan Logika Bisnis (Business Logic Layer):** Modul *Pengelola Tugas Akhir*, Modul *Validasi Syarat SKS & Kuota*, serta Modul *Penjadwalan Sidang*.
* **Lapisan Data (Data Access Layer):** Modul *Repositori Dokumen Skripsi* dan Modul *Repositori Nilai Akademik*.

> **Keterangan Diagram:** Kode dibagi ke dalam tiga lapisan terisolasi agar perubahan aturan bisnis atau validasi syarat SKS hanya menyentuh lapisan logika tanpa menaikkan atau melompati lapisan di atasnya. Lapisan tampilan hanya memanggil modul pengelola tugas akhir dan tidak mengakses data secara langsung.

---

## 2. Struktur Komponen dan Konektor (Component & Connector / C&C Structure)
Struktur C&C menunjukkan elemen-elemen *runtime* (proses, layanan, dan penyimpanan) yang aktif berjalan saat sistem dipakai beserta jenis interaksi konektornya:

* **Browser Pengguna** terhubung melalui protokol **HTTPS** ke **Server Web Tugas Akhir**.
* **Server Web** melakukan baca/tulis cepat ke **Cache (Kuota & Jadwal)** serta mengirimkan (*publish*) transaksi pendaftaran ke **Antrean Pesan (Message Queue)**.
* **Worker Service** mengambil (*consume*) data dari antrean untuk diproses secara latar belakang (*background process*).
* Komponen berinteraksi dengan **Cloud Object Storage** (untuk penyimpanan dokumen draf skripsi) dan **Basis Data Akademik Pusat** (untuk transaksi data utama).

> **Keterangan Diagram:** Permintaan unggah dokumen berukuran besar dan proses penjadwalan sidang dimasukkan ke dalam antrean pesan (*message queue*) agar sistem tahan terhadap lonjakan beban akses serentak tanpa mengalami *request timeout*.

---

## 3. Struktur Alokasi (Allocation Structure)
Struktur alokasi menjawab dua hal utama: di mana perangkat lunak dijalankan pada infrastruktur fisik/cloud serta bagaimana penugasan modul dibagi kepada tim pengembang:

* **Penempatan Lingkungan (*Deployment*):** Perangkat pengguna (Browser) terhubung ke **Server Aplikasi di Cloud Kampus UMI** (yang memuat Web Server, Message Queue, Worker, dan Cache), yang kemudian mengakses **Server Data & Penyimpanan Kampus** (Basis data pusat dan Cloud Object Storage).
* **Alokasi Tim Pengembang (Pembagian Kerja):**
  * **Tim A:** Bertanggung jawab pada modul tampilan (*Halaman Pengajuan Judul*, *Form Logbook & Sidang*).
  * **Tim B:** Bertanggung jawab pada modul logika bisnis (*Pengelola Tugas Akhir*, *Validasi SKS & Kuota*, *Penjadwalan Sidang*).
  * **Tim C:** Bertanggung jawab pada modul penyimpanan dan data (*Repositori Dokumen Skripsi*, *Repositori Nilai Akademik*).
  * **Tim D:** Bertanggung jawab pada infrastruktur cloud, manajemen *message queue*, serta pengujian beban sistem (*load testing*).
> **Keterangan Diagram:** Aplikasi inti dijalankan pada server aplikasi di cloud kampus, sementara data master tetap berada di server data pusat universitas. Pembagian modul ke dalam empat tim terstruktur memungkinkan proses pengembangan kode dapat berjalan secara paralel.
