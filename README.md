# VendGo

#### Nama : Galen Taris Bariqi
#### NPM : 2206029052
#### Kelas : PBP C


#### TUGAS 7

<details>
<summary>
1. Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?
</summary>

**Stateless Widget**

- Tidak memiliki keadaan internal yang berubah (stateless) setelah widget dibuat.
- Mereka dibangun sekali dan tidak pernah memperbarui diri mereka sendiri kecuali ketika data eksternal yang diberikan ke mereka berubah.
- Ideal untuk kasus di mana UI bisa bergantung pada informasi yang diberikan melalui konstruktor saja, dan tidak diharapkan untuk berubah selama waktu hidup widget.
- Contoh stateless widget termasuk ikon, teks, dan tombol yang tidak berubah setelah mereka dibuat.

**Stateful Widget**

- Memiliki keadaan internal yang dapat berubah selama waktu hidup widget.
- Ketika keadaan internal berubah, widget dapat memicu proses rebuild untuk memperbarui tampilan pada UI.
- Mereka menggunakan dua kelas: satu kelas untuk widget itu sendiri dan satu kelas untuk keadaan widget (State).
- Ideal untuk kasus di mana UI perlu berubah secara dinamis berdasarkan interaksi pengguna atau data yang berubah dari waktu ke waktu, seperti kotak centang, slider, atau formulir yang bisa di-edit.

Secara umum, jika UI yang Anda bangun tidak bergantung pada keadaan yang berubah seiring waktu, gunakan StatelessWidget. Jika UI perlu memperbarui tampilan sebagai respons terhadap perubahan data atau interaksi pengguna, gunakan StatefulWidget.

</details>

<details>
<summary>
2. Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.
</summary>

- MaterialApp = Widget ini adalah titik awal dari aplikasi Flutter yang menggunakan material design. Ia membungkus sejumlah widget yang mengimplementasikan desain material, dan juga menyiapkan aplikasi untuk navigasi, tema, dan lainnya.
- Scaffold = Widget ini menyediakan struktur dasar halaman pada aplikasi material design. Ini termasuk app bar, body, floating action button, dan drawer.
- AppBar = Sebuah widget yang umumnya ditampilkan di bagian atas layar, AppBar menyediakan tempat untuk judul, ikon aksi, dan navigasi.
- Text = Widget ini menampilkan string teks dengan gaya yang bisa diatur.
- Padding = Padding digunakan untuk memberikan ruang tambahan di sekitar widget anaknya. Ini bisa digunakan untuk memberikan ruang antara widgets atau untuk mengatur posisi widgets dalam layar.
- Column = Widget ini memungkinkan Anda untuk menata widgets anaknya secara vertikal.
- GridView = Widget ini memungkinkan pembangunan grid yang terdiri dari elemen-elemen yang dapat disusun dalam bentuk baris dan kolom.
- ShopCard = Ini adalah widget kustom yang dibuat untuk keperluan ini. Widget ini menggabungkan beberapa widget seperti Material, InkWell, Container, dan Icon untuk membuat kartu yang bisa diklik.
- InkWell = Widget yang bereaksi terhadap sentuhan dengan menampilkan efek semburan air. Ini biasa digunakan untuk menambahkan efek interaktif pada widget yang lain.
- Icon = Widget ini menampilkan ikon dari berbagai library ikon yang tersedia di Flutter.
- Center = Widget ini mengatur anak widgetnya agar berada di tengah-tengah parent widgetnya.
- ClipRRect = Widget ini memotong anak widgetnya agar memiliki sudut yang melengkung (rounded corners).

</details>

<details>
<summary>
3. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial)
</summary>

Pada Tugas 7 ini, saya membuat aplikasi inventory bernama VendGo berbasis mobile.

- Membuat sebuah program Flutter baru dengan tema inventory seperti tugas-tugas sebelumnya.
Pada tahap ini, pada terminal, saya melakukan command ``flutter create vend_go`` dan ``cd vend_go``. Setelah itu, aplikasi dengan direktori bernama vend_go akan muncul pada direktori lokal.

-  Membuat tiga tombol sederhana dengan ikon dan teks untuk:
    - Melihat daftar item (Lihat Item)
    - Menambah item (Tambah Item)
    - Logout (Logout)
Selanjutnya, saya mengubah class MyHomePage dari stateful menjadi stateless widget. Di dalam `menu.dart`, saya mendefinisikan sebuah list dari `ShopItem`:

```dart
final List<ShopItem> items = [
  ShopItem("Lihat Item", Icons.checklist, Colors.indigo),
  ShopItem("Tambah Item", Icons.add_shopping_cart, const Color.fromARGB(255, 33, 150, 243)),
  ShopItem("Logout", Icons.logout, Color.fromARGB(255, 33, 243, 33)),
];
```

Kemudian, menggunakan GridView.count saya menampilkan setiap ShopItem sebagai ShopCard:
```
GridView.count(
  crossAxisCount: 3,
  shrinkWrap: true,
  children: items.map((ShopItem item) {
    return ShopCard(item);
  }).toList(),
),
```

