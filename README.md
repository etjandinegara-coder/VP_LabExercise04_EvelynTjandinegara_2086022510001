1. A Text inside a Row overflows. Which part of "constraints go down, sizes go up, parent sets position" was violated, and by which widget?
= 'Row' memberi ruang horizontal kepada child, tetapi 'Text' bisa meminta ukuran selebar isi teksnya. Kalau teks terlalu panjang, ukurannya lebih besar daripada ruang yang tersedia maka akan terjadi overflow.
   Jadi perbaikiannya adalah hubungan Row dengan Text, diperbaiki menggunakan Expanded/Flexible dan maxLines + TextOverflow.ellipsis.

2. Why is adding width: 150 to the text the wrong fix, even if the stripes disappear?
= Karena width: 150 hanya memaksa angka ukuran tertentu. Mungkin overflow hilang pada satu ukuran layar, tetapi tidak tentu pada layar lain.

3. You fixed the landscape overflow by wrapping everything in a SingleChildScrollView and setting shrinkWrap: true on the list. Which test fails, and why does it matter once the data comes from an API?
= Yang akan bermasalah adalah Test 7: 500 items. File memang menyediakan kBigMenu berisi 500 item untuk menguji kasus ini.
shrinkWrap: true membuat list mencoba menghitung ukuran berdasarkan semua item terlebih dahulu. Kalau data nanti berasal dari API dan jumlahnya bisa sangat banyak, cara ini tidak efisien.
Karena itu rule lab mewajibkan: No shrinkWrap: true on a long list. A list you do not control is lazy.

4. Why does the tablet layout use LayoutBuilder rather than MediaQuery.sizeOf(context)?
= Karena yang kita butuhkan adalah lebar ruang yang diberikan kepada widget tersebut, bukan selalu ukuran seluruh layar. LayoutBuilder memberikan constraints dari parent

5. The empty-data crash was not a layout error. Why does it belong in a layout lab anyway?
= Karena layout tidak hanya tentang mencegah overflow. Layout juga harus bisa menangani kondisi ketika tidak ada data. Kalau hasil API nanti kosong, screen tetap harus punya tampilan yang masuk akal, bukan crash atau menampilkan list kosong tanpa informasi. Jadi empty state termasuk layout karena kita menentukan bagaimana UI beradaptasi ketika kondisi data berubah, bukan hanya bagaimana UI beradaptasi ketika ukuran layar berubah.