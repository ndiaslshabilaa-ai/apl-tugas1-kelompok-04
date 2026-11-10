# U1. Konteks dan ASR (Architectural Significant Requirements)

## 1.1 Ringkasan Layanan
Layanan Tugas Akhir (subsistem *Assignment & Assessment*) merupakan bagian integral dari platform *Smart Campus* Universitas Muslim Indonesia (UMI). Sistem ini dirancang untuk mendigitalkan dan mengelola seluruh siklus akademik mahasiswa tingkat akhir, mulai dari pengajuan judul proposal, pencatatan bimbingan (*logbook*), penjadwalan seminar/sidang, hingga pengarsipan dokumen draf skripsi dan rekapitulasi nilai akhir secara terpusat.

## 1.2 Masalah Utama Layanan dan Bukti Lapangan
* **Masalah Utama:** 
  Terjadinya *request timeout*, kegagalan unggah berkas draf skripsi berukuran besar (hingga 25 MB), serta *race condition* pada modul pendaftaran sidang akibat lonjakan trafik serentak (*traffic spike*) pada jam pembukaan kuota. Masalah ini diperparah oleh ketergantungan pada koordinasi manual via grup pesan instan (WhatsApp) yang menyebabkan rekam jejak revisi sering hilang dan tidak terpantau.
* **Bukti Lapangan (Berdasarkan Wawancara Responden):**
  * **R1 (Mahasiswa Akhir):** Mengalami kegagalan berulang (*upload failed*) saat mengunggah draf skripsi mendekati batas waktu (*deadline*) akibat server tidak responsif.
  * **R2 (Dosen Pembimbing/Penguji):** Mengeluhkan kesulitan melacak riwayat bimbingan dan keabsahan dokumen revisi karena tercecer di luar platform resmi.

## 1.3 Stakeholder Utama
1. **Mahasiswa Tingkat Akhir (Calon & Pendaftar Sidang):** Mengakses pendaftaran, mengunggah draf skripsi, dan memantau jadwal sidang. *(Kategori: Keep Informed / Power: Rendah, Interest: Tinggi)*
2. **Dosen Pembimbing & Penguji:** Melakukan validasi bimbingan, menilai ujian sidang, dan memberikan catatan revisi. *(Kategori: Manage Closely / Power: Tinggi, Interest: Tinggi)*
3. **Ketua Program Studi / Fakultas:** Mengawasi rekapitulasi kelulusan dan menetapkan kuota penguji. *(Kategori: Keep Satisfied / Power: Tinggi, Interest: Rendah)*
4. **Tim Pengembang IT Kampus (DevOps & Backend):** Memelihara infrastruktur server dan memastikan keandalan sistem. *(Kategori: Monitor / Power: Rendah, Interest: Rendah)*

## 1.4 Kebutuhan Signifikan Arsitektur (ASR) & Karakteristik Pendorong
* **ASR-1 (Performance Efficiency):** Sistem harus mampu menangani 500 pengguna konkuren pada saat pendaftaran sidang serentak tanpa mengalami *downtime* atau *server crash*.
* **ASR-2 (Security & Integrity):** Menjaga kerahasiaan dokumen draf skripsi dan integritas rekam nilai sidang dari manipulasi akses ilegal (*unauthorized access*).
* **ASR-3 (Maintainability):** Mempermudah pembaruan aturan logika bisnis terkait persyaratan SKS kelulusan tanpa merusak modul antarmuka atau basis data lainnya.
* **Karakteristik Pendorong Utama:** 
  1. *Performance Efficiency*
  2. *Security*
  3. *Maintainability*

## 1.5 Bagian yang Diperbarui dari Tugas Kelompok Sebelumnya
Dibandingkan dengan tugas sebelumnya, bagian ini diperbarui dengan:
* Penajaman fokus pada akar permasalahan teknis (*traffic spike* pendaftaran dan kegagalan unggah berkas).
* Penguatan bukti empiris berdasarkan transkrip wawancara lintas peran (R1, R2, dan R5).
* Perumusan spesifikasi ASR yang terikat langsung dengan karakteristik pendorong kualitas perangkat lunak.
