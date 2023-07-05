# PROJECT UAS 
# 202131005 <BR> RADEN RONGGO BINTANG P. P

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

<h3>Penjelasan program</h3>

1. importing library yang di butuhkan
2. Baca image ke dalam kode menggunakan ```cv2.imwrite``` dan simpan dalam sebuah variabel
3. Ubah data citra tersebut dari BGR ke Grayscale
4. Bisa kita plot data Grayscale nya menggunakan pyplot dari numpy, dengan color-mapping = gray
5. Setelah itu kita bisa membuat filter dan mengaplikasikannya.
6. Filter pertama itu kita gunakan bilateral-filter yang berguna untuk mengurangi Noise pada citra dan tetap mempertahankan detail tepi gambar
7. Filter kedua saya gunakan cv2.Canny yang berguna membantu mendeteksi tepi gambar, dengan parameter citra sudah harus masuk ke filter pertama. kode nya adalah :
    ```python
    b_filter = cv2.bilateralFilter(gray, 11, 17, 17)  #Noise reduction
    edged = cv2.Canny(b_filter, 30, 100)  #Edge detection
    plt.imshow(edged, cmap='gray')
    ```
8. Setelah mengaplikasikan kedua filter tsb. maka bisa kita lihat citra menggunakan pyplot lagi
9. Dengan terlihatnya tepi pada citra, maka kita bisa mengambil kontur pada citra. **Tujuan nya adalah agar bisa kita crop plat nomor mobilnya**
10. Pertama-tama kita buat titik kuncinya terlebih dahulu. menggunakan fungsi ```cv2.findContours``` yang berguna untuk mendapatkan kontur-kontur pada citra yang memiliki channel warna tunggal. Kontur sendiri adalah garis tepi yang menghubungkan piksel-piksel dengan intensitas yang sama atau mirip. Dengan parameter : <br>
    a. Data dari citra yang tepi nya sudah di deteksi <br>
    b. mode : ```cv2.RETR_TREE``` yang berguna untuk mengambil semua kontur dengan hirarki lengkap <br>
    c. metode : ```cv2.CHAIN_APPROX_SIMPLE```
11. Kontur sendiri menggunakan library ``imutils``
12. Menggunakan fungsi ``imutils.grab_contours`` dengan parameter dari titik kunci.
13. Setelah mendapatkan kontur, saya mengurutkan kontur yang ada secara ``descending`` di urutkan berdasarkan area konturnyam, ``cv2.contourArea``. bisa kita lihat pada kode berikut ini :
    ```python
    key_point = cv2.findContours(edged.copy(), cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
    contours = imutils.grab_contours(key_point)
    contours = sorted(contours, key=cv2.contourArea, reverse=True)[:10]
    ```
14. Kemudian bisa lanjut mencari posisi x1, y1 sampai x4, y4 untuk mendapatkan posisi dari plat nomor, kenapa 4? karena bentuk dari plat nomor kendaraan adalah persegi panjang. maka kode yang saya buat adalah :
    ```python
    location = None
    for contour in contours:
        approx = cv2.approxPolyDP(contour, 10, True)
        if len(approx) == 4:
            location = approx
            break
    ```

15. Menggunakan Looping untuk memperkirakan kontur yang ada pada citra agar mendapatkan posisi x,y dari plat.
16. Kemudian kita membuat mask layer dengan menggunakan shape yang sama dari data citra ``gray`` kita deklarasikan sebagai array 0
17. Lalu bisa kita menggambarkan kontur menggunakan mask dan lokasi, nilai selain dari lokasi akan di isi dengan warna putih (255) ketebalan kontur -1 dan indeks kontur di mulai dari 0. Kode nya adalah :
    ```python
    mask = np.zeros(gray.shape, np.uint8)
    new_image = cv2.drawContours(mask, [location], 0, 255, -1)
    new_image = cv2.bitwise_and(img, img, mask=mask)
    ```
18. Maka kalau kita cetak citra-nya kita sudah bisa melihat hanya plat nomor saja
19. kita akan crop secara otomatis secara otomatis menggunakan kode berikut ini :
    ```python
    x, y = np.where(mask == 255)
    x1, y1 = np.min(x), np.min(y)
    x2, y2 = np.max(x), np.max(y)
    cropped_image = gray[x1:x2 + 1, y1:y2 + 1]
    ```
    x dan y akan di ambil dari mask yang bernilai 255 <br>
    x1 dan y1 adalah nilai minmum dari x dan y <br>
    x2 dan y2 adalah nilai maximum dari x dan y <br>
    kita crop citra yang disimpan di variable gray dengan rumus koordinat x = ``x1 sampai x2 + 1`` dan koordinat y = ``y1 sampai y2 + 1``
20. Nah sekarang kita sudah bisa melihat data citra gray yang sudah di crop
21. Tahap berikutnya adalah kita membuat dari citra gryascale ke citra biner dan deteksi tepi dari citra grayscale
    ```python
    cropped_edge = cv2.Canny(cropped_image, 30, 200)  # Edge detection
    thresh, binary = cv2.threshold(cropped_image, 128, 255, cv2.THRESH_BINARY | cv2.THRESH_OTSU)
    ```
    seperti sebelumnya kita menggunakan fungsi Canny untuk deteksi tepi <br>
    untuk merubah ke citra biner, kita menggunakan ambang, nilai ambang nya adalah 128, di atas 128 akan menjadi putih dan di bawah 128 akan menjadi hitam.
22. Setelah itu bisa kita tampilkan side-by-side menggunakan kode berikut ini :
    ```python
    fig, axs = plt.subplots(1, 2, figsize=(15, 5))
    axs = axs.ravel()

    axs[0].imshow(cropped_edge, cmap='gray')
    axs[0].set_title('citra edged')

    axs[1].imshow(binary, cmap='gray')
    axs[1].set_title('citra biner')
    ```
23. Kita simpan gambar tersebut di directory kerja kita dengan kode berikut ini :
    ```python
    cv2.imwrite('./plat-citra-tepi.png', cropped_edge)
    cv2.imwrite('./plat-citra-biner.png', binary)
    ```

<h3>Penjelasan Alur</h3>
installing library
```python
pip install numpy
pip install opencv-python
pip install imutils 
pip install matplotlib
pip install Pillow
```

<h3>Sumber - sumber</h3>
[PyPi - Mencari library Python](https://pypi.org) <br>
[Open - CV](https://docs.opencv.org/3.4/) <br>
[Deteksi Kontur](https://learnopencv.com/contour-detection-using-opencv-python-c/#What-are-Contours) <br>
[AI - penjelasan baris kode tertentu](https://chat.openai.com) <br>
[Metode Belajar](https://unydevelopernetwork.com/index.php/2021/05/03/membuat-deteksi-plat-nomer-kendaraan-sederhana-dengan-opencv-python/) <br>



