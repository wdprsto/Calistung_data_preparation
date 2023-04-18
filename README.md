# Calistung Data Preparation

## Latar Belakang
Berdasarkan hasil mentoring yang dilakukan bersama salah satu Capstone Advisor di Bangkit 2022, terdapat beberapa masukan yang kami peroleh dalam mengembangkan model,
1.  Carilah implementasi serupa yang sudah dipublikasikan sehingga kita dapat memperoleh model dengan hasil akurasi terbaik.
2.  Tambahkan dataset. Seperti yang kita ketahui, dataset Kaggle A-Z dan MNIST 0-9 memiliki distribusi yang tidak merata, atau biasa dikenal sebagai imbalanced dataset. Untuk itu, kita dapat menambahkan data dengan cara menambahkan tulisan tangan kita sendiri ke dalam data yang sudah ada. Di samping itu, dataset Kaggle dan MNIST bersumber dari tulisan tangan anak di negara Eropa/Amerika, sehingga mungkin saja terdapat perbedaan cara penulisan huruf/angka, seperti pada huruf Z tanpa strip ditengah, 1 tanpa serif, dan lainnya. Untuk itu, dibuatlah sebuah notebook yang mampu mengekstrak karakter tulisan tangan yang telah dengan sengaja dituliskan dalam dokumen berukuran A4.

## Batasan Masalah
1.  Tulisan tangan ditulis menggunakan *pentab* oleh penulis, di dokumen berukuran A4.
2.  Tiap-tiap karakter yang berhasil diekstrak akan ditambahkan ke dataset Kaggle Alphabet A-Z atau MNIST 0-9 sesuai dengan kelasnya masing-masing.

## Metodologi
Proses ekstraksi ini menerapkan proses pengolahan citra dan segmentasi citra menggunakan library OpenCV. Tahapan pengolahan citra merupakan tahapan yang bertujuan untuk menormalisasi gambar serta membuat karakter lebih menonjol sebelum dilakukan prediksi. Praproses citra terdiri dari tahapan grayscaling, thresholding, dilate, dan edge detection. Tahapan ini dapat divisualisasikan secara bertahap sehingga prosesnya tampak seperti pada Gambar berikut.

![](assets/2-visualisasi%20praproses.PNG)

Pada tahap segmentasi, citra yang telah diproses akan di-crop pada bagian konten. Segmentasi dilakukan pada level karakter. Karakter-karakter yang terdapat dalam sebuah gambar akan dilokalisasi melalui proses contour detection dengan fungsi findContours yang dilanjutkan dengan penerapan fungsi boundingRect untuk menghasilkan bounding rectangle berdasarkan kontur yang terdeteksi. Kotak pembatas kemudian digunakan terhadap citra asli untuk mengekstrak piksel karakter pada posisi yang bersesuaian. Visualisasi dari pendeteksian kotak pembatas pada tahapan ini tampak pada Gambar berikut.

![](assets/3-hasil%20segmentasi.PNG)

## Hasil dan Pembahasan
Pada dataset gabungan, dilakukan penambahan data tulisan tangan penulis agar model dapat mempelajari data dunia nyata yang menjadi input dalam aplikasi Capstone Project Bangkit. Jumlah data tulisan tangan yang ditambahkan pada dataset dirincikan pada Tabel berikut.

| Karakter | Label | Jumlah |
|:--------:|:-----:|:------:|
|     0    |   0   |   524  |
|     1    |   1   |   391  |
|     2    |   2   |   379  |
|     3    |   3   |   352  |
|     4    |   4   |   335  |
|     5    |   5   |   763  |
|     6    |   6   |   341  |
|     7    |   7   |   661  |
|     8    |   8   |   748  |
|     9    |   9   |   383  |
|     A    |   10  |   274  |
|     B    |   11  |   343  |
|     C    |   12  |   301  |
|     D    |   13  |   627  |
|     E    |   14  |   315  |
|     F    |   15  |   276  |
|     G    |   16  |   298  |
|     H    |   17  |   337  |
|     I    |   18  |   472  |
|     J    |   19  |   307  |
|     K    |   20  |   331  |
|     L    |   21  |   320  |
|     M    |   22  |   427  |
|     N    |   23  |   388  |
|     O    |   24  |   554  |
|     P    |   25  |   281  |
|     Q    |   26  |   313  |
|     R    |   27  |   369  |
|     S    |   28  |   336  |
|     T    |   29  |   383  |
|     U    |   30  |   332  |
|     V    |   31  |   353  |
|     W    |   32  |   335  |
|     X    |   33  |   283  |
|     Y    |   34  |   321  |
|     Z    |   35  |   428  |

Adapun sampel data yang ditambahkan, ialah sebagai berikut:
![](assets/1-dataset%20tambahan.png)