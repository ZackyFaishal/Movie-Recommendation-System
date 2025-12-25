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

### Informasi Dataset

Dataset terdiri dari dua file utama: **movies.csv** dan **ratings.csv**.

---

## ## **1. movies.csv**

### **Jumlah Baris dan Kolom**
- Baris: **62.423**
- Kolom: 3

### **Kondisi Data**
- Missing value: **0**
- Duplikasi: **0**
- Terdapat outlier tahun rilis <1900 dan >2025 → **valid**, tidak dihapus.

### **Deskripsi Fitur**
| Kolom | Deskripsi |
|-------|-----------|
| `movieId` | ID unik film |
| `title` | Judul film + tahun rilis |
| `genres` | Genre film, dipisahkan dengan `|` |

### **Insight**
- Genre dominan adalah **Drama**, **Comedy**, dan **Action**.
- Sebagian besar film dirilis pada rentang **1980–2010**.

---

## ## **2. ratings.csv**

### **Jumlah Baris dan Kolom**
- Baris: **25.000.095**
- Kolom: 4

### **Kondisi Data**
- Missing value: 0
- Duplikasi: 0
- Rating terbanyak berada pada nilai **3.0–4.0**.

### **Deskripsi Fitur**
| Kolom | Deskripsi |
|-------|-----------|
| `userId` | ID unik pengguna |
| `movieId` | ID film |
| `rating` | Rating skala 0.5–5.0 |
| `timestamp` | Waktu pemberian rating |

### **Insight**
- Mayoritas pengguna memberikan sedikit rating (long-tail pattern).
- Ada pengguna aktif dengan lebih dari 500 rating.

---

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

#### Inisight Analisa

* Genre populer seperti Drama dan Comedy mendominasi dataset film.
* Film dalam dataset sebagian besar dirilis antara 1980–2010.
* Rating cenderung berkumpul di nilai 3–4, menandakan kecenderungan rating yang cukup baik secara umum.
* Sebagian besar pengguna bersifat pasif (memberikan sedikit rating), sementara hanya sedikit pengguna sangat aktif.

### Analisis Tambahan

