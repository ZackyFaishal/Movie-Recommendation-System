# 🎬 Movie Recommendation Project  

## 📄 Deskripsi Proyek  
Proyek **Movie Recommendation Project** ini bertujuan untuk membangun **sistem rekomendasi film** berbasis:
- **Content-Based Filtering** dengan TF-IDF pada fitur **genre** film
- **Deep Learning** dengan pendekatan embedding pengguna dan film  

Proyek ini menggunakan dataset **movies.csv** dan **ratings.csv** yang mencakup:
- Informasi film (judul, genre, tahun rilis)
- Rating yang diberikan pengguna pada film  

---

## 🚀 Tujuan Utama  
- Menyediakan rekomendasi film yang relevan untuk pengguna berdasarkan preferensi genre  
- Menggunakan pembelajaran mendalam untuk memprediksi rating pengguna terhadap film yang belum pernah mereka tonton  
- Mengevaluasi performa sistem rekomendasi menggunakan metrik standar seperti **Precision@K**, **Recall@K**, dan **MAE**  

---

## 📊 Tahapan Proyek  

### 1. **Data Understanding**
- **movies.csv** berisi informasi film (`movieId`, `title`, `genres`)
- **ratings.csv** berisi informasi rating pengguna (`userId`, `movieId`, `rating`, `timestamp`)

### 2. **Data Cleaning**
- Tidak ada missing value dan duplikasi data  
- Ekstraksi **tahun rilis** film dari kolom `title`  
- Deteksi film dengan genre “(no genres listed)”  

### 3. **Exploratory Data Analysis (EDA)**
- Analisis distribusi **genre** film  
- Analisis distribusi **tahun rilis**  
- Distribusi **rating** per pengguna dan per film  
- Visualisasi Top 10 film dengan rating terbanyak  

### 4. **Content-Based Filtering**
- Menggunakan **TF-IDF Vectorizer** pada kolom `genres`  
- Menghitung kemiripan antar film dengan **Cosine Similarity**  
- Fungsi rekomendasi berdasarkan kata kunci judul film  

### 5. **Deep Learning Model**
- **Embedding Layer** untuk `userId` dan `movieId`  
- **Concatenate Layer** diikuti **Dense Layers** untuk memprediksi rating  
- Normalisasi rating ke [0–1]  
- Split data 80% train dan 20% test  
- **Optimizer:** Adam, **Loss:** MSE, **Metric:** MAE  

### 6. **Evaluasi Model**
- **Content-Based Filtering:** Precision@K & Recall@K  
- **Deep Learning:** MAE (Mean Absolute Error)  
- Visualisasi Training vs Validation Loss dan MAE  

---
