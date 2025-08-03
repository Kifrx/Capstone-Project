# ANALISIS REVIEW NEGATIF PRODUK DI AMAZON 

</div>

## - PROJEK OVERVIEW

* Latar belakang:
E-commerce menyediakan fitur ulasan terkait produk yang telah dibeli. Ini berguna untuk memberikan kesan kepada produk yang dibeli pembeli. Contohnya seperti di e-commerce Amazon. Terdapat banyak sekali ulasan pembeli dan rating, ulasan-ulasan tersebut ada yang berupa positif dan negatif terhadap produknya. Rating/bintang merupakan gambaran nilai keseluruhan suatu produk. Semakin tinggi Ratingnya (bintang 3-5) semakin baik atau berkualitas pula barangnya, namun sebaliknya jika rating (bintang dibawah 3) maka barang tersebut memeliki kekurangan atau kurang layak dibeli. Peningkatan kualitas barang dan memahami kelemahannya sangat dibutuhkan untuk mengevaluasi produk
yang dibuat. Hal ini dapat meningkatkan kekurangan-kekurangan yang dimiliki suatu produk.

* Tujuan projek: 
Menganalisis ulasan negatif (bintang 1 & 2) pada produk dengan ulasan negatif terbanyak untuk menemukan 2 keluhan teknis utama yang bisa menjadi masukan bagi tim pengembangan produk.


* Pendekatan:
Proyek ini menggunakan pendekatan kuantitatif dengan memanfaatkan Natural Language Processing (NLP) yang didukung oleh AI. Alur kerja dimulai dari pembersihan data ulasan Amazon, lalu mengidentifikasi produk dengan jumlah ulasan negatif terbanyak untuk memastikan analisis yang relevan. Selanjutnya, AI (Large Language Model) digunakan untuk dua tugas utama: pertama, mengidentifikasi jenis produk berdasarkan sampel ulasannya, dan kedua, mengklasifikasikan setiap ulasan negatif ke dalam kategori keluhan yang spesifik. Hasil klasifikasi kemudian diagregasi dan divisualisasikan untuk menemukan keluhan utama, yang pada akhirnya menjadi dasar bagi AI untuk menghasilkan rekomendasi strategis bagi tim produk.

## - ANALISIS PROYEK
Langkah-langkah analisis dilakukan secara sistematis untuk mengubah data ulasan mentah menjadi insight yang dapat ditindaklanjuti.

1. Persiapan Data dan Lingkungan

Data dari file Reviews.csv dibaca menggunakan library pandas di Google Colab. Lingkungan kerja disiapkan dengan menginstal library yang dibutuhkan (langchain_community, replicate) dan mengkonfigurasi API token untuk model AI.

Alasan: pandas adalah standar industri untuk manipulasi data di Python karena efisien dan mudah digunakan. Google Colab dipilih karena menyediakan akses gratis ke sumber daya komputasi dan kemudahan integrasi dengan berbagai library.

2. Seleksi Target Analisis

Daripada menganalisis produk secara acak, target analisis difokuskan pada produk yang paling bermasalah. Ini dilakukan dengan memfilter seluruh dataset untuk hanya menyisakan ulasan negatif (Skor < 3), kemudian menghitung ProductId yang paling sering muncul menggunakan value_counts() dan idxmax().

Alasan: Pendekatan ini memastikan bahwa analisis yang dilakukan memiliki dampak maksimal, karena langsung menyasar produk dengan tingkat ketidakpuasan pelanggan tertinggi.

3. Identifikasi Produk dengan AI

Setelah mendapatkan ProductId target (B000KV61FC), beberapa sampel ulasan dari produk tersebut digabungkan menjadi satu konteks. Konteks ini kemudian dimasukkan ke dalam prompt yang dirancang untuk bertanya kepada model AI, "Produk apakah ini?".

Alasan: ProductId tidak memberikan informasi deskriptif. Menggunakan AI untuk "menebak" produk berdasarkan ulasannya adalah cara yang efisien untuk mendapatkan pemahaman kontekstual sebelum melakukan analisis mendalam. Hasilnya menunjukkan produk tersebut adalah mainan anjing "Tug-a-Jug".

4. Klasifikasi Keluhan dengan AI

Sebuah fungsi prompt spesifik untuk produk mainan anjing dibuat. Setiap ulasan negatif dari produk "Tug-a-Jug" dimasukkan ke dalam prompt ini. Model AI kemudian mengklasifikasikan setiap ulasan ke dalam salah satu kategori yang telah ditentukan (misalnya: 'Daya Tahan & Kualitas', 'Desain & Fungsi', dll.). Proses ini diulang untuk semua ulasan negatif yang relevan.

