Evaluasi ATAM Layanan Tugas Akhir

Masalah utama: alur layanan Tugas Akhir lambat dan tidak transparan. Persetujuan berbelit, koordinasi jadwal ruang dan penguji sulit, dosen kurang responsif, dan penilaian antar-penguji subjektif. Masalah ini diturunkan dari kekurangan yang berulang pada Pola 1 dan Pola 2 di lima tahap: pengajuan judul, penetapan pembimbing, bimbingan, seminar dan sidang, serta penilaian.

Solusi yang dievaluasi: sistem layanan terpadu berlapis, yaitu lapisan presentasi (dasbor matriks status), lapisan layanan (satu modul per tahap), lapisan aturan bisnis (validasi judul, kuota dan jadwal, rubrik nilai), dan lapisan data.

1. Pohon utilitas mini (3 skenario)

<img width="772" height="551" alt="Pohon Utilitas" src="https://github.com/user-attachments/assets/329f96ed-becf-4498-8c88-502779f9037c" />

Atribut mutu	Skenario	Penting	Sulit
Efisiensi	S1: verifikasi judul selesai ≤ 3 hari kerja untuk 95% pengajuan saat puncak (200 pengajuan)	Tinggi	Sedang
Transparansi	S2: status tahap dan alasan penolakan terlihat dalam ≤ 2 klik; notifikasi ≤ 5 menit	Tinggi	Rendah
Modifiabilitas	S3: prodi mengubah kuota dosen atau bobot rubrik tanpa ubah kode, selesai ≤ 1 hari	Sedang	Rendah

S1 dan S2 langsung menjawab kekurangan berulang (alur berbelit dan kriteria tidak transparan). S3 menjaga agar aturan kebijakan bisa disesuaikan.

2. Trade-off berbobot: dua alternative

Alternatif A: sistem terpadu berlapis dengan aturan otomatis.
Alternatif B: semi-manual, yaitu perbaikan SOP, formulir daring, dan koordinasi lewat email atau WhatsApp.

Skor 1-5 (5 = terbaik).

Kriteria	Bobot	A: skor	A: nilai	B: skor	B: nilai
Efisiensi waktu (S1)	30	5	150	2	60
Transparansi (S2)	25	5	125	2	50
Modifiabilitas (S3)	15	4	60	3	45
Biaya dan waktu implementasi	15	2	30	5	75
Kemudahan adopsi	15	3	45	4	60
Total (maks. 500)	100		410 (4,10)		290 (2,90)

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

Kekurangan (dari kedua pola)	Penanganan arsitektur	Status
Kriteria judul tidak transparan, persetujuan berbelit	Validasi judul, dasbor status, alasan penolakan terlihat	Teratasi
Koordinasi jadwal ruang dan penguji	Modul kuota dan jadwal otomatis	Teratasi
Subjektivitas penilaian antar-penguji	Rubrik terstandar, nilai per penguji terpantau	Berkurang, belum hilang
Penentuan pembimbing tidak sesuai harapan	Pencocokan berbasis keahlian dan kuota	Berkurang (Risiko 1)
Dosen kurang responsif	Pengingat dan eskalasi	Belum tentu (Risiko 2)
Stres sidang, keterbatasan jumlah pakar	Tidak tercakup sistem	Belum teratasi

Arsitektur ini efektif menghilangkan hambatan struktural, yaitu ketidakjelasan dan koordinasi manual. Hambatan perilaku dan kapasitas, seperti respons dosen, jumlah pakar, dan tekanan psikologis, hanya bisa dikurangi lewat kebijakan: SLA yang disepakati, beban bimbingan yang adil, dan pendampingan menjelang sidang. Sistem hanya membuat masalah itu terlihat dan terukur.
