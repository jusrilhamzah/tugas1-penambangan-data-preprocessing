# Tugas 1 Penambangan Data: Data Preprocessing

Repository ini berisi hasil pengerjaan **Tugas 1 Mata Kuliah Penambangan Data** (Program Studi Sistem Informasi, Universitas Internasional Semen Indonesia) yang berfokus pada identifikasi dan penanganan berbagai permasalahan kualitas data menggunakan tahapan **Data Preprocessing** dengan pendekatan **Input – Proses – Output**.

## Informasi Studi Kasus & Partner
* **Pembuat Kasus (Partner):** Marry Desy Chatrin Ora (NIM: `3022410031`)
* **Topik Kasus:** Analisis Transaksi dan Kinerja Pelayanan Kafe *"Kopi Nusantara"* (3 Outlet di Surabaya: Pusat, Timur, dan Barat)
* **Periode Data:** 1 Januari – 28 Februari 2026

---

## Struktur File Repository

Seluruh berkas yang dipersyaratkan dikumpulkan dalam direktori utama repository ini:

* `Laporan_Data_Preprocessing.pdf` — Dokumen laporan lengkap yang menjelaskan alur kerja **Input – Proses – Output**, tabel statistik deskriptif, dan analisis setiap tahapan preprocessing.
* `Data_Preprocessing_Kopi_Nusantara.ipynb` — File program Jupyter Notebook berisi kode eksekusi Python dari pemuatan data mentah hingga dataset siap pemodelan.
* `Marry Desy Chatrin Ora_3022410031.txt` — Dokumen deskripsi kasus, latar belakang masalah, dan kamus variabel dari partner.
* **Dataset Mentah (8 File CSV):**
  1. `dataset_awal.csv` — Data utama transaksi pelanggan (248 baris, 12 variabel).
  2. `data_pelanggan.csv` — Profil keanggotaan pelanggan (125 baris, 10 variabel).
  3. `transaksi_januari.csv` — Pecahan transaksi bulan Januari 2026 (124 baris, 12 variabel).
  4. `transaksi_februari.csv` — Pecahan transaksi bulan Februari 2026 (124 baris, 12 variabel).
  5. `transaksi_harian.csv` — Rekap operasional harian per outlet (181 baris, 11 variabel).
  6. `transaksi_mingguan.csv` — Rekap mingguan per outlet (27 baris, 13 variabel).
  7. `pelayanan_detik.csv` — Catatan durasi pelayanan dalam satuan detik (124 baris, 10 variabel).
  8. `pelayanan_menit.csv` — Catatan durasi pelayanan dalam satuan menit (124 baris, 10 variabel).

---

## Ringkasan Tahapan Data Preprocessing

1. **Eksplorasi & Verifikasi Pecahan Dataset:** Memeriksa struktur 8 file CSV dan memverifikasi bahwa gabungan `transaksi_januari.csv` dan `transaksi_februari.csv` identik dengan `dataset_awal.csv` (248 baris).
2. **Data Cleaning (Duplikat, Noise, & Outlier):**
   * Menghapus baris duplikat identik (misalnya `dataset_awal.csv` berkurang dari 248 menjadi 240 baris unik).
   * Membersihkan *noise* teks/simbol pada kolom numerik (seperti `"dua"`, `"30 th"`, dan `"Rp 21.000"`).
   * Mengisolasi nilai tidak logis dan *outlier* ekstrem (usia negatif/di atas 85 tahun, rating di luar skala 1–5, dan kesalahan ketik nominal jutaan rupiah) menjadi `NaN`.
   * Melakukan rekonsiliasi silang antar tabel serta imputasi *missing value* menggunakan **statistik deskriptif** (**Median** untuk variabel numerik dan **Modus** untuk variabel kategorik).
3. **Konsistensi Data & Penyeragaman Satuan:** Menyeragamkan variasi penulisan kategori (`outlet`, `jenis_kelamin`, `kategori_menu`, `metode_pembayaran`), mengonversi berbagai format tanggal menjadi standar ISO `YYYY-MM-DD`, serta mengonversi satuan waktu pada `pelayanan_detik.csv` ke satuan **menit**.
4. **Data Integration:** Menggabungkan tabel transaksi utama dengan profil pelanggan (`id_pelanggan`), detail waktu pelayanan (`id_transaksi`), dan rekap cuaca/pendapatan harian (`tanggal_transaksi` & `outlet`) menghasilkan tabel terpadu berdimensi **240 baris × 27 atribut**.
5. **Data Transformation & Data Reduction:** Menerapkan diskretisasi (*binning*), *Ordinal Encoding* pada `status_member`, *One-Hot Encoding* pada fitur kategorik nominal, penskalaan **Min-Max** dan **Z-Score**, serta seleksi fitur hingga menghasilkan dataset bersih berdimensi **240 baris × 35 fitur** dengan **0 missing value**.

---

## Teknologi yang Digunakan
* **Bahasa Pemrograman:** Python 3
* **Library:** `pandas`, `numpy`, `scikit-learn`
* **Environment:** Jupyter Notebook
