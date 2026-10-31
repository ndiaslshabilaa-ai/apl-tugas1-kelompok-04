## ADR-002: Penerapan Asynchronous Message Queue untuk Proses Penjadwalan Sidang
- Status: Diterima
- Tanggal: 24-10-2026
- Pengambil keputusan: Artika Milad Arhidayah

## Context
Proses pendaftaran dan penjadwalan sidang melibatkan validasi kuota dosen penguji, pengecekan ketersediaan ruangan, serta pengiriman notifikasi massal secara serentak. Jika diproses secara sinkron (*synchronous*), sistem berpotensi mengalami keterlambatan respons (*latency*) tinggi atau *request timeout*. Masalah ini berhubungan erat dengan kebutuhan kuantitatif pada kode ASR: **A4-1** (target respons < 3 detik saat lonjakan 500 pengguna simultan) dan **A4-2** (keandalan pemrosesan transaksi).

## Decision
Kami akan menerapkan antrean pesan asinkron (*Asynchronous Message Queue*) untuk menangani pemrosesan pendaftaran dan pengiriman notifikasi secara bertahap melalui pemrosesan latar belakang (*background worker*).

## Consequences
- Dampak Positif: Sistem tahan terhadap lonjakan beban transaksi bersamaan, menjaga waktu tanggap antarmuka tetap cepat (< 3 detik), dan mencegah kegagalan koneksi di sisi pengguna.
- Dampak Negatif & Trade-off: Kompleksitas arsitektur bertambah karena memerlukan komponen infrastruktur baru serta mekanisme pemantauan khusus terhadap status antrean (*queue monitoring*).

## Compliance
Keputusan ini dipatuhi dengan melakukan pengujian beban (*load testing*) menggunakan JMeter/k6 pada alur pendaftaran sidang massal serta pemantauan (*monitoring*) antrean pesan sebelum sistem diunggah ke lingkungan produksi kampus.
