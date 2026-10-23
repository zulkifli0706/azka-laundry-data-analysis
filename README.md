# Analisis Data Transaksi Azka Laundry

Analisis data transaksi laundry dengan Python (pandas, matplotlib) di Jupyter Notebook: pembersihan data, omzet, pola waktu, layanan terlaris, pelanggan, keterlambatan, dan sisa tagihan.

> **Catatan:** Data adalah **data dummy** yang dihasilkan dari aplikasi web Azka Laundry buatan saya sendiri (azka-laundry). Nama pelanggan, nomor HP, dan seluruh angka transaksi bukan data usaha laundry yang sebenarnya. Proyek ini dibuat untuk latihan analisis data dan portofolio.

**Ringkasan data:** 5.200 nota, 6.236 item layanan, total omzet Rp254.079.500, rata-rata sekitar Rp48.900 per nota.

## Tujuan Analisis

1. Bagaimana tren omzet dari bulan ke bulan?
2. Hari dan jam apa yang paling ramai dan paling sepi?
3. Layanan dan kategori apa yang paling menyumbang pendapatan?
4. Bagaimana pelanggan membayar?
5. Seberapa sering nota terlambat diselesaikan?
6. Seberapa loyal pelanggan, dan seberapa besar ketergantungan pada pelanggan tertentu?
7. Berapa tagihan yang belum tertagih?

## Langkah Pengerjaan

1. **Persiapan:** impor library (pandas, numpy, matplotlib), lalu muat `file_azka.csv`. Kolom `no_hp_pelanggan` dibaca sebagai teks agar angka 0 di depan nomor tidak hilang.
2. **Pemeriksaan data:** lihat struktur dan tipe kolom dengan `df.info()`, lalu hitung jumlah nilai kosong per kolom.
3. **Pembuangan kolom:** buang kolom yang tidak dipakai (`id_transaksi`, `total_masuk`, `tahap_terakhir`, `keterangan_item`, `nama_kasir`) beserta kolom turunan bawaan (`tanggal`, `bulan`, `hari`, `jam`, `sisa_tagihan`) supaya dihitung ulang sendiri.
4. **Pembersihan data:**
   - Ubah 5 kolom tanggal ke format datetime dan `pernah_terlambat` ke boolean.
   - Isi `jumlah_pembayaran` yang kosong dengan 0 dan `metode_pembayaran` yang kosong dengan "belum ada pembayaran". Setelah itu tidak ada nilai kosong tersisa.
5. **Validasi data:**
   - Cek baris duplikat.
   - Cek total tiap nota harus sama dengan jumlah subtotal item-itemnya (selisih lebih dari 1 dianggap tidak cocok).
   - Cek tidak ada `qty` ≤ 0 dan `subtotal` negatif.
6. **Pembuatan fitur:** dari `tanggal_transaksi` diturunkan `tanggal`, `bulan`, `hari` (dalam bahasa Indonesia), dan `jam`. Sisa tagihan dihitung dari `total_nota` dikurangi `total_dibayar`.
7. **Pemisahan tabel:** data dibagi menjadi tiga tabel agar tidak terjadi hitungan ganda:
   - `df_item`: 1 baris = 1 item layanan (dipakai untuk analisis layanan dan kategori).
   - `df_nota`: 1 baris = 1 nota (dipakai untuk omzet, waktu, pembayaran, keterlambatan, dan sisa tagihan).
   - `df_pelanggan`: 1 baris = 1 pelanggan berdasarkan nomor HP, dengan jumlah transaksi dan total belanja. Pelanggan dengan lebih dari 1 transaksi diberi tipe "Repeat", sisanya "Sekali beli".
8. **Analisis dan visualisasi:** 9 grafik (omzet per bulan, nota per hari, nota per jam, top 10 layanan, pendapatan per kategori, metode pembayaran, persen nota terlambat per bulan, komposisi pelanggan, sisa tagihan per status bayar).
9. **Kesimpulan:** insight dan rekomendasi per poin.

## Hasil, Insight, dan Rekomendasi

### 1. Omzet per Bulan
<img width="698" height="555" alt="image" src="https://github.com/user-attachments/assets/e70535e2-d4b9-4357-b73d-f55f799c595d" />

- **Insight:** Omzet naik stabil dari Juni (±Rp48 juta) ke September (±Rp56 juta, puncak). Mei dan Oktober tampak rendah karena periodenya tidak penuh (data Mei mulai 25 Mei, data Oktober belum satu bulan penuh), bukan karena usaha menurun.
- **Rekomendasi:** Pelajari pendorong kenaikan Juni–September (promo, musim, pelanggan baru) lalu ulangi. Bandingkan antar bulan hanya untuk bulan yang penuh.

### 2. Jumlah Nota per Hari
<img width="692" height="610" alt="image" src="https://github.com/user-attachments/assets/8cf534f7-d62f-49c3-9e71-97ac0963a2ab" />

- **Insight:** Sabtu paling ramai (±870 nota), disusul Senin dan Jumat. Selasa dan Kamis paling sepi (±650–670 nota).
- **Rekomendasi:** Tambah tenaga dan kapasitas mesin pada Sabtu, Senin, dan Jumat. Pakai Selasa dan Kamis untuk promo atau pekerjaan non-rutin seperti perawatan mesin.

