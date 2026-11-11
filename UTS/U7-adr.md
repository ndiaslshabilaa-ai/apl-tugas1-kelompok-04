# U7. Architecture Decision Records (ADR)

Dokumen Architectural Decision Record (ADR) ini mencatat keputusan-keputusan arsitektur penting yang ditetapkan dalam perancangan Layanan Tugas Akhir pada *subsistem Assignment & Assessment* Universitas Muslim Indonesia (UMI). Setiap ADR memuat konteks permasalahan, keputusan yang dipilih, serta konsekuensi teknis yang ditimbulkan berdasarkan kebutuhan dan hasil evaluasi arsitektur.

---

## ADR 001: Penggunaan *Message Broker* untuk Penanganan Lonjakan Trafik Pendaftaran Sidang

* **Status:** Diterima (*Accepted*)
* **Konteks:** 
  Pada periode pembukaan pendaftaran sidang akhir semester, sistem mengalami lonjakan trafik (*traffic spike*) secara masif di mana ribuan mahasiswa mengakses server secara bersamaan untuk mengunggah draf skripsi (ukuran berkas hingga 25 MB) dan mengirimkan data pendaftaran. Pendekatan sinkron langsung ke basis data berisiko tinggi menyebabkan *database bottleneck*, *race condition*, dan kegagalan server (*server crash*).
* **Keputusan:** 
  Menerapkan **Message Broker Pattern** menggunakan antrean pesan (*RabbitMQ/Redis Queue*) yang dikombinasikan dengan *Background Worker* untuk memproses pengajuan pendaftaran dan unggahan berkas secara asinkron.
* **Konsekuensi:**
  * **Positif:** Sistem menjadi jauh lebih tahan banting (*resilient*) terhadap lonjakan beban, menekan tingkat kegagalan (*error rate*) hingga mendekati 0%, serta menjaga waktu tanggap server tetap cepat.
  * **Negatif / Tantangan:** Menambahkan kompleksitas infrastruktur operasional (*deployment* dan pemantauan layanan *broker*). Status pendaftaran mahasiswa menjadi bersifat konsisten secara bertahap (*eventual consistency*), sehingga memerlukan indikator status "Dalam Antrean" pada antarmuka pengguna.

---

## ADR 002: Penerapan *JWT Authentication* dan *Role-Based Access Control (RBAC)*

* **Status:** Diterima (*Accepted*)
* **Konteks:** 
  Subsistem Layanan Tugas Akhir melibatkan multi-pengguna dengan hak akses yang sangat sensitif, mulai dari pengunggahan draf dokumen mahasiswa, validasi berkas oleh Staf Administrasi Akademik, hingga penginputan nilai ujian oleh Dosen Penguji. Sistem memerlukan mekanisme autentikasi yang aman, *stateless*, dan terenkripsi untuk mencegah manipulasi data dan akses tidak sah.
* **Keputusan:** 
  Menggunakan **JWT (JSON Web Token)** untuk autentikasi sesi pengguna berbasis API serta menerapkan **Role-Based Access Control (RBAC)** secara ketat guna membatasi hak akses berdasarkan peran aktor (Mahasiswa, Dosen, dan Staf Administrasi).
* **Konsekuensi:**
  * **Positif:** Memastikan integritas dan kerahasiaan data akademik terlindungi dengan baik, serta memudahkan pengelolaan skalabilitas sesi pengguna tanpa membebani memori server pusat (*stateless*).
  * **Negatif / Tantangan:** Memerlukan penanganan kedaluwarsa token (*token expiration*) dan mekanisme *refresh token* yang cermat agar tidak mengganggu kenyamanan pengguna saat berinteraksi dengan sistem.

---

## ADR 003: Penerapan *Layered Architecture* dan *Split Module*

* **Status:** Diterima (*Accepted*)
* **Konteks:** 
  Seiring bertambahnya fitur di masa mendatang (seperti penambahan jenis evaluasi baru atau integrasi sistem akademik universitas lainnya), kode sumber subsistem harus mudah dipelihara (*maintainable*) dan dikembangkan oleh tim pengembang yang berbeda tanpa memicu kerusakan pada modul yang sudah berjalan.
* **Keputusan:** 
  Menerapkan pola **Layered Architecture** (Pemisahan tegas antara *Presentation Layer*, *Business Logic Layer*, dan *Data Layer*) serta memecah fungsionalitas ke dalam modul-modul mandiri (*Split Module* / SRP).
* **Konsekuensi:**
  * **Positif:** Mempermudah proses pengujian unit (*unit testing*), mengurangi dampak kerusakan turunan (*ripple effect*) saat ada perubahan kode, dan meningkatkan keterbacaan kode sumber (*maintainability*).
  * **Negatif / Tantangan:** Menuntut kedisiplinan tim pengembang yang tinggi dalam menjaga batas-batas arsitektur (*layer boundaries*) agar tidak terjadi ketergantungan silang yang melanggar prinsip modularitas.
