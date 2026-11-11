**U7. Architectural Decision Records (ADR)**

Dokumen Architectural Decision Record (ADR) ini mencatat keputusan-keputusan arsitektur penting yang ditetapkan dalam perancangan Layanan Tugas Akhir pada **subsistem Assignment & Assessment** Universitas Muslim Indonesia (UMI). Setiap ADR memuat konteks permasalahan, keputusan yang dipilih, serta konsekuensi teknis yang ditimbulkan berdasarkan kebutuhan dan hasil evaluasi arsitektur.

**ADR-001: Penerapan Layered Architecture untuk Memudahkan Perubahan Aturan Akademik**

**-Title:** ADR-001: Penerapan Layered Architecture dengan Pemisahan Lapisan Aturan Bisnis pada Layanan Tugas Akhir.

**-Status:** Accepted

**-Context:**
Layanan Tugas Akhir memiliki beberapa proses, mulai dari pengajuan judul, penetapan dosen pembimbing, bimbingan, seminar, sidang, hingga penilaian. Setiap proses memiliki aturan yang perlu disesuaikan dengan kebijakan akademik. Berdasarkan hasil analisis pada U1 dan skenario Maintainability pada U2, perubahan aturan seperti persyaratan SKS dan kuota dosen diharapkan dapat dilakukan dalam waktu kurang dari 2 hari kerja. Jika aturan tersebut digabungkan dengan bagian tampilan dan penyimpanan data, pengembang akan lebih sulit melakukan perubahan tanpa memengaruhi bagian lainnya.

Hal ini juga sesuai dengan hasil wawancara R4 (Ketua Program Studi) yang menyampaikan bahwa pemantauan kuota dosen pembimbing masih menjadi kendala. Oleh karena itu, diperlukan pembagian bagian layanan yang lebih teratur agar perubahan aturan akademik lebih mudah dilakukan.

**- Decision:**
Kelompok menyepakati penggunaan Layered Architecture dengan membagi layanan menjadi empat lapisan, yaitu:

**1. Presentation Layer:** Menampilkan halaman pengajuan judul, dasbor, formulir bimbingan, jadwal sidang, dan hasil penilaian.

**2. Service Layer:** Mengelola proses pengajuan judul, penetapan pembimbing, bimbingan, seminar, sidang, dan penilaian.

**3. Business Rules Layer:** Mengatur validasi judul, kuota dosen pembimbing, jadwal sidang, serta aturan penilaian.

**4. Data Layer:** Menyimpan data mahasiswa, dokumen tugas akhir, riwayat bimbingan, jadwal, dan nilai.
  Pembagian ini mengikuti rancangan arsitektur pada U5. Aturan akademik ditempatkan pada lapisan tersendiri agar perubahan kebijakan tidak perlu mengubah tampilan maupun penyimpanan data.

**- Consequences:**

**- Positif:** Pengembang lebih mudah memperbaiki atau mengubah aturan akademik, seperti kuota dosen dan persyaratan tugas akhir, tanpa mengganggu bagian layanan lainnya.

**- Positif:** Setiap bagian memiliki tugas yang lebih jelas sehingga lebih mudah diperiksa dan diuji.

**- Negatif:** Struktur kode menjadi lebih banyak dan membutuhkan pengaturan komunikasi antar-lapisan agar proses tetap berjalan dengan baik.

**ADR-002: Penerapan Controlled Override untuk Penanganan Kondisi Khusus Akademik**

**- Title: ADR-002:** Penerapan Controlled Override dengan RBAC dan Audit Log untuk Penyesuaian Aturan Akademik.

**- Status:** Accepted

**- Context:**
Berdasarkan hasil wawancara R3 dengan dosen pembimbing/penguji dan R4 dengan Ketua Program Studi, penjadwalan sidang dapat mengalami benturan dengan jadwal mengajar dosen, sedangkan pembagian kuota dosen pembimbing terkadang belum merata. Hasil evaluasi ATAM pada U6 juga menunjukkan bahwa aturan otomatis memang membantu proses menjadi lebih teratur, tetapi belum tentu dapat menangani semua kondisi khusus.

Jika aturan diterapkan terlalu ketat, pihak program studi akan kesulitan melakukan penyesuaian ketika terjadi keterbatasan dosen atau benturan jadwal. Namun, perubahan tersebut tetap harus memiliki batasan agar tidak dilakukan oleh sembarang pengguna dan riwayatnya tetap dapat diperiksa.

**- Decision:**
Kelompok menyepakati penerapan mekanisme Controlled Override, yaitu memberikan kesempatan kepada pihak yang berwenang untuk melakukan penyesuaian terhadap aturan tertentu apabila terdapat kondisi khusus dalam proses tugas akhir.

**Mekanisme ini diterapkan dengan ketentuan sebagai berikut:**

**1. Role-Based Access Control (RBAC):** Hanya Ketua Program Studi atau staf akademik yang diberikan kewenangan yang dapat melakukan penyesuaian.

**2. Alasan Perubahan:** Setiap penyesuaian wajib disertai alasan agar dapat diketahui mengapa aturan otomatis perlu dilewati.

**3. Audit Log:** Setiap perubahan dicatat, meliputi identitas pengguna, waktu perubahan, dan tindakan yang dilakukan.
  Dengan cara ini, penyesuaian dapat dilakukan ketika terjadi masalah jadwal atau pembagian dosen, tetapi tetap berada dalam pengawasan pihak yang berwenang.

**- Consequences:**

**- Positif:** Membantu pihak program studi menangani benturan jadwal dan keterbatasan dosen tanpa harus mengabaikan seluruh aturan yang sudah ditetapkan.

**- Negatif:** Membutuhkan pengaturan hak akses dan pencatatan aktivitas yang baik agar kewenangan tersebut tidak disalahgunakan.
