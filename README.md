Analisis Data Transaksi Azka Laundry

Analisis data transaksi laundry dengan Python (pandas, matplotlib) di Jupyter Notebook: pembersihan data, omzet, pola waktu, layanan terlaris, pelanggan, keterlambatan, dan sisa tagihan.

Catatan: Data dalam proyek ini adalah data dummy yang dihasilkan dari aplikasi web Azka Laundry buatan saya sendiri (azka-laundry). Nama pelanggan, nomor HP, dan seluruh angka transaksi bukan data usaha laundry yang sebenarnya. Proyek ini dibuat untuk latihan analisis data dan portofolio.

Ringkasan data: 5.200 nota, 6.236 item layanan, total omzet Rp254.079.500, rata-rata sekitar Rp48.900 per nota.

Hasil dan insight
1. Omzet per Bulan
<img src="images/01_omzet_per_bulan.png" width="600" alt="Omzet per Bulan">
Omzet naik stabil dari Juni (sekitar Rp48 juta) ke September (sekitar Rp56 juta), yang menjadi puncaknya.
Mei dan Oktober tampak rendah karena periodenya tidak penuh (data Mei mulai 25 Mei, data Oktober belum satu bulan penuh), jadi bukan tanda penurunan usaha.
2. Jumlah Nota per Hari
<img src="images/02_nota_per_hari.png" width="600" alt="Jumlah Nota per Hari">
Sabtu paling ramai (sekitar 870 nota), disusul Senin dan Jumat.
Selasa dan Kamis paling sepi (sekitar 650–670 nota), cocok untuk promo atau pekerjaan non-rutin.
3. Jumlah Nota per Jam
<img src="images/03_nota_per_jam.png" width="600" alt="Jumlah Nota per Jam">
Ada dua jam sibuk: pagi pukul 08.00–10.00 (puncak pukul 09.00 dengan 664 nota) dan sore pukul 15.00–17.00 (puncak pukul 16.00 dengan 561 nota).
Pukul 12.00–14.00 relatif sepi, dan pukul 07.00 serta 19.00 paling sedikit.
4. Top 10 Layanan (Pendapatan)
<img src="images/04_top10_layanan.png" width="600" alt="Top 10 Layanan">
Cuci + Setrika (Reguler) menyumbang Rp106,5 juta, sekitar 42% omzet, dan jauh di atas layanan lain.
Sneakers / Casual (Rp32,9 juta) menjadi layanan terbesar kedua. Layanan sepatu lain (kulit, gunung, white shoes) juga masuk 10 besar.
5. Pendapatan per Kategori
<img src="images/05_pendapatan_per_kategori.png" width="600" alt="Pendapatan per Kategori">
Cucian Kiloan (Rp139 juta, sekitar 55%) dan Sepatu (Rp59 juta, sekitar 23%) bersama-sama menyumbang sekitar 78% omzet.
Kategori lain jauh lebih kecil, dan Sajadah & Perlengkapan Ibadah paling rendah.
6. Metode Pembayaran
<img src="images/06_metode_pembayaran.png" width="450" alt="Metode Pembayaran">
Tunai paling dominan (67,9%), lalu transfer (23,9%) dan gabungan tunai + transfer (7,0%).
Sebanyak 1,2% nota belum ada pembayaran sama sekali.
7. Persentase Nota Terlambat per Bulan
<img src="images/07_nota_terlambat_per_bulan.png" width="600" alt="Nota Terlambat per Bulan">
Dari Mei sampai September, sekitar 21% nota terlambat (kisaran 20,7–23,8%), tertinggi di Juli.
Angka Oktober (13,4%) kemungkinan belum akurat karena banyak nota bulan itu belum sampai jatuh tempo.
8. Komposisi Pelanggan
<img src="images/08_komposisi_pelanggan.png" width="450" alt="Komposisi Pelanggan">
Sebanyak 91,4% pelanggan adalah pelanggan repeat dan hanya 8,6% yang sekali beli, jadi basis pelanggan sangat loyal.
Lima pelanggan teratas menyumbang sekitar 10% omzet, dan pelanggan teratas sudah bertransaksi 184 kali.
9. Sisa Tagihan per Status Bayar
<img src="images/09_sisa_tagihan.png" width="600" alt="Sisa Tagihan per Status Bayar">
Total sisa tagihan Rp4,78 juta (sekitar 1,9% omzet): Rp3,46 juta berstatus belum bayar dan Rp1,32 juta berstatus DP.
Nota berstatus sudah bayar tidak punya sisa tagihan, sesuai yang diharapkan.
Tata cara menjalankan
Clone repositori.
git clone https://github.com/zulkifli0706/azka-laundry-data-analysis.git
cd azka-laundry-data-analysis
Pasang library.
pip install pandas numpy matplotlib jupyter
Buka notebook.
jupyter notebook azka_laundry_analysis.ipynb
Pastikan file_azka.csv satu folder dengan notebook, lalu jalankan semua sel dari atas ke bawah (Run All).
Catatan

Karena data berupa data dummy, temuan di atas menggambarkan pola dari data simulasi dan tidak mewakili kondisi usaha laundry yang nyata.
