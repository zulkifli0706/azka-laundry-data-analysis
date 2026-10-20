# azka-laundry-data-analysis
Analisis data transaksi laundry dengan Python (pandas, matplotlib): pembersihan data, analisis frekuensi, omzet, dan keterlambatan, serta visualisasi.
# Analisis Data Transaksi Azka Laundry

Proyek analisis data dengan Python untuk usaha laundry. Python mengambil data dari MySQL, membersihkannya, menghitung metrik bisnis, lalu membuat grafik.

<img width="1451" height="545" alt="image" src="https://github.com/user-attachments/assets/137b9fc2-2bcf-4ee4-bfea-525404ff76b6" />

<img width="1531" height="842" alt="image" src="https://github.com/user-attachments/assets/ef86a5f6-3169-4615-bfd3-fed13e094e3a" />


## Masalah bisnis

Pemilik laundry belum punya ringkasan yang menjawab lima pertanyaan ini:

1. Layanan dan kategori apa yang paling sering dipesan?
2. Berapa pendapatan yang diterima dan berapa tagihan yang belum lunas?
3. Berapa persen nota yang selesai melewati estimasi?
4. Layanan apa yang paling sering terlambat?
5. Hari apa yang paling sibuk?

## Data

Sumber: database MySQL dari aplikasi kasir laundry. Data diambil per 20 Oktober 2026.

| Tabel | Isi |
|---|---|
| transaksi | nota, pelanggan, total harga, status bayar, estimasi |
| status_cucian | status pengerjaan dan waktu pembaruan |
| detail_transaksi | item per nota, jumlah, subtotal |
| detail_barang | nama item dan satuan |
| kategori_barang | kategori layanan |

Ukuran data: 124 nota, 178 baris detail, 23 jenis item, 8 kategori.

## Proses analisis

**1. Data collecting (`collect.py`)**

Python menjalankan query SQL dengan JOIN antar tabel. Data bisa difilter per periode: hari ini, minggu ini, bulan ini, tahun ini, tahun lalu, semua waktu, atau tanggal bebas.

**2. Data processing (`process.py`)**

- Ubah tipe angka dan tanggal.
- Buang baris tanpa tanggal.
- Isi nama item yang kosong dari kolom keterangan.
- Isi kategori yang kosong.
- Buat rekap per item: frekuensi, jumlah nota, total jumlah, omzet, dan persentase. Proses ini menyusutkan 178 baris detail menjadi 23 item.
- Buat rekap per kategori: 23 item menjadi 8 kategori.
- Tandai nota terlambat dari tanggal estimasi. Aturan: <tulis aturan dari process.py>.
- Hitung keterlambatan per item.
- Hitung tren pendapatan dan pola nota per hari.

**3. Data visualization (`visualize.py`)**

matplotlib membuat grafik, termasuk jumlah nota per hari. Batang hari tersibuk diberi warna lebih gelap.

**4. Insight otomatis**

Kalimat ringkasan dibuat dari hasil hitungan. Contohnya layanan terlaris dan jumlah tagihan yang belum terbayar.

## Metrik yang dihitung

- Jumlah nota dan jumlah pemesanan item per periode
- Pendapatan diterima dan tagihan belum terbayar
- Layanan dan kategori paling sering dipesan
- Persentase nota yang melewati estimasi
- Keterlambatan per layanan
- Tren pendapatan dan pola nota per hari

## Temuan (data per 20 Oktober 2026)

- Pendapatan diterima Rp4.340.700.
- Tagihan belum terbayar Rp756.000.
- Sneakers / Casual (Canvas, Mesh) paling sering dicuci.
- Cucian Kiloan menjadi kategori yang paling banyak dipesan.
- 26 dari 124 nota (21%) melewati estimasi.

Angka ini adalah potret data pada tanggal di atas. Hasilnya berubah mengikuti data terbaru di database.

## Keterbatasan

- Data hanya 124 nota. Tren jangka panjang belum bisa disimpulkan.
- Analisis bersifat deskriptif. Belum ada prediksi atau uji statistik.
- <tambahkan catatan jika ada nota tanpa estimasi atau data kosong>

## Rencana pengembangan

- Prediksi jumlah nota per minggu
- Analisis pelanggan yang memesan berulang
- Notebook Jupyter untuk eksplorasi data

## Teknologi

Python 3.10, pandas, matplotlib, PyMySQL, MySQL

## Struktur folder

```
azka-laundry-data-analysis/
├── README.md
├── python/
│   ├── collect.py
│   ├── process.py
│   ├── visualize.py
│   ├── insight_cli.py
│   ├── demo_data.py
│   └── requirements.txt
└── images/
```

## Cara menjalankan

**Mode demo (tanpa database)**

```
pip install -r python/requirements.txt
python python/insight_cli.py --periode semua --demo
```

**Dengan database**

1. Import database MySQL.
2. Buat file `.env` di folder utama dengan isi berikut. Sesuaikan nilainya.

```
DB_HOST=127.0.0.1
DB_USER=root
DB_PASS=
DB_NAME=azka_laundry
DB_CHAR=utf8mb4
```

3. Jalankan:

```
pip install -r python/requirements.txt
python python/insight_cli.py --periode semua
```

Pilihan periode: `hari_ini`, `minggu_ini`, `bulan_ini`, `tahun_ini`, `tahun_lalu`, `semua`, atau `custom` dengan `--mulai` dan `--akhir`.

Hasilnya berupa JSON di terminal. Aplikasi web PHP menampilkan hasil yang sama di halaman Insight.

## Kontak

[LinkedIn]www.linkedin.comzulkifli-h-a81387249 | 123kifri622@gmail.com
