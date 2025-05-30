# Laporan Proyek Machine Learning Sistem Rekomendasi - Sindi Aprilianti

## Project Overview

Di era digital saat ini, industri hiburan mengalami pertumbuhan yang pesat, terutama di sektor perfilman. Layanan streaming seperti Netflix dan Disney+ terus menambahkan ribuan judul fim dan serial televisi ke dalamnya. Meskipun hal ini memperluas pilihan bagi user, banyak dari mereka justru kesulitan menemukan tontonan yang sesuai preferensi pribadi. Situasi ini sering disebut sebagai information overload, yaitu kondisi ketika volume informasi yang tersedia melampaui kemampuan individu untuk menyaring dan memprosesnya secara efektif. 

Untuk mengatasi masalah tersebut, banyak platform menggunakan sistem rekomendasi, yang merupakan bagian dari sistem penyaringan informasi yang dirancang untuk mengatasi masalah information overload. Sistem ini bekerja dengan menyaring inforamsi penting dari sejumlah besar data yang dihasilkan secara dinamis, berdasarkan preferensi, minat, atau perilaku pengguna terhadap suatu item. Sistem rekomendasi juga memiliki kemampuan untuk memprediksi apakah seorang pengguna kemungkinan besar menyukai suatu item atau tidaknya berdasarkan profil pengguna mereka (Isinkayea, et al. 2015). Dengan adanya sistem rekomendasi film tersebut, diharapkan dapat membantu pengguna dalam menemukan film yang sesuai dengan selera mereka secara cepat dan akurat. 

Daftar Pustaka
Isinkayea, F.O., Folajimi, Y.O., Ojokoh, B.A. 2015. Recommendation Systems: Principles, Methods, and Evaluation. Egyptian Infomatics Journal. Available at: https://www.sciencedirect.com/science/article/pii/S1110866515000341. 

**Rubrik/Kriteria Tambahan (Opsional)**:
- Jelaskan mengapa dan bagaimana masalah tersebut harus diselesaikan
- Menyertakan hasil riset terkait atau referensi. Referensi yang diberikan harus berasal dari sumber yang kredibel dan author yang jelas.
- Format Referensi dapat mengacu pada penulisan sitasi [IEEE](https://journals.ieeeauthorcenter.ieee.org/wp-content/uploads/sites/7/IEEE_Reference_Guide.pdf), [APA](https://www.mendeley.com/guides/apa-citation-guide/) atau secara umum seperti [di sini](https://penerbitdeepublish.com/menulis-buku-membuat-sitasi-dengan-mudah/)
- Sumber yang bisa digunakan [Scholar](https://scholar.google.com/)

## Business Understanding

Pada bagian ini, Anda perlu menjelaskan proses klarifikasi masalah.

Bagian laporan ini mencakup:

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1
- Pernyataan Masalah 2
- Pernyataan Masalah n

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1
- Jawaban pernyataan masalah 2
- Jawaban pernyataan masalah n

Semua poin di atas harus diuraikan dengan jelas. Anda bebas menuliskan berapa pernyataan masalah dan juga goals yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**:
- Menambahkan bagian “Solution Approach” yang menguraikan cara untuk meraih goals. Bagian ini dibuat dengan ketentuan sebagai berikut: 

    ### Solution statements
    - Mengajukan 2 atau lebih solution approach (algoritma atau pendekatan sistem rekomendasi).

## Data Understanding
Dataset berasal dari Kaggle yang berjudul "Movielens Dataset".
Dataset ini terdiri atas dua file csv, yaitu 
Paragraf awal bagian ini menjelaskan informasi mengenai jumlah data, kondisi data, dan informasi mengenai data yang digunakan. Sertakan juga sumber atau tautan untuk mengunduh dataset. Contoh: [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Restaurant+%26+consumer+data).

Selanjutnya, uraikanlah seluruh variabel atau fitur pada data. Sebagai contoh:  

Variabel-variabel pada Restaurant UCI dataset adalah sebagai berikut:
- accepts : merupakan jenis pembayaran yang diterima pada restoran tertentu.
- cuisine : merupakan jenis masakan yang disajikan pada restoran.
- dst

**Rubrik/Kriteria Tambahan (Opsional)**:
- Melakukan beberapa tahapan yang diperlukan untuk memahami data, contohnya teknik visualisasi data beserta insight atau exploratory data analysis.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan proses data preparation yang dilakukan
- Menjelaskan alasan mengapa diperlukan tahapan data preparation tersebut.

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

