Topik : CBR dan NLP

- Identifikasi persoalan praktis yang menurut anda perlu diselesaikan melalui penelitian :
  
  Pada saat bertanya di komunitas terbuka seperti stack overflow dll, perlu menunggu waktu beberapa saat sampai ada user lain yang menjawab pertanyaan tersebut, padahal mungkin di database sudah terdapat pertanyaan serupa diikuti jawaban-jawaban yang sudah verified. oleh karena itu, dilakukan penelitian yang dapat mencari pertanyaan yang serupa dari database untuk kemudian ditampilkan jawaban yang sudah verified tanpa perlu menunggu user lain menjawab pertanyaan tersebut. diperlukan juga sistem yang dapat menjawab multiple question yang masih relevan dengan pertanyaan di awal.
Contoh multiple question :
![hasil yang diharapkan](https://github.com/aulakharisma/riset-if/assets/74193184/b758f131-42ff-4825-b8a7-ccc9b6d15bc1)

- metode yang digunakan di penelitian :

  bayesian semantic sebagai identifikasi per kata dan cbr sebagai pengambil keputusan. Bayesian semantic digunakan karena terdapat sebuah penelitian yang menunjukkan bahwa penggunaan metode bayes dalam semantic menghasilkan akurasi yang cukup tinggi.
  ![image](https://github.com/aulakharisma/riset-if/assets/74193184/1649c29b-38d0-4f14-9804-5267194bc076)

  proses retrieve pertanyaan menggunakan semantic-bayesian graph

  cbr digunakan agar lebih efisien, karena dengan data yang sedikit dapat menghasilkan akurasi yang besar. Metode CBR yang digunakan yaitu fuzzy logic. berikut merupakan cycle dalam case based reasoning.

  ![image](https://github.com/aulakharisma/riset-if/assets/74193184/0393de9d-8b8e-4a79-9452-2126a6c568b6)

  terdapat 4 fase yaitu retrieve, reuse, revise dan retain

- research questions :
  1. bagaimana metode bayes dan cbr digunakan di penelitian ini?
  2. bagaimana mendapatkan data yang digunakan untuk penelitian ?
   
- Uraikan beberapa teori yang menurut anda mempunyai keterkaitan dengan topik yang telah diidentifikasi (untuk menunjang aspek Tinjauan Kepustakaan pada saat pembuatan proposal nanti)
  teori terdapat pada jurnal :
Chergui, Oumayma; Begdouri, Ahlame; Groux-Leclet, Dominique (2019). Integrating a Bayesian semantic similarity approach into CBR for knowledge reuse in Community Question Answering. Knowledge-Based Systems, (), 104919–. doi:10.1016/j.knosys.2019.104919 https://sci-hub.hkvisa.net/10.1016/j.knosys.2019.104919

  Kim, Han-joon; Kim, Jiyun; Kim, Jinseog; Lim, Pureum (2018). Towards perfect text classification with Wikipedia-based semantic Naïve Bayes learning. Neurocomputing, (), S0925231218308282–. doi:10.1016/j.neucom.2018.07.002 https://sci-hub.hkvisa.net/10.1016/j.neucom.2018.07.002
