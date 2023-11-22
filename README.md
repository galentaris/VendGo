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

#### TUGAS 9

<details>
<summary>
1. Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?
</summary>

Ya, pengembang bisa mengambil data JSON tanpa membuat model terlebih dahulu. Dalam konteks pemrograman dan pengembangan perangkat lunak, "model" sering merujuk pada struktur data atau representasi objek yang mendefinisikan bagaimana data disimpan, diorganisir, dan diproses. Dalam kasus JSON, Hal tersebut adalah format data yang ringan dan mudah dibaca oleh manusia, serta mudah untuk diparsing oleh mesin.

Terkait apakah pengambilan data JSON tanpa membuat model lebih baik daripada membuat model sebelum melakukan pengambilan data JSON. Kedua metode tersebut tergantung pada kebutuhan spesifik dari masing-masing project pengembang.
- Untuk kasus penggunaan yang sederhana, langsung mengambil dan menggunakan data JSON mungkin lebih efisien dan cepat.
- Untuk aplikasi yang lebih kompleks dan skalabel, mendefinisikan model dapat membantu dalam jangka panjang dengan menyediakan struktur yang lebih terorganisir dan memudahkan pengelolaan data.

</details>

<details>
<summary>
2. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
</summary>

Dalam Flutter, konsep CookieRequest mungkin tidak secara langsung terkait dengan framework Flutter itu sendiri, tetapi lebih kepada manajemen HTTP request dan cookie dalam pengembangan aplikasi. Cookie biasanya merupakan data kecil yang disimpan di perangkat pengguna dan sering digunakan untuk mengelola sesi pengguna, menyimpan preferensi, atau untuk keperluan pelacakan. Sebuah CookieRequest bisa diartikan sebagai permintaan HTTP yang mengirim atau menerima cookie ini. Alasan untuk membagikan instance CookieRequest ke seluruh komponen di aplikasi Flutter terkait dengan beberapa faktor penting. Pertama, ini memudahkan pengelolaan sesi pengguna; dengan mengirimkan cookie yang sama dalam setiap request, aplikasi dapat menjaga konsistensi sesi di seluruh komponen. Kedua, hal ini membantu dalam menjaga konsistensi preferensi pengguna dan data lainnya di seluruh aplikasi. Ketiga, dari sisi pengembangan, ini mengurangi duplikasi kode dan meningkatkan efisiensi karena pengembang tidak perlu mengulangi logika yang sama untuk setiap komponen. Terakhir, pendekatan ini memfasilitasi manajemen state aplikasi secara lebih terpusat, yang sangat berguna terutama dalam aplikasi skala besar. Meski begitu, detail yang lebih spesifik tergantung pada konteks penggunaan CookieRequest dalam proyek Flutter tertentu

</details>

<details>
<summary>
3. Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
</summary>

1. Pembuatan HTTP Request:

Pertama, aplikasi Flutter perlu membuat HTTP request ke server atau API yang menyediakan data JSON. Ini biasanya dilakukan menggunakan paket http yang tersedia di Flutter.
Contoh: http.get('https://example.com/data.json');

2. Pengolahan Respon:

Setelah request terkirim, aplikasi akan menerima respon dari server. Respon ini biasanya dalam format JSON.
Pengembang perlu memeriksa status respon untuk memastikan bahwa request berhasil.

3. Parsing Data JSON:

Data JSON yang diterima kemudian perlu diparsing atau diubah dari format string ke format yang bisa dibaca oleh Flutter/Dart.
Flutter menggunakan jsonDecode() dari library dart:convert untuk mengubah data JSON string menjadi Map atau List yang bisa diproses oleh Dart.

4. Mendefinisikan Model Data (Opsional):

Meskipun ini tidak wajib, mendefinisikan model data membantu dalam mengelola data tersebut secara lebih efisien.
Model ini adalah kelas Dart yang mendefinisikan struktur data dan metode untuk mengolah data tersebut.

5. Menyimpan Data ke State:

Setelah data JSON diparsing, data tersebut disimpan dalam state aplikasi. Flutter menggunakan berbagai cara untuk mengelola state, seperti setState, Provider, atau state management lain seperti Bloc.
Data ini disimpan dalam bentuk yang memudahkan widget untuk membangun UI berdasarkan data tersebut.

6. Membangun UI:

