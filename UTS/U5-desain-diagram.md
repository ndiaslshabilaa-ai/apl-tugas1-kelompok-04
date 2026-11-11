# U5. Desain Arsitektur dan Diagram

Bagian ini mendokumentasikan tiga prinsip desain perangkat lunak yang diterapkan serta tiga diagram arsitektur utama beserta keterangannya untuk subsistem Layanan Tugas Akhir (*Assignment & Assessment*).

---

## 5.1 Tiga Prinsip Desain yang Diterapkan
1. **Separation of Concerns (SoC):** 
   Memisahkan tanggung jawab fungsional sistem secara tegas ke dalam lapisan yang berbeda—antara antarmuka pengguna (*UI*), pemrosesan logika bisnis akademik, dan manajemen penyimpanan basis data. Hal ini memastikan setiap komponen berfokus pada satu domain spesifik tanpa saling tumpang tindih.
2. **Single Responsibility Principle (SRP):** 
   Setiap modul atau entitas kode dirancang untuk hanya memiliki satu alasan untuk berubah (satu tanggung jawab spesifik). Contohnya, modul pendaftaran terisolasi secara mandiri dari modul penilaian sidang dan modul pengelolaan berkas draf skripsi.
3. **High Cohesion & Low Coupling:** 
   Memastikan elemen-elemen di dalam suatu modul memiliki keterkaitan internal yang sangat erat (*high cohesion*), sementara ketergantungan antar-modul dibuat seminimal mungkin (*low coupling*). Pendekatan ini mencegah perubahan kode di satu modul memicu kerusakan (*bug*) pada modul lainnya.

---

## 5.2 Tiga Diagram Arsitektur Beserta Keterangan

### Diagram 1: Diagram Konteks & Aktor (*Use Case / Context Diagram*)
* **Keterangan:** Diagram ini memetakan batas sistem (*system boundary*) Layanan Tugas Akhir beserta interaksi tiga aktor utama di luar sistem, yaitu Mahasiswa Akhir (pendaftar dan pengunggah draf), Dosen Pembimbing & Penguji (pengelola bimbingan dan penilai ujian), serta Staf Administrasi Akademik (verifikator berkas dan penjadwal).

![Diagram modul](../diagram-uts/Diagramkonteks.drawio.png)
