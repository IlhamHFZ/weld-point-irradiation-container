# Pengembangan *Image Processing* untuk Penentuan Posisi *Welding Torch* Berdasarkan Ketebalan Kapsul Iradiasi
Penelitian ini tentang pemanfaatan *image processing* pengaplikasian pengukuran dan penentuan titik las berdasarkan ketebalan untuk kapsul iradiasi. Ketepatan dalam proses pengelasan bagian kapsul iradiasi sangat diperlukan dikarenakan mengingat kebutuhan spesifikasi kapsul iradiasi berupa kedap udara dan kedap air untuk menjaga keamanan reaktor nuklir untuk proses aktivasi material menjadi radioisotop. Pengukuran dilakukan menggunakan *edge detection* untuk mengukur ketebalan bagian kapsul iradiasi lalu dari hasil pengukuran dilakukan perhitungan untuk penentuan titik las.

# *Programming Requirements*
Program ini menggunakan bahas pemrograman Python versi 3.11 yang ditulis di JupyterLab. Program ini dikembangakan dalam sistem operasi Windows 8.

Berikut ini adalah link untuk [*install* Anaconda](https://www.anaconda.com/download). Install *library* yang dibutuhkan yaitu ```OpenCV```, ```matplotlib```, ```numpy```, ```glob```, dan ```pandas``` di Anaconda Prompt dengan perintah di bawah ini.
```
conda install opencv matplotlib numpy glob pandas
```
Pastikan *library* sudah terinstall dengan melihat di daftar *packages in environment* dengan perintah.
```
conda list
```

# Tahapan Pengunaan Program
Terdapat 3 tahapan sebelum melakukan pengukuran dan penentuan titik las yaitu kalibrasi kamera, *set-up* kamera, dan kalibrasi piksel. Jika semua tahapan sudah dilakukan maka program untuk pengukuran dan penentuan titik las dapat dilakukan.

## Kalibrasi Kamera
Kalibrasi kamera dilakukan untuk menghilangkan distors lensa pada kamera yang digunakan. Distorsi lensa yang terjadi jika dibiarkan akan memengaruhi hasil pengukuran oleh karna itu diperlukan pengkoreksian citra dari hasil yang didapatkan. Untuk melakukan kalibrasi kamera diperlukan sekumpulan citra papan catur. Kalibrasi kamera yang dilakukan hanya berlaku untuk jenis kamera yang digunakan dan pengaturan panjang fokal yang digunakan.

<p align="center">
<img src="/image-markdown/algoritmKalibrasiKamera.png" width=30% align="center">
</p>

## _set-up_ Kamera
_set-up_ bertujuan untuk pengambilan citra yang diinginkan dalam keadaan yang sama dengan objek yang ingin diolah citranya. Pengambilan citra dilakukan dengan mengatur posisi kamera secara vertikal tegak lurus dari permukaan kapsul iradiasi. Posisi diambil untuk menghidari distorsi geometrik. Kamera yang digunakan kamera industri _webcast_ panjang fokal lensa 5-50 mm 720p dengan sambungan USB. Skema pengambilan citra ditunjukan di bawah ini

<p align="center">
<img src="/image-markdown/skemakamera.png" width=30% align="center">
</p>

Tahapan ini akan menghasilkan sebuah citra kapsul iradiasi seperti gambar di bawah ini.

<p align="center">
<img src="/Dataset/A1.jpg" width=70% align="center">
</p>

## Kalibrasi Piksel
Kalibrasi piksel dilakukan untuk mengkonversi satuan piksel ke satuan milimeter. Kalibrasi piksel dilakukan dengan mendeteksi citra kotak berkontras dengan latar belakang yang diketahui dimensi fisiknya. Citra kotak didapatkan dengan pengambilan citra seperti skema pada tahapan _set-up_ kamera. Citra kotak diolah sehingga didapatkan dimensinya dalam satuan piksel. Dengan diketahuinya dimensi dalam piksel dan satuan panjang milimeter, faktor kalibrasi dapat diketahui dengan menghitung dengan persamaan di bawah ini.

$$\text{Faktor Kalibrasi Piksel}=\frac{\text{Lebar Objek (mm)}}{\text{Jumlah Piksel (piksel)}}$$

<p align="center">
<img src="/image-markdown/algoritmKalibrasiPiksel.png" width=30% align="center">
</p>

## Pengolahan Citra Pengukuran dan Penentuan Titik las
Citra kapsul iradiasi yang diambil akan diolah untuk mendapatkan 2 ROI (_Region of Interest_) yaitu ROI tutup dan ROI tabung. Ketebalan bagian kapsul iradiasi diukur dari ROI yang didapatkan. Pengukuran dilakukan dengan menghitung panjang tiap ketebalan tiap derajat. Panjang garis dapat dihitung dengan persamaan di bawah ini.

$$\text{Panjang Garis}=\sqrt{(x_{1}-x_{2})^{2}+(y_{1}-y_{2})^{2}}$$

Dari hasil pengukuran tiap bagian per derajat selanjutnya menghitung posisi titik las dengan persamaan di bawah ini.

$$\text{Posisi Titik Las}=\frac{\text{Tebal Bibir Tutup}+\text{Tebal Tabung}}{2}$$

Pengolahan citra kapsul iradiasi dilakukan dengan _flowchart_ di bawah ini.

<p align="center">
  <img src="/image-markdown/algoritmprogramta.png" width=50% align="center">
</p>

# Hasil
Proses pemisahan bagian kapsul iradiasi, program melakukan deteksi lingkaran dengan transformasi Hough. Diperlukan 3 lingkaran untuk bisa memisahkan tiap bagian kapsul iradiasi sehingga dapat menghasilkan ROI tutup dan ROI tabung. Hasil deteksi lingkaran dapat dilihat gambar di bawah ini.

<p align="center">
  <img src="/image-markdown/7.B2-Circle.jpg" width=30% align="center">
</p>

Hasil segmentasi akan memengaruhi hasil pengukuran dan penentuan titik las. berikut ini adalah hasil segmentasi untuk tutup dan tabung.

<p align="center">
  <img src="/image-markdown/8.B2-Cap.jpg" width=30% alt="ROI Tutup"> <img src="/image-markdown/9.B2-Tube.jpg" width=30% alt="ROI Tabung">
</p>

Langkah selanjutnya yaitu mengukur ketebalan bagian kapsul iradiasi tiap derajat dari tepi ke tepi. Hasil pengukuran selanjutnya akan menentukan titik las. Didapatkan hasil pengukuran ketebalan tutup dan tabung kapsul iradiasi serta titik las berupa grafik.
<p align="center">
  <img src="/image-markdown/hasiltutup.png" width=60%>
  <img src="/image-markdown/hasiltabung.png" width=60%>
  <img src="/image-markdown/hasiltitiklas.png" width=60%>
</p>
