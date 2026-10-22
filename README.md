Analisis Data Transaksi Azka Laundry

Analisis data transaksi laundry dengan Python (pandas, matplotlib) di Jupyter Notebook: pembersihan data, omzet, pola waktu, layanan terlaris, pelanggan, keterlambatan, dan sisa tagihan.

Catatan: Data dalam proyek ini adalah data dummy yang dihasilkan dari aplikasi web Azka Laundry buatan saya sendiri (azka-laundry). Nama pelanggan, nomor HP, dan seluruh angka transaksi bukan data usaha laundry yang sebenarnya. Proyek ini dibuat untuk latihan analisis data dan portofolio.

Ringkasan data: 5.200 nota, 6.236 item layanan, total omzet Rp254.079.500, rata-rata sekitar Rp48.900 per nota.

Hasil dan insight
1. Omzet per Bulan
<img width="698" height="555" alt="image" src="https://github.com/user-attachments/assets/e70535e2-d4b9-4357-b73d-f55f799c595d" />

Omzet naik stabil dari Juni (sekitar Rp48 juta) ke September (sekitar Rp56 juta), yang menjadi puncaknya.
Mei dan Oktober tampak rendah karena periodenya tidak penuh (data Mei mulai 25 Mei, data Oktober belum satu bulan penuh), jadi bukan tanda penurunan usaha.
2. Jumlah Nota per Hari
<img width="692" height="610" alt="image" src="https://github.com/user-attachments/assets/8cf534f7-d62f-49c3-9e71-97ac0963a2ab" />

Sabtu paling ramai (sekitar 870 nota), disusul Senin dan Jumat.
Selasa dan Kamis paling sepi (sekitar 650–670 nota), cocok untuk promo atau pekerjaan non-rutin.
3. Jumlah Nota per Jam
<img width="750" height="572" alt="image" src="https://github.com/user-attachments/assets/c58ea217-1f20-485e-bfd1-583b6de96cc9" />

Ada dua jam sibuk: pagi pukul 08.00–10.00 (puncak pukul 09.00 dengan 664 nota) dan sore pukul 15.00–17.00 (puncak pukul 16.00 dengan 561 nota).
Pukul 12.00–14.00 relatif sepi, dan pukul 07.00 serta 19.00 paling sedikit.
4. Top 10 Layanan (Pendapatan)
<img width="1142" height="557" alt="image" src="https://github.com/user-attachments/assets/a00b54da-4d8a-4e23-a964-2a14a896e994" />

Cuci + Setrika (Reguler) menyumbang Rp106,5 juta, sekitar 42% omzet, dan jauh di atas layanan lain.
Sneakers / Casual (Rp32,9 juta) menjadi layanan terbesar kedua. Layanan sepatu lain (kulit, gunung, white shoes) juga masuk 10 besar.
5. Pendapatan per Kategori
<img width="1065" height="562" alt="image" src="https://github.com/user-attachments/assets/54c836b2-52d3-4742-a960-8d9a64e5de86" />

Cucian Kiloan (Rp139 juta, sekitar 55%) dan Sepatu (Rp59 juta, sekitar 23%) bersama-sama menyumbang sekitar 78% omzet.
Kategori lain jauh lebih kecil, dan Sajadah & Perlengkapan Ibadah paling rendah.
6. Metode Pembayaran
<img width="656" height="512" alt="image" src="https://github.com/user-attachments/assets/1847c560-a6e3-4efc-960c-8e2b069a9c5f" />

Tunai paling dominan (67,9%), lalu transfer (23,9%) dan gabungan tunai + transfer (7,0%).
Sebanyak 1,2% nota belum ada pembayaran sama sekali.
7. Persentase Nota Terlambat per Bulan
<img width="722" height="568" alt="image" src="https://github.com/user-attachments/assets/2b036cc7-744f-4afd-9b53-31e4b8fcb376" />

Dari Mei sampai September, sekitar 21% nota terlambat (kisaran 20,7–23,8%), tertinggi di Juli.
Angka Oktober (13,4%) kemungkinan belum akurat karena banyak nota bulan itu belum sampai jatuh tempo.
8. Komposisi Pelanggan
<img width="597" height="465" alt="image" src="https://github.com/user-attachments/assets/e9c2d5a6-c44d-4477-ac92-bfb964fc7039" />

Sebanyak 91,4% pelanggan adalah pelanggan repeat dan hanya 8,6% yang sekali beli, jadi basis pelanggan sangat loyal.
Lima pelanggan teratas menyumbang sekitar 10% omzet, dan pelanggan teratas sudah bertransaksi 184 kali.
9. Sisa Tagihan per Status Bayar
<img width="677" height="656" alt="image" src="https://github.com/user-attachments/assets/0f48b80c-0a25-4753-830c-b43d4f862697" />

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
