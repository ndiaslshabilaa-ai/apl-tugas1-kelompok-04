# A4. Kebutuhan Signifikan (ASR)

<!-- Penanggung jawab: [Artika Milad Arhidayah] -->

Berikut adalah tiga Kebutuhan Signifikan Secara Arsitektural (*Architectural Significant Requirements* / ASR) untuk Layanan Tugas Akhir pada subsistem *Assignment & Assessment*, beserta analisis mengapa kebutuhan tersebut sangat memengaruhi perancangan arsitektur perangkat lunak:

## 1. ASR 1: Kinerja dan Penanganan Lonjakan Beban (Performance Efficiency)
* **Pernyataan Kebutuhan:** Pada periode pendaftaran seminar/sidang akhir atau menjelang tenggat pengumpulan berkas, sistem harus mampu menangani hingga 500 mahasiswa dan dosen yang mengakses secara bersamaan, dengan waktu muat halaman web rata-rata kurang dari 3 detik.
* **Alasan Pengaruh pada Arsitektur:** Kebutuhan ini sangat memengaruhi desain arsitektur karena lonjakan akses secara simultan berpotensi menyebabkan *bottleneck* pada server web dan basis data relasional pusat. Oleh karena itu, arsitektur sistem harus mengadopsi mekanisme penanganan beban seperti *caching* data referensi dan antrean proses (*message queue*) untuk menjaga stabilitas respons sistem.

## 2. ASR 2: Integritas Data dan Rekam Jejak Audit (Integrity & Auditability)
* **Pernyataan Kebutuhan:** Setiap aktivitas penting—seperti pengajuan judul, persetujuan dosen pembimbing, catatan logbook bimbingan, hingga penginputan nilai akhir sidang—wajib terekam secara permanen, aman, dan tidak dapat dimanipulasi (*tamper-proof audit trail*).
* **Alasan Pengaruh pada Arsitektur:** Aspek hukum akademik dan validitas kelulusan mahasiswa menuntut tingkat keandalan data yang tinggi. Hal ini memaksa perancang arsitektur untuk menetapkan batasan transaksi basis data (*ACID transactions*) yang ketat serta memisahkan lapisan pencatatan log aktivitas (*audit logging service*) dari logika bisnis utama agar setiap perubahan status dokumen memiliki jejak digital yang jelas.

## 3. ASR 3: Keamanan dan Otorisasi Akses Berkas Sensitif (Security & Confidentiality)
* **Pernyataan Kebutuhan:** Berkas dokumen draf skripsi, lembar pengesahan bertanda tangan, dan hasil penilaian sidang bersifat rahasia dan hanya boleh diakses oleh pihak yang memiliki hak otorisasi (mahasiswa bersangkutan, dosen pembimbing, dosen penguji, serta Ketua Program Studi).
* **Alasan Pengaruh pada Arsitektur:** Kebutuhan keamanan ini menuntut perancangan arsitektur yang menerapkan sistem otentikasi berbasis token terenkripsi (seperti JWT/OAuth2) serta pengelolaan hak akses berlapis (*Role-Based Access Control* / RBAC). Selain itu, penyimpanan berkas digital tidak boleh diletakkan pada direktori publik yang mudah ditebak tautannya, melainkan harus dilindungi melalui mekanisme *secure tokenized URL* pada lapisan *Object Storage*.
