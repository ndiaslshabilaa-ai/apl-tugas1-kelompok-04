# B2. Atribut Kualitas yang Terukur

<!-- Penanggung jawab: [Artika Milad Arhidayah] -->

Berikut adalah rumusan ukuran kuantitatif terukur untuk 3 karakteristik pendorong utama pada Layanan Tugas Akhir (subsistem *Assignment & Assessment*), yang mencakup angka target, kondisi pengukuran, dan cara pengujiannya:

| No | Karakteristik Pendorong | Angka Target Kuantitatif | Kondisi Pengukuran | Cara Menguji |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **Performance Efficiency** | 95% halaman layanan dan proses unggah berkas draf skripsi (< 25 MB) selesai dalam waktu **< 3 detik**. | Saat 500 pengguna (mahasiswa akhir dan dosen pembimbing) mengakses sistem secara bersamaan di masa pendaftaran sidang. | Dilakukan pengujian beban (*load testing*) menggunakan *tool* seperti *JMeter* atau *k6* sebelum sistem diluncurkan. |
| 2 | **Security & Integrity** | **100%** data nilai sidang terenkripsi dengan standar keamanan tinggi dan 0 celah kerentanan kritis (*critical vulnerability*) pada sistem otorisasi. | Saat proses penginputan nilai oleh dosen penguji dan pengunggahan berkas lembar pengesahan oleh mahasiswa. | Dilakukan *Penetration Testing* dasar dan pengujian kontrol akses berbasis peran (*Role-Based Access Control* / RBAC). |
| 3 | **Maintainability** | Penyesuaian atau perubahan aturan logika bisnis (misalnya aturan syarat SKS atau batasan kuota bimbingan) dapat diselesaikan dalam waktu **< 2 hari kerja** tanpa memengaruhi modul lainnya. | Saat terjadi pembaruan pedoman akademik atau penyesuaian regulasi tugas akhir dari pihak fakultas/universitas. | Dilakukan simulasi pengujian perubahan kode (*change scenario testing*) dan audit tingkat modularitas (*code coupling*). |
