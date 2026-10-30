# BAB I. Pendahuluan

<!-- Gambaran subsistem dan layanan inti yang ditugaskan, ruang lingkup, dan sumber data. -->
<!-- Penanggung jawab: [Annisa Rezzky Ashriani] -->

## 1.1 Gambaran layanan inti
Layanan Tugas Akhir adalah bagian dari subsistem Assignment & Assessment di lingkungan Universitas Muslim Indonesia (UMI). Layanan ini mendukung seluruh proses penyelesaian studi mahasiswa tingkat akhir secara digital, mulai dari pengajuan judul, penentuan dosen pembimbing, pencatatan logbook bimbingan, pengunggahan berkas draf, pendaftaran dan penjadwalan sidang, sampai penilaian dan rekapitulasi nilai sidang akhir.

Dari sisi teknis, layanan ini terintegrasi dengan basis data pusat SIAKAD untuk memvalidasi prasyarat SKS kelulusan mahasiswa. Layanan ini juga terhubung dengan sistem manajemen dokumen digital untuk mengelola berkas draf skripsi secara aman. Pengembangan dan pemeliharaannya dilakukan secara iteratif oleh tim pengembang internal kampus, menyesuaikan kalender akademik dan regulasi ujian penutupan studi. Pengelolaan dilakukan oleh tenaga profesional Pusat Data dan Teknologi Informasi (PDTI) UMI dengan standar kepatuhan terhadap keamanan data akademik dan privasi dokumen mahasiswa.

Dari sisi bisnis, layanan ini bertujuan mempercepat proses administratif akademik, meningkatkan transparansi riwayat bimbingan antara mahasiswa dan dosen, serta menjamin akurasi rekapitulasi nilai sidang akhir.

Terdapat enam pemangku kepentingan yang dipetakan dengan matriks Power/Interest (Mendelow Matrix) [5], seperti pada Gambar 1:

Manage Closely: Dosen Pembimbing & Penguji, serta Ketua Program Studi (Kaprodi).
Keep Satisfied: Tim Pengembang IT (PDTI UMI) dan Lembaga Penjaminan Mutu (LPMI).
Keep Informed: Mahasiswa Akhir dan Staf Administrasi Akademik.
Monitor: Pihak eksternal pendukung lainnya.

Gambar 1. Peta Power/Interest Stakeholder (Mendelow Matrix)

Gambar 1. Peta Power/Interest Stakeholder (Mendelow Matrix) Layanan Tugas Akhir.

Perancangan arsitektur layanan ini berpedoman pada praktik arsitektur perangkat lunak [1][2]. Tiga karakteristik pendorong utamanya adalah Performance Efficiency, Security & Integrity, dan Maintainability, yang dipetakan ke standar ISO/IEC 25010 [3]. Keputusan arsitektur dicatat dalam format Architecture Decision Record (ADR) [4].

## 1.2 Ruang lingkup (3-5 kasus penggunaan)
Ruang lingkup dokumen ini adalah subsistem Assignment & Assessment untuk Layanan Tugas Akhir, dengan integrasi ke SIAKAD tanpa perombakan skema tabel inti yang dikelola universitas. Lima kasus penggunaan utama beserta komponen arsitektur yang terlibat adalah sebagai berikut.

Pengajuan dan verifikasi judul. Mahasiswa mengajukan judul melalui Halaman Pengajuan Judul. Modul Pengelola Tugas Akhir meneruskan permintaan ke Validasi Syarat SKS & Kuota. Dosen memverifikasi judul, dan mahasiswa menerima notifikasi status persetujuan secara real-time.
Penentuan dosen pembimbing dan pencatatan logbook bimbingan. Kaprodi menentukan dosen pembimbing. Setiap sesi bimbingan dicatat melalui Halaman Logbook Bimbingan yang dikelola oleh Pengelola Tugas Akhir, sehingga riwayat bimbingan transparan.
Pengunggahan berkas draf tugas akhir. Mahasiswa mengunggah proposal, draf skripsi, dan lembar pengesahan dalam format PDF (maksimal 25 MB per dokumen). Permintaan masuk melalui Server Web ke Antrean Pesan, diproses Worker Service, dan berkas disimpan di Cloud Object Storage melalui Repositori Dokumen Skripsi (Gambar 3).
Pendaftaran dan penjadwalan sidang. Staf administrasi memvalidasi berkas persyaratan. Modul Penjadwalan Sidang memeriksa kuota dosen penguji dan ketersediaan ruangan menggunakan Cache Kuota & Jadwal. Notifikasi dikirim secara bertahap melalui antrean pesan.
Penilaian sidang dan rekapitulasi nilai. Dosen penguji menginput nilai melalui Form Penilaian Sidang. Nilai disimpan melalui Repositori Nilai Akademik ke Basis Data Akademik Pusat dengan jejak audit yang tidak dapat dimanipulasi.

Struktur desain yang melandasi kelima kasus penggunaan ini ditunjukkan oleh tiga gambar berikut.

Gambar 2. Struktur Modul

Gambar 2. Struktur Modul: unit kode dan hubungan "menggunakan".

Gambar 3. Struktur Komponen dan Konektor (C&C)

Gambar 3. Struktur Komponen dan Konektor (C&C).

Gambar 4. Struktur Alokasi

Gambar 4. Struktur Alokasi: penempatan perangkat lunak dan penugasan tim.

## 1.3 Sumber data
<!-- Pengalaman pengguna, informasi publik, wawancara responden. Tanpa identitas pribadi. -->
Dokumen ini disusun dari hasil analisis kelompok berikut.

Analisis empat konteks arsitektur: teknis, siklus hidup proyek, bisnis, dan profesional.
Stakeholder register dan peta Power/Interest [5] yang memuat enam pemangku kepentingan beserta kebutuhan dan strategi pengelolaannya (Gambar 1).
Batasan sistem pada kategori teknologi, bisnis, dan operasional, beserta dampaknya terhadap arsitektur.
Tiga Architecturally Significant Requirements (ASR): kinerja dan penanganan lonjakan beban, integritas data dan rekam jejak audit, serta keamanan dan otorisasi akses berkas sensitif.
Dua dokumen ADR [4]: penggunaan Cloud Object Storage (ADR-001) dan penerapan Asynchronous Message Queue (ADR-002).
Identifikasi karakteristik arsitektur, atribut kualitas terukur, pemetaan ke ISO/IEC 25010 [3], dan analisis trade-off.
Tiga struktur desain (modul, komponen dan konektor, serta alokasi) pada Gambar 2 sampai Gambar 4.
Literatur pendukung pada Daftar Pustaka [1]–[5].
