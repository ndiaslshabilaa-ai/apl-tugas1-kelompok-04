# B1. Identifikasi dan Klasifikasi Karakteristik

**Penanggung Jawab:** [B.Nadia Salsabila]

## B1.1 Identifikasi Kandidat Karakteristik Arsitektur

Identifikasi karakteristik arsitektur dilakukan berdasarkan hasil wawancara dengan mahasiswa tingkat akhir, dosen pembimbing dan penguji, serta Ketua Program Studi terkait layanan tugas akhir.

Kategori karakteristik dibagi menjadi operasional (perilaku sistem saat dijalankan), struktural (susunan dan pengembangan sistem), serta lintas sektor (memengaruhi beberapa bagian sistem). Sifat eksplisit merupakan kebutuhan yang disampaikan langsung oleh responden, sedangkan implisit merupakan hasil analisis dari kebutuhan yang disampaikan.

| No. | Karakteristik | Kategori | Sifat | Alasan |
|---|---|---|---|---|
| 1 | Performance Efficiency | Operasional | Eksplisit | Sistem lambat saat pendaftaran dan proses unggah dokumen membutuhkan waktu lama atau gagal. |
| 2 | Usability | Lintas sektor | Eksplisit | Mahasiswa kesulitan memahami persyaratan sidang dan fitur logbook kurang fleksibel. |
| 3 | Data Integrity | Lintas sektor | Eksplisit | Diperlukan data bimbingan, draf, dan penilaian yang terpusat serta akurat. |
| 4 | Availability | Operasional | Implisit | Sistem perlu tetap dapat diakses saat terjadi lonjakan pengguna pada periode pendaftaran. |
| 5 | Security | Lintas sektor | Eksplisit | Dokumen tugas akhir dan rekam jejak bimbingan membutuhkan penyimpanan yang aman. |
| 6 | Auditability | Lintas sektor | Eksplisit | Aktivitas bimbingan dan penilaian perlu memiliki rekam jejak yang dapat ditelusuri. |
| 7 | Maintainability | Struktural | Implisit | Sistem perlu mudah disesuaikan dengan perubahan aturan dan persyaratan akademik. |
| 8 | Interoperability | Struktural | Implisit | Data mahasiswa, dosen, dan akademik berpotensi membutuhkan pertukaran data dengan layanan lain. |
| 9 | Reliability | Operasional | Implisit | Proses pengajuan, bimbingan, penjadwalan, dan penilaian perlu berjalan secara konsisten. |

## B1.2 Tiga Karakteristik Pendorong

| No. | Karakteristik | Alasan Pemilihan | Dampak terhadap Arsitektur |
|---|---|---|---|
| 1 | Performance Efficiency | Sistem mengalami latency saat pendaftaran dan kendala unggah dokumen. | Optimasi proses, pengelolaan unggah dokumen, dan penanganan akses bersamaan. |
| 2 | Data Integrity | Diperlukan penyimpanan terpusat dan rekapitulasi data yang akurat. | Validasi data, pengelolaan basis data, dan pengendalian perubahan data. |
| 3 | Usability | Mahasiswa mengalami kebingungan terkait persyaratan sidang dan penggunaan logbook. | Antarmuka sederhana, navigasi jelas, dan alur proses yang mudah dipahami. |

## B1.3 Pengujian Tiga Karakteristik Pendorong

Pengujian dilakukan menggunakan tiga ciri karakteristik arsitektur, yaitu bukan sekadar kebutuhan domain, memengaruhi struktur arsitektur, dan penting bagi keberhasilan sistem.

| No. | Karakteristik | Bukan Sekadar Kebutuhan Fungsional | Memengaruhi Struktur Arsitektur | Penting bagi Keberhasilan Sistem | Kesimpulan |
|---|---|---|---|---|---|
| 1 | Performance Efficiency | Ya, berkaitan dengan kualitas kinerja sistem. | Ya, memengaruhi pengelolaan beban dan proses dokumen. | Ya, sistem lambat menghambat proses pendaftaran. | Memenuhi |
| 2 | Data Integrity | Ya, berkaitan dengan konsistensi dan keakuratan data. | Ya, memengaruhi basis data, validasi, dan penyimpanan. | Ya, kesalahan data dapat mengganggu proses akademik. | Memenuhi |
| 3 | Usability | Ya, berkaitan dengan kemudahan penggunaan sistem. | Ya, memengaruhi antarmuka dan alur interaksi. | Ya, kesulitan penggunaan menghambat mahasiswa. | Memenuhi |
