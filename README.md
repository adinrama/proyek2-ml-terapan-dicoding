# Laporan Proyek Machine Learning - Adin Rama Ariyanto Putra

## Project Overview

Business Intelligence (BI) adalah rangkaian teknologi dan proses yang memungkinkan organisasi mengubah data mentah menjadi informasi yang bermakna untuk pengambilan keputusan bisnis. Dengan semakin banyaknya solusi BI yang tersedia di pasar, organisasi sering menghadapi kesulitan dalam memilih perangkat lunak yang paling sesuai dengan kebutuhan spesifik mereka. 

Banyak organisasi menghadapi tantangan dalam memilih perangkat lunak BI yang tepat dari sekian banyak pilihan yang tersedia. Proses pemilihan manual membutuhkan waktu dan sumber daya yang signifikan, dan organisasi mungkin tidak memiliki pengetahuan mendalam tentang semua opsi yang tersedia. Selain itu, para pengambil keputusan sering kesulitan dalam mengevaluasi perangkat lunak mana yang akan memberikan nilai terbaik berdasarkan kebutuhan spesifik mereka.

Salah satu pendekatan yang dapat digunakan untuk menentukan perangkat lunak berdasarkan kebutuhan yang spesifik adalah dengan cara membuat sistem rekomendasi. Dataset yang digunakan berisi informasi tentang berbagai produk perangkat lunak BI dengan fitur-fitur mereka seperti kategori, industri yang dilayani, skala bisnis yang didukung, jenis pengguna, dll. Data ini dapat dimanfaatkan untuk membangun sistem rekomendasi yang membantu organisasi menemukan perangkat lunak BI yang paling sesuai dengan preferensi dan kebutuhan mereka.

## Business Understanding

### Problem Statements

- Bagaimana kita dapat memprediksi rating perangkat lunak BI berdasarkan karakteristik dan kebutuhan pengguna?
- Bagaimana kita dapat merekomendasikan perangkat lunak BI yang paling sesuai dengan kebutuhan spesifik organisasi?

### Goals (Tujuan)

- Membangun sistem rekomendasi collaborative filtering yang dapat memprediksi rating yang mungkin diberikan pengguna pada produk BI yang belum mereka gunakan.
- Menyediakan rekomendasi perangkat lunak BI yang personal dan relevan berdasarkan kebutuhan dan preferensi organisasi.
- Meminimalkan kesalahan prediksi rating untuk meningkatkan akurasi rekomendasi.

## Data Understanding

