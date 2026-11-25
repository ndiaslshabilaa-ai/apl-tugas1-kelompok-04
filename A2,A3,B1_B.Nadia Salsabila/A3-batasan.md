# A3. Batasan Sistem


**Penanggung Jawab:** [B.Nadia Salsabila]

Batasan sistem pada Layanan Tugas Akhir dalam subsistem *Assignment & Assessment* ditetapkan untuk memastikan pengembangan dan pengoperasian sistem sesuai dengan kebutuhan akademik Universitas Muslim Indonesia (UMI). Batasan ini dikelompokkan ke dalam tiga kategori utama, yaitu teknologi, bisnis, dan operasional, beserta dampaknya terhadap perancangan arsitektur perangkat lunak.

## 1. Batasan Teknologi (*Technology Constraints*)

- **Integrasi dengan Sistem Akademik:** Layanan Tugas Akhir perlu terhubung dengan sistem akademik yang telah digunakan universitas, khususnya untuk memperoleh dan memvalidasi data mahasiswa serta status akademiknya tanpa mengganggu sistem yang sudah berjalan.
- **Pengelolaan Dokumen Digital:** Sistem dibatasi pada pengelolaan dokumen tugas akhir dalam format digital, seperti dokumen pengajuan judul, proposal, laporan tugas akhir, dan dokumen persyaratan seminar atau sidang. Pengelolaan dokumen harus memperhatikan kapasitas penyimpanan dan keamanan data.

### Dampak pada Arsitektur:

Arsitektur sistem perlu menyediakan mekanisme integrasi dengan sistem akademik melalui API atau layanan integrasi yang sesuai. Selain itu, diperlukan pengelolaan penyimpanan dokumen secara terstruktur, pembatasan akses berdasarkan hak pengguna, serta mekanisme pencadangan data untuk menjaga keamanan dan ketersediaan dokumen tugas akhir.

## 2. Batasan Bisnis (*Business Constraints*)

- **Kepatuhan terhadap Aturan Akademik:** Seluruh proses layanan tugas akhir, mulai dari pengajuan judul, penetapan dosen pembimbing, proses bimbingan, seminar atau sidang, hingga penilaian, harus mengikuti ketentuan akademik yang berlaku di UMI.
- **Penyesuaian Kalender Akademik:** Pelaksanaan layanan tugas akhir harus menyesuaikan jadwal akademik dan ketentuan waktu yang ditetapkan program studi, termasuk jadwal seminar atau sidang serta batas waktu pengumpulan nilai.
- **Kewenangan dalam Proses Akademik:** Sistem tidak dapat mengambil keputusan akademik secara otomatis tanpa persetujuan pihak yang berwenang. Persetujuan judul, penetapan pembimbing, kelayakan seminar atau sidang, serta penilaian tetap mengikuti kewenangan dosen dan pihak program studi.

### Dampak pada Arsitektur:

Sistem perlu menerapkan aturan bisnis (*business rules*) yang sesuai dengan prosedur akademik. Setiap proses harus memiliki alur persetujuan dan hak akses yang jelas. Selain itu, sistem dirancang secara modular agar perubahan aturan akademik, jadwal, maupun prosedur layanan dapat disesuaikan tanpa mengubah keseluruhan sistem.

## 3. Batasan Operasional (*Operational Constraints*)

- **Keterlibatan Pengguna Sesuai Peran:** Sistem digunakan oleh mahasiswa, dosen pembimbing, dosen penguji, staf administrasi akademik, dan pihak program studi. Setiap pengguna hanya dapat mengakses fitur dan data sesuai kewenangan masing-masing.
- **Ketersediaan Dukungan Teknis:** Pemeliharaan dan penanganan kendala sistem bergantung pada ketersediaan tim pengelola atau tenaga teknis kampus. Oleh karena itu, sistem perlu dirancang agar mudah dipantau dan dipelihara.
- **Lonjakan Aktivitas pada Periode Tertentu:** Aktivitas pengguna dapat meningkat pada masa pengajuan judul, periode bimbingan, pendaftaran seminar atau sidang, serta pengumpulan nilai. Sistem harus mampu menangani aktivitas tersebut dengan baik agar pelayanan tetap berjalan.

### Dampak pada Arsitektur:

Sistem perlu menerapkan autentikasi dan pengaturan hak akses berdasarkan peran (*Role-Based Access Control*), serta menyediakan pencatatan aktivitas (*logging*) untuk membantu pemantauan dan penelusuran kendala. Selain itu, arsitektur harus memperhatikan kinerja dan kestabilan sistem ketika terjadi peningkatan jumlah pengguna, terutama pada periode akademik yang padat.

