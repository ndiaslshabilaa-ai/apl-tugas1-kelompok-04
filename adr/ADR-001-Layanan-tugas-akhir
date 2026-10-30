# ADR-001: Penerapan Role-Based Access Control (RBAC) dan Audit Trail

- **Status:** Diterima 
- **Tanggal:** 30-10-2026
- **Pengambil keputusan:** B.Nadia Salsabila 

## Context
Layanan Tugas Akhir mengelola berbagai data akademik yang bersifat penting dan rahasia, seperti pengajuan judul skripsi, dokumen draf tugas akhir, catatan bimbingan (logbook), serta hasil penilaian sidang. Setiap pengguna memiliki hak akses yang berbeda sesuai dengan perannya. Apabila tidak terdapat pembatasan akses yang jelas, sistem berisiko mengalami kebocoran dokumen, perubahan nilai tanpa izin, dan manipulasi riwayat aktivitas akademik.

## Decision
Kami akan menerapkan mekanisme Role-Based Access Control (RBAC) untuk mengatur hak akses berdasarkan peran pengguna. Selain itu, sistem akan menggunakan mekanisme Audit Trail untuk mencatat seluruh aktivitas penting secara otomatis, seperti pengajuan judul, persetujuan dosen, perubahan dokumen, dan penginputan nilai sidang.

Hak akses akan dibedakan berdasarkan peran mahasiswa, dosen pembimbing, dosen penguji, Ketua Program Studi, staf administrasi, dan administrator sistem. Dengan demikian, setiap pengguna hanya dapat mengakses fitur dan data sesuai dengan kewenangannya.
## Consequences
**Positif:** Keamanan dan kerahasiaan dokumen tugas akhir lebih terjamin. Sistem dapat mencegah akses oleh pihak yang tidak berwenang serta menyediakan rekam jejak aktivitas yang dapat digunakan untuk pemeriksaan dan audit akademik.
**Negatif:** Sistem membutuhkan konfigurasi hak akses yang lebih terperinci, tambahan penyimpanan untuk mencatat aktivitas pengguna, serta pengujian keamanan secara berkala.

## Compliance
Penerapan RBAC dan Audit Trail akan diuji melalui pengujian hak akses berdasarkan peran pengguna (Role-Based Access Testing) dan pemeriksaan catatan aktivitas sistem. Evaluasi dilakukan secara berkala untuk memastikan keamanan dan integritas data akademik tetap terjaga.
