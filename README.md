Sistem Rekomendasi Kursus Wisata untuk Wisatawan

1. Deskripsi Proyek
Proyek ini bertujuan untuk membangun sistem rekomendasi yang dapat mencocokkan kebutuhan dan preferensi wisatawan (dari data tourist) dengan jenis kursus atau pelatihan di bidang pariwisata (dari data travel). Dengan memanfaatkan Natural Language Processing (NLP), sistem ini mengubah teks menjadi representasi vektor dan menghitung tingkat kemiripan antar teks untuk menghasilkan rekomendasi yang relevan.

2. Metodologi dan Pendekatan
Untuk membangun sistem ini, dilakukan beberapa tahapan utama, yaitu:
- Preprocessing Teks
Semua teks dibersihkan dari karakter yang tidak perlu dan diubah ke format yang konsisten (huruf kecil, tanpa tanda baca jika perlu). Hal ini penting untuk memastikan bahwa proses vektorisasi berjalan optimal dan tidak bias terhadap format penulisan.
- Representasi Teks (Vektorisasi)
Proyek ini menggunakan tiga pendekatan vektorisasi yang berbeda:
a. TF-IDF (Term Frequency - Inverse Document Frequency)
TF-IDF mengukur seberapa penting kata tertentu dalam satu dokumen relatif terhadap kumpulan dokumen lainnya.
Keunggulan: Cepat dan sederhana, cocok untuk baseline model.
Kelemahan: Tidak mempertimbangkan urutan kata atau konteks makna.

b. Word2Vec
Word2Vec memetakan kata-kata menjadi vektor berdasarkan konteks sekitar kata tersebut di kalimat.
Dalam proyek ini, vektor kalimat dibentuk dengan cara merata-ratakan vektor setiap kata dalam teks.
Keunggulan: Mampu menangkap makna semantik.
Kelemahan: Tidak mempertimbangkan konteks kalimat secara keseluruhan.

c. BERT (Bidirectional Encoder Representations from Transformers)
Menggunakan model pretrained paraphrase-MiniLM-L6-v2 dari SentenceTransformers.
BERT membaca keseluruhan kalimat dan menghasilkan vektor yang mempertimbangkan makna kontekstual secara menyeluruh.
Keunggulan: Akurasi tinggi dalam memahami maksud kalimat secara menyeluruh.
Kelemahan: Lebih berat secara komputasi dibanding metode lainnya.

3. Hasil Rekomendasi
Sistem ini menghitung kemiripan antara vektor dari teks tourist dengan seluruh data kursus di travel menggunakan cosine similarity. Hasil dengan skor tertinggi dianggap sebagai rekomendasi terbaik.
Contoh Rekomendasi (Model BERT)
Input (tourist):
"I want to explore cultural sites and heritage locations"
Top 3 Kursus yang Direkomendasikan:
Course on World Heritage Tourism
Cultural Tourism Planning
Managing Historic Destinations

Input (tourist):
"Interested in adventure and nature travel"
Top 3 Kursus yang Direkomendasikan:
Eco-tourism and Conservation
Adventure Travel Planning
Sustainable Nature Tours

Rekomendasi tersebut dihasilkan berdasarkan tingkat kemiripan vektor antar kalimat, bukan keyword semata, sehingga lebih relevan secara konteks.

4. Refleksi Proyek
Kendala yang Ditemui:
- Ambiguitas Kalimat: Kalimat pada kolom tourist yang terlalu pendek atau umum sulit dicocokkan secara akurat.
- Waktu Pemrosesan: Penggunaan model seperti BERT membutuhkan waktu lebih lama, terutama jika dataset besar.
- Ketidakseimbangan Data: Beberapa deskripsi travel bersifat terlalu teknis sehingga tidak langsung cocok dengan bahasa yang digunakan wisatawan.

5. Solusi yang Diterapkan:
- Menambahkan preprocessing untuk menyederhanakan dan menyamakan format teks sebelum vektorisasi.
- Menggunakan varian BERT ringan (MiniLM) agar proses encoding tetap efisien.
- Mengoptimalkan jumlah rekomendasi (misalnya top-3 saja) untuk menghindari overload informasi.


