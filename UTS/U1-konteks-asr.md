# U1. Konteks dan ASR (Architectural Significant Requirements)

## 1.1 Ringkasan Layanan
Layanan Tugas Akhir merupakan salah satu layanan akademik pada platform *Smart Campus* Universitas Muslim Indonesia (UMI), yang termasuk dalam subsistem *Assignment & Assessment*. Layanan ini membantu mahasiswa dalam mengurus tugas akhir, mulai dari pengajuan judul proposal, penentuan dosen pembimbing, pengisian kegiatan bimbingan (*logbook*), sampai pemantauan perkembangan skripsi.

Proses lainnya meliputi pengumpulan dan pemeriksaan berkas persyaratan, pengaturan jadwal seminar dan sidang akhir, serta pencatatan nilai hasil penilaian. Dengan adanya layanan ini, mahasiswa, dosen, dan staf akademik dapat mengelola setiap tahapan tugas akhir dengan lebih mudah dan teratur.

## 1.2 Masalah Utama Layanan dan Bukti Lapangan
* **Masalah Utama:**
  
Berdasarkan hasil wawancara dengan lima responden, ditemukan beberapa kendala dalam pengelolaan Layanan Tugas Akhir. Permasalahan utama meliputi lambatnya respons layanan hingga berpotensi terjadi request timeout, serta kegagalan atau lamanya proses unggah draf skripsi, terutama pada dokumen berukuran besar dan memiliki banyak gambar. Peningkatan jumlah pengguna secara bersamaan saat pembukaan pendaftaran juga dapat menyebabkan layanan sulit diakses dan mengganggu proses pendaftaran seminar maupun sidang.

Selain itu, pencatatan bimbingan dan revisi belum terkelola dengan baik sehingga riwayat perkembangan tugas akhir terkadang sulit dipantau. Kendala lainnya mencakup informasi persyaratan sidang yang kurang jelas, penjadwalan yang berpotensi berbenturan, pemantauan kuota dosen pembimbing, serta pemeriksaan berkas mahasiswa yang masih harus dilakukan berulang kali.

Beberapa temuan tersebut diperoleh dari wawancara dengan responden sebagai berikut:
* **Bukti Lapangan (Berdasarkan Wawancara Responden):**
  
  **R1 Mahasiswa Akhir(25 Oktober 2026):** Akses melambat saat pendaftaran ramai, notifikasi persetujuan logbook belum otomatis, dan unggah dokumen terkendala ukuran file.
  
  **R3 Dosen Pembimbing/Penguji(26 Oktober 2026):** Pemeriksaan draf dan riwayat bimbingan belum terpusat; jadwal sidang berpotensi berbenturan dengan jadwal mengajar.
  
  **R5 Staf administrasi akademik (27 Oktober 2026):** Berkas persyaratan yang tidak lengkap atau salah format menyebabkan pemeriksaan harus dilakukan berulang kali. Penggunaan ruangan sidang juga berpotensi berbenturan saat periode puncak.
    
## 1.3 Stakeholder Utama
Pihak-pihak yang memiliki peran dalam pengelolaan Layanan Tugas Akhir pada subsistem Assignment & Assessment Universitas Muslim Indonesia (UMI) adalah sebagai berikut:
**1	Mahasiswa tingkat akhir	Mengajukan judul, mengisi logbook, mengunggah dokumen, dan memantau status persetujuan tugas akhir.	Keep Informed**
**2	Dosen pembimbing dan penguji	Memeriksa judul dan dokumen, memberikan bimbingan, serta melakukan penilaian seminar dan sidang.	Key Player**
**3	Ketua Program Studi	Mengatur penugasan dosen pembimbing, memantau perkembangan mahasiswa, dan mengawasi hasil kelulusan.	Key Player**
**4	Staf administrasi akademik	Memeriksa persyaratan mahasiswa, mengatur jadwal dan ruangan sidang, serta mengelola data nilai.	Keep Informed**

## 1.4 Kebutuhan Signifikan Arsitektur (ASR) 
Berdasarkan hasil analisis dan wawancara, terdapat tiga kebutuhan utama yang perlu diperhatikan dalam perancangan Layanan Tugas Akhir, yaitu:
**1	Performance (Kinerja)**:Layanan harus mampu menangani hingga 500 pengguna secara bersamaan dengan target waktu muat halaman rata-rata kurang dari 3 detik.
**2	Integrity & Auditability**:Setiap aktivitas penting, seperti pengajuan judul, persetujuan bimbingan, dan pencatatan nilai harus tersimpan serta memiliki riwayat yang dapat ditelusuri.
**3	Security (Keamanan)**:Dokumen tugas akhir dan nilai mahasiswa harus terlindungi serta hanya dapat diakses oleh pihak yang memiliki wewenang.
Ketiga kebutuhan tersebut diprioritaskan agar layanan tetap responsif, data terjaga, dan setiap proses tugas akhir dapat dipantau dengan baik.

## 1.5 Keterkaitan Quality Drivers dengan ASR
 Quality Drivers dipilih berdasarkan kebutuhan utama Layanan Tugas Akhir. Hubungan antara keduanya dapat dilihat pada tabel berikut:
**1	Performance Efficiency**:	Performance	Membantu layanan tetap cepat meskipun diakses banyak pengguna secara bersamaan.
**2	Security & Integrity**:	Security dan Integrity & Auditability	Menjaga data tugas akhir agar tidak diakses sembarang pihak dan memastikan setiap aktivitas penting tercatat.
**3	Maintainability**:	Mendukung seluruh ASR	Memudahkan pengelolaan dan perbaikan layanan jika ada perubahan aturan akademik.
Ketiga Quality Drivers tersebut dipilih karena sesuai dengan kendala dan kebutuhan yang ditemukan dari hasil wawancara. Dengan begitu, layanan diharapkan lebih mudah digunakan, aman, dan tidak sulit diperbaiki ketika diperlukan.
