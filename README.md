# Perbandingan Performa Collaborative Filtering dan Hybrid Filtering untuk Sistem Rekomendasi Film #
Dalam era digital saat ini, industri hiburan mengalami perkembangan pesat, khususnya dalam penyediaan layanan streaming film. Untuk meningkatkan pengalaman pengguna, sistem rekomendasi menjadi elemen kunci yang memastikan pengguna mendapatkan konten yang sesuai dengan preferensi mereka. Dua pendekatan utama yang digunakan dalam sistem rekomendasi adalah collaborative filtering (CF) dan hybrid filtering (HF).
Meskipun collaborative filtering telah berhasil dalam merekomendasikan item berdasarkan perilaku pengguna serupa, masih ada beberapa kendala, seperti cold start problem dan sparsity. Di sisi lain, hybrid filtering menggabungkan berbagai metode untuk mengatasi kelemahan masing-masing, menciptakan potensi untuk meningkatkan akurasi rekomendasi.
Penelitian ini bertujuan untuk membandingkan efektivitas algoritma collaborative filtering dan hybrid filtering dalam konteks sistem rekomendasi film. Beberapa aspek yang menjadi fokus penelitian melibatkan akurasi rekomendasi, penanganan masalah cold start, dan kinerja sistem pada dataset yang memiliki tingkat sparsity yang berbeda.

