# U6. Evaluasi Arsitektur (ATAM & Utility Tree)

Bab ini menyajikan evaluasi kualitas arsitektur perangkat lunak menggunakan metode *Architecture Tradeoff Analysis Method* (ATAM) dan *Utility Tree* untuk subsistem Layanan Tugas Akhir (*Assignment & Assessment*). Evaluasi ini melibatkan umpan balik dari pemangku kepentingan utama, khususnya **Staf Administrasi Akademik**, guna memastikan sistem memenuhi atribut kualitas yang disyaratkan.

---

## 6.1 Utility Tree (Pohon Utilitas)
*Utility Tree* digunakan untuk menerjemahkan kebutuhan kualitas bisnis dan operasional akademik ke dalam skenario spesifik yang dapat diukur secara arsitektural.

| Atribut Kualitas | Skenario Stimulus | Respon yang Diharapkan | Taktik Arsitektur yang Diterapkan |
| :--- | :--- | :--- | :--- |
| **1. Performance Efficiency** | Lonjakan 2.000 mahasiswa melakukan pendaftaran sidang dan unggah draf skripsi (25 MB) secara serentak. | Sistem tetap responsif, antrean pendaftaran tertampung tanpa *server crash*, dan waktu tanggap rata-rata di bawah 3 detik. | • *Message Broker (RabbitMQ/Redis)*<br>• *Background Worker (Asynchronous)*<br>• *Cloud Object Storage* |
| **2. Security & Integrity** | Upaya akses tidak sah atau manipulasi data nilai ujian oleh pihak luar/mahasiswa. | Seluruh komunikasi API terenkripsi, sesi pengguna diverifikasi secara ketat, dan integritas data nilai terlindungi. | • *JWT Authentication (JSON Web Token)*<br>• *Role-Based Access Control (RBAC)* |
| **3. Maintainability** | Pembaruan aturan validasi SKS atau penambahan modul verifikasi berkas oleh pengembang. | Modifikasi kode dapat dilakukan secara cepat tanpa merusak modul lain atau memicu *ripple effect*. | • *Layered Architecture*<br>• *Single Responsibility Principle (SRP)* |

---

## 6.2 Analisis Metode ATAM (*Architecture Tradeoff Analysis Method*)

### 1. Titik Sensitivitas (*Sensitivity Points*)
* **Penggunaan *Message Broker* pada Pendaftaran:** Menjadi titik sensitif utama terhadap atribut *Performance Efficiency*. Jika konfigurasi antrean (*queue*) tidak dioptimalkan, penumpukan data (*bottleneck*) dapat terjadi pada *worker*.
* **Pemisahan Lapisan (*Layered Architecture*):** Menjadi titik sensitif terhadap *Maintainability*. Keputusan memisahkan *Business Logic Layer* dari *Presentation Layer* memastikan perubahan logika akademik tidak memerlukan perombakan pada antarmuka pengguna.

### 2. Titik Pertukaran (*Tradeoff Points*)
* **Kompleksitas Keamanan vs. Kinerja Sistem:** 
  * *Pertukaran:* Penerapan verifikasi token berlapis (*JWT & Session Check*) pada setiap permintaan unggah berkas besar (25 MB) menambah overhead komputasi jaringan. 
  * *Solusi:* Kompleksitas ini diterima demi menjamin tingkat keamanan dan kerahasiaan dokumen akademik (*Security & Integrity*).
* **Asinkronisitas Pesan vs. Konsistensi Data Langsung:** 
  * *Pertukaran:* Penggunaan *Message Broker* membuat status pendaftaran mahasiswa tidak langsung ditulis ke basis data utama pada detik yang sama (*eventual consistency*). 
  * *Solusi:* Sistem memberikan notifikasi status "Dalam Antrean (*Queued*)" kepada pengguna untuk menjaga transparansi pengalaman pengguna (*UX*).

### 3. Risiko dan Non-Risiko (*Risks & Non-Risks*)
* **Risiko (*Risks*):** Ketergantungan penuh pada layanan pihak ketiga atau *broker* eksternal (seperti Redis/RabbitMQ). Jika layanan tersebut mengalami kegagalan (*outage*), proses pendaftaran sidang dapat tertunda sementara.
* **Non-Risiko (*Non-Risks*):** Desain modular (*split module*) pada subsistem penilaian terbukti aman dan tidak menimbulkan dampak negatif terhadap modul bimbingan (*logbook*) yang berjalan secara paralel.
