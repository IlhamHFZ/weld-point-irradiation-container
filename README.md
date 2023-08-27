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
Kalibrasi kamera dilakukan untuk menghilangkan distors lensa pada kamera yang digunakan. Distorsi lensa yang terjadi jika dibiarkan akan memengaruhi hasil pengukuran oleh karna itu diperlukan pengkoreksian citra dari hasil yang didapatkan. 
