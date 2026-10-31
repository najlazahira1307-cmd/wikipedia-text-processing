# Text Clustering

Proyek ini bertujuan untuk mengelompokkan (*clustering*) dokumen teks berbahasa Indonesia berbasis artikel Wikipedia menggunakan dua metode utama: **Hierarchical Clustering** (Single, Complete, dan Average Linkage) serta **K-Means Clustering**. Fitur numerik yang digunakan sebagai basis pengelompokan adalah matriks **TF-IDF** hasil dari tahapan *Feature Engineering*.

---

## 📋 Anggota Kelompok
* **Najla Zahira** (NIM: 25031554041)
* **Moza Athaillah Azzahra** (NIM: 25031554185)

---

## 📁 Dataset
Dataset yang digunakan berisi 100 dokumen artikel Wikipedia dengan metadata (`no`, `judul`, `topik`) dan 1.500 fitur numerik representasi nilai TF-IDF.
* **Tautan Dataset:** [Google Drive - Dataset Hasil TF-IDF](https://drive.google.com/file/d/1Lioi1yyYc44BMFIfFMDilfjPqPDDxrZC/view?usp=sharing)

---

## 🛠️ Alur Kerja & Metodologi

Proyek ini dibagi menjadi beberapa tahapan utama:

### 1. Load Dataset & Persiapan Fitur
* Memuat dataset `hasil_tfidf.csv`.
* Memisahkan kolom metadata (`no`, `judul`, `topik`) dari matriks fitur TF-IDF ($100 \times 1500$).
* Melakukan verifikasi kelengkapan data (memastikan tidak ada nilai *missing* atau baris berisi nilai nol secara keseluruhan).

### 2. Hierarchical Clustering (Agglomerative)
* Menghitung matriks jarak antar-dokumen berbasis **Cosine Distance**.
* Mengaplikasikan 3 jenis metode *linkage* dengan jumlah cluster awal $k = 4$:
  * **Single Linkage:** Mengukur jarak terkecil antar anggota kelompok.
  * **Complete Linkage:** Mengukur jarak terbesar antar anggota kelompok.
  * **Average Linkage:** Mengukur rata-rata jarak antar seluruh pasangan dokumen antar kelompok.
* Memvisualisasikan hirarki pengelompokan menggunakan **Dendrogram** (Average Linkage).

### 3. K-Means Clustering & Evaluasi Optimalitas
* Menilai kualitas kelompok menggunakan **Silhouette Score**.
* Mencari jumlah cluster optimal ($k = 2$ hingga $10$) pada K-Means dengan mengevaluasi:
  * **Elbow Method (Inertia/WCSS)**
  * **Silhouette Score Evaluation**

---

## 📊 Hasil Eksperimen

### 1. Perbandingan Hierarchical Clustering ($k = 4$)

| Metode Linkage | Jumlah Cluster | Silhouette Score | Karakteristik Distribusi Dokumen |
| :--- | :---: | :---: | :--- |
| **Average Linkage** | 4 | **0.0316** | Mendominasi di 1 cluster besar (93 dokumen) |
| **Complete Linkage** | 4 | **0.0252** | Distribusi lebih seimbang (35, 15, 45, dan 5 dokumen) |
| **Single Linkage** | 4 | **0.0220** | Mengalami *chaining effect* (97 dokumen di 1 cluster, sisa 1 dokumen per cluster) |

### 2. Evaluasi K-Means Clustering ($k = 2$ s.d. $10$)

| Nilai $k$ | Inertia | Silhouette Score |
| :---: | :---: | :---: |
| 2 | 89.1054 | 0.0242 |
| 3 | 87.4408 | 0.0318 |
| 4 | 85.8665 | 0.0325 |
| 5 | 84.6229 | 0.0259 |
| 6 | 83.4625 | 0.0280 |
| 7 | 81.1487 | 0.0458 |
| 8 | 80.4654 | 0.0343 |
| **9** | **78.6674** | **0.0512** |
| 10 | 77.6331 | 0.0431 |

> **Kesimpulan Evaluasi:** 
> * Pada Hierarchical Clustering, **Average Linkage** memberikan Silhouette Score tertinggi untuk $k = 4$.
> * Pada K-Means Clustering, performa terbaik dicapai pada **$k = 9$** dengan **Silhouette Score = 0.0512**.

---

## 🚀 Cara Menjalankan Code

### 1. Prasyarat (*Dependencies*)
Pastikan Python 3.x dan pustaka berikut telah terinstal:
```bash
pip install pandas numpy scikit-learn matplotlib scipy