# B5. Analisis Trade-off

<!-- Penanggung jawab: [Artika Milad Arhidayah] -->

Berikut adalah analisis dua pasang karakteristik arsitektur yang saling memengaruhi pada Layanan Tugas Akhir (subsistem *Assignment & Assessment*), beserta keputusan prioritas dan alasannya:

## 1. Pasang Trade-off 1: Keamanan (Security) vs Kinerja (Performance Efficiency)
* **Dampak Saling Memengaruhi:**
  Penerapan autentikasi JWT berlapis, verifikasi tanda tangan digital pada draf skripsi, serta enkripsi data nilai sidang meningkatkan tingkat keamanan sistem secara signifikan. Namun, proses enkripsi dan dekripsi berkas serta pemeriksaan token akses secara terus-menerus menambah beban komputasi dan memperlambat waktu respons sistem (*latency*).
* **Keputusan Prioritas & Alasan:**
  * **Keputusan:** *Security* didahulukan untuk modul yang menangani data nilai sidang dan lembar pengesahan, sedangkan *Performance Efficiency* didahulukan untuk modul antarmuka pencatatan logbook harian dan pengajuan judul.
  * *Alasan:* Pemalsuan nilai atau kebocoran dokumen skripsi memiliki dampak cacat hukum akademik yang fatal, sehingga keamanan data mutlak diutamakan. Sebaliknya, pencatatan logbook harian membutuhkan responsivitas yang cepat dan ringan agar kenyamanan interaksi mahasiswa tetap terjaga.

---

## 2. Pasang Trade-off 2: Fleksibilitas (Flexibility) vs Kemudahan Perawatan (Maintainability)
* **Dampak Saling Memengaruhi:**
  Menyediakan opsi penyesuaian alur persetujuan judul yang berbeda-beda untuk tiap program studi meningkatkan fleksibilitas layanan. Namun, hal tersebut menambah kompleksitas percabangan kode logika (*conditional branching*) yang akan memperrumit pemeliharaan dan pembaruan sistem (*maintainability*) ke depannya.
* **Keputusan Prioritas & Alasan:**
  * **Keputusan:** *Maintainability* didahulukan dengan menetapkan satu alur standar *Tugas Akhir* yang berlaku universal di tingkat universitas, dengan opsi kustomisasi minimal yang dibatasi hanya pada parameter tertentu.
  * *Alasan:* Mengengingat
