# Laporan Proyek Machine Learning Sistem Rekomendasi - Sindi Aprilianti

## Project Overview

Di era digital saat ini, industri hiburan mengalami pertumbuhan yang pesat, terutama di sektor perfilman. Layanan streaming seperti Netflix dan Disney+ terus menambahkan ribuan judul fim dan serial televisi ke dalamnya. Meskipun hal ini memperluas pilihan bagi user, banyak dari mereka justru kesulitan menemukan tontonan yang sesuai preferensi pribadi. Situasi ini sering disebut sebagai information overload, yaitu kondisi ketika volume informasi yang tersedia melampaui kemampuan individu untuk menyaring dan memprosesnya secara efektif. Untuk mengatasi masalah tersebut, banyak platform menggunakan sistem rekomendasi, yang merupakan bagian dari sistem penyaringan informasi yang dirancang untuk mengatasi masalah information overload. Sistem ini bekerja dengan menyaring inforamsi penting dari sejumlah besar data yang dihasilkan secara dinamis, berdasarkan preferensi, minat, atau perilaku pengguna terhadap suatu item. Sistem rekomendasi juga memiliki kemampuan untuk memprediksi apakah seorang pengguna kemungkinan besar menyukai suatu item atau tidaknya berdasarkan profil pengguna mereka (Isinkayea, et al. 2015). Dengan adanya sistem rekomendasi film tersebut, diharapkan dapat membantu pengguna dalam menemukan film yang sesuai dengan selera mereka secara cepat dan akurat. 

Daftar Pustaka

Isinkayea, F.O., Folajimi, Y.O., Ojokoh, B.A. 2015. Recommendation Systems: Principles, Methods, and Evaluation. Egyptian Infomatics Journal. Available at: https://www.sciencedirect.com/science/article/pii/S1110866515000341. 

## Business Understanding

### Problem Statements

Menjelaskan pernyataan masalah:
- Pernyataan Masalah 1: Bagaimana cara memberikan rekomendasi film yang relevan untuk setiap pengguna berdasarkan data historis mereka?
- Pernyataan Masalah 2: Bagaimana sistem dapat memberikan rekoemndasi yang bersifat personal untuk setiap pengguna?

### Goals

Menjelaskan tujuan proyek yang menjawab pernyataan masalah:
- Jawaban pernyataan masalah 1: Mmembangun sistem rekomendasi yang dapat memberikan saran film yang sesuai minat pengguna
- Jawaban pernyataan masalah 2: Meningkatkan personalisasi dalam rekomendasi film


    ### Solution statements
    - Menerapkan content based filtering yang akan menganalisis karakteristik konten film, seperti genre yang disukai pengguna, lalu merekomendasikan film dengan karakteristik yang serupa.
    - Menerapkan collaborative filtering yang akan merekomendasikan film berdasarkan pola kesamaan antar pengguna atau antar film. Sistem akan mencari pengguna lain yang memiliki preferensi serupa, lalu menyarankan film yang mereka sukai tapi belum ditonton pengguna. 

## Data Understanding
Dataset berasal dari Kaggle yang berjudul "Movielens Dataset", yang dapat diunduh pada tautan berikut: https://www.kaggle.com/datasets/ayushimishra2809/movielens-dataset. Dataset ini terdiri atas dua file csv, yaitu movies.csv dan ratings.csv

### Variabel-variabel pada Movielens dataset adalah sebagai berikut:
- movieId: merupakan id unik untuk tiap film dalam dataset
- title: merupakan judul film
- genres: merupakan kategori atau jenis film. Satu film bisa memiliki lebih dari satu genre
- userId: merupakan id unik untuk setiap pengguna
- rating: merupakan nilai yang diberikan pengguna terhadap suatu film
- timestamp: merupakan waktu saat rating diberikan oleh pengguna

Beberapa tahap EDA yang dilakukan pada dataset

Pada dataset movies.csv