Widget Flutter kemudian dapat menggunakan data yang telah diproses untuk membangun UI.
Misalnya, sebuah ListView.builder dapat digunakan untuk menampilkan daftar item yang data-datanya diambil dari JSON.

7. Pembaruan UI secara Dinamis:

Saat data berubah atau diperbarui, UI perlu diperbarui. Ini dilakukan dengan memicu rebuild widget yang tergantung pada data tersebut.

</details>

<details>
<summary>
4. Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
</summary>

1. Input Data di Flutter:

Pengguna memasukkan data akun (biasanya username dan password) melalui antarmuka Flutter.
Flutter mengumpulkan data ini, biasanya dalam sebuah form.
Pengiriman Data ke Django:

Flutter mengirimkan data akun ke server Django menggunakan HTTP request (biasanya POST request).
Request ini melibatkan pengaturan header yang sesuai (seperti Content-Type: application/json) dan body yang berisi data akun dalam format JSON.

2. Penerimaan dan Pengolahan di Django:

Server Django menerima request tersebut.
Django kemudian mengurai (parse) data JSON dan melakukan proses autentikasi. Ini biasanya melibatkan pencocokan username dan password dengan data yang ada di database.
Jika Django menggunakan Django Rest Framework, proses ini bisa dikelola oleh APIView atau ViewSet.

3. Pengembalian Respon oleh Django:

Setelah autentikasi, Django mengirimkan respon kembali ke aplikasi Flutter.
Respon ini bisa berupa status autentikasi (sukses/gagal), token (untuk autentikasi berbasis token seperti JWT), atau pesan error.

4. Pengolahan Respon di Flutter:

Aplikasi Flutter menerima respon dan memprosesnya.
Jika autentikasi berhasil, Flutter mungkin menyimpan token ke dalam storage lokal (seperti SharedPreferences) untuk sesi yang persisten.

5. Navigasi ke Menu Utama:

Berdasarkan respon dari Django, Flutter kemudian melakukan navigasi ke layar atau menu utama aplikasi.
Jika autentikasi gagal, Flutter mungkin menampilkan pesan error dan meminta pengguna untuk mencoba lagi.

6. Manajemen Sesi:

Untuk setiap request berikutnya yang memerlukan autentikasi, aplikasi Flutter akan mengirimkan token yang diterima dari Django (jika menggunakan autentikasi berbasis token).
Django akan memverifikasi token ini untuk setiap request yang membutuhkan autentikasi.

</details>

<details>
<summary>
5. Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.
</summary>

1. Scaffold:

Memberikan struktur dasar material design untuk layar, termasuk AppBar, Drawer, dan Body.

2. AppBar:

Menampilkan bar di bagian atas layar yang biasanya berisi judul dan beberapa aksi.

3. LeftDrawer:

Widget kustom (sepertinya dibuat oleh Anda) yang berfungsi sebagai menu geser (drawer) di sisi kiri layar.

4. FutureBuilder:

Widget yang membangun dirinya sendiri berdasarkan hasil terbaru dari interaksi dengan Future. Digunakan untuk menampilkan data yang sedang diambil atau menampilkan indikator saat data sedang dimuat.

5. CircularProgressIndicator:

Menampilkan indikator loading berputar, menunjukkan bahwa proses sedang berlangsung, seperti pengambilan data.

6. ListView.builder:

Widget yang efisien untuk membuat daftar yang dapat digulir berdasarkan jumlah item yang ditentukan.

7. Container:

Kotak dekorasi yang dapat diubah ukurannya, sering digunakan untuk memberi padding, margin, atau dekorasi lain ke widget di dalamnya.

8. Column:

Widget layout untuk menempatkan anak-anaknya secara vertikal.

9. Text:

Menampilkan string teks dengan gaya yang bisa disesuaikan.

10. SizedBox:

Kotak dengan ukuran tetap, sering digunakan untuk memberikan jarak antar widget.
11. TextField:

Input teks yang memungkinkan pengguna memasukkan data.

12. ElevatedButton:

Tombol bertema material design yang menonjol dari latar belakangnya.

13. TextButton:

Tombol teks sederhana tanpa latar belakang atau border.

14. AlertDialog:

Dialog yang menampilkan informasi penting atau mengumpulkan input dari pengguna.

15. Form:

Kontainer untuk FormField yang memungkinkan validasi input.

