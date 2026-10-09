# Feature Engineering

Dokumentasi ini berisi penjelasan lengkap mengenai alur kerja *Feature Engineering* menggunakan algoritma **TF-IDF (Term Frequency–Inverse Document Frequency)** pada dataset artikel Wikipedia yang telah di-*preprocess* sebelumnya.

---

## 👥 Anggota Kelompok
- **Najla Zahira** (25031554041)
- **Moza Athaillah Azzahra** (25031554185)

---

## 📌 Ringkasan Alur Kerja

Proses *Feature Engineering* dilakukan dalam **11 tahapan terstruktur**:

1. **Step 1 — Load dan Validasi Dataset:** Memuat dataset `hasil_preprocessed.csv` (100 dokumen x 4 kolom) dan memastikan tidak ada nilai kosong (*null*).
2. **Step 2 — Menentukan Teks sebagai Input:** Mengambil kolom `teks_clean` sebagai *corpus* utama, serta memisahkan kolom metadata (`no`, `judul`, `topik`).
3. **Step 3 — Ekstraksi Fitur dengan TF-IDF (Baseline):** Ekstraksi awal menggunakan kombinasi Unigram & Bigram (`ngram_range=(1,2)`), `min_df=2`, dan `max_df=0.85`.
4. **Step 4 — Inspeksi Fitur dan Bobot TF-IDF:** Memeriksa 10 fitur dengan bobot terkuat pada sampel dokumen pertama (`Algoritma bias`).
5. **Step 5 — Refinement Fitur TF-IDF:** Melakukan penyaringan lebih ketat (`min_df=3`, `max_df=0.70`, `max_features=1500`) untuk mengontrol dimensi dan mengurangi *noise*.
6. **Step 6 — Perbandingan TF-IDF Baseline dan Refined:** Menganalisis efisiensi reduksi dimensi dari baseline ke *refined*.
7. **Step 7 — Menetapkan Matriks TF-IDF Final:** Menetapkan matriks *refined* (100 x 1.500) sebagai representasi numerik akhir dokumen.
8. **Step 8 — Analisis Fitur Dominan pada Corpus:** Menghitung total bobot akumulatif TF-IDF di seluruh dokumen untuk mengidentifikasi term paling dominan.
9. **Step 9 — Integrasi Metadata dan Fitur TF-IDF:** Menggabungkan kembali matriks fitur TF-IDF dengan metadata (`no`, `judul`, `topik`).
10. **Step 10 — Menyimpan Hasil Feature Engineering:** Mengekspor matriks fitur akhir ke file `hasil_tfidf.csv`.
11. **Step 11 — Validasi Hasil Akhir:** Membaca kembali file `hasil_tfidf.csv` untuk memastikan integritas data terjamin.

---

## 📊 Hasil Statistik & Evaluasi

| Indikator Evaluasi | Nilai Baseline | Nilai Refined (Final) | Keterangan |
| :--- | :--- | :--- | :--- |
| **Jumlah Dokumen** | 100 | 100 | Konsisten (4 topik) |
| **Jumlah Fitur Kata** | 9.228 | 1.500 | Berhasil direduksi **83,75%** |
| **Dimensi Matriks Fitur** | (100, 9228) | (100, 1500) | Bebas dari *Curse of Dimensionality* |
| **Ukuran File Output** | ~2,5 MB | ~390 KB | Kompak dan efisien untuk *modelling* |

### **20 Fitur Paling Dominan pada Corpus (Top Accumulative TF-IDF):**
`model`, `informasi`, `komputer`, `ai`, `bahasa`, `cerdas`, `tahun`, `web`, `teknologi`, `perangkat`, `tingkat`, `kembang`, `hasil`, `nilai`, `algoritma`, `cerdas buat`, `ajar`, `bisnis`, `internet`, `jaring`.

---

## 📁 File Input & Output

* **Input File:** `hasil_preprocessed.csv` *(Dataset artikel hasil preprocessing)*
* **Output File:** `hasil_tfidf.csv` *(Matriks TF-IDF 1.500 fitur + 3 kolom metadata, total 1.503 kolom)*

---

## 🛠️ Pustaka / Library yang Digunakan

* `pandas` (Pengolahan data dan manipulasi DataFrame)
* `scikit-learn` (`TfidfVectorizer` untuk ekstraksi dan pembobotan fitur)