# Rancang Bangun E-commerce dengan Algoritma Hybrid Filtering Sebagai Sistem Rekomendasi #
Kendala utama yang dihadapi dalam pengembangan e-commerce saat ini adalah kurangnya personalisasi dalam memberikan rekomendasi kepada pengguna. Penelitian ini bertujuan untuk merancang dan membangun sebuah platform e-commerce yang dilengkapi dengan sistem rekomendasi menggunakan algoritma hybrid filtering. Dalam konteks ini, algoritma hybrid filtering menggabungkan dua pendekatan utama, yaitu collaborative filtering dan content-based filtering, untuk meningkatkan akurasi dan relevansi rekomendasi produk kepada pengguna. Penelitian ini berfokus pada pengembangan sistem rekomendasi yang dapat memahami preferensi pengguna berdasarkan perilaku sebelumnya dan karakteristik produk. Dengan merancang dan membangun e-commerce yang menggunakan algoritma hybrid filtering, diharapkan dapat meningkatkan pengalaman belanja online pengguna, mempercepat proses pencarian produk yang relevan, dan secara efektif meningkatkan konversi penjualan di platform e-commerce tersebut.

## Metode Penelitian ##
Hybrid Filtering, yaitu model rekomendasi yang menggabungkan algoritma content based filtering dan collaborative filtering untuk saling melengkapi masing-masing kekurangan. Dimana kekurangan model content based filtering adalah keterbatasan rekomendasi hanya pada konten saja, dalam hal ini kita sebut produk, sementara algoritma collaborative filtering kurang efektif jika digunakan pada user baru karena sistem tidak memiliki data dari user tersebut sebelumnya (cold start). Algoritma hybrid filtering sudah banyak digunakan oleh platform-platform besar, seperti amazon, netflix, spotify, dll.

Model hybrid yang digunakan mengacu pada paper yang ditulis oleh Anand Shanker pada tahun 2020 yang mengajukan model hybrid filtering baru dengan menggunakan 6 block. Yaitu Profile construction, content similarity finder, neighbor finder, items generator, items weight generator, dan final recommendation block. Setiap blok mempunyai fungsi khusus dan semuanya bekerja sama satu sama lain. Berikut merupakan cara kerja dari blok-blok ini:

### *Profile construction Block* (PC) ###
Blok ini membuat profil untuk setiap pengguna dan item. Dalam studi kasus ecommerce, setiap penjual menyediakan keywords untuk menggambarkan properti barang yang akan dijual di website e-commerce. Blok PC membuat profil item berdasarkan konten dengan kata kunci yang ditetapkan yang disediakan oleh penjual. Setelah profil item dibuat, blok PC menggunakan profil item ini untuk membuat profil pengguna. Blok PC menemukan semua item yang digunakan oleh pengguna dan kemudian membuat profil pengguna dari kata kunci di profil item tersebut. Blok ini juga menyimpan peringkat item yang berbeda yang diberikan oleh pengguna target di profilnya.

### *Content Similarity Finder Block* (CSF) ###
Blok CSF menemukan pengguna serupa lainnya yang memiliki minat serupa dengan pengguna target berdasarkan profil pengguna yang dibuat oleh blok PC(a). Blok ini mencari kesamaan berdasarkan kosinus antara pengguna target dan pengguna lain menggunakan persamaan 1.
![image](https://github.com/aulakharisma/riset-if/assets/74193184/deaf867a-eb1d-4517-8ddb-4fdf509fa7cf)

### *Neighbour Finder Block* (NF) ###
Blok ini mengekstrak peringkat yang diberikan oleh pengguna target ke item berbeda dengan bantuan blok PC. Blok NF kemudian menemukan kesamaan pengguna target dengan pengguna lain yang tersedia di website berdasarkan rating. Blok NF menggunakan rumus korelasi Pearson untuk mencari kesamaan antar pengguna, sebagaimana ditunjukkan pada persamaan 2.
![image](https://github.com/aulakharisma/riset-if/assets/74193184/d45c4ddb-1418-43f7-b7d1-a08556015614)
Blok NF dengan bantuan blok CSF, menemukan semua pengguna serupa yang memiliki kesamaan konten dengan pengguna target lebih besar dari ambang Kesamaan Konten, yang disediakan oleh pakar domain. Setelah pengguna serupa dipilih, blok NF kemudian menemukan kesamaan peringkat berdasarkan peringkat antara pengguna target dan pengguna serupa ini, dan memilih semua pengguna yang memiliki kesamaan peringkat lebih besar dari ambang batas Kesamaan Peringkat, yang sekali lagi disediakan oleh pakar domain. Akhirnya, blok NF menghasilkan daftar tetangga potensial dari pengguna target.

### *Items Generator Block* (IG) ###
Blok IG mengambil masukan dari blok NF dan memilih semua tetangga dari pengguna target. IG kemudian memilih semua item yang dinilai oleh tetangga, yang tidak dinilai oleh pengguna target. Ini menciptakan daftar item yang mungkin direkomendasikan kepada pengguna target.

### *Items Weight Generator Block* (IWG) ###
Blok IWG menerima semua item yang mungkin direkomendasikan kepada pengguna target dari blok IG dan kemudian menghitung dua jenis bobot untuk masing-masing item tersebut. Pertama, ia menghitung bobot spesifik item pengguna target yang dipersonalisasi, lalu menghitung bobot item umum. Nilai bobot spesifik item pengguna target yang dipersonalisasi berbeda untuk setiap pasangan item pengguna dan dihitung menggunakan persamaan 3.
![image](https://github.com/aulakharisma/riset-if/assets/74193184/216518e5-9bba-41a9-ace9-6faf014fb202)

### *Final Recomendation Block* (FR) ###
Blok ini menghasilkan rekomendasi akhir untuk pengguna target. Dibutuhkan input dari blok PC, IG dan IWG. Blok FR memprediksi peringkat semua item yang dihasilkan oleh blok IG. Pertama, ia menemukan kesamaan kosinus yang disesuaikan (Sim) dari item yang sudah dinilai oleh pengguna target dengan item yang dihasilkan oleh blok IG menggunakan persamaan 5.
![image](https://github.com/aulakharisma/riset-if/assets/74193184/80672089-243e-4c04-8648-cf947421e7ea)
