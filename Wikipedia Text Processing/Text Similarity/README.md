# Text Similarity

Dokumentasi ini berisi penjelasan lengkap mengenai alur kerja *Text Similarity* menggunakan metode **Cosine Similarity** pada dataset matriks fitur TF-IDF (100 dokumen x 1.500 fitur) yang telah dihasilkan pada tahap *Feature Engineering* sebelumnya.

---

## 👥 Anggota Kelompok
- **Najla Zahira** (25031554041)
- **Moza Athaillah Azzahra** (25031554185)

---

## 📌 Ringkasan Alur Kerja

Proses perhitungan dan analisis *Text Similarity* dilakukan dalam **8 tahapan terstruktur**:

1. **Step 1 — Load dan Validasi Dataset:** Memuat dataset `hasil_tfidf.csv` (100 dokumen x 1.503 kolom) serta memisahkan kolom metadata (`no`, `judul`, `topik`) dari matriks numerik fitur TF-IDF (100 x 1.500).
2. **Step 2 — Perhitungan Cosine Similarity:** Menghitung nilai kemiripan antar-dokumen menggunakan `cosine_similarity` dari `scikit-learn` untuk menghasilkan matriks simetris berukuran $100 \times 100$.
3. **Step 3 — Validasi Properti Matriks:** Memastikan matriks kemiripan memenuhi kriteria matematis: berukuran $100 \times 100$, simetris ($S_{i,j} = S_{j,i}$), nilai diagonal utama $S_{i,i} \approx 1.0$, serta bebas dari nilai `NaN` atau `Inf`.
4. **Step 4 — Ekstraksi Pasangan Dokumen Unik:** Mengambil elemen segitiga atas matriks (*upper triangle*) menggunakan `np.triu_indices(100, k=1)` untuk memperoleh 4.950 pasangan dokumen unik tanpa duplikasi dan tanpa membandingkan dokumen dengan dirinya sendiri.
5. **Step 5 — Analisis Pasangan Kemiripan Tertinggi & Terendah:** Mengurutkan skor kemiripan untuk mengidentifikasi 5 pasangan dokumen paling mirip (*Top 5 Most Similar*) dan 5 pasangan dokumen paling tidak mirip (*Top 5 Least Similar*).
6. **Step 6 — Perhitungan Statistik Deskriptif:** Menghitung ringkasan statistik dari seluruh skor kemiripan (Rata-rata, Standar Deviasi, Nilai Minimum, Nilai Maksimum, serta Kuartil Q1, Q2/Median, Q3).
7. **Step 7 — Visualisasi Distrbusi Kemiripan:** Menampilkan distribusi skor kemiripan seluruh pasangan dokumen menggunakan Histogram & KDE plot, serta visualisasi $100 \times 100$ Heatmap matriks kemiripan.
8. **Step 8 — Analisis Kualitatif & Kesimpulan:** Menggevaluasi hubungan antar-topik pada pasangan dokumen dan menganalisis keterbatasan metode kemiripan berbasis pembobotan leksikal TF-IDF.

---

## 📊 Hasil Statistik & Evaluasi

| Indikator Evaluasi | Nilai / Deskripsi | Keterangan |
| :--- | :--- | :--- |
| **Jumlah Dokumen** | 100 | Memperoleh matriks kemiripan $100 \times 100$ |
| **Total Pasangan Unik** | 4.950 Pasangan | Hasil dari $\frac{100 \times 99}{2}$ tanpa diagonal utama |
| **Properti Matriks** | Simetris & Valid | Diagonal $= 1.0$, $S_{i,j} = S_{j,i}$, bebas `NaN`/`Inf` |
| **Karakteristik Kemiripan** | Tinggi pada Topik Sama | Dokumen setopik memiliki skor cosine similarity lebih tinggi |

### **Ringkasan Temuan Utamanya:**
* **Pasangan Kemiripan Tinggi ($\approx 0.7 - 0.9$):** Didominasi oleh dokumen yang berada dalam kelompok **topik yang sama** karena memiliki irisan kata (*vocabulary overlap*) yang signifikan.
* **Pasangan Kemiripan Terendah ($\approx 0.0 - 0.05$):** Berasal dari dokumen dengan **topik berbeda** yang hampir tidak memiliki irisan istilah (*term*) dalam matriks TF-IDF.
* **Keterbatasan Leksikal:** Perhitungan kemiripan TF-IDF sangat bergantung pada pencocokan kata secara eksak (*exact term match*) dan belum memperhitungkan kesamaan makna secara semantik mendalam (*semantic representation*).

---

## 📁 File Input & Output

* **Input File:** `hasil_tfidf.csv` *(Matriks fitur TF-IDF 1.500 fitur + 3 kolom metadata)*
* **Output Artifact:** Matriks Cosine Similarity ($100 \times 100$), Pasangan Dokumen Unik (4.950 pasang), serta Plot Distribusi & Heatmap.

---

## 🛠️ Pustaka / Library yang Digunakan

* `pandas` (Pengolahan data dan manipulasi DataFrame)
* `numpy` (Operasi matriks dan pemrosesan *upper triangle indices*)
* `scikit-learn` (`cosine_similarity` untuk kalkulasi jarak/kemiripan antar-vektor)
* `matplotlib` & `seaborn` (Visualisasi Histogram, KDE, dan Heatmap)