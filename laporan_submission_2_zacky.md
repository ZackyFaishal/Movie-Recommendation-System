# **LAPORAN MOVIE RECOMENDATION PROJECT** 
## *By : Zacky Faishal Abror*

# Project Overview

Sistem rekomendasi merupakan elemen krusial dalam platform digital modern seperti **Netflix**, **YouTube**, dan **Amazon**, yang berfungsi untuk memandu pengguna dalam menemukan konten yang relevan di tengah lautan pilihan. Proyek ini dikembangkan menggunakan **Movie Recommendation System Dataset**, yang mencakup data komprehensif dari pengguna, judul film dan rating film. Dataset ini memuat informasi detail film (judul, tahun rilis, genre) serta data rating yang diberikan oleh pengguna.

Tujuan utama dari proyek ini adalah untuk membangun dan mengevaluasi sistem rekomendasi film yang efektif dan personal. Dalam proyek ini, dua pendekatan utama dikembangkan:

- **Content-Based Filtering**: Menganalisis fitur film, khususnya genre, untuk merekomendasikan film yang memiliki kemiripan konten dengan yang pernah disukai pengguna.
- **Deep Learning (Collaborative Filtering)**: Memanfaatkan arsitektur **Multi-Layer Perceptron (MLP)** untuk mempelajari pola tersembunyi (_latent patterns_) dari interaksi pengguna-film berdasarkan data rating historis.

Dengan menerapkan kedua metode ini, sistem diharapkan dapat memberikan rekomendasi yang tidak hanya relevan berdasarkan konten, tetapi juga mampu menangkap preferensi unik pengguna, sehingga menciptakan pengalaman menonton yang lebih memuaskan dan personal.

