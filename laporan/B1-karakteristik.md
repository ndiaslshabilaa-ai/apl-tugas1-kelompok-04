# B1. Identifikasi dan Klasifikasi Karakteristik

<!-- Penanggung jawab: [Artika Milad Arhidayah] -->

Berikut adalah daftar kandidat karakteristik arsitektur untuk Layanan Tugas Akhir pada subsistem *Assignment & Assessment*, diklasifikasikan berdasarkan kategori, sifat, serta penentuan 3 karakteristik pendorong utama:

## 1. Daftar Kandidat Karakteristik Arsitektur

| No | Karakteristik Arsitektur | Kategori | Sifat | Alasan Pemilihan |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **Performance Efficiency** | Operasional | Eksplisit | Mengatasi lonjakan akses mahasiswa dan dosen saat pendaftaran sidang massal agar sistem tidak mengalami kelambatan (*latency*). |
| 2 | **Security** | Lintas Sektor | Eksplisit | Melindungi dokumen draf skripsi, lembar pengesahan, dan kerahasiaan nilai sidang dari akses pihak tak berwenang |
| 3 | **Integrity & Auditability** | Lintas Sektor | Eksplisit | Menjamin jejak digital rekam bimbingan (*logbook*) dan pengesahan nilai valid serta tidak dapat dimanipulasi |
| 4 | **Availability** | Operasional | Implisit | Menjaga layanan tetap dapat diakses secara andal selama masa krusial pendaftaran sidang dan tenggat wisuda |
| 5 | **Maintainability** | Struktural | Implisit | Memudahkan penyesuaian logika bisnis dan aturan SKS jika terjadi perubahan regulasi akademik kampus |
| 6 | **Scalability** | Operasional | Implisit | Mampu menangani peningkatan volume penyimpanan dokumen digital skripsi tiap semester |
| 7 | **Usability** | Lintas Sektor | Eksplisit | Memberikan kenyamanan antarmuka bagi mahasiswa dan dosen dalam proses pengajuan serta penilaian |
| 8 | **Reliability** | Operasional | Implisit | Menjamin transaksi penyimpanan berkas dan penginputan nilai berhasil terekam tanpa adanya data yang hilang |

---

## 2. Tiga Karakteristik Pendorong Utama (Driving Characteristics)

Berdasarkan pengujian terhadap tiga ciri karakteristik arsitektur (berdampak pada struktur desain, tidak tergantung pada domain fungsional tunggal, serta sangat penting bagi keberhasilan sistem), dipilih 3 karakteristik pendorong utama:

1. **Performance Efficiency (Operasional):**
   * *Alasan:* Kegagalan menangani beban puncak saat pendaftaran sidang serentak dapat melumpuhkan alur akademik dan mengganggu jadwal kelulusan serta wisuda universitas. Karakteristik ini memaksa perancangan arsitektur menggunakan antrean pesan (*message queue*) dan *caching*.
2. **Security & Integrity (Lintas Sektor):**
   * *Alasan:* Dokumen tugas akhir dan nilai sidang merupakan produk hukum akademik yang harus terbebas dari pemalsuan serta akses tanpa otorisasi yang sah. Hal ini menuntut lapisan autentikasi dan kontrol akses berlapis.
3. **Maintainability (Struktural):**
   * *Alasan:* Regulasi operasional tugas akhir sering kali mengalami penyesuaian aturan dari universitas atau fakultas. Oleh karena itu, struktur kode modul harus mudah dimodifikasi (*low coupling*) tanpa merusak modul lainnya.