16. FormState:

Status yang mengelola Form, sering digunakan untuk validasi.

17. TextFormField:

TextField yang terintegrasi dengan Form.

18. Padding:

Menambahkan padding di sekitar anaknya.

19. MaterialApp:

Widget root yang mengatur tema dan navigasi untuk aplikasi.

20. Provider:

Library manajemen state yang memungkinkan data atau objek dibagikan ke seluruh widget dalam pohon.

21. CookieRequest:

Objek yang sepertinya berfungsi untuk manajemen cookie dan request HTTP, mungkin bagian dari paket pbp_django_auth.
GlobalKey<FormState>:

Kunci yang digunakan untuk mengidentifikasi Form secara unik dalam pohon widget.

22. SingleChildScrollView:

Widget yang memungkinkan pengguliran konten yang mungkin lebih besar daripada ruang layar yang tersedia.

</details>

<details>
<summary>
6. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).
</summary>

1. Memastikan Deployment Proyek Tugas Django Berjalan dengan Baik:

Saya menggunakan localhost karena deployment saya mengalami error saat saya menambahkan authentication.

2. Membuat Halaman Login pada Proyek Tugas Flutter:

Halaman login sudah ada di login.dart. Saya menggunakan TextField untuk memasukkan username dan password, dan ElevatedButton yang, ketika ditekan, memanggil metode untuk mengirimkan data tersebut ke server Django.

3. Mengintegrasikan Sistem Autentikasi Django dengan Proyek Tugas Flutter:

Sistem autentikasi terintegrasi di login.dart menggunakan CookieRequest. Saya mengirimkan data login ke endpoint Django dan menangani respons. Jika login berhasil, saya menavigasi ke halaman utama.

4. Membuat Model Kustom Sesuai dengan Proyek Aplikasi Django:

Model Welcome di product.dart sudah mencerminkan struktur data JSON dari backend Django. Ini digunakan untuk parsing data produk yang diterima dari API.

5. Membuat Halaman yang Berisi Daftar Semua Item dari Endpoint JSON di Django:

Di ProductPage (list_product.dart), saya menggunakan FutureBuilder untuk mengambil data dari API Django. Data ini kemudian ditampilkan dalam ListView.builder.

6. Menampilkan Name, Amount, dan Description dari Masing-Masing Item:

Di ProductPage, saya menampilkan name, price, dan description untuk setiap item. Kode untuk menampilkan ini adalah sebagai berikut:

```
ListView.builder(
  itemCount: snapshot.data!.length,
  itemBuilder: (_, index) => ListTile(
    title: Text(snapshot.data![index].fields.name),
    subtitle: Text("${snapshot.data![index].fields.price} - ${snapshot.data![index].fields.description}"),
  ),
);
```

7. Membuat Halaman Detail untuk Setiap Item:

Untuk membuat halaman detail, saya akan menambahkan sebuah halaman baru, ProductDetailPage. Berikut contoh kode untuk halaman tersebut:

```
class ProductDetailPage extends StatelessWidget {
  final Welcome product;

  ProductDetailPage({Key? key, required this.product}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(product.fields.name),
      ),
      body: Padding(
        padding: EdgeInsets.all(8),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            Text("Price: ${product.fields.price}"),
            Text("Description: ${product.fields.description}"),
            // Lainnya...
          ],
        ),
      ),
    );
  }
}
```

8. Mengakses Halaman Detail dengan Menekan Item pada Halaman Daftar Item:

Di ProductPage, saya akan menambahkan logika untuk menavigasi ke ProductDetailPage saat item ditekan:

```
itemBuilder: (_, index) => ListTile(
  title: Text(snapshot.data![index].fields.name),
  onTap: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => ProductDetailPage(product: snapshot.data![index])),
    );
  },
);
```

9. Menampilkan Seluruh Atribut pada Model Item di Halaman Detail:

Di ProductDetailPage, saya menampilkan semua atribut dari product, seperti ditunjukkan dalam contoh kode di atas.

10. Menambahkan Tombol untuk Kembali ke Halaman Daftar Item:

Flutter secara default menyediakan tombol kembali di AppBar saat menggunakan Navigator.push(). Jadi, pengguna dapat kembali ke halaman daftar item dengan menggunakan tombol kembali bawaan.

</details>