# U2. Skenario Atribut Kualitas

Bagian ini merinci tiga skenario atribut kualitas berdasarkan karakteristik pendorong utama (*Performance Efficiency*, *Security*, dan *Maintainability*). Masing-masing skenario diuraikan ke dalam 6 komponen ATAM (*Architecture Tradeoff Analysis Method*), di mana Skenario 1 dirancang khusus untuk menjawab masalah utama terkait lonjakan trafik pendaftaran dan kendala unggah berkas draf skripsi.

---

## Skenario 1: Performance Efficiency (Menjawab Masalah Utama)
* **Sumber (*Source*):** Mahasiswa tingkat akhir.
* **Stimulus (*Stimulus*):** Mengakses tombol "Daftar Sidang" dan mengunggah berkas draf skripsi berukuran besar (hingga 25 MB) secara serentak pada pukul 08.00 WITA.
* **Artefak (*Artifact*):** Modul Pendaftaran (*Assignment & Assessment*) dan *Message Queue Broker*.
* **Lingkungan (*Environment*):** Kondisi beban puncak (*peak traffic load* dengan 500 pengguna konkuren).
* **Respons (*Response*):** Sistem menampung permintaan masuk ke dalam antrean terpusat (*message queue*) dan memprosesnya secara asinkron di latar belakang (*background worker*) tanpa mengalami *crash* atau *race condition*.
* **Ukuran Respons (*Response Measure*):** 
  * Waktu tanggap (*latency*) antarmuka tetap stabil di bawah **3 detik** per permintaan.
  * Tingkat kegagalan sistem (*error rate*) sebesar **0%** (seluruh antrean pendaftaran berhasil diproses).

---

## Skenario 2: Security & Integrity (Keamanan Dokumen Draf Skripsi)
* **Sumber (*Source*):** Pengguna eksternal atau pihak tidak berwenang.
* **Stimulus (*Stimulus*):** Mencoba mengunduh berkas draf skripsi atau rekam nilai sidang mahasiswa lain melalui manipulasi tautan URL langsung (*direct object reference*).
* **Artefak (*Artifact*):** Modul Otorisasi dan Layanan *Cloud Object Storage*.
* **Lingkungan (*Environment*):** Operasional harian sistem.
* **Respons (*Response*):** Sistem memvalidasi token akses berbasis peran (*Role-Based Access Control / JWT*) dan langsung menolak permintaan unduh jika pengguna tidak memiliki hak akses yang sah.
* **Ukuran Respons (*Response Measure*):** 
  * **100%** upaya akses ilegal terdeteksi, diblokir, dan dicatat ke dalam log audit keamanan (*security audit log*).

---

## Skenario 3: Maintainability (Kemudahan Pemeliharaan & Modifikasi Aturan)
* **Sumber (*Source*):** Administrator akademik / Fakultas.
* **Stimulus (*Stimulus*):** Melakukan perubahan pada parameter aturan minimum persyaratan SKS kelulusan tugas akhir di dalam kode sumber sistem.
* **Artefak (*Artifact*):** Lapisan Logika Bisnis (*Business Logic Layer*).
* **Lingkungan (*Environment*):** Tahap pemeliharaan sistem (*maintenance phase*).
* **Respons (*Response*):** Tim pengembang memperbarui modul aturan validasi secara terisolasi tanpa merusak modul tampilan antarmuka (*UI*) maupun struktur basis data dokumen.
* **Ukuran Respons (*Response Measure*):** 
  * Waktu total implementasi perubahan kode dan pengujian ulang (*change implementation time*) selesai dalam waktu kurang dari **2 hari kerja**.