Data yang digunakan pada proyek ini adalah [BI Software Recommendation Dataset](https://www.kaggle.com/datasets/devsubhash/bi-software-recommendation-dataset) yang berasal dari Kaggle. Pada pengerjaan proyek ini, hanya akan menggunakan dataset ini sehingga tidak perlu menambahkan data lain atau melakukan penggabungan dataset lagi. Selain itu, dataset ini juga cukup bersih sehingga tidak terlalu banyak memerlukan proses data cleaning.

Dataset yang digunakan terdiri dari 100 baris dan 11 kolom. Kolom disini terdiri dari fitur numerik dan non-numerik. Fitur numerik terdiri dari *product_id* dan *rating*. Sedangkan fitur non-numerik terdiri dari *category*, *industry*, *Business_scale*, *user_type*, *no_of_users*, *deployment*, *OS*, *mobile_apps*, *pricing*, *rating*, dan *user_profile*.

### Variabel-variabel pada BI Software Recommendation dataset adalah sebagai berikut:
- product_id: id produk.
- category: jenis alat BI.
- industry: industri di mana alat BI ini dapat digunakan karena tidak semua alat BI melayani semua industri.
- Business_scale: ukuran bisnis yang dilayani oleh alat BI, yaitu kecil, menengah, besar.
- user_type: jenis pengguna bisnis atau analis dengan keterampilan ilmu data (Tidak semua alat BI mudah digunakan dan tidak semua alat memiliki kemampuan pemrosesan data yang kuat).
- no_of_users: jenis penggunaan lisensi pengguna, yaitu tunggal atau ganda.
- deployment: informasi tentang bagaimana alat BI dapat digunakan yaitu Cloud, On-premise atau Hybrid.
- OS: jenis persyaratan sistem operasi untuk instalasi alat.
- mobile_apps: menunjukkan apakah alat tersebut memiliki versi seluler untuk visualisasi data.
- pricing: menunjukkan apakah alat tersebut open source, versi freemium, edisi perusahaan.
- rating: peringkat alat pengguna pada skala 5.0.

### Tahapan yang dilakukan saat eksplorasi data (EDA):
- Mengecek informasi dan deskripsi statistik data.
- Mengecek missing value, invalid data, maupun data duplikat.
- Melakukan analisis univariate dan multivariate.
- Melakukan visualisasi selama tahap EDA.

## Data Preparation
- Memuat data secara melalui file csv.
- Melakukan check terhadap deskripsi statistik data untuk menarik insight data secara keseluruhan.
- Melakukan check terhadap informasi dari data, apakah terdapat missing value, invalid data, maupun data duplikat.
- Melakukan analisis univariate dan multivariate.
- Melihat nilai unik di setiap kolom/fitur.
- Melakukan one-hot-encoding untuk fitur kategori. Hal ini bertujuan untuk mengubah fitur menjadi numerik agar dapat diproses oleh model machine learning.
- Membuat surrogate user_id untuk simulasi collaborative filtering. Nantinya ini akan menjadi id pengguna.
- Melakukan mapping terhadap user_profile ke user_id numerik.
- Mengonversi product_id menjadi item_id numerik agar lebih efisien untuk model.
- Melakukan split data menjadi set training dan testing.
- Melakukan normalisasi rating untuk meningkatkan kinerja model.

## Modeling
Pada bagian ini penulis hanya menggunakan satu pendekatan untuk membangun sistem rekomendasi, yakni menggunakan **Collaborative Filtering**. Cara ini dipilih karena collaborative filtering bekerja berdasarkan asumsi bahwa pengguna dengan preferensi serupa di masa lalu cenderung menyukai item yang serupa di masa depan. Dalam konteks perangkat lunak BI, organisasi dengan karakteristik serupa (industri, skala bisnis, jenis pengguna) cenderung memiliki kebutuhan dan preferensi yang mirip. Pendekatan ini mampu menangkap pola implisit yang mungkin tidak tertangkap oleh fitur eksplisit. Pendekatan ini juga dapat mengatasi sebagian dari masalah *"cold start"* untuk pengguna baru. Pengguna baru dapat langsung mendapatkan rekomendasi berdasarkan profil mereka tanpa harus memberikan rating terlebih dahulu.

![image](https://github.com/user-attachments/assets/bbd1fe45-c798-41ea-9f39-da9f0ee3fdd8)

![image](https://github.com/user-attachments/assets/a846901c-9f30-4c68-8119-34855f04a346)

![image](https://github.com/user-attachments/assets/2209e2ca-0582-4eb0-b0fa-78a28d9cfffb)

## Evaluation
Pada bagian ini menggunakan 2 metrik evaluasi, yakni Mean Absoulte Error (MAE) dan Root Mean Squared Error (RMSE). Kedua metrik ini berfungsi untuk menilai seberapa baik model dapat memprediksi data latih berdasarkan nilai error.

- **Mean Absoulte Error (MAE)**: untuk mengukur seberapa besar rata-rata kesalahan absolut antara nilai prediksi dan nilai aktual dalam suatu model.

![image](https://github.com/user-attachments/assets/c85d506b-1b27-44b2-befb-1bbaac526602)

![image](https://github.com/user-attachments/assets/8ae91607-f841-4402-8b8b-6779455017ff)

- **Root Mean Squared Error (RMSE)**: untuk mengukur seberapa jauh nilai yang dihasilkan sebuah model dari nilai aktual, dengan memberikan penalti lebih besar pada kesalahan yang besar.

![image](https://github.com/user-attachments/assets/8bcec62e-f13c-4ffc-9ebd-458f327fc20c)
 
## Uji Coba Sampel
![image](https://github.com/user-attachments/assets/799bc4e8-9396-492c-83bd-37bd74b0fe14)

![image](https://github.com/user-attachments/assets/1d169f0b-0185-4116-9dc8-5270a7f42108)

![image](https://github.com/user-attachments/assets/57267312-a101-4432-ac28-53ec700d15dd)

## Ringkasan Akhir Evaluasi
- Root Mean Squared Error (RMSE): 0.7634
- Mean Absolute Error (MAE): 0.3365

Kemampuan model dalam memprediksi rating:
- Model memiliki akurasi yang cukup baik namun masih perlu ditingkatkan

Kategori perangkat lunak dengan prediksi terbaik:
- Data Discovery: RMSE = 0.0039
- Performance Metrics: RMSE = 0.2000
- Benchmarking: RMSE = 0.2115

Kategori perangkat lunak dengan prediksi terburuk:
- Predictive Analytics: RMSE = 1.0031
- Ad-hoc reporting: RMSE = 1.0042
- Embedded BI: RMSE = 1.0046

### Rekomendasi Personal:
Sistem dapat merekomendasikan perangkat lunak BI berdasarkan profil pengguna yang dibentuk dari kombinasi industri, skala bisnis, dan jenis pengguna.

### Rekomendasi Item Serupa:
Sistem juga dapat menemukan perangkat lunak BI yang serupa berdasarkan fitur latennya, yang berguna untuk memperkenalkan alternatif kepada pengguna.
