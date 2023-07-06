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

### Sumber yang di butuhkan dan digunakan 
Mencari Library python : [PyPi](https://pypi.org) <br>
Open Computer Vision : [Open-CV](https://docs.opencv.org/3.4/) <br>
Bahan Belajar [Deteksi Kontur](https://learnopencv.com/contour-detection-using-opencv-python-c/#What-are-Contours) <br>
Penjelasan Baris Program yang tak dapat dipahami [AI - penjelasan baris kode tertentu](https://chat.openai.com) <br>
Bahan Belajar [Deteksi Plat](https://unydevelopernetwork.com/index.php/2021/05/03/membuat-deteksi-plat-nomer-kendaraan-sederhana-dengan-opencv-python/) <br>


### TEORI PENDUKUNG
- Image Channel Converting <br>
pada ujian kali ini kita akan menggunakan konversi channel warna pada citra, dari RGB / BGR ke grayscale dan sebaliknya
pada saat awal citra dibaca dengan 3 channel warna; Blue-Green-Red, kemudian kita akan mengubah data citra dari BGR ke Grayscale dengan rumus = (0.299 * Red) + (0.587 * Green) + (0.114 * Blue).
Formula ini menghitung nilai keabuan berdasarkan proporsi yang berbeda untuk masing-masing saluran warna RGB. Nilai tersebut kemudian digunakan sebagai tingkat keabuan piksel dalam citra grayscale.


- Bilateral Filter
Bilateral filter adalah metode pengolahan citra yang digunakan untuk mengurangi noise atau menghaluskan citra dengan mempertahankan tepi atau detail penting. Filter ini bekerja dengan mempertimbangkan kedua jarak spasial dan perbedaan intensitas piksel. <br> <br>
Dalam bilateral filter, setiap piksel dalam citra diproses dengan mempertimbangkan dua faktor utama: jarak spasial antara piksel-piksel dan perbedaan intensitas warna antara piksel yang sedang diproses dengan piksel-piksel tetangganya. <br> <br>
Secara sederhana, piksel tetangga yang memiliki perbedaan warna yang signifikan dengan piksel yang sedang diproses akan memberikan kontribusi yang lebih kecil dalam proses penghalusan. Hal ini membantu mempertahankan tepi atau detail penting dalam citra, karena perbedaan intensitas yang signifikan dianggap sebagai tanda adanya tepi. <br>


- Deteksi Tepi menggunakan Operator Canny
Deteksi tepi dalam pengolahan citra adalah proses identifikasi dan penyorotan perubahan tajam dalam intensitas piksel di sekitar suatu objek atau struktur dalam citra. Tepi adalah perbatasan atau transisi antara dua wilayah dengan intensitas yang berbeda dalam citra. <br> <br>
Deteksi tepi penting dalam analisis citra karena tepi sering kali mengandung informasi penting tentang struktur objek, kontur, atau batas. Tepi dapat digunakan untuk segmentasi objek, pemrosesan lanjutan, ekstraksi fitur, dan tugas pengenalan pola lainnya. <br> <br>
Metode deteksi tepi umumnya melibatkan penerapan operator gradien, seperti Sobel, Prewitt, atau Roberts, yang mengukur perubahan intensitas spasial dalam citra. Operator ini memberikan informasi tentang arah dan kekuatan perubahan intensitas di setiap piksel. <br> <br>
Setelah menghitung gradien, langkah-langkah tambahan seperti non-maximum suppression, ambang batas, atau penghubungan tepi dapat diterapkan untuk meningkatkan akurasi dan kejelasan tepi yang dihasilkan. <br> <br>
Deteksi tepi membantu dalam pengolahan dan analisis citra dengan mengidentifikasi dan menyoroti informasi yang penting secara visual dalam citra. Ini merupakan langkah awal yang umum dalam banyak aplikasi pengolahan citra yang lebih lanjut dan dapat digunakan dalam berbagai bidang seperti visi komputer, pengenalan pola, dan penglihatan mesin. <br> <br>
Operator Canny adalah salah satu teknik deteksi tepi yang populer dalam pengolahan citra. Metode ini dikembangkan oleh John F. Canny pada tahun 1986 dan dianggap sebagai salah satu pendekatan terbaik untuk deteksi tepi. <br> <br>
Operator Canny menghasilkan tepi yang tajam, mempertahankan tepi penting, dan mengurangi kesalahan deteksi tepi. Metode ini sering digunakan dalam berbagai aplikasi pengolahan citra, seperti deteksi objek, segmentasi citra, analisis kontur, dan pengenalan pola. <br> 


- Kontur pada Citra 
Kontur adalah garis atau kurva yang menggambarkan perbatasan atau tepi antara objek dan latar belakang dalam sebuah gambar atau citra. Kontur menunjukkan perubahan tajam dalam intensitas piksel, yang bisa menjadi indikator adanya perubahan objek atau struktur dalam citra. Kontur merupakan representasi visual dari bentuk dan struktur dalam citra dan dapat digunakan untuk berbagai tujuan seperti deteksi objek, segmentasi, pengenalan pola, dan analisis bentuk.


- Mask Layer
Mask layer dalam pengolahan citra adalah lapisan tambahan yang digunakan untuk membatasi efek atau operasi tertentu hanya pada area tertentu dalam citra. Mask layer, juga dikenal sebagai lapisan mask atau lapisan seleksi, berfungsi sebagai penanda atau pemilih yang mengontrol di mana manipulasi atau efek akan diterapkan dalam citra. <br> <br>
Biasanya, mask layer adalah citra biner dengan dua nilai piksel yang berbeda: 0 dan 255. Nilai 255 (putih) menandakan area yang dipilih, sementara nilai 0 (hitam) menandakan area yang tidak dipilih. Mask layer ini diterapkan pada citra asli atau lapisan gambar lainnya dalam proses kompositing atau pengeditan citra.<br> <br>
Dengan menggunakan mask layer, Anda dapat mengaplikasikan efek tertentu, seperti pengaburan, pencahayaan, atau perubahan warna, hanya pada area yang dipilih sesuai dengan pola mask layer. Ini memberikan fleksibilitas dan kontrol yang lebih besar dalam pengolahan citra, karena Anda dapat menargetkan dan membatasi manipulasi hanya pada area yang diinginkan, sambil mempertahankan detail atau bagian lain dalam citra yang tidak terpengaruh. <br> <br>
Mask layer dapat digunakan dalam berbagai aplikasi pengolahan citra, termasuk kompositing, retouching, segmentasi, dan efek khusus. Dengan memanfaatkan mask layer, Anda dapat menciptakan efek yang kompleks dan mengatur pengaruh visual secara selektif dalam citra.


- Citra Biner
Citra biner adalah jenis citra yang hanya memiliki dua nilai piksel yang mungkin, yaitu hitam dan putih. Dalam citra biner, setiap piksel diwakili oleh satu bit informasi, di mana nilai 0 menandakan piksel hitam dan nilai 1 menandakan piksel putih. <br> <br>
Citra biner sering digunakan untuk merepresentasikan gambar dalam bentuk yang lebih sederhana dan efisien. Dalam citra biner, perbedaan intensitas warna tidak dihiraukan, hanya ada perbedaan antara piksel yang dianggap objek (putih) dan piksel yang dianggap latar belakang (hitam). Ini membuat citra biner berguna dalam berbagai aplikasi, termasuk pengenalan pola, pemrosesan lanjutan, segmentasi, dan analisis struktur. <br> <br>
Proses mengubah citra ke dalam bentuk biner melibatkan penerapan thresholding, yaitu menentukan ambang batas yang membagi piksel menjadi hitam dan putih berdasarkan intensitas warnanya. Piksel dengan intensitas di atas ambang batas diubah menjadi putih, sementara piksel dengan intensitas di bawah ambang batas diubah menjadi hitam.<br> <br>
Dengan mempertahankan informasi objek dan latar belakang secara sederhana, citra biner memungkinkan pengolahan dan analisis citra yang lebih mudah dan efisien dalam beberapa konteks aplikasi.<br> <br>

## Penjelasan program

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