- Memunculkan Snackbar dengan tulisan:
    - "Kamu telah menekan tombol Lihat Item" ketika tombol Lihat Item ditekan.
    - "Kamu telah menekan tombol Tambah Item" ketika tombol Tambah Item ditekan.
    - "Kamu telah menekan tombol Logout" ketika tombol Logout ditekan.

Dalam ShopCard, saya menggunakan widget InkWell untuk mendeteksi ketukan dan menampilkan SnackBar:
```
InkWell(
  onTap: () {
    ScaffoldMessenger.of(context)
      ..hideCurrentSnackBar()
      ..showSnackBar(SnackBar(
        content: Text("Saya telah menekan tombol ${item.name}!")));
  },
  // ... (child widgets)
),
```

- Melakukan add-commit-push ke GitHub.

</details>

#### TUGAS 8

<details>
<summary>
1. Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement(), disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!
</summary>

**1. Navigator.push()**

Metode Navigator.push() digunakan untuk menambahkan rute baru ke tumpukan navigasi dalam aplikasi Flutter.
Ini memungkinkan pengguna untuk kembali ke rute sebelumnya dengan tombol "Back". Cocok untuk menambahkan rute baru yang ingin Anda pertahankan dalam tumpukan navigasi.

Contoh penggunaan Navigator.push():
```
// Navigasi ke halaman DetailA
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => DetailA()),
);
```

**2. Navigator.pushReplacement()**

Metode Navigator.pushReplacement() digunakan untuk menambahkan rute baru ke tumpukan navigasi dan menggantikan rute saat ini. Berguna ketika Anda ingin menggantikan rute saat ini dengan rute yang baru, seperti ketika tugas atau langkah tertentu selesai.

Contoh penggunaan Navigator.pushReplacement():
```
// Mengganti rute saat ini dengan halaman DetailB
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => DetailB()),
);
```
Dengan Navigator.pushReplacement(), rute saat ini dihapus dari tumpukan navigasi dan diganti dengan rute yang baru. Ini memungkinkan pengguna untuk menggantikan rute saat ini dengan rute yang lebih sesuai tanpa perlu kembali ke rute sebelumnya.

</details>

<details>
<summary>
2. Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!
</summary>

**1. Container**
Container adalah widget yang digunakan untuk mengelompokkan dan mengatur widget lain ke dalam kotak dengan properti tertentu. Pengembang dapat mengatur properti seperti margin, padding, warna latar belakang, dan lainnya. Container sering digunakan untuk mengatur tata letak sederhana dan sebagai wadah untuk widget lain.

**2. Row dan Column**
Row dan Column adalah widget yang digunakan untuk mengatur widget secara horizontal (dalam Row) atau vertikal (dalam Column). Mereka sering digunakan untuk mengatur tata letak berbasis baris dan kolom, seperti tata letak tabel atau daftar item.

**3. ListView:**
ListView adalah widget yang digunakan untuk membuat daftar gulir (scrollable list) dari widget. Berguna ketika pengembang memiliki daftar item yang lebih panjang daripada layar, dan pengguna perlu menggulir untuk melihat seluruh kontennya.

**4. Stack**
Stack adalah widget yang digunakan untuk menumpuk widget satu di atas yang lain. Pengembang dapat mengatur widget dalam tumpukan (stack) dengan memberikan properti posisi seperti atas, bawah, kiri, dan kanan. Berguna ketika pengembang ingin menempatkan widget secara bebas di atas satu sama lain.

**5. Expanded**
Expanded adalah widget yang digunakan untuk mengisi ruang yang tersedia dalam Row atau Column. Ini memungkinkan widget anak untuk mengisi sebanyak mungkin ruang yang tersedia, sehingga berguna dalam tata letak yang responsif.

**6. Card**
Card adalah widget yang digunakan untuk membuat kotak dengan bayangan dan sudut yang terlihat seperti kartu fisik. Berguna untuk pengembang dalam menampilkan konten terkait dalam bentuk kartu yang dapat dipisahkan dari konten lain.

**7. Wrap**
Wrap adalah widget yang digunakan untuk mengatur widget dalam baris dan kolom seperti Row atau Column, tetapi dapat memindahkan widget ke baris atau kolom berikutnya jika tidak cukup ruang. Berguna untuk pengembang dalam menangani konten yang dapat meluas ke samping tanpa memicu gulir.

**8. GridView**
GridView adalah widget yang digunakan untuk mengatur widget dalam grid dengan baris dan kolom. Pengembang dapat mengatur jumlah kolom, menggulir grid jika diperlukan, dan lainnya.

**9. SingleChildScrollView**
SingleChildScrollView adalah widget yang mengizinkan satu anak widget saja dan digunakan untuk membuat daftar gulir konten tunggal. Berguna ketika pengembang memiliki sedikit konten yang perlu digulir di layar.

**10. Flow**
Flow adalah widget yang digunakan untuk mengatur widget dalam aliran non-hirarkis, mirip dengan Wrap.
Widget dalam Flow diatur berdasarkan kendali alur tertentu.

</details>

<details>
<summary>
3. Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!
</summary>

