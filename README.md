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