## Collaborative Filtering(CF) ##
Collaborative Filtering merupakan pendekatan yang berdasarkan pada pola rating yang diberikan oleh user terhadap film yang sudah ditonton. CF memiliki 2 fase utama untuk menghasilkan rekomendasi, yaitu similaritas film, dan prediksi rating pada film. berikut merupakan alur dalam pendekatan CF. <br>
![image](https://github.com/aulakharisma/riset-if/assets/74193184/cc12bea7-81ee-4a9c-8a3f-a31c009ea709)
### 1. Menghitung Similaritas Film ###
similaritas film merupakan pendekatan untuk menghitung similaritas antara film berdasarkan rating pada film. algoritma yang diimplementasikan adalah adjusted-cosine similarity, fungsi umum yang digunakan di pendekatan collaborative filtering yaitu : <br>
![image](https://github.com/aulakharisma/riset-if/assets/74193184/9d0c7784-d13f-4ea8-9ed8-a316c7d6f562) <br>
Input    : Data Rating Film<br>
Proses   :
   - menghitung rata-rata rating dari masing-masing user
   - mendapatkan list user yang sudah memberi ratinng pada film
   - implementasi algoritma ahjusted-cosine similarity untuk mendapatkan similaritas antar film
     
<br>Output    : matrix similaritas film

### 2. Prediksi Rating dan Rekomendasi Film ###
prediksi rating adalah tahap untuk memprediksi rating yang telah diberikan oleh user target untuk film yang belum diberi rating. hasil prediksi ini kemudian diurutkan secara descending untuk mengahasilkan list film yang direkomendasikan.
prediksi rating film untuk user target dapat dihitung dengan rumus berikut : <br>
![image](https://github.com/aulakharisma/riset-if/assets/74193184/09e51708-fb70-484b-be7a-2f196277d447) <br>
   Input      : matrix similaritas film <br>
   Proses     : <br>
   - Tentukan jumlah ݇k untuk menentukan ukuran film yang serupa.
   - Menciptakan daftar ݇k film yang memiliki kesamaan tertinggi dengan setiap film.
   - implementasikan fungsi prediksi (persamaan nomor 2) untuk menghitung peringkat film yang belum dinilai

   <br>Output : Prediksi rating film

## Hybrid Filtering ##
hybrid filtering merupakan pndekatan yang menambahkan manfaat Content based filtering pada pendekatan cillaborative filtering. oleh karena itu, pendekatan ini juga membutuhkan data film dan proses tambahan.
Pendekatan Hybrid filtering memiliki 4 fase utama untuk menghasilkan rekomendasi film, yaitu text processing, term weighting, movie clustering, dan collaborative filtering. proses tersebut digambarkan dalam digram berikut. <br>
![image](https://github.com/aulakharisma/riset-if/assets/74193184/20628d27-769d-4dd7-9ce8-7460eb7419ab) <br>
### 1. Text Prepprocessing ###
Pra-pemrosesan teks adalah teknik untuk mengubah teks tak terstruktur menjadi bentuk yang lebih mudah dibaca untuk merepresentasikan film. disini akan diterapkan pra-pemrosesan teks untuk mengubah data film menjadi daftar istilah dalam setiap film. Data film mencakup judul dan sinopsis film. disini akan digunakan Porter Stemmer karena merupakan algoritma stemming yang paling umum digunakan untuk bahasa Inggris. <br>
Input     : data judul film dan sinopsis <br>
Proses    : <br>
   - case folding, mengubah semua huruf menjadi huruf kecil(lowercase)
   - tokenisasi, memisahkan per kata, dari data yang sudah diolah diproses case folding.
   - filtering, menghapus stop words (cth: kata sambung, dan kata yang kurang memiliki makna) dari hasil tokenisasi, sehingga yang tersisa hanya kata yang bermakna
   - stemming, mendapat akar setiap kata dalam himpunan teks yang telah difilter.

<br>Output    : Daftar frasa atau istilah yang terdapat dalam setiap film.
### 2. Pembobotan TF-IDF ###
Term weighting adalah teknik yang umum digunakan dalam studi informasi retrieval yang menghitung bobot setiap istilah dalam setiap dokumen. disini akan diterapkan teknik pembobotan TF-IDF untuk menghitung bobot setiap istilah dalam setiap film berdasarkan daftar istilah dalam setiap film. <br>
input     : Daftar frasa atau istilah yang terdapat dalam setiap film <br>
proses    : 
   - Term Frequency (TF), mengukur seberapa sering suatu kata kunci muncul dalam suatu item atau dokumen. contoh, Jika kata "movie" muncul 5 kali dalam suatu ulasan film yang terdiri dari 100 kata, maka TF untuk kata "movie" dalam ulasan tersebut adalah 0.05.
   - Inverse Document Frequency (IDF),  mengukur seberapa unik atau jarang suatu kata kunci muncul di seluruh dataset. contoh, Jika ada 1000 dokumen dalam dataset dan kata "movie" muncul di 100 dokumen, maka IDF untuk kata "movie" adalah 
log(1000/100)
   - TF-IDF, produk dari TF dan IDF dan digunakan untuk memberikan bobot pada suatu kata kunci dalam suatu dokumen terkait dengan keseluruhan dataset. contoh, Jika TF untuk kata "movie" dalam suatu dokumen adalah 0.05 dan IDF untuk kata "movie" adalah 2, maka TF-IDF untuk kata "movie" dalam dokumen tersebut adalah 0.1.
     
<br>Output     : matrix pembobotan istilah
### 3. K-Means Clustering ###
Clustering adalah teknik yang mengelompokkan data yang dianggap mirip ke dalam klaster yang sama. Proses ini diperlukan karena ukuran data film yang besar dapat menyebabkan masalah skalabilitas. disini akan diterapkan teknik pengelompokan K-Means untuk mengelompokkan film berdasarkan matriks bobot istilah-film. Teknik K-Means mengelompokkan data berdasarkan jaraknya ke centroid.<br>
Input     : Jumlah kluster, matrix pembobotan istilah <br>
proses    :
   - Inisialisasi nilai C centroid secara acak
   - Hitung jarak setiap film ke setiap titik centroid. Tentukan setiap film ke centroid terdekatnya.
   - Perbarui setiap centroid dengan mengambil rata-rata dari poin-poin film yang diassign ke klaster terkait.
   - ulangi step 2 dan 3
     
<br>output   : C cluster

### Collaborative Filtering ###
Daftar rekomendasi film dalam pendekatan berbasis Hybrid dihasilkan dengan menerapkan pendekatan berbasis Collaborative Filtering (sebagaimana yang sudah dijelaskan sebelumnya). Perlu diperhatikan bahwa kesamaan film dihitung hanya antara film-film dalam klaster yang sama.

## Dataset ##
Dataset MovieLens yang diambil dari kaggle.com yang kemudian dilakukan filtrasi hanya kepada film yang memiliki judul dan sinopsis yang lengkap. data saat ini yang digunakan berisi 671 user, 3290 film, dan 42023 rating<br>
https://www.kaggle.com/datasets/snehal1409/movielens