1. Nama Produk (name):
  Jenis Input = TextFormField
  Saya menggunakan elemen input tersebut untuk memasukkan nama produk. Sebagai elemen dasar dari setiap item, nama produk penting untuk identifikasi dan deskripsi. TextFormField cocok untuk input teks seperti ini.

2. Harga Produk (price):
  Jenis Input = TextFormField dengan keyboardType diatur ke TextInputType.number
  Saya menggunakan elemen input tersebut karena harga produk harus berupa angka, oleh karena itu, TextFormField dengan keyboard numerik digunakan untuk memastikan pengguna hanya memasukkan angka.

3. Deskripsi Produk (description):
  Jenis Input = TextFormField
  Saya menggunakan elemen input tersebut untuk memberikan informasi lebih detail tentang produk. TextFormField digunakan untuk memungkinkan pengguna memasukkan teks bebas, yang dapat mencakup informasi detail atau catatan tambahan tentang produk.

4. Jumlah Produk (amount):
  Jenis Input = TextFormField dengan keyboardType diatur ke TextInputType.number
  Saya menggunakan elemen input tersebut untuk mengindikasikan stok atau jumlah unit yang tersedia atau yang akan ditambahkan. Sama seperti harga, jumlah ini harus berupa angka sehingga input numerik digunakan untuk memudahkan penggunaan dan menghindari kesalahan input.

</details>

<details>
<summary>
4. Bagaimana penerapan clean architecture pada aplikasi Flutter?
</summary>

Clean Architecture memungkinkan aplikasi Flutter untuk menjadi lebih bersih, terstruktur dengan baik, dan mudah dikelola dengan mengisolasi komponen dan meminimalkan ketergantungan. Hal ini membuat aplikasi lebih skalabel dan mudah dipelihara seiring berjalannya waktu. Pada aplikasi Flutter, clean architecture melibatkan pemisahan aplikasi menjadi lapisan Presentasi, Bisnis, dan Data dengan prinsip Dependency Inversion. Ini memungkinkan pengelolaan dependensi, isolasi logika bisnis, pengujian unit yang efektif, serta fleksibilitas dalam mengganti tampilan atau sumber data. Prinsip SOLID juga digunakan untuk menjaga kode tetap terstruktur dengan baik dan mudah diubah.

</details>

<details>
<summary>
5. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial)
</summary>

- Membuat minimal satu halaman baru pada aplikasi, yaitu halaman formulir tambah item baru dengan beberapa ketentuan.

Pertama, saya memulai dengan membuat file baru bernama shoplist_form.dart. Di sini, saya menggunakan StatefulWidget karena perlu mengupdate status berdasarkan input pengguna. Dalam build method, saya menambahkan Form dengan sebuah GlobalKey untuk mengelola status form.

Di dalam form ini, saya menambahkan empat TextFormField untuk name, price, description, dan amount. Untuk setiap field ini, saya memastikan ada validasi yang memeriksa apakah field tersebut tidak kosong dan memenuhi kriteria tipe data yang sesuai, seperti angka untuk harga dan jumlah.

Kemudian, saya menambahkan sebuah tombol 'Save'. Saya menggunakan ElevatedButton untuk ini. Dalam onPressed dari tombol ini, saya mengecek dulu apakah form valid menggunakan _formKey.currentState.validate(). Jika ya, saya simpan datanya ke list dan menampilkan pop-up menggunakan showDialog yang menampilkan informasi item yang baru disimpan.

- Mengarahkan pengguna ke halaman form tambah item baru ketika menekan tombol Tambah Item pada halaman utama.

Di MyHomePage, saya menambahkan sebuah widget yang, ketika ditekan, akan membawa pengguna ke ShopFormPage untuk menambah item baru. Saya menggunakan GridView untuk menampilkan opsi ini.

- Memunculkan data sesuai isi dari formulir yang diisi dalam sebuah pop-up setelah menekan tombol Save pada halaman formulir tambah item baru.

Pada form yang saya buat, saya menambahkan empat TextFormField untuk name, price, description, dan amount. Dan tidak lupa, saya memastikan bahwa setiap kali tombol 'Save' di ShopFormPage ditekan, item yang baru ditambahkan disimpan ke dalam listItem yang didefinisikan di item.dart.

- Membuat sebuah drawer pada aplikasi dengan beberapa ketentuan.

Selanjutnya, saya membuat file left_drawer.dart untuk widget Drawer. Saya menambahkan dua ListTile di dalam ListView di Drawer ini. Satu untuk navigasi ke 'Halaman Utama' dan satu lagi untuk 'Tambah Item'.

Di setiap ListTile, saya menetapkan onTap untuk melakukan navigasi. Untuk 'Halaman Utama', saya gunakan Navigator.pushReplacement menuju MyHomePage, dan untuk 'Tambah Item', saya gunakan Navigator.push menuju ShopFormPage.

Setelah itu, saya mengintegrasikan LeftDrawer ke dalam Scaffold dari MyHomePage dan ShopFormPage. Ini memungkinkan saya untuk memiliki drawer yang sama di kedua halaman tersebut dengan fungsionalitas navigasi yang sudah saya tetapkan.

</details>