- Melihat informasi pada dataset movies.csv dengan movies_df.info()
  
  ![image](https://github.com/user-attachments/assets/e395d5a1-8ac8-46a0-8829-0d76c3689a86)
  
  menunjukkan bahwa movies_df memiliki 3 kolom yang berisi movieId dengan tipe data int64, title bertipe object, dan genres yang bertipe object. Dataset ini memiliki 10.329 entri data
  
- Melihat contoh data dengan movies_df.head()
  
  ![image](https://github.com/user-attachments/assets/63bc65b2-60f4-4b76-9b19-ed9ae08b2e68)
  
  Menampilkan contoh 5 data dalam movies_df. Setiap movie ternyata dapat memiliki lebih dari satu genre yang dipisahkan oleh simbol | 

- Melihat banyaknya movieId dan banyaknya judul unik
  
  ![image](https://github.com/user-attachments/assets/badc9264-44fd-4c0d-aa08-05e929fae7ce)
  
  Terdapat 10.329 movie, tapi judul uniknya ada 10.329, ini berarti ada dua movie dengan title yang sama persis tapi memiliki movieId yang berbeda.

- Melihat movie dengan title sama tapi memiliki movieId lebih dari satu
  
  ![image](https://github.com/user-attachments/assets/abcce303-d967-447f-bb86-39da3ae24b81)

  Diketahui bahwa movie berjudul "War of the Worlds (2005)" dan "Men with Guns (1997)" muncul dua kali, maka duplikat ini nantinya harus dihapus. 

- Melihat genre pada dataset
  
  ![image](https://github.com/user-attachments/assets/74562b81-ffc6-4570-832c-66bcd6e4262e)

  Genre yang ada pada data adalah action, adventure, animation, children, comedy, crime, documentary, drama, fantasy, film-noir, horror, imax, musical, mystery, roamnce, sci-fi, thriller, war, dan western. Kemudian diketahui bahwa hampir setiap movie memiliki beberapa genre

- Melihat missing values pada movies_df dengan isna()
  
  ![image](https://github.com/user-attachments/assets/44ca3fe6-1806-4f45-9a33-d65eb651b523)
  
  movies_df tidak memiliki missing values

Pada dataset ratings.csv

- Melihat informasi pada dataset ratings.csv dengan ratings_df.info()
  
  ![image](https://github.com/user-attachments/assets/3fe59a34-1cd3-488e-9e74-d6a19b5935a2)

  ratings_df memiliki 4 kolom yaitu userId (int64), movieId (int64), rating (float64), dan timestamp (int64). Dataset ini memiliki 105.339 entri data.

- Melihat contoh data dengan ratings_df.head()
  
  ![image](https://github.com/user-attachments/assets/ad8c76d5-21ed-4b04-9906-54862f48f684)

  Menampilkan contoh 5 data dalam ratings_df. Setiap user dapat memberi rating untuk banyak film. 

- Melihat banyaknya data dan jenis rating yang ada
  
  ![image](https://github.com/user-attachments/assets/1a533b03-75bb-4e63-bd3a-5f332391ccd3)

  UserId memiliki 668 data, ini berarti ada 668 user berbeda yang memberikan rating movie. Jenis rating yang ada yaitu 0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 3.5, 4.0, 4.5, dan 5.0.

- Melihat jumlah kombinasi userId + movieId yang unik
  
  ![image](https://github.com/user-attachments/assets/ad460fb2-9e09-453e-8efb-fda6f10b7c3a)

  Ini untuk memastikan satu userId tidak memberi rating lebih dari sekali untuk movieId yang sama. Hasilnya menunjukkan duplikasi tersebut tidak ada. 

- Melihat missing values pada ratings_df dengan isnull().sum()
  
  ![image](https://github.com/user-attachments/assets/5d71e238-f7a7-4fde-bf43-cd2709a66391)
  
  Tidak terdapat missing values pada ratings_df

- Melihat statistik deskriptif pada ratings_df dengan describe()
  
  ![image](https://github.com/user-attachments/assets/b2069574-b086-4c7b-9cd2-13645310e379)

  Pada hasil describe, kita fokus pada kolom rating. Diketahui bahwa 0.5 merupakan minimal rating dan 5.0 merupakan maximal rating yang diberikan pengguna. Diketahui bahwa rating minimal yang diberikan pengguna adalah 0.5, 25% dengan rating 3.0, 50% dengan rating 3.5, 75% dengan rating 4.0, dan maximal dengan rating 5.0.

## Data Preparation
Pada bagian ini Anda menerapkan dan menyebutkan teknik data preparation yang dilakukan. Teknik yang digunakan pada notebook dan laporan harus berurutan.

- Menghapus duplikat data pada movies_df
  
  ![image](https://github.com/user-attachments/assets/545e9b92-613b-4632-8b42-a2feb68191f0)
  
  Judul yang sama persis dengan movieId lebih dari satu telah berhasil dihapus, sehingga jumlah datanya menjadi 10.327. Langkah ini dilakukan karena duplikasi dapat menyebabkan bias dalam model karena data yang sama diperhitungkan lebih dari sekali. 

- Menggabungkan movies_df dengan ratings_df menggunakan kolom movieId
  
  ![image](https://github.com/user-attachments/assets/ffab7f12-3f7f-48ab-99c0-91052e4c1569)
  
  Hasil penggabungan disimpan di df. Penggabungan ini penting agar tiap baris dalam dataset memiliki informasi yang lengkap

- Menampilkan contoh data hasil merge dengan head()
  
  ![image](https://github.com/user-attachments/assets/c88df15e-e4a5-4295-802c-3d98b863d29c)
  
  movies_df dengan ratings_df berhasil digabungkan

- Mengecek jumlah baris dan kolom df dengan df.shape
  
  ![image](https://github.com/user-attachments/assets/b8e4eb3c-4762-454a-a2e5-5552b8a979f6)
  
  df memiliki 105.339 baris data dengan 6 kolom

- Mengecek missing values pada df dengan isnull()
  
  ![image](https://github.com/user-attachments/assets/f12e2eab-59c4-488f-ac3c-60b9c413b483)
  
  Tidak terdapat missing values pada df. Langkah ini untuk meastikan tidak ada missing values, karena jika ada akan mengganggu pemodelan.

- Mengecek data duplikat pada df dengan duplicated()
  
  ![image](https://github.com/user-attachments/assets/16612a6b-0b51-4665-83da-fdb1b25fce72)
  
  Tidak terdapat data duplikat. Ini untuk memastikan tidak terjadi duplikasi data setelah dilakukan merge

- Mengubah movieId, title, dan genres menjadi list dan membuat df baru bernama movie_df dengan tiga kolom yang berisi informasi terkait movie, yaitu id, titile, dan genre tersebut
  
  ![image](https://github.com/user-attachments/assets/bfb17441-8576-4997-86be-064bdef7f166)

  Ini untuk membuat data khusus mengenai informasi film yang akan berguna untuk eksplorasi konten film secara terpisah dari rating atau user. 

- Mengecek len dari movieId, movieTitle, dan movieGenres
  
  ![image](https://github.com/user-attachments/assets/bf8c7207-78b6-416e-9878-b5f1d95b4b6c)

  ketiganya memiliki len yang sama, yaitu 105.339. Langkah ini untuk memastikan jumlah elemen di setiap list itu sama. Konsistensi jumlah elemen penting agar tidak terjadi kesalahan saat menyusun kembali movie_df

- Mengecek dan menampilkan jumlah data berisi NaN pada kolom genre menggunakan isna()
  
  ![image](https://github.com/user-attachments/assets/5eca40dd-77b9-4c6f-8673-71acd222f564)
  
  Terdapat 5 data pada genre yang berisi NaN

- Mengganti NaN menjadi string kosong
  
    Sudah tidak terdapat NaN. Ini perlu dilakukan, karena jika terdapat nilai NaN dapat menyebabkan error saat pemodelan berbasis genre. Mengganti NaN dengan string kosong untuk menjaga kestabilan data tanpa harus menghapus baris penting. 

## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

### Content Based Filtering

##### Metode TF-IDF Vectorizer



**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menyajikan dua solusi rekomendasi dengan algoritma yang berbeda.
- Menjelaskan kelebihan dan kekurangan dari solusi/pendekatan yang dipilih.

## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

