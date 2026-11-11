# U5. Desain Arsitektur dan Diagram

Bab ini menyajikan rujukan perancangan tingkat lanjut untuk subsistem *Assignment & Assessment* (Layanan Tugas Akhir UMI). Perancangan ini didasarkan pada prinsip-prinsip rekayasa perangkat lunak modern untuk menjamin skalabilitas, kemudahan pemeliharaan, serta integritas data akademik.

---

## 5.1 Prinsip Desain Arsitektur yang Diterapkan
Penerapan prinsip desain arsitektur pada subsistem Layanan Tugas Akhir dijabarkan melalui tiga pilar utama berikut:

1. **Separation of Concerns (SoC - Pemisahan Kepentingan):**
   * **Implementasi:** Sistem dibagi secara tegas menjadi tiga lapisan mandiri: **Lapisan Antarmuka (*Presentation Layer*)** untuk interaksi pengguna, **Lapisan Logika Bisnis (*Business Logic Layer*)** untuk aturan validasi SKS dan penjadwalan, serta **Lapisan Penyimpanan (*Data & Storage Layer*)** untuk basis data relasional dan *Object Storage*.
   * **Manfaat:** Memastikan perubahan pada tampilan antarmuka (misalnya pembaruan UI web/mobile) tidak akan merusak aturan validasi logika bisnis di backend.

2. **Single Responsibility Principle (SRP - Prinsip Tanggung Jawab Tunggal):**
   * **Implementasi:** Setiap modul, kelas, atau komponen layanan dirancang hanya memiliki satu alasan spesifik untuk berubah. Sebagai contoh, Modul Pendaftaran Sidang terisolasi secara murni untuk mengelola antrean pendaftaran, terpisah dari Modul Pengelolaan Berkas Skripsi (*File Uploader*) dan Modul Input Nilai Ujian.
   * **Manfaat:** Mengurangi *coupling* antar-modul dan memudahkan proses pengujian unit (*unit testing*) secara terisolasi.

3. **High Cohesion & Low Coupling (Kohesi Tinggi & Ketergantungan Rendah):**
   * **Implementasi:** Elemen-elemen fungsional yang saling berkaitan erat dikelompokkan ke dalam satu modul yang sama (*High Cohesion*), sementara komunikasi antar-modul dibatasi menggunakan antarmuka atau kontrak pesan yang terstandarisasi (*Low Coupling*).
   * **Manfaat:** Meminimalkan dampak kerusakan (*ripple effect*) apabila terjadi perbaikan atau penambahan fitur baru pada masa mendatang.

---

## 5.2 Penjelasan Diagram Arsitektur

### Diagram 1: Diagram Konteks & Aktor (*Use Case / Context Diagram*)

#### Deskripsi Fungsional & Batasan Sistem
Diagram konteks mendefinisikan batas sistem (*system boundary*) dari platform Layanan Tugas Akhir *Smart Campus* UMI. Sistem ini melayani tiga aktor utama yang memiliki hak akses dan batasan fungsional berbeda:

* **Mahasiswa Akhir:** Berperan sebagai pemrakarsa utama yang melakukan pengajuan judul, mengunggah draf skripsi (hingga 25 MB), serta mendaftarkan diri ke jadwal sidang.
* **Dosen Pembimbing & Penguji:** Berperan dalam mengontrol proses bimbingan berkala (*logbook*) serta memberikan evaluasi dan input nilai akhir ujian sidang.
* **Staf Administrasi Akademik:** Berperan sebagai verifikator administratif yang memvalidasi kelayakan berkas persyaratan sidang serta mengatur penjadwalan ruang dan dewan penguji.

![Diagram Konteks](../diagram-uts/Diagram%20konteks.drawio.png)

---

### Diagram 2: Diagram Arsitektur Penerapan Pola (*Component & Connector / Broker Diagram*)

#### Penjelasan Komponen dan Alur Runtime
Diagram ini memetakan arsitektur saat sistem berjalan (*runtime architecture*) untuk menjawab tantangan *Performance Efficiency* (khususnya mengatasi lonjakan trafik / *traffic spike* pada jam pembukaan pendaftaran sidang).

* **`Application Server (Web Server & Laravel)`:**
  Menerima permintaan HTTP awal dari pengguna. Web Server (Nginx) meneruskan *request* pendaftaran ke *backend* tanpa langsung mengeksekusi penulisan berat ke basis data secara sinkron.
* **`Messaging Layer (RabbitMQ/Redis & Background Worker)`:**
  Permintaan pendaftaran ditampung ke dalam antrean (*queue*) pesan. *Background Worker* mengambil antrean secara bertahap untuk diproses secara asinkron (*asynchronous processing*), sehingga mencegah *server crash* dan *race condition*.
* **`Database & Storage Layer (Relational DB & Object Storage)`:**
  Data transaksi pendaftaran disimpan ke basis data relasional, sedangkan berkas draf skripsi berukuran besar (25 MB) diunggah langsung ke *Cloud Object Storage* agar komputasi server utama tetap ringan.

![Diagram C&C](../diagram-uts/Diagram%20C&C.drawio.png)

---

### Diagram 3: Diagram UML Modul & Relasi Kelas (*Class Diagram*)

#### Struktur Data dan Hubungan Antar-Entitas
Diagram kelas ini menggambarkan pemodelan data struktural dari basis data relasional subsistem *Assignment & Assessment*:

* **Kelas `Mahasiswa`:** 
  Memuat atribut identitas (`nim`, `nama`, `programStudi`) dan metode `ajukanSidang()`. Berelasi *1-to-0..1* dengan pendaftaran sidang.
* **Kelas `PendaftaranSidang`:** 
  Entitas transaksional yang mencatat rekam pendaftaran (`id_pendaftaran`, `tanggal_daftar`, `status_berkas`) serta metode `validasiBerkas()`.
* **Kelas `BerkasSkripsi`:** 
  Berelasi *1-to-1* dengan pendaftaran sidang untuk merekam metadata berkas digital (`id_berkas`, `file_path`, `ukuran_mb`) dan metode `unggahBerkas()`.
* **Kelas `DosenPenguji`:** 
  Berelasi *0..*-to-*2..3* dengan pendaftaran sidang untuk merekam data dosen penguji (`nidn`, `nama`) serta metode `inputNilai()`.

  ![Diagram UML Modul](../diagram-uts/Diagram%20UML%20Modul.drawio.png)
