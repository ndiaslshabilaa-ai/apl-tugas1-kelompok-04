ADR-001: Penggunaan Cloud Object Storage untuk Berkas Draf Tugas Akhir
- Status: Diterima
- Tanggal: 24-10-2026
- Pengambil keputusan: Artika Milad Arhidayah, Andi Naqia Aura W.R, Annisa Rezky Ashriani, B.Nadia Salsabila

Context
Mahasiswa tingkat akhir mengunggah berkas proposal, draf skripsi, dan lembar pengesahan berukuran hingga 25 MB per dokumen. Jika berkas disimpan langsung pada direktori lokal server aplikasi utama, kapasitas penyimpanan server akan cepat penuh dan berisiko membebani pemrosesan I/O server. Hal ini berdampak langsung pada kegagalan memenuhi target kinerja waktu tanggap aplikasi (terkait langsung dengan kode ASR: **A4-1** mengenai efisiensi kinerja saat unggah berkas massal dan **A3-1** terkait batasan ukuran berkas).

Decision
Kami akan menggunakan layanan Cloud Object Storage terpusat yang terisolasi khusus untuk menampung seluruh berkas digital dokumen tugas akhir mahasiswa.

Consequences
- Dampak Positif: Skalabilitas penyimpanan menjadi tinggi, aman, dan memisahkan pemrosesan I/O berkas sehingga tidak membebani server aplikasi maupun basis data utama.
- Dampak Negatif & Trade-off: Memerlukan tambahan konfigurasi jaringan aman (SDK/API khusus) serta pengelolaan otorisasi akses unduh berkas yang lebih ketat, yang sedikit menambah kompleksitas integrasi.

Compliance
Keputusan ini dipatuhi melalui peninjauan kode (*code review*) pada modul pengunggahan berkas serta pengujian integrasi API penyimpanan sebelum masa pendaftaran sidang dibuka.
