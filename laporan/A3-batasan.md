# A3. Batasan Sistem

<!-- Penanggung jawab: [Artika Milad Arhidayah] -->

Berikut adalah batasan-batasan sistem pada Layanan Tugas Akhir yang dikelompokkan ke dalam tiga kategori utama (teknologi, bisnis, dan operasional), beserta analisis dampaknya terhadap perancangan arsitektur perangkat lunak:

## 1. Batasan Teknologi (Technology Constraints)
* **Keterlibatan Infrastruktur Basis Data Pusat:** Sistem Layanan Tugas Akhir wajib terintegrasi dengan basis data pusat SIAKAD UMI yang sudah ada tanpa melakukan perombakan skema tabel inti yang dikelola oleh universitas.
* **Kapasitas Unggah Berkas Dokumen:** Batasan ukuran maksimum untuk unggah berkas draf proposal, laporan skripsi, dan lembar pengesahan berformat PDF dibatasi hingga 25 MB per dokumen guna mengoptimalkan kapasitas penyimpanan server.

### Dampak pada Arsitektur:
Arsitektur perangkat lunak harus mengimplementasikan lapisan *API Gateway* atau layanan *wrapper* khusus agar dapat melakukan sinkronisasi data dengan basis data pusat secara aman tanpa melanggar batasan skema lama. Selain itu, diperlukan pemisahan modul penyimpanan (*Object Storage*) khusus untuk berkas dokumen berukuran besar agar tidak membebani performa basis data relasional.

## 2. Batasan Bisnis (Business Constraints)
* **Kepatuhan Kalender Akademik:** Peluncuran dan pemeliharaan fitur Layanan Tugas Akhir tidak boleh mengganggu jadwal krusial universitas, khususnya periode pendaftaran wisuda dan batas akhir pemasukan nilai sidang.
* **Regulasi Alur Birokrasi Kampus:** Seluruh alur proses bisnis (mulai dari pengajuan judul, penentuan dosen pembimbing oleh Kaprodi, hingga rekapitulasi nilai sidang) harus mematuhi pedoman akademik resmi yang berlaku di lingkungan UMI.

### Dampak pada Arsitektur:
Struktur kode aplikasi harus dirancang dengan modularitas tinggi (terutama pada modul logika aturan bisnis/ *business rules*), sehingga apabila terjadi perubahan kebijakan atau penyesuaian regulasi akademik universitas, perubahan kode dapat dilakukan dengan cepat tanpa merombak modul antarmuka atau komponen lainnya.

## 3. Batasan Operasional (Operational Constraints)
* **Keterbatasan Sumber Daya Tim IT:** Pengelolaan, pemantauan, dan pemeliharaan sistem didukung oleh tim IT internal (PDTI) dengan jumlah personel yang terbatas serta jam dukungan operasional yang mengikuti jam kerja kantor kampus.
* **Lonjakan Akses Musiman (Peak Load):** Sistem dioperasikan pada lingkungan server cloud kampus dengan alokasi sumber daya komputasi yang ketat, di mana lonjakan aktivitas pengguna hanya terjadi pada momen tertentu (seperti masa pendaftaran sidang atau menjelang batas akhir bimbingan).

### Dampak pada Arsitektur:
Sistem harus dirancang agar memiliki tingkat pemeliharaan (*maintainability*) yang baik, fitur pemantauan otomatis (*logging & error tracking*), serta mekanisme penanganan beban puncak (seperti antrean proses/ *message queue*) agar sistem tetap stabil meskipun dikelola oleh tim operasional yang terbatas.
