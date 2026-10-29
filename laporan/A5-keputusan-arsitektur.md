# A5. Keputusan Arsitektur dan ADR

<!-- Penanggung jawab: [Artika Milad Arhidayah] -->

Berikut adalah dua dokumen *Architecture Decision Record* (ADR) untuk Layanan Tugas Akhir pada subsistem *Assignment & Assessment*, beserta penjelasan rencana komunikasi kelompok untuk menghindari anti-pattern dalam pengambilan keputusan arsitektur.

---

## 1. Arsitektur Decision Record (ADR)

### ADR-001: Penggunaan Cloud Object Storage untuk Penyimpanan Berkas Draf Tugas Akhir
* **Status:** Accepted
* **Context:** Mahasiswa akhir mengunggah dokumen proposal, draf skripsi, dan lembar pengesahan berukuran hingga 25 MB per dokumen. Jika disimpan langsung di direktori lokal server aplikasi utama, kapasitas penyimpanan server akan cepat penuh dan berisiko mengganggu kinerja basis data relasional saat terjadi unggah massal menjelang tenggat sidang.
* **Decision:** Kami akan menggunakan layanan *Cloud Object Storage* terpusat yang terisolasi khusus untuk menampung seluruh berkas digital dokumen tugas akhir mahasiswa.
* **Consequences:** 
  * *Untung:* Skalabilitas penyimpanan tinggi, aman, dan tidak membebani database relasional utama.
  * *Rugi:* Memerlukan tambahan konfigurasi jaringan aman (SDK/API khusus) serta manajemen otorisasi akses unduh berkas yang ketat.
* **Compliance:** Ditinjau setiap akhir semester dan diuji melalui pemeriksaan integritas tautan unggah dokumen sebelum masa pendaftaran sidang dimulai.

### ADR-002: Penerapan Asynchronous Message Queue untuk Proses Penjadwalan Sidang
* **Status:** Accepted
* **Context:** Proses penjadwalan sidang melibatkan validasi kuota dosen penguji, pengecekan ketersediaan ruangan, serta pengiriman notifikasi massal secara bersamaan kepada dosen dan mahasiswa, yang dapat memicu keterlambatan respons sistem (*latency*).
* **Decision:** Kami akan menerapkan antrean pesan asinkron (*Asynchronous Message Queue*) untuk menangani pemrosesan data pendaftaran dan distribusi notifikasi secara bertahap (*background worker*).
* **Consequences:** 
  * *Untung:* Sistem tahan terhadap lonjakan beban transaksi dan mencegah terjadinya *request timeout* pada sisi pengguna.
  * *Rugi:* Kompleksitas arsitektur bertambah dan memerlukan pemantauan khusus terhadap status antrean pesan (*queue monitoring*).
* **Compliance:** Ditinjau melalui pengujian beban (*load testing*) simulasi pendaftaran sidang sebelum diunggah ke lingkungan produksi kampus.

---

## 2. Rencana Komunikasi dan Pencegahan Anti-Pattern

Untuk memastikan seluruh anggota kelompok memahami dan menyetujui setiap keputusan arsitektur yang diambil, serta menghindari kesalahan umum dalam dokumentasi (*anti-pattern*), kelompok menerapkan strategi komunikasi sebagai berikut:

* **Penyimpanan Dokumen ADR:** Seluruh dokumen ADR disimpan secara transparan di dalam folder `/adr` pada repository GitHub kelompok, sehingga setiap anggota dapat meninjau dan melacak perubahannya.
* **Saluran Pemberitahuan:** Anggota tim diberi tahu mengenai adanya keputusan atau pembaruan ADR melalui pesan singkat (*instant messaging*) berupa tautan langsung ke berkas terkait di repository, bukan melalui isi email yang rentan terabaikan.
* **Pencegahan Tiga Anti-Pattern Keputusan Arsitektur:**
  1. *Covering Your Assets (CYA):* Menghindari pembuatan keputusan yang terlalu rumit hanya untuk menghindari disalahkan; setiap keputusan harus berdasarkan kebutuhan nyata (*ASR*).
  2. *Groundhog Day:* Menghindari perdebatan berulang terhadap masalah yang sama dengan cara mendokumentasikan alasan dan konteks keputusan secara jelas di dalam format ADR.
  3. *Email-Driven Architecture:* Menghindari keputusan arsitektur yang hanya diputuskan lewat percakapan email pribadi; seluruh keputusan wajib dicatat secara resmi melalui *Pull Request* atau *commit* berkas markdown di dalam repository kelompok.
