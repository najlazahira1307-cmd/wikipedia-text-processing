# Web Scraping Wikipedia Exercise

Folder ini berisi implementasi kode program untuk melakukan ekstraksi data (*web scraping*) artikel Wikipedia Bahasa Indonesia secara otomatis menggunakan dua metode utama: **HTTP Request dengan BeautifulSoup** dan **MediaWiki API**.

---

## 👥 Anggota Kelompok
- **Najla Zahira** (25031554041)
- **Moza Athaillah Azzahra** (25031554185)

---

## 📌 Alur Kerja & Metodologi

1. **Eksplorasi & Ekstraksi URL (HTTP)**
   - Mengambil daftar URL artikel dari 9 kategori utama di Wikipedia Bahasa Indonesia (Komputasi, Kecerdasan Buatan, Ilmu Komputer, Pengolahan Data, Penyimpanan Data, Manajemen Data, Teknologi Informasi, Teknologi Digital, dan Internet) menggunakan `requests` dan `BeautifulSoup`.
   - Melakukan parsing pada elemen `<div id="mw-pages">` untuk mendapatkan total 479 URL artikel unik.

2. **Parsing Konten Teks & Metadata Artikel**
   - Mengekstrak elemen judul (`h1`), riwayat suntingan terakhir (`footer-info-lastmod`), dan paragraf isi (`mw-parser-output`).
   - Menyimpan sampel awal 10 baris dan keseluruhan artikel ke dalam struktur DataFrame Pandas.

3. **Filter Kualitas & Pembagian Kategori Topic**
   - Melakukan evaluasi duplikasi judul/URL dan analisis distribusi panjang teks (karakter).
   - Memfilter artikel berdasarkan kriteria panjang teks (>= 1500 karakter) untuk memastikan kualitas data.
   - Mengelompokkan artikel ke dalam **4 Topik Utama** secara proporsional (Total **100 artikel final**):
     - **Computer Science**: 30 artikel
     - **AI (Artificial Intelligence)**: 25 artikel
     - **Technology & Internet**: 25 artikel
     - **Data & Statistics**: 20 artikel

4. **Ekstraksi Data Menggunakan MediaWiki API**
   - Menggunakan endpoint resmi MediaWiki API (`https://id.wikipedia.org/w/api.php`) dengan parameter `action=query`, `prop=extracts`, dan `explaintext=True`.
   - Mengimplementasikan mekanisme penanganan *rate limiting* (HTTP Status 429) dan *retry delay* untuk memastikan keberhasilan ekstraksi tanpa terblokir.

5. **Komparasi Hasil Scraping (HTTP vs API)**
   - Menggabungkan data hasil scraping HTML (`Overview_Isi`) dan hasil ekstrak API (`API_Text`).
   - Menganalisis selisih panjang karakter antara kedua metode, di mana hasil ekstraksi API secara rata-rata memberikan teks yang lebih lengkap dan terstruktur.

---

## 🛠️ Pustaka & Teknologi yang Digunakan

- **Python 3.x**
- **Requests**: Untuk mengirimkan HTTP GET Request ke halaman web dan endpoint API.
- **BeautifulSoup4 (`bs4`)**: Untuk parsing markup HTML.
- **Pandas**: Untuk manipulasi, pembersihan, klasifikasi, dan analisis data.
- **Re (`re`)**: Untuk pencocokan pola teks dan klasifikasi topik berbasis regex.

---

## 📁 File Output

- `hasil_scraping_http.csv`: Data hasil ekstraksi scraping HTML via Requests & BeautifulSoup (100 artikel).
- `hasil_scraping_api.csv`: Data hasil ekstraksi teks bersih via MediaWiki API (100 artikel).
- `hasil_scraping_compare.csv`: Perbandingan berdampingan antara teks hasil HTTP dan API beserta metadata topik.