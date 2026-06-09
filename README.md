# Case-Based Reasoning (CBR) System - Pidana Khusus Hak Cipta

Proyek ini mengimplementasikan sistem Case-Based Reasoning (CBR) berbasis Python untuk mendukung analisis putusan pengadilan pada perkara **Pidana Khusus Hak Cipta**. Sistem ini menggunakan data riil dari Direktori Putusan Mahkamah Agung Republik Indonesia dengan total 37 dokumen putusan.

## 📁 Struktur Repositori
Sesuai dengan ketentuan standar komposition proyek, berikut adalah struktur direktori yang digunakan:
* `/data/` : Memuat data mentah (raw text) dan data hasil pemrosesan (processed data).
* `/notebooks/` : Memuat file Jupyter Notebook (.ipynb) untuk setiap tahapan siklus CBR.
* `README.md` : Dokumentasi petunjuk instalasi dan eksekusi pipeline proyek.

---

## 💾 Raw & Processed Data
Bagian ini menjelaskan pembagian berkas data yang digunakan dalam sistem:

* **data/raw/** : Berisi 37 dokumen putusan riil (.txt) yang telah dibersihkan dari noise (header, footer, watermark) dan diubah menjadi format lower-case. Penamaan berkas menggunakan format standar `case_001.txt` sampai `case_037.txt`.
* **data/processed/** : Berisi file `cases.csv` yang merupakan hasil ekstraksi metadata terstruktur (Case Representation), memuat kolom wajib: `case_id`, `no_perkara`, `tanggal`, `ringkasan_fakta`, `pasal`, `pihak`, `hukuman_solusi`, dan `text_full`.
* **data/eval/** : Berisi berkas `queries.json` untuk pengujian kueri faset hukum dan `retrieval_metrics.csv` yang menyimpan hasil kalkulasi performa model.
* **data/results/** : Berisi berkas `predictions.csv` yang menyimpan hasil prediksi solusi amar putusan hukuman.

---

## 📓 Jupyter Notebooks Per Tahap
Seluruh pipeline eksperimen siklus CBR dibagi secara modular ke dalam berkas berikut:

1. **01_clean_data.ipynb** (Tahap 1: Membangun Case Base)
   Melakukan loading data mentah, konversi, pembersihan teks dari komponen pengganggu, serta validasi keutuhan teks berkas putusan.
2. **02_case_representation.ipynb** (Tahap 2: Case Representation)
   Melakukan ekstraksi metadata utama (Nomor perkara, nama pihak, pasal, tanggal) dan ringkasan fakta menggunakan regular expression (Regex) ke dalam berkas CSV.
3. **03_case_retrieval.ipynb** (Tahap 3: Case Retrieval)
   Melakukan pembagian data (splitting) dengan rasio 80:20, pembobotan statistik menggunakan TF-IDF (Term Frequency - Inverse Document Frequency), dan penghitungan kedekatan teks kueri baru menggunakan Cosine Similarity.
4. **04_predict.ipynb** (Tahap 4: Case Solution Reuse)
   Mengambil elemen solusi amar putusan dari kasus masa lalu terdekat (Top-K) untuk menghasilkan rekomendasi prediksi hukuman kasus baru.
5. **05_evaluation.ipynb** (Tahap 5: Model Evaluation)
   Melakukan kalkulasi performa akurasi sistem komputasi menggunakan metrik Accuracy, Precision, Recall, dan F1-score.

---

## 🛠️ Petunjuk Instalasi & Eksekusi

### 1. Instalasi Dependensi
Pastikan telah menginstal Python di komputermu. Pasang seluruh library yang diperlukan dengan menjalankan perintah berikut pada terminal:

pip install -r requirements.txt
