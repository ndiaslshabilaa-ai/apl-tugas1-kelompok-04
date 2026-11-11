# U4. Pola dan Gaya Arsitektur

Bagian ini mendokumentasikan perbedaan mendasar antara gaya arsitektur dan pola arsitektur, serta merinci dua pola dari kategori berbeda yang diterapkan pada perancangan subsistem Layanan Tugas Akhir (*Assignment & Assessment*).

---

## 1. Perbedaan Gaya Arsitektur (*Architectural Style*) dan Pola Arsitektur (*Architectural Pattern*)
* **Gaya Arsitektur (*Architectural Style*):** Merupakan bentuk atau kerangka pengorganisasian tingkat tinggi dari sebuah sistem secara keseluruhan yang mendefinisikan bentuk topologi globalnya (contoh: gaya berlapis/*layered style*, gaya klien-peladen/*client-server style*). Gaya memberikan batasan umum pada bentuk sistem.
* **Pola Arsitektur (*Architectural Pattern*):** Merupakan solusi spesifik, teruji, dan dapat berulang (*reusable solution*) untuk menyelesaikan masalah desain tertentu yang terjadi dalam konteks batasan gaya arsitektur tersebut (contoh: penerapan pola *Broker* untuk antrean pesan atau pola *MVC* untuk pemisahan antarmuka).

---

## 2. Penerapan Dua Pola Arsitektur dari Kategori Berbeda

### Pola 1: Layered Architecture (Kategori: Structural Patterns)
* **Alasan Penggunaan:** 
  Diterapkan untuk memisahkan tanggung jawab fungsional sistem Layanan Tugas Akhir secara tegas ke dalam lapisan-lapisan logis: Lapisan Presentasi (*UI*), Lapisan Logika Bisnis (*Business Logic*), dan Lapisan Akses Data (*Data Access Layer*).
* **Kelebihan:**
  * Mempermudah pemeliharaan (*maintainability*) dan pengujian unit (*unit testing*) secara terisolasi pada masing-masing lapisan.
  * Mendukung pembagian kerja kelompok pengembang secara modular tanpa saling mengganggu kode di lapisan lain.
* **Kekurangan:**
  * Berpotensi menimbulkan penundaan waktu tanggap (*latency*) jika alur pemrosesan harus melewati terlalu banyak lapisan secara berurutan (*layers skipping risk*).

---

### Pola 2: Publish-Subscribe / Message Broker Pattern (Kategori: Distributed / Messaging Patterns)
* **Alasan Penggunaan:** 
  Diterapkan untuk mengatasi masalah utama berupa lonjakan trafik pendaftaran sidang secara serentak (*traffic spike*) serta mencegah terjadinya *race condition* dan *server crash*.
* **Kelebihan:**
  * Menjaga ketersediaan sistem (*high availability*) dan memastikan seluruh permintaan pendaftaran mahasiswa tertampung dengan aman tanpa ada data yang hilang.
  * Memisahkan proses penerimaan permintaan pengguna dari proses eksekusi berat di basis data (*asynchronous decoupling*).
* **Kekurangan:**
  * Menambah kompleksitas arsitektur sistem secara keseluruhan, sehingga membutuhkan pemantauan infrastruktur tambahan (*queue monitoring*) dan penanganan kegagalan pesan (*dead-letter queue*).