### 3. Jumlah Nota per Jam
<img width="750" height="572" alt="image" src="https://github.com/user-attachments/assets/c58ea217-1f20-485e-bfd1-583b6de96cc9" />

- **Insight:** Ada dua jam sibuk: pagi pukul 08.00–10.00 (puncak 09.00 dengan 664 nota) dan sore pukul 15.00–17.00 (puncak 16.00 dengan 561 nota). Pukul 12.00–14.00 relatif sepi, dan pukul 07.00 serta 19.00 paling sedikit.
- **Rekomendasi:** Atur jadwal karyawan agar penuh di dua jam sibuk. Gunakan jam sepi siang untuk istirahat bergiliran dan mengerjakan cucian yang menumpuk.

### 4. Top 10 Layanan (Pendapatan)
<img width="1142" height="557" alt="image" src="https://github.com/user-attachments/assets/a00b54da-4d8a-4e23-a964-2a14a896e994" />

- **Insight:** Cuci + Setrika (Reguler) menyumbang Rp106,5 juta (±42% omzet), jauh di atas layanan lain. Sneakers / Casual (Rp32,9 juta) menjadi kedua, dan layanan sepatu lain (kulit, gunung, white shoes) juga masuk 10 besar.
- **Rekomendasi:** Jaga kualitas dan ketepatan waktu layanan utama karena omzet bergantung padanya. Kembangkan layanan sepatu, misalnya paket langganan atau promo antar-jemput.

### 5. Pendapatan per Kategori
<img width="1065" height="562" alt="image" src="https://github.com/user-attachments/assets/54c836b2-52d3-4742-a960-8d9a64e5de86" />

- **Insight:** Cucian Kiloan (Rp139 juta, ±55%) dan Sepatu (Rp59 juta, ±23%) bersama-sama menyumbang ±78% omzet. Sajadah & Perlengkapan Ibadah paling rendah.
- **Rekomendasi:** Fokuskan promosi pada Kiloan dan Sepatu. Untuk kategori kecil, tawarkan sebagai tambahan (bundling) atau evaluasi apakah layak dipertahankan.

### 6. Metode Pembayaran
<img width="656" height="512" alt="image" src="https://github.com/user-attachments/assets/1847c560-a6e3-4efc-960c-8e2b069a9c5f" />

- **Insight:** Tunai paling dominan (67,9%), lalu transfer (23,9%) dan tunai + transfer (7,0%). Sebanyak 1,2% nota belum ada pembayaran sama sekali.
- **Rekomendasi:** Pastikan pencatatan tunai rapi karena porsinya terbesar. Sediakan QRIS atau transfer yang mudah, dan tindak lanjuti nota yang belum dibayar sama sekali.

### 7. Persentase Nota Terlambat per Bulan
<img width="722" height="568" alt="image" src="https://github.com/user-attachments/assets/2b036cc7-744f-4afd-9b53-31e4b8fcb376" />

- **Insight:** Mei–September sekitar 21% nota terlambat (kisaran 20,7–23,8%), tertinggi di Juli. Angka Oktober (13,4%) kemungkinan belum akurat karena banyak nota bulan itu belum jatuh tempo.
- **Rekomendasi:** Keterlambatan 1 dari 5 nota cukup tinggi. Tambah kapasitas di hari dan jam sibuk, beri estimasi selesai yang lebih realistis, dan cari tahu penyebab lonjakan di Juli.

### 8. Komposisi Pelanggan
<img width="597" height="465" alt="image" src="https://github.com/user-attachments/assets/e9c2d5a6-c44d-4477-ac92-bfb964fc7039" />

- **Insight:** 91,4% pelanggan adalah repeat dan hanya 8,6% sekali beli, jadi basis pelanggan sangat loyal. Lima pelanggan teratas menyumbang ±10% omzet, dan pelanggan teratas sudah bertransaksi 184 kali.
- **Rekomendasi:** Buat program loyalitas (poin atau diskon langganan). Beri perhatian khusus pada pelanggan teratas karena kehilangan mereka berdampak besar.

### 9. Sisa Tagihan per Status Bayar
<img width="677" height="656" alt="image" src="https://github.com/user-attachments/assets/0f48b80c-0a25-4753-830c-b43d4f862697" />

- **Insight:** Total sisa tagihan Rp4,78 juta (±1,9% omzet): Rp3,46 juta berstatus belum bayar dan Rp1,32 juta berstatus DP. Nota sudah bayar tidak punya sisa tagihan, sesuai yang diharapkan.
- **Rekomendasi:** Kirim pengingat rutin (WhatsApp) untuk nota belum bayar dan DP. Pertimbangkan aturan pengambilan cucian setelah pelunasan atau batas waktu pelunasan.

## Cara Menjalankan

1. Clone repositori:
   ```bash
   git clone https://github.com/zulkifli0706/azka-laundry-data-analysis.git
   cd azka-laundry-data-analysis
   ```
2. Pasang library:
   ```bash
   pip install pandas numpy matplotlib jupyter
   ```
3. Buka notebook:
   ```bash
   jupyter notebook azka_laundry_analysis.ipynb
   ```
4. Pastikan `file_azka.csv` satu folder dengan notebook, lalu pilih **Run > Run All Cells**.

## Catatan

Karena data berupa data dummy, temuan di atas menggambarkan pola dari data simulasi dan tidak mewakili kondisi usaha laundry yang nyata.
