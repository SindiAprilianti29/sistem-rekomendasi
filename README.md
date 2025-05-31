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
  
  Terdapat 5 missing values pada title dan genre di df. Langkah ini untuk meastikan tidak ada missing values, karena jika ada akan mengganggu pemodelan.

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

- Mengecek dan menampilkan jumlah data yang memiliki nilai NaN pada title

  ![image](https://github.com/user-attachments/assets/ffe33778-3adf-4c30-bc42-6a73b3bf407f)

- Menghapus baris yang memiliki NaN pada kolom title

  ![image](https://github.com/user-attachments/assets/be36e9f5-f49f-49ee-aa0b-5a4b91efb2cb)

  Hasilnya sudah tidak ada missing values

- Menghapus duplikat yang ada pada movie_df

- Melakukan TF-IDF Vectorizer

  Memproses data genre film menjadi fitur kata unik yang bsia digunakan untuk perhitungan similarity

  ![image](https://github.com/user-attachments/assets/b1ef4b2c-96d0-4931-a88e-8f9587e2dbf0)

  Kemudian mengubah vektor tf-idf menjadi bentuk list

  ![image](https://github.com/user-attachments/assets/18ded09d-4f01-44fe-9f17-09c23dc46a0e)

  Berfungsi mengubah teks, misalnya genre film menjadi representasi numerik yang menunjukkan pentingnya kata dalam dokumen relatif terhadap seluruh koleksi data. Dalam content based filtering, TF-IDF membantu memproses fitur konten.
Berikut merupakan contoh hasil TD-IDF

![image](https://github.com/user-attachments/assets/385df708-de6e-40fd-8999-f1a549de3bfd)

Hasil TF-IDF menunjukkan representasi numerik dari genre genre film berdasarkan pentingnya setiap genre dalam tiap film tersebut. Setiap barisnya mewakili title film, dan kolom adalah genre. Nilai di tiap sel adalah bobot TF-IDF yang menandakan seberapa relevan genre tersebut untuk film itu, makin besar nilainya, maka semakin kahs genre tersebut bagi film. Misalnya Pada film Demetrius and the Glafiators (1954) memiliki nilai 1.000 pada genre Drama, artinya genre itu sangat spesifik dan penting untuk dilm tersebut, sementara genre lain bernilai 0 yanag berarti tidak terkait. Ini bantu sistem merekomendasikan film dengan genre mirip berdasarkan bobot kata yang dihitung. 

- pada ratings_df dilakukan pemetaan userId dan movieId ke dalam indeks numerik (user_id_to_index, movie_id_to_index)
  Mengubah userId dan movieId menjadi indeks numerik yang terurut agar lebih mudah diproses oleh model. Kode akan mengambil daftar userId dan movieId yang unik dari dataset, kemudian membuat dua dictionary untuk masing masing, yaitu memetakan userId dan movieId asli ke indeks numerik serta sebaliknya
  
- Melakukan penambahan kolom user_index dan movie_index ke ratings_df
  isinya indeks numerik hasil pemetaan dari userId dan movieId. Ini agar model yang menggunakan embedding layer dapat menerima input berupa indeks numerik bukan Id asli, sehingga proses training dan prediksi menjadi lebih terstruktur
  
- melakukan random data (ratings_df.sample(frac=1)
  mengacak urutan baris dalam dataset ratings_df. sample(frac=1) akan mengambil 100% data tapi dalam urutan yang diacak.Tujuannya untuk menghindari bias urutan data.
  
- Melakukan normalisasi nilai rating ((val - min_raing) / (max_rating - min_rating))
  Kolom rating dinormalisasi ke rentang 0 - 1 menggunakan metode min max scaling agar bisa langsung digunakan untuk training model di RecommenderNet
  
- Melakukan pembagian dataset menjadi data latih dan data validasi dengan rasio 80:20
  
## Modeling
Tahapan ini membahas mengenai model sisten rekomendasi yang Anda buat untuk menyelesaikan permasalahan. Sajikan top-N recommendation sebagai output.

Modeling yang dilakukan pada project ini adalah content based filtering dan collaborative filtering. 

### Content Based Filtering
Content Based Filtering menggunakan hasil TF-IDF Vectorizer dan cosine similarity

#### Cosine Similarity
Berfungsi mengukur seberapa mirip dua buah vektor, misal dua film berdasarkan genrenya dengan menghitung sudut kosinus antar vektor tersebut. Dalam content based filtering, cosine similarity digunakan untuk menemukan film yang paling mirip berdasarkan fitur tersebut. Semakin nilai cosine mendekati 1, maka semakin mirip kedua item tersebut. 

![image](https://github.com/user-attachments/assets/be56f368-0bce-44a3-aeab-1b8508de8fcb)

Hasil cosine similarity menunjukkan seberapa mirip genre antar film berdasarkan representasi teks genre mereka ayng telah diproses menggunakan TF-IDF Vectorizer. Misalnya Honeydripper (2007) memiliki nilai 1.000 terhadap film Nixon (1995) yang menunjukkan bahwa film ini sangat mirip dari segi genre. Film seperti Turner & Hooch (1989) memiliki nilai 0.0 terhadap film-film lain menunjukkan bahwa genrenya tidak memiliki kemiripan sama sekali dengan yang dibandingkannya. 

Ketika dilakukan percobaan untuk merekomendasikan film kepada user yang menyukai Transformers: Age of Extinction (2014), berikut ini merupakan 5 film yang direkomendasikan. Kelimanya memiliki genre yang serupa, yaitu Action, Adventure, dan Sci-fi.

![image](https://github.com/user-attachments/assets/a275d7a7-4ccb-46de-8b3a-aa9f4ff5b637)

Hasil ini bisa digunakan dalam content based filtering untuk merekomendasikan film yang genrenya mirip dengan film yang disukai pengguna. Misal jika pengguna menyukai Honeydripper (2007) maka film dengan nilai cosine similarity tinggi seperti Nixon (1995) bisa direkoemndasikan. 

Kelebihan content based filtering
- Tidak tergantung pada pengguna lain, rekomendasinya berdasarkan atribut item, cocok untuk pengguna baru
- Konsisten dengan minat pengguna karena merekomendasikan film yang mirip dengan yang disukai sebelumnya, jadi hasil lebih relevan
- Asalkan data item seperti genre ada, sistem tetap bisa bekerja (tidak terpengaruh sparsity)

Kekurangan content based filtering
- Kurang bervariasi karena cenderung merekomendasikan item yang terlalu mirip
- Membutuhkan data konten yang lengkap karena jika informasi genre atau atribut lain tidak lengkap sistem jadi tidak akurat
- Sulit menangkap pola kompleks karena tidak mempertimbangkan interaksi antar pengguna yang bisa memberi informasi tambahan

### Collaborative Filtering
Pendekatan collaborative filtering bekerja dengan memetakan setiap pengguna dan film ke dalam indeks numerik yang unik. Setelah data dinormalisasi dan dibagi menjadi data latih dan data test, model dikembangkan menggunakan arsitektur embedding, di mana tiap pengguna dan film direpresentasikan sebagai vektor dalam ruang berdimensi tertentu. Model kemudian mempelajari hubungan antara pengguna dan film melalui operasi dot product pada vektor embedding untuk prediksi rating yang diberikan. Tujuan metode ini adalah menangkap pola preferensi pengguna berdasarkan interaksi historis mereka dengan film tanpa perlu info konten dari film itu sendiri. 

Hasil yang direkomendasikan kepada user 541 adalah sebagai berikut.

![image](https://github.com/user-attachments/assets/761c7b2d-7ecd-497b-bc63-df30f40b661c)

Pengguna ini memiliki preferensi terhadap film dengan genre Sci-fi, Thriller, dan Drama. Hal ini terlihat dari daftar film dengan rating tertinggi yang diberikan user mayoritas bergenre sci-fi dan thriller seperti Blade Runner, Gattaca, dan Dark City. 
Sistem rekomendasi berhasil menangkap pola preferensi tersebut, karena sebagain besar film dalam daftar Top 10 rekomendasi juga mengandung elemen Sci-fi, Thriller, atau Drama, seperti Memories (1995), Interstate 60 (2002), dan Never Let Me Go (2010). Sehingga dapat disimpulkan bahwa model rekomendasi ini telah bekerja cukup baik dan dapat melakukan personalisasi, karena rekomendasinya konsisten dengan selera pengguna berdasarkan histori rating sebelumnya. 

Kelebihan collaborative filtering
- Tidak membutuhkan data konten film karena sistem hanya bergantung pada interaksi seperti rating antar pengguna dan item
- Mampu menangkap pola kompleks karena bisa menemukan hubungan tidak terduga antara film dan pengguna berdasarkan kesamaan perilaku
- Mempertimbangkan kebiasaan banyak pengguna lain dengan preferensi serupa

Kekurangan collaborative filtering
- Cold start problem, dia tidak bisa memberikan rekoemndasi yang baik untuk pengguna baru atau film baru karena belum ada cukup data interaksi
- Jika data interaksi sangat sedikit model sulit belajar karena terlalu banyak missing values
- Membutuhkan sumber daya lebih besar saat jumlah pengguna atau item sangat besar
  
## Evaluation

Metrik yang digunakan adalah Root Mean Squared Error (RMSE), yaitu metrik untuk mengukur seberapa jauh prediksi model dari nilai sebenarnya. RMSE menghitung akar kuadrat dari rata-rata kuadrat selisih antara nilai prediksi dan nilai aktual. Nilai RMSE yang lebih kecil menunjukkan bahwa model memberikan prediksi yang lebih akurat, karena error prediksi lebih kecil. RMSE sering digunakan utnuk masalah regresi dan sistem rekomendasi. Berikut merupakan formula untuk RMSE:

![image](https://github.com/user-attachments/assets/1df0c67b-272f-4d9e-9abd-e9f5cfebf632)

Hasil evaluasi model sebagai berikut

![image](https://github.com/user-attachments/assets/869249c2-1035-4bda-b273-5914104de283)

Grafik menunjukkan performa model berdasarkan metrik RMSE pada data pelatihan dan pengujian selama 100 epoch. Terlihat bahwa RMSE pada data train mengalami penurunan tajam pada awal pelatihan dan kemudian stabil di sekitar 0.19, menandakan bahwa model mampu belajar dengan baik dari data latih. Sementara itu, RMSE pada data test juga menurun di awal, namun cenderung stagnan dan berfluktuasi di kisaran 0.20 hingga 0.205. Secara keseluruhan, model menunjukkan performa cukup baik.


