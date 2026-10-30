# BAB IV. Penutup

<!-- Kesimpulan dan saran. Penanggung jawab: [Annisa Rezky Ashriani] -->

## 4.1 Kesimpulan
Berdasarkan analisis dan perancangan yang telah dilakukan, kesimpulan arsitektur Layanan Tugas Akhir pada subsistem Assignment & Assessment UMI adalah sebagai berikut.
1.	Layanan Tugas Akhir mendukung proses pengajuan judul, bimbingan, unggah berkas, penjadwalan sidang, dan penilaian secara digital. Tujuannya mempercepat administrasi akademik, meningkatkan transparansi bimbingan, dan menjamin akurasi nilai sidang akhir.
2.	Enam pemangku kepentingan telah dipetakan pada matriks Power/Interest (Gambar 1). Dosen Pembimbing & Penguji serta Kaprodi masuk kuadran Manage Closely. PDTI UMI dan LPMI masuk Keep Satisfied. Mahasiswa Akhir dan Staf Administrasi Akademik masuk Keep Informed.
3.	Batasan sistem mencakup integrasi dengan SIAKAD tanpa perombakan skema inti, batas unggah 25 MB per dokumen, kepatuhan terhadap kalender akademik dan regulasi birokrasi kampus, serta keterbatasan tim IT dan lonjakan akses musiman.
4.	Tiga ASR, yaitu kinerja saat lonjakan beban (500 pengguna simultan), integritas dan audit trail, serta keamanan akses berkas, menjadi dasar tiga karakteristik pendorong: Performance Efficiency, Security & Integrity, dan Maintainability. Targetnya adalah 95% proses selesai dalam waktu kurang dari 3 detik, 0 kerentanan kritis pada sistem otorisasi, dan perubahan aturan bisnis selesai dalam waktu kurang dari 2 hari kerja. Ketiganya dipetakan ke ISO/IEC 25010.
5.	Dua keputusan arsitektur dicatat dalam ADR: Cloud Object Storage (ADR-001) agar penyimpanan berkas tidak membebani basis data relasional, dan Asynchronous Message Queue (ADR-002) agar sistem tahan terhadap beban puncak. Konsekuensinya adalah tambahan konfigurasi jaringan aman, manajemen otorisasi unduh, dan pemantauan antrean.
6.	Arsitektur dijabarkan dalam tiga struktur: struktur modul berlapis presentasi, logika bisnis, dan data (Gambar 2); struktur C&C yang menghubungkan browser, server web, cache, message queue, worker, Cloud Object Storage, dan basis data pusat (Gambar 3); serta struktur alokasi berupa penempatan di cloud kampus dan pembagian modul ke Tim A sampai Tim D (Gambar 4).
7.	Analisis trade-off menunjukkan bahwa Security didahulukan untuk modul nilai sidang dan lembar pengesahan, sedangkan Performance Efficiency didahulukan untuk logbook dan pengajuan judul. Maintainability didahulukan atas fleksibilitas melalui satu alur standar universitas dengan kustomisasi minimal.

## 4.2 Saran
1.	Pengujian sebelum peluncuran. Lakukan load testing (misalnya dengan JMeter atau k6) dan penetration testing dasar serta pengujian RBAC sebelum masa pendaftaran sidang, agar target kinerja dan keamanan terverifikasi.
2.	Pemantauan operasional. Terapkan logging, error tracking, dan queue monitoring otomatis agar tim PDTI yang jumlahnya terbatas tetap dapat menjaga stabilitas sistem.
3.	Pemeliharaan ADR. Tinjau ADR setiap akhir semester dan simpan di folder /adr pada repository. Catat setiap keputusan baru melalui Pull Request agar terhindar dari anti-pattern Covering Your Assets, Groundhog Day, dan Email-Driven Architecture.
4.	Menjaga modularitas aturan bisnis. Pertahankan modul Validasi Syarat SKS & Kuota dan Penjadwalan Sidang agar tetap terpisah dari antarmuka, sehingga perubahan regulasi akademik dapat diterapkan tanpa merombak komponen lain.
5.	Menjaga ketersediaan dan kapasitas. Pastikan layanan tetap tersedia pada periode krusial seperti pendaftaran sidang dan tenggat wisuda, serta pantau pertumbuhan volume dokumen di Cloud Object Storage setiap semester.