Alasan: Menggunakan AI untuk klasifikasi teks (zero-shot classification) jauh lebih cepat dan fleksibel daripada melatih model machine learning tradisional. Ini memungkinkan pembuatan kategori on-the-fly yang disesuaikan dengan konteks produk.


5. Generasi Rekomendasi dengan AI

Temuan utama (Top 2 keluhan) disajikan kembali kepada AI dalam sebuah prompt final. AI diberi peran sebagai "Product Manager Analyst" dan diminta untuk memberikan rekomendasi yang bisa ditindaklanjuti berdasarkan data temuan tersebut.

Alasan: Langkah ini memanfaatkan kemampuan penalaran dan sintesis dari AI untuk mengubah insight mentah menjadi narasi strategis, yang merupakan tujuan akhir dari proyek ini.

6. Agregasi dan Visualisasi Hasil

Hasil klasifikasi dari AI (kolom 'Kategori' yang baru) dihitung menggunakan value_counts() untuk menemukan frekuensi setiap keluhan. Hasilnya kemudian divisualisasikan menggunakan seaborn untuk membuat grafik batang.

Alasan: Visualisasi adalah cara paling efektif untuk menyajikan distribusi data dan dengan cepat mengidentifikasi temuan kunci.


## - RAW DATASET LINK
https://www.kaggle.com/datasets/arhamrumi/amazon-product-reviews

## - INSIGHT & FINDINGS
1. Identifikasi Produk Paling Bermasalah: Dari keseluruhan dataset, produk dengan jumlah ulasan negatif terbanyak adalah produk dengan ID B000KV61FC, yang berhasil diidentifikasi oleh AI sebagai mainan anjing interaktif "Tug-a-Jug".

2. Keluhan Utama Pelanggan: Analisis terhadap ulasan negatif produk "Tug-a-Jug" menunjukkan dua keluhan teknis yang paling dominan adalah:
    * Daya Tahan & Kualitas Material: Ini adalah keluhan yang paling sering muncul. Pelanggan melaporkan bahwa mainan tersebut mudah hancur, pecah, atau rusak parah bahkan oleh anjing berukuran sedang. Ini menunjukkan material yang digunakan tidak cukup kuat untuk menahan gigitan anjing.

    * Desain & Fungsi: Keluhan kedua berpusat pada mekanisme mainan. Banyak pengguna melaporkan bahwa lubang tempat keluarnya makanan/camilan terlalu besar sehingga isinya keluar terlalu cepat, atau sebaliknya, terlalu sulit sehingga membuat anjing frustrasi dan kehilangan minat. Pelanggan juga mencatat bahwa mereka akhirnya membawa-bawa mainan tersebut tanpa berinteraksi dengannya, yang menunjukkan kegagalan fungsi mainan tersebut sebagai mainan interaktif

## - AI SUPPORT EXPLANATION

Dukungan AI (model IBM Granite) adalah inti dari proyek ini dan digunakan dalam tiga kapasitas yang berbeda dan krusial:

1. Identifikasi Kontekstual: AI pertama kali digunakan untuk menjawab pertanyaan "Produk apa ini?" hanya dengan melihat beberapa ulasan. Ini adalah tugas ekstraksi informasi dari teks tidak terstruktur untuk memberikan pemahaman awal yang vital sebelum analisis lebih lanjut.

2. Klasifikasi Teks Tanpa Pelatihan: Penggunaan utama AI adalah untuk mengklasifikasikan ratusan ulasan negatif ke dalam kategori yang relevan. Dengan merancang prompt yang efektif, model LLM dapat melakukan klasifikasi ini secara langsung tanpa perlu proses fine-tuning yang memakan waktu. Kemampuan ini memungkinkan analisis yang cepat dan adaptif sesuai dengan jenis produk yang ditemukan.

3. Generasi Sintesis & Rekomendasi: Pada tahap akhir, AI tidak hanya menyajikan data tetapi juga menginterpretasikannya. Dengan memberikan ringkasan temuan (Top 2 keluhan), AI diminta untuk bertindak sebagai analis. Kemampuan AI untuk melakukan penalaran dan sintesis digunakan untuk menghasilkan rekomendasi yang konkret dan relevan secara bisnis, yang merupakan tujuan akhir dari proyek ini.
