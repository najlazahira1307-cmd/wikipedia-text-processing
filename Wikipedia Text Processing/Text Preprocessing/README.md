# Text Preprocessing Wikipedia Dataset

Folder ini berisi implementasi pipeline pembersihan dan pra-pemrosesan data teks (*text preprocessing*) untuk 100 artikel Wikipedia Bahasa Indonesia hasil scraping. Proses ini bertujuan untuk mengurangi *noise* (derau) dan menyiapkan data teks ke dalam bentuk token bersih yang siap digunakan untuk tahapan pemodelan Machine Learning atau analisis NLP lanjutan.

---

## 👥 Anggota Kelompok
- **Najla Zahira** (25031554041)
- **Moza Athaillah Azzahra** (25031554185)

---

## 📌 Alur & Tahapan Preprocessing

1. **Load & Verifikasi Dataset**
   - Memuat dataset `hasil_scraping_api.csv` yang berisi 100 artikel dengan 4 kolom utama (`no`, `judul`, `teks`, dan `topik`).

2. **Pembersihan Notasi LaTeX & Ekspresi Matematika**
   - Mengabaikan elemen markup LaTeX seperti `{\\displaystyle ...}` dan perintah matematis (misal: `\\frac`, `\\mathbb`, `\\alpha`, dll.) menggunakan ekspresi reguler (*regex*).

3. **Pembersihan Special Characters & Unicode Invalid**
   - Menghapus simbol khusus Unicode blok *Private Use Area* (`\\uE000-\\uF8FF`), sitasi dalam kurung siku (`[1]`, `[2]`), serta karakter khusus di luar huruf, angka, dan spasi.

4. **Pembersihan URL & Tautan Web**
   - Menghapus seluruh tautan berupa URL/domain web yang diawali `http://`, `https://`, atau `www.`.

5. **Normalisasi Whitespace**
   - Mengubah karakter *newline* (`\\n`), *carriage return* (`\\r`), dan *tab* (`\\t`) menjadi spasi tunggal serta merapikan spasi ganda bertumpuk.

6. **Case Folding**
   - Mengonversi seluruh huruf Kapital (A-Z) menjadi huruf kecil (*lowercase*) secara menyeluruh.

7. **Tokenisasi (Tokenization)**
   - Memecah deretan teks kalimat menjadi daftar kata (*list of tokens*) terpisah berbasis spasi.

8. **Stopword Removal**
   - Mengeliminasi kata-kata umum yang kurang memiliki bobot informasi menggunakan pustaka **Sastrawi** (123 kata dalam kamus stopword).

9. **Stemming Bahasa Indonesia**
   - Mengubah kata berimbuhan menjadi bentuk kata dasarnya menggunakan algoritma `StemmerFactory` dari **Sastrawi**.

10. **Analisis Evaluasi (Before vs After)**
    - Melakukan evaluasi kuantitatif terhadap reduksi jumlah kata sebelum dan sesudah *preprocessing*.

---

## 📊 Hasil & Evaluasi Reduksi Data

Berdasarkan eksekusi pipeline pada corpus 100 artikel Wikipedia:
- **Total Kata Sebelum Preprocessing**: 108.688 kata
- **Total Kata Sesudah Preprocessing**: 81.228 kata
- **Rata-rata Kata per Artikel**: 1.086,9 -> 812,3 kata
- **Efisiensi Reduksi Noise**: **25,26%** kata berlebih/derau berhasil dibuang

---

## 🛠 Pustaka & Teknologi yang Digunakan

- **Python 3.x**
- **Pandas**: Untuk manipulasi struktur data DataFrame dan ekspor dataset.
- **Re (`re`)**: Untuk pencocokan pola regex pada pembersihan LaTeX, URL, Unicode PUA, dan spesial karakter.
- **Sastrawi**: Pustaka khusus Bahasa Indonesia untuk tahapan *Stopword Removal* dan *Stemming*.

---

## 📁 File Output

- `hasil_preprocessed.csv`: Dataset akhir berformat CSV yang berisi 100 artikel terproses bersih dengan kolom `no`, `judul`, `topik`, dan `teks_clean`.