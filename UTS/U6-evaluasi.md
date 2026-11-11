Evaluasi ATAM Layanan Tugas Akhir

Masalah utama: alur layanan Tugas Akhir lambat dan tidak transparan. Persetujuan berbelit, koordinasi jadwal ruang dan penguji sulit, dosen kurang responsif, dan penilaian antar-penguji subjektif. Masalah ini diturunkan dari kekurangan yang berulang pada Pola 1 dan Pola 2 di lima tahap: pengajuan judul, penetapan pembimbing, bimbingan, seminar dan sidang, serta penilaian.

Solusi yang dievaluasi: sistem layanan terpadu berlapis, yaitu lapisan presentasi (dasbor matriks status), lapisan layanan (satu modul per tahap), lapisan aturan bisnis (validasi judul, kuota dan jadwal, rubrik nilai), dan lapisan data.

1. Pohon utilitas mini (3 skenario)

<img width="772" height="551" alt="Pohon Utilitas" src="https://github.com/user-attachments/assets/329f96ed-becf-4498-8c88-502779f9037c" />

Gambar 1. Pohon utilitas mini: tiga atribut mutu (efisiensi, transparansi, modifiabilitas), masing-masing dengan satu skenario terukur beserta prioritasnya (Penting dan Sulit).

S1 (Efisiensi): verifikasi judul selesai ≤ 3 hari kerja untuk 95% pengajuan saat puncak (200 pengajuan).
S2 (Transparansi): status tahap dan alasan penolakan terlihat dalam ≤ 2 klik; notifikasi ≤ 5 menit.
S3 (Modifiabilitas): prodi mengubah kuota dosen atau bobot rubrik tanpa ubah kode, selesai ≤ 1 hari.

S1 dan S2 langsung menjawab kekurangan berulang (alur berbelit dan kriteria tidak transparan). S3 menjaga agar aturan kebijakan bisa disesuaikan.

2. Trade-off berbobot: dua alternatif
Alternatif A: sistem terpadu berlapis dengan aturan otomatis.
Alternatif B: semi-manual, yaitu perbaikan SOP, formulir daring, dan koordinasi lewat email atau WhatsApp.

Skor 1-5 (5 = terbaik). Bobot: efisiensi 30, transparansi 25, modifiabilitas 15, biaya dan waktu implementasi 15, kemudahan adopsi 15.

<img alt="Trade-off Berbobot" src="GANTI_DENGAN_URL_GAMBAR_2" />

Gambar 2. Nilai terbobot per kriteria. Total: A = 410 (4,10) dan B = 290 (2,90).

Kesimpulan: Alternatif A unggul. Hasilnya cukup kokoh: B baru menang jika bobot biaya naik sekitar 20 poin dengan mengorbankan bobot efisiensi, artinya prodi harus lebih mementingkan anggaran daripada kecepatan layanan.

3. Analisis ala ATAM

Risiko 1: data keahlian dosen tidak mutakhir.
Pencocokan pembimbing otomatis bergantung pada data keahlian dan kuota. Jika data usang, penugasan tetap tidak sesuai harapan, sehingga kekurangan tahap penetapan pembimbing bertahan meski prosesnya sudah digital.
Mitigasi: dosen memperbarui profil tiap semester, dan koordinator punya hak koreksi.

Risiko 2: bottleneck berpindah ke antrean digital.
Sistem tidak memaksa dosen merespons. Tanpa batas waktu respons (SLA) dan eskalasi otomatis, target S1 gagal karena persetujuan menumpuk di dosen, bukan di prosedur.
Mitigasi: pengingat bertahap, eskalasi ke koordinator setelah batas waktu, dan data waktu respons yang terlihat.

Non-risiko: pemisahan lapisan aturan bisnis dari presentasi.
Perubahan kuota atau bobot rubrik cukup lewat konfigurasi di lapisan aturan, tanpa menyentuh tampilan atau data. Keputusan ini aman untuk S3.

Sensitivity point: kuota dosen per semester.
Perubahan kecil pada kuota sangat memengaruhi waktu tunggu penetapan pembimbing, dan lewat itu memengaruhi S1. Parameter ini harus dipantau dan diubah dengan hati-hati.

Trade-off point: ketatnya aturan otomatis.
Aturan yang ketat (validasi judul, kuota keras) menaikkan konsistensi dan transparansi (S1, S2), tetapi menurunkan fleksibilitas. Kasus khusus seperti dosen pakar langka atau jadwal penguji bentrok jadi sulit ditangani dan menambah beban koordinator (S3).
Rekomendasi: sediakan override terkontrol dengan alasan yang tercatat.

4. Apakah masalah utama teratasi?

Teratasi sebagian, dan bagian yang tersisa bukan masalah teknis.

<img alt="Status Masalah Utama" src="GANTI_DENGAN_URL_GAMBAR_3" />

Gambar 3. Status tiap kekurangan: teratasi (hijau), sebagian atau belum tentu (kuning), belum teratasi (koral).

Arsitektur ini efektif menghilangkan hambatan struktural, yaitu ketidakjelasan dan koordinasi manual. Hambatan perilaku dan kapasitas, seperti respons dosen, jumlah pakar, dan tekanan psikologis, hanya bisa dikurangi lewat kebijakan: SLA yang disepakati, beban bimbingan yang adil, dan pendampingan menjelang sidang. Sistem hanya membuat masalah itu terlihat dan terukur.