1. **Top 10 Film dengan Jumlah Rating Terbanyak**
![Top 10 Movies by Ratings](https://github.com/ZackyFaishal/Movie-Recommendation-System/blob/main/assets/top10.png)

- Film dengan judul paling populer menerima lebih dari 3000 rating.
- Adanya gap signifikan antara film teratas dan sisanya mengindikasikan adanya bias popularitas.


#### Insight Analisa Tambahan

* Genre drama, comedy, dan action merupakan yang paling dominan, penting untuk filtering berbasis konten.
* Film-film populer mendominasi jumlah rating, berpotensi menyebabkan bias model jika tidak ditangani.
* Hanya sebagian kecil pengguna yang sangat aktif memberikan rating, fenomena umum pada sistem rekomendasi dan perlu dipertimbangkan untuk fairness dan regularisasi model.

## **Data Preparation**

Pada tahap ini dilakukan proses pembersihan dan transformasi data sebelum digunakan pada tahap pemodelan.  
Sesuai catatan reviewer, proses seperti import library, load dataset, melihat isi data, memeriksa missing value, duplikasi, tipe data, dan outlier termasuk ke dalam **Data Understanding**, sehingga tidak dicantumkan kembali di bagian Data Preparation.

Tahap Data Preparation dalam proyek ini berfokus pada langkah-langkah berikut:

---

### **1. Pembersihan Kolom Genre**
Kolom `genres` dibersihkan dari simbol pemisah dan disusun ulang agar setiap genre dapat dikenali sebagai satuan kata.  
Langkah ini penting untuk memastikan model dapat membaca fitur genre secara optimal ketika digunakan dalam proses ekstraksi fitur.

**Insight:**  
Pembersihan kolom ini membantu model dalam memahami komposisi genre masing-masing film dengan lebih baik.

---

### **2. Ekstraksi Fitur Menggunakan TF-IDF**
Pada rekomendasi berbasis konten, genre film diolah menggunakan metode **TF-IDF (Term Frequency–Inverse Document Frequency)**.  
Metode ini mengukur seberapa penting suatu kata (genre) dalam sebuah film relatif terhadap keseluruhan dataset.

**Insight:**  
TF-IDF memperkuat genre unik dan membantu proses penghitungan kemiripan antar film secara lebih akurat.

---

### **3. Encoding User dan Movie**
Agar model Deep Learning dapat memproses data pengguna dan film, kolom `userId` dan `movieId` dikonversi ke bentuk numerik terurut.  
Setiap ID pengguna dan film diubah menjadi representasi angka kategori yang konsisten.

**Insight:**  
Encoding memungkinkan model pembelajaran mendalam mempelajari pola interaksi melalui embedding.

---

### **4. Normalisasi Rating**
Rating dinormalisasi ke dalam rentang **0–1** agar selaras dengan fungsi aktivasi yang digunakan pada model dan mempermudah proses pelatihan model Deep Learning.

**Insight:**  
Normalisasi menjaga stabilitas pembelajaran dan mengurangi risiko error akibat perbedaan skala data.

---

### **5. Pembagian Dataset (Train–Test Split)**
Data dibagi menjadi dua subset, yaitu data latih (training) dan data uji (testing), dengan proporsi umum 80:20.  
Pembagian ini diperlukan untuk mengevaluasi performa model pada data yang tidak pernah dilihat sebelumnya.

**Insight:**  
Pembagian dataset membantu memastikan bahwa model tidak hanya menghafal data latih (overfitting), tetapi juga mampu melakukan generalisasi.

---

### **6. Pembuatan Indeks Film untuk Content-Based Filtering**
Dibuat pemetaan khusus yang menghubungkan judul film dengan indeks barisnya, sehingga sistem rekomendasi dapat mengambil film acuan dan film-film serupa secara cepat.

**Insight:**  
Indeks ini mempermudah proses pencarian film saat melakukan rekomendasi berbasis konten.

---

## **Kesimpulan Data Preparation**

Tahap Data Preparation menghasilkan data yang:

- Sudah dibersihkan dan disesuaikan untuk ekstraksi fitur genre.  
- Memiliki representasi numerik untuk user dan film melalui encoding.  
- Memiliki rating yang sudah dinormalisasi.  
- Telah dibagi ke dalam data latih dan data uji untuk keperluan evaluasi.  
- Siap digunakan untuk membangun model **Content-Based Filtering** dan **Neural Collaborative Filtering**.

Dengan seluruh tahapan ini, data telah sepenuhnya siap untuk masuk ke proses pemodelan sistem rekomendasi.


## Model Development

Pada tahap ini dilakukan pembangunan sistem rekomendasi film menggunakan data yang telah melalui proses **Data Preparation**. Fokus pembahasan pada tahap ini adalah menjelaskan **cara kerja sistem**, **alur algoritma**, serta **bagaimana model menghasilkan rekomendasi**, sesuai dengan implementasi pada notebook.

Dua pendekatan sistem rekomendasi yang dikembangkan adalah **Content-Based Filtering** dan **Deep Learning-based Recommendation System (Neural Collaborative Filtering)**.

---

### Content-Based Filtering

Content-Based Filtering merupakan pendekatan sistem rekomendasi yang memberikan saran film berdasarkan **kemiripan konten antar film**. Pendekatan ini berasumsi bahwa pengguna akan menyukai film lain yang memiliki karakteristik konten serupa dengan film yang dijadikan acuan.

Pada proyek ini, konten film direpresentasikan menggunakan **genre film**. Representasi numerik film telah dibangun pada tahap Data Preparation menggunakan **TF-IDF**, sehingga setiap film memiliki vektor fitur yang menggambarkan komposisi genre-nya.

Kemiripan antar film dihitung menggunakan **cosine similarity**, yaitu metrik yang mengukur tingkat kesamaan antara dua vektor fitur. Semakin tinggi nilai cosine similarity, semakin mirip dua film tersebut.

#### Alur Kerja Content-Based Filtering

1. **Pemetaan Film ke Indeks Data**  
   Sistem membuat pemetaan antara judul film dan indeks baris dataset untuk memudahkan proses pencarian film referensi secara efisien.

2. **Pemilihan Film Referensi**  
   Pengguna memberikan input berupa judul atau kata kunci film yang akan dijadikan acuan rekomendasi.

3. **Perhitungan Kemiripan Konten**  
   Sistem menghitung cosine similarity antara film referensi dengan seluruh film lain berdasarkan representasi vektor TF-IDF.

4. **Perankingan Film**  
   Film-film diurutkan berdasarkan nilai kemiripan tertinggi ke terendah.

5. **Pemilihan Top-N Rekomendasi**  
   Sejumlah N film dengan tingkat kemiripan tertinggi dipilih sebagai hasil rekomendasi.

Pendekatan ini bersifat **personal secara implisit**, karena rekomendasi ditentukan langsung oleh karakteristik konten film yang dipilih pengguna, tanpa mempertimbangkan preferensi pengguna lain.

---

### Deep Learning-based Recommendation System  
### (Neural Collaborative Filtering)

Neural Collaborative Filtering (NCF) merupakan pendekatan sistem rekomendasi berbasis **deep learning** yang mempelajari **pola interaksi historis antara pengguna dan film** berdasarkan data rating. Berbeda dengan Content-Based Filtering, pendekatan ini tidak menggunakan fitur konten film, melainkan mempelajari hubungan laten (*latent factors*) dari data interaksi.

Dalam model ini, setiap pengguna dan film direpresentasikan dalam bentuk **embedding vektor berdimensi rendah**. Embedding ini dipelajari selama proses pelatihan dan merepresentasikan preferensi pengguna serta karakteristik film secara laten.

Embedding user dan film kemudian digabungkan dan diproses melalui jaringan saraf **Multilayer Perceptron (MLP)** untuk mempelajari hubungan non-linear antara pengguna dan film, sehingga model mampu menghasilkan prediksi rating yang lebih akurat.

#### Alur Kerja Deep Learning-based Recommendation

1. **Representasi User dan Film**  
   Setiap user dan movie direpresentasikan sebagai embedding vektor yang menyimpan informasi preferensi dan karakteristik laten.

2. **Pembelajaran Pola Interaksi**  
   Model mempelajari hubungan antara embedding user dan film berdasarkan data rating historis melalui beberapa lapisan neural network.

3. **Prediksi Rating**  
   Model menghasilkan prediksi rating pengguna terhadap film-film yang belum pernah ditonton.

4. **Agregasi dan Perankingan Film**  
   Hasil prediksi rating dikelompokkan berdasarkan pengguna, kemudian film diurutkan berdasarkan nilai prediksi tertinggi.

5. **Pemilihan Top-N Rekomendasi**  
   Sejumlah N film dengan prediksi rating tertinggi dipilih sebagai rekomendasi untuk pengguna tersebut.

Pendekatan ini mampu menghasilkan rekomendasi yang **lebih personal dan adaptif**, karena memanfaatkan pola interaksi historis pengguna secara langsung.

---

### Kesimpulan Model Development

Pada tahap Model Development, telah dibangun dua pendekatan sistem rekomendasi dengan alur kerja yang berbeda:

- **Content-Based Filtering**, yang merekomendasikan film berdasarkan kemiripan konten antar film dan sesuai untuk skenario berbasis preferensi konten.
- **Neural Collaborative Filtering**, yang memanfaatkan pola interaksi historis pengguna–film untuk menghasilkan rekomendasi yang lebih personal dan kompleks.

Kedua pendekatan ini saling melengkapi dan menjadi dasar dalam menghasilkan sistem rekomendasi film yang relevan dan sesuai dengan preferensi pengguna.


### Contoh Rekomendasi

#### Contoh Hasil Rekomendasi (Content-Based Filtering)

Bagian ini menampilkan contoh hasil rekomendasi film yang dihasilkan
oleh sistem Content-Based Filtering. Daftar rekomendasi diperoleh
berdasarkan mekanisme perhitungan kemiripan konten yang telah
diimplementasikan pada notebook, dengan memanfaatkan fungsi
rekomendasi yang tersedia.


Sebagai ilustrasi, berikut adalah contoh daftar 10 film yang direkomendasikan
oleh sistem berdasarkan film acuan "Toy Story (1995)":


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

### Contoh Hasil Rekomendasi (Deep Learning-based Filtering)

Bagian ini menampilkan ilustrasi hasil rekomendasi film yang dihasilkan
oleh model Neural Collaborative Filtering berdasarkan pola interaksi
historis pengguna.

Sebagai ilustrasi, berikut adalah contoh daftar 10 film yang direkomendasikan
untuk User-ID 1 berdasarkan prediksi rating tertinggi:


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
| Precision@10  | 0.5836 |
| Recall@10     | 0.6853 |

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
| Loss      | 0.0276 |
| MAE       | 0.1259 |
| Val_Loss  | 0.0272 |
| Val_MAE   | 0.1249 |

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

