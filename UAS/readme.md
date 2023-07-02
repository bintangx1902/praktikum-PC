# PROJECT UAS 
Title terlampir di file [uas.ipynb](https://github.com/bintangx1902/praktikum-PC/blob/main/UAS/uas.ipynb) <br>
untuk data citra bernama [starlet.jpg](https://github.com/bintangx1902/praktikum-PC/blob/main/UAS/starlet.jpg) (mobil toyota starlet) <br>
untuk detail dari citra bisa di lihat di [detail-starlet.jpg](https://github.com/bintangx1902/praktikum-PC/blob/main/UAS/detail-starlet.jpg)

<br>
<h3>Library yang di gunakan dan harus di install</h3>
<ul>
    <li>imutils</li>
    <li>opencv</li>
    <li>numpy</li>
    <li>matplotlib</li>
</ul>

<h3>Penjelasan alur program</h3>

1. importing library yang di butuhkan
2. Baca image ke dalam kode menggunakan ```cv2.imwrite``` dan simpan dalam sebuah variabel
3. Ubah data citra tersebut dari BGR ke Grayscale
4. Bisa kita plot data Grayscale nya menggunakan pyplot dari numpy, dengan color-mapping = gray
5. Setelah itu kita bisa membuat filter dan mengaplikasikannya.
6. Filter pertama itu kita gunakan bilateral-filter yang berguna untuk mengurangi Noise pada citra dan tetap mempertahankan detail tepi gambar
7. Filter kedua saya gunakan cv2.Canny yang berguna membantu mendeteksi tepi gambar, dengan parameter citra sudah harus masuk ke filter pertama
8. Setelah mengaplikasikan kedua filter tsb. maka bisa kita lihat citra menggunakan pyplot lagi
9. Dengan terlihatnya tepi pada citra, maka kita bisa mengambil kontur pada citra. **Tujuan nya adalah agar bisa kita crop plat nomor mobilnya**
10. Pertama-tama kita buat titik kuncinya terlebih dahulu. menggunakan fungsi ```cv2.findContours``` yang berguna untuk mendapatkan kontur-kontur pada citra yang memiliki channel warna tunggal. Kontur sendiri adalah garis tepi yang menghubungkan piksel-piksel dengan intensitas yang sama atau mirip. Dengan parameter : <br>
    a. Data dari citra yang tepi nya sudah di deteksi <br>
    b. mode : ```cv2.RETR_TREE``` yang berguna untuk mengambil semua kontur dengan hirarki lengkap <br>
    c. metode : ```cv2.CHAIN_APPROX_SIMPLE```
11. Kontur sendiri menggunakan library ``imutils``
12. Menggunakan fungsi ``imutils.grab_contours`` dengan parameter dari titik kunci.
13. Setelah mendapatkan kontur, saya mengurutkan kontur yang ada secara ``descending`` di urutkan berdasarkan area konturnyam, ``cv2.contourArea``
14. Kemudian bisa lanjut mencari posisi x1, y1 sampai x4, y4 untuk mendapatkan posisi dari plat nomor, kenapa 4? karena bentuk dari plat nomor kendaraan adalah persegi panjang.
15. Menggunakan Looping 
    