## Referensi
> [Resnick, P., & Varian, H. R. (1997). *Recommender Systems*. Communications of the ACM, 40(3), 56–58.](https://dl.acm.org/doi/10.1145/245108.245121)  
> [Koren, Y., Bell, R., & Volinsky, C. (2009). *Matrix Factorization Techniques for Recommender Systems*. Computer, 42(8), 30–37.](https://doi.org/10.1109/MC.2009.263)  
> [Aggarwal, C. C. (2016). *Recommender Systems: The Textbook*. Springer.](https://link.springer.com/book/10.1007/978-3-319-29659-3)

---

## Dataset
https://www.kaggle.com/datasets/parasharmanas/movie-recommendation-system

## Business Understanding

### Problem Statements

1. **Pengguna Kesulitan Menemukan Film yang Sesuai**  
   Dengan puluhan ribu judul film yang tersedia di berbagai platform, pengguna seringkali menghadapi *paradox of choice*, yaitu kesulitan dalam memilih film yang benar-benar sesuai dengan selera mereka.

2. **Rekomendasi yang Diberikan Kurang Personal**  
   Banyak sistem rekomendasi yang bersifat umum dan tidak cukup mampu menangkap preferensi unik setiap individu, sehingga film yang disarankan seringkali tidak relevan.

3. **Potensi Menurunnya Keterlibatan Pengguna**  
   Ketika pengguna terus-menerus kesulitan menemukan tontonan yang menarik, hal ini dapat menyebabkan kelelahan dalam memilih (*decision fatigue*) dan pada akhirnya menurunkan minat serta keterlibatan mereka pada platform.

---

## Goals

- **Mengembangkan Sistem Rekomendasi Film yang Relevan**  
  Membangun sebuah sistem yang dapat secara efektif menyarankan film-film yang sangat sesuai dengan preferensi dan riwayat tontonan pengguna.

- **Meningkatkan Personalisasi Rekomendasi**  
  Memberikan saran yang lebih personal dengan menganalisis data rating historis dan fitur konten film untuk menangkap selera unik setiap pengguna.

- **Memudahkan Proses Penemuan Konten**  
  Membantu pengguna mengatasi banyaknya pilihan dengan menyajikan daftar film yang lebih terkurasi dan relevan, sehingga memudahkan mereka dalam menemukan tontonan berikutnya.

---

## Solution Statements

- **Content-Based Filtering**  
  Menerapkan *Content-Based Filtering* untuk merekomendasikan film berdasarkan kemiripan konten. Metode ini akan menganalisis genre film untuk menyarankan judul-judul lain dengan genre serupa yang kemungkinan besar akan disukai oleh pengguna.

- **Deep Learning: Collaborative Filtering**  
  Mengembangkan model *Deep Learning* dengan pendekatan *Collaborative Filtering* untuk menangkap preferensi pengguna yang lebih kompleks. Dengan menggunakan *embedding* untuk pengguna dan film, model ini dapat mengidentifikasi pola laten dari data rating historis dan memberikan rekomendasi yang lebih akurat dan tidak terduga, melampaui sekadar kemiripan genre.


## Data Understanding

---

### Deskripsi Dataset

Dataset yang digunakan dalam proyek ini adalah **Movie Recommendation System Dataset**. Dataset ini berisi data film dan rating yang diberikan oleh pengguna, yang sangat relevan untuk membangun **recommender system**. Data ini mencerminkan interaksi pengguna terhadap berbagai film, menjadikannya cocok untuk penelitian dan pengembangan sistem rekomendasi film.

---

#### **Deskripsi Variabel**

##### movies.csv

| Column Name | Description |
| :---------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `movieId` | **ID Film**: Nomor unik yang ditetapkan untuk setiap film. (Numerik) |
| `title` | **Judul Film**: Judul film beserta tahun rilisnya. (Nominal) |
| `genres` | **Genre**: Kategori genre film, dipisahkan oleh karakter `|`. (Nominal) |

##### ratings.csv

| Column Name | Description |
| :---------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `userId` | **ID Pengguna**: Nomor unik yang ditetapkan untuk setiap pengguna. (Numerik) |
| `movieId` | **ID Film**: Nomor unik yang ditetapkan untuk setiap film yang diberi rating. (Numerik) |
| `rating` | **Rating**: Rating yang diberikan oleh pengguna kepada film, dalam skala tertentu (misalnya 0.5 hingga 5.0). (Numerik) |
| `timestamp` | **Stempel Waktu**: Waktu ketika rating dibuat. (Numerik, biasanya dalam format Unix timestamp) |


## Eksplorasi Data dan Visualisasi 

Eksplorasi Data berupa visualisasi dilakukan untuk memahami karakteristik data secara univariat serta menggali informasi tambahan terkait pola-pola utama dalam dataset film dan rating pengguna.

### Analisis

Analisis dilakukan terhadap beberapa variabel penting berikut:

1. **Distribusi Genre Film**
![Genre Distribution](https://github.com/ZackyFaishal/Movie-Recommendation-System/blob/main/assets/distribusi_genre.png)

- Genre film didominasi oleh beberapa genre populer seperti Drama, Comedy, dan Action.
- Banyak film memiliki lebih dari satu genre; genre diformat dalam bentuk string dan kemudian diekstrak menjadi daftar untuk eksplorasi frekuensi.
- Visualisasi menunjukkan dominasi beberapa genre tertentu yang dapat digunakan dalam model content-based filtering.

2. **Distribusi Tahun Rilis Film**
![Release Year Distribution](https://github.com/ZackyFaishal/Movie-Recommendation-System/blob/main/assets/distribusi_tahun.png)

- Sebagian besar film dirilis antara tahun 1980 hingga 2010, dengan puncak sekitar tahun 2000.
- Terlihat adanya nilai ekstrem seperti tahun sebelum 1900 atau setelah 2025, yang perlu ditangani dalam proses pembersihan data.
- Distribusi miring ke kiri menunjukkan kecenderungan lebih banyak film lama dibandingkan yang sangat baru dalam dataset.

3. **Distribusi Nilai Rating**
![Rating Distribution](https://github.com/ZackyFaishal/Movie-Recommendation-System/blob/main/assets/distribusi_rating.png)

- Rating yang paling sering diberikan adalah 3.0 dan 4.0.
- Sangat sedikit rating di bawah 1.0 atau maksimal 5.0, namun distribusi menunjukkan bahwa pengguna cenderung memberikan rating menengah ke atas.
- Tidak ada rating kosong (0), karena hanya interaksi eksplisit yang dimasukkan ke dataset.

4. **Jumlah Rating per Pengguna**
![User Rating Count Distribution](https://github.com/ZackyFaishal/Movie-Recommendation-System/blob/main/assets/distribusi_rating_pengguna.png)

- Mayoritas pengguna memberikan kurang dari 50 rating.
- Terdapat outlier yaitu pengguna yang sangat aktif memberikan lebih dari 500 rating.
- Distribusi ini menggambarkan pola long-tail umum pada sistem rekomendasi, di mana sebagian kecil pengguna memberikan kontribusi besar.

#### Kesimpulan Analisa

* Genre populer seperti Drama dan Comedy mendominasi dataset film.
* Film dalam dataset sebagian besar dirilis antara 1980–2010.
* Rating cenderung berkumpul di nilai 3–4, menandakan kecenderungan rating yang cukup baik secara umum.
* Sebagian besar pengguna bersifat pasif (memberikan sedikit rating), sementara hanya sedikit pengguna sangat aktif.

### Analisis Tambahan

1. **Top 10 Film dengan Jumlah Rating Terbanyak**
![Top 10 Movies by Ratings](https://github.com/ZackyFaishal/Movie-Recommendation-System/blob/main/assets/top10.png)

- Film dengan judul paling populer menerima lebih dari 3000 rating.
- Adanya gap signifikan antara film teratas dan sisanya mengindikasikan adanya bias popularitas.


#### Kesimpulan Analisa Tambahan

* Genre drama, comedy, dan action merupakan yang paling dominan, penting untuk filtering berbasis konten.
* Film-film populer mendominasi jumlah rating, berpotensi menyebabkan bias model jika tidak ditangani.
* Hanya sebagian kecil pengguna yang sangat aktif memberikan rating, fenomena umum pada sistem rekomendasi dan perlu dipertimbangkan untuk fairness dan regularisasi model.

## Persiapan Data

Tahap persiapan data bertujuan untuk memastikan bahwa data yang digunakan dalam sistem rekomendasi film sudah bersih, terstruktur, dan siap dianalisis lebih lanjut.

#### Langkah-langkah Persiapan Data

Berikut ini adalah langkah-langkah yang dilakukan dalam proses persiapan data:

1. **Import Library**
   - Melakukan import library yang dibutuhkan seperti `pandas`, `matplotlib.pyplot`, dan `seaborn` untuk membantu dalam manipulasi dan visualisasi data.

2. **Load Dataset**
   - Mengimpor dua file dataset utama yaitu:
     - `movies.csv` berisi informasi tentang film.
     - `ratings.csv` berisi informasi rating yang diberikan oleh pengguna terhadap film.

3. **Melihat Sekilas Data**
   - Melihat beberapa baris pertama dari masing-masing dataset (`head()`) untuk memahami struktur kolom dan jenis data yang tersedia.

4. **Mengecek Ukuran Dataset**
   - Menghitung jumlah baris dan kolom dalam dataset untuk mengetahui ukuran dataset yang akan digunakan.

5. **Mengecek Missing Values**
   - Melakukan pengecekan apakah terdapat nilai kosong (missing values) dalam kedua dataset.

6. **Mengecek Data Duplikat**
   - Memastikan tidak ada data ganda (duplikat) yang dapat menyebabkan bias dalam proses analisis dan modeling.

7. **Memeriksa Tipe Data**
   - Memastikan tipe data pada kolom-kolom penting seperti `movieId`, `userId`, dan `rating` sudah sesuai (numerik) agar tidak terjadi error saat proses analisis dan modeling.

8. **Memeriksa Outlier**
- Melakukan pengecekan apakah ada nilai yang sangat berbeda dari nilai normal
![outlier picture](https://github.com/ZackyFaishal/Movie-Recommendation-System/blob/main/assets/outlier.png)
Hasil dan Analisis:<br>
Visualisasi box plot akan menunjukkan beberapa titik di sisi kiri, yang merupakan film-film yang dirilis sebelum tahun 1900.

Kesimpulan: Titik-titik ini adalah outlier statistik, tetapi bukan data yang salah. Ini adalah film-film historis yang valid. Untuk pembuatan model rekomendasi, data ini tidak perlu dihapus, namun kita perlu sadar akan keberadaannya.

9. **Penggabungan Dataset**
- Menggabungkan kedua dataset (`movies.csv` dan `ratings.csv`) berdasarkan MOVIE ID

### Kesimpulan Persiapan Data

Dari hasil proses persiapan data yang telah dilakukan, dapat disimpulkan bahwa:

- Dataset **movies** dan **ratings** berhasil dimuat dengan baik.
- Tidak ditemukan missing values maupun duplikasi yang signifikan dalam kedua dataset.
- Struktur data dan tipe data sudah sesuai dengan kebutuhan analisis berikutnya.
- Dataset telah siap digunakan untuk tahap selanjutnya, yaitu **Data Understanding** dan **Modeling Sistem Rekomendasi**.


## Model Development

Pada tahap ini dilakukan pembangunan model sistem rekomendasi menggunakan dataset yang sudah dipersiapkan sebelumnya. Model dikembangkan dengan dua pendekatan utama yaitu **Content-Based Filtering** dan **Deep Learning-based Recommendation System**.

### Content-Based Filtering

Pendekatan ini merekomendasikan film kepada user berdasarkan kemiripan konten film. Sistem akan menganalisis atribut film seperti genre dan judul untuk menemukan film yang mirip dengan film yang sebelumnya disukai oleh pengguna.

#### Langkah-langkah Content-Based Filtering:

1. **Ekstraksi Fitur Teks**
   - Menggabungkan berbagai fitur film seperti genre dan judul menjadi satu representasi teks.
   - Proses ini dilakukan agar model bisa memahami informasi konten setiap film.

2. **Transformasi Fitur Teks**
   - Menggunakan metode TF-IDF untuk mengubah representasi teks menjadi format numerik (vector) sehingga bisa dihitung kemiripannya.

3. **Penghitungan Similaritas**
   - Menggunakan cosine similarity untuk mengukur seberapa mirip satu film dengan film lainnya.

4. **Membangun Fungsi Rekomendasi**
   - Membuat fungsi rekomendasi yang dapat menerima input berupa judul film, lalu mengembalikan daftar film-film lain yang memiliki tingkat kemiripan konten paling tinggi.

### Deep Learning-based Recommendation System (Model Neural Collaborative Filtering)

Selain metode content-based, digunakan juga pendekatan deep learning untuk meningkatkan akurasi rekomendasi dengan memanfaatkan data interaksi pengguna.

Model deep learning yang dibangun adalah **Neural Collaborative Filtering (NCF)** berbasis **Multilayer Perceptron (MLP)**.

#### Langkah-langkah Deep Learning-based Recommendation:

1. **Encoding User dan Movie**
   - Mengonversi `userId` dan `movieId` menjadi format numerik menggunakan teknik encoding agar dapat diproses oleh neural network.

2. **Membentuk Embedding Layer**
   - Membangun embedding layer untuk user dan movie.
   - Setiap user dan movie direpresentasikan dalam vektor berdimensi tetap yang dipelajari selama training.

3. **Membangun Arsitektur Neural Network**
   - Menggunakan beberapa hidden layer dengan aktivasi ReLU.
   - Dropout digunakan untuk mengurangi risiko overfitting.

4. **Menyiapkan Target dan Split Data**
   - Target dari model adalah rating dari user terhadap movie.
   - Dataset dibagi menjadi training set dan test set (biasanya 80:20) agar bisa dilakukan evaluasi model.

5. **Proses Training**
   - Model dilatih menggunakan optimizer Adam dan loss function Mean Squared Error (MSE).
   - Proses training dilakukan dalam beberapa epoch hingga model dapat mempelajari pola interaksi antara user dan movie.

6. **Melakukan Prediksi**
   - Model yang sudah dilatih digunakan untuk memprediksi rating user terhadap seluruh film yang belum pernah ditonton oleh user tersebut.
   - Prediksi diurutkan berdasarkan skor tertinggi.

7. **Membuat Fungsi Rekomendasi**
   - Menghasilkan daftar top-N rekomendasi film untuk setiap user berdasarkan hasil prediksi dari model.

#### Kesimpulan Model Development

Pada tahap pengembangan model ini, telah dibangun dua jenis sistem rekomendasi:

- **Content-Based Filtering** yang menghasilkan rekomendasi berdasarkan kemiripan konten film.
- **Deep Learning-based Recommendation (Neural Collaborative Filtering)** yang memanfaatkan pola interaksi historis antara user dan film.

Kedua pendekatan ini diharapkan dapat saling melengkapi dalam meningkatkan akurasi dan relevansi rekomendasi film kepada pengguna.

### Contoh Top 10 Rekomendasi

#### Contoh Top 10 Content-Based Filtering

Mencari rekomendasi film yang mirip dengan judul **"Toy Story (1995)"**:

| MovieId | Title                           |
| ------  | ------------------------------- |
| 3114    | Toy Story 2 (1999)              |
| 78499   | Toy Story 3 (2010)              |
| 2571    | Matrix, The (1999)              |
| 356     | Forrest Gump (1994)             |
| 318     | Shawshank Redemption, The (1994)|
| 593     | Silence of the Lambs, The (1991)|
| 595     | Fargo (1996)                    |
| 2858    | American Beauty (1999)          |
| 1270    | Back to the Future (1985)       |
| 47      | Seven (a.k.a. Se7en) (1995)     |

*Hasil di atas menunjukkan daftar 10 film dengan tingkat kemiripan konten tertinggi dibandingkan dengan film "Toy Story (1995)".*

---

#### Contoh Top 10 Deep Learning-based Filtering

Mencari rekomendasi film untuk **User-ID 1** berdasarkan model deep learning:

| MovieId | Title                                 |
| ------  | ------------------------------------- |
| 1193    | One Flew Over the Cuckoo's Nest (1975)|
| 2571    | Matrix, The (1999)                    |
| 2858    | American Beauty (1999)                |
| 2959    | Fight Club (1999)                     |
| 4993    | Lord of the Rings: The Fellowship...  |
| 5952    | Lord of the Rings: The Two Towers...  |
| 7153    | Lord of the Rings: The Return of...   |
| 4995    | Gladiator (2000)                      |
| 8529    | Pirates of the Caribbean: The...      |
| 79132   | Inception (2010)                      |

*Rekomendasi di atas adalah daftar 10 film dengan prediksi rating tertinggi yang belum pernah ditonton oleh User-ID 1, menurut model Deep Learning.*

---

### Kesimpulan Hasil Rekomendasi

Dua pendekatan rekomendasi yang telah dibuat menunjukkan hasil yang relevan dengan preferensi pengguna:

- **Content-Based Filtering** merekomendasikan film-film yang secara konten mirip dengan film referensi.
- **Deep Learning-based Filtering** memberikan prediksi film terbaik berdasarkan pola interaksi user sebelumnya.

Kombinasi kedua pendekatan ini diharapkan dapat meningkatkan kepuasan pengguna dalam mendapatkan rekomendasi film yang sesuai dengan selera mereka.

## Evaluation Model

### Evaluasi Content-Based Filtering

Evaluasi dilakukan untuk mengukur performa sistem rekomendasi berbasis konten (*Content-Based Filtering*) yang telah dibangun menggunakan pendekatan TF-IDF.

Berbeda dengan pendekatan deep learning, metode ini merekomendasikan film berdasarkan kemiripan konten antar film (seperti genre dan judul film).

Metrik yang digunakan dalam evaluasi ini adalah **Precision@K** dan **Recall@K**, dua metrik populer dalam evaluasi sistem rekomendasi top-K.

- **Precision@K**: Mengukur proporsi film relevan dalam K rekomendasi teratas.
- **Recall@K**: Mengukur seberapa banyak film relevan yang berhasil direkomendasikan dibandingkan dengan seluruh film relevan.

Evaluasi dilakukan dengan tahapan berikut:

- Mengelompokkan hasil rekomendasi berdasarkan user.
- Mengambil top-K film dengan skor similarity tertinggi untuk setiap user.
- Menggunakan ambang threshold tertentu pada rating untuk menentukan relevansi.

---

#### Hasil Evaluasi Content-Based Filtering

##### Top-K Rekomendasi untuk K = 10

| Metrik        | Nilai  |
| :------------ | :----- |
| Precision@10  | 0.1316 |
| Recall@10     | 0.5469 |

Nilai **Precision@10 sebesar 0.1316** menunjukkan bahwa sekitar **13,16%** dari 10 film teratas yang direkomendasikan adalah benar-benar relevan untuk pengguna.  
Sedangkan **Recall@10 sebesar 0.5469** menunjukkan bahwa sistem berhasil mencakup sekitar **54,69%** dari total film relevan.

Hasil ini memperlihatkan bahwa sistem cukup baik dalam mencakup film relevan (recall cukup tinggi), meskipun masih perlu peningkatan dalam presisi rekomendasi.

---

### Evaluasi Deep Learning-based Filtering (Neural Collaborative Filtering)

Evaluasi sistem rekomendasi berbasis deep learning dilakukan untuk mengetahui seberapa baik model dalam memprediksi rating user terhadap film.

Metrik evaluasi yang digunakan adalah:

- **Loss (Mean Squared Error - MSE)**: Mengukur rata-rata error kuadrat antara prediksi dan nilai sebenarnya.
- **MAE (Mean Absolute Error)**: Mengukur rata-rata selisih absolut antara nilai prediksi dan nilai aktual.

Selain itu, performa pada data validasi juga dievaluasi menggunakan **val_loss** dan **val_mae**.

---

#### Hasil Evaluasi Deep Learning

##### Hasil Pelatihan Selama 3 Epoch

| Metrik    | Nilai  |
| :-------- | :----- |
| Loss      | 0.0339 |
| MAE       | 0.1007 |
| Val_Loss  | 0.1524 |
| Val_MAE   | 0.2737 |

Model menunjukkan **loss training yang rendah (0.0339)** dan **MAE sebesar 0.1007**, yang menandakan bahwa model cukup baik dalam memprediksi rating user.

Meskipun terdapat gap antara performa training dan validation (val_loss lebih tinggi), hal ini masih dalam batas wajar dan menunjukkan model generalisasi yang cukup baik.

---

### Dampak terhadap Business Understanding

**Menjawab Problem Statement**:

- Sistem rekomendasi membantu pengguna menemukan film sesuai preferensi mereka.
- Mengurangi kebingungan pengguna dalam memilih film dari koleksi yang sangat besar.

**Mencapai Goals**:

- Menghasilkan rekomendasi film yang relevan dan personal.
- Mengurangi effort pengguna dalam mencari film.
- Memanfaatkan data historis interaksi user dengan baik.

**Dampak terhadap Solution Statement**:

- Model deep learning berhasil mempelajari pola rating pengguna terhadap berbagai film.
- Sistem mampu memberikan rekomendasi dengan relevansi tinggi, baik dari segi kemiripan konten maupun histori interaksi.
- Menghasilkan sistem rekomendasi hybrid (gabungan content-based dan deep learning) yang meningkatkan kualitas personalisasi.

---

## Kesimpulan

Proyek ini berhasil membangun dua pendekatan sistem rekomendasi film:

- **Content-Based Filtering**, yang fokus pada kemiripan konten antar film.
- **Deep Learning-based Filtering (Neural Collaborative Filtering)**, yang fokus pada pola interaksi user dan film.

Hasil evaluasi menunjukkan performa yang cukup baik, baik dalam hal recall untuk content-based maupun dalam prediksi rating untuk deep learning.

**Saran untuk Pengembangan Lebih Lanjut:**

- Menambahkan fitur tambahan seperti genre, direktur, atau ringkasan film.
- Melakukan hyperparameter tuning untuk meningkatkan performa model deep learning.
- Mengembangkan sistem rekomendasi hybrid untuk memadukan kelebihan kedua pendekatan.
- Menggunakan data interaksi pengguna yang lebih banyak untuk meningkatkan akurasi.

Dengan pengembangan lanjutan, diharapkan sistem ini mampu memberikan rekomendasi film yang semakin relevan dan personal sesuai kebutuhan pengguna.

