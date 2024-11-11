# Tugas Individu 7 #

#### Stateless widget dan stateful widget, serta perbedaannya. ####

Stateless widget merupakan widget yang tidak memiliki state internal dan tidak dapat berubah setelah dibuat. Artinya, tampilan yang dibuat oleh stateless widget akan tetap sama selama program berjalan; jika ada perubahan, widget harus dibuat ulang dari awal. Contoh stateless widget adalah `Text`, `Icon`, dan `Image`. 

Di sisi lain, stateful widget adalah widget yang memiliki state dan dapat mengalami perubahan tampilan seiring perubahan state internalnya. Stateful widget memiliki dua komponen, yaitu kelas widget itu sendiri dan kelas state yang menangani logika dan perubahan data. Misalnya, saat pengguna menekan tombol atau mengetik dalam field input, state dalam stateful widget bisa diperbarui, dan widget akan render ulang dirinya untuk mencerminkan perubahan tersebut. Contoh stateful widget adalah `Checkbox`, `Slider`, dan `TextField`. 

Berikut perbedaan utama dari stateless widget dan stateful widget:
1) Perubahan State
   * Stateless: Tidak dapat mengubah state internal
   * Stateful: Dapat mengubah state menggunakan setState()

2) Lifecycle
   * Stateless: Hanya memiliki method build()
   * Stateful: Memiliki lifecycle lebih kompleks (initState, dispose, dll)

3) Performa
   * Stateless: Lebih ringan dan cepat
   * Stateful: Membutuhkan lebih banyak resource

4) Penggunaan
   * Stateless: UI statis, tampilan yang tidak berubah
   * Stateful: UI dinamis, interaktif, form input

5) Rebuild
   * Stateless: Di-rebuild saat parent widget berubah
   * Stateful: Di-rebuild saat setState() dipanggil atau parent berubah

#### Widget yang digunakan pada proyek ini serta fungsinya. ####

1) `Scaffold`: Memberikan struktur dasar layout aplikasi, seperti AppBar, Body, dan Bottom Navigation.
2) `AppBar`: Menampilkan section di bagian atas layar dengan judul, ikon, dan tindakan penting.
3) `Column dan Row`: Menyusun widget secara vertikal (Column) atau horizontal (Row) untuk layout yang rapi.
4) `Padding`: Menambahkan ruang di sekitar widget sebagai jarak.
5) `InfoCard`: Custom widget untuk menampilkan informasi dalam format kartu dengan judul dan konten.
6) `ItemCard`: Menampilkan item individual dengan icon dan text, memudahkan navigasi.
7) `InkWell`: Memberikan efek ripple saat pengguna berinteraksi dengan item, meningkatkan feedback visual.
8) `SnackBar`: Menampilkan pesan singkat di bagian bawah layar sebagai respons tindakan.
9) `MaterialApp`: Membungkus aplikasi dan mengatur konfigurasi global seperti tema dan rute.
10) `ThemeData`: Mengatur skema warna dan gaya tema aplikasi untuk konsistensi visual.

#### Fungsi dari `setState()` serta variabel yang dapat terdampak dengan fungsi tersebut. ####

Fungsi `setState()` digunakan dalam widget stateful di Flutter untuk memberi tahu framework bahwa ada perubahan pada state internal widget, yang membutuhkan pembaruan tampilan (UI). Ketika `setState()` dipanggil, Flutter menjalankan kembali metode `build()` widget untuk memperbarui UI sesuai dengan perubahan data atau variabel di dalam state.

Variabel yang dapat terdampak oleh `setState()` adalah variabel yang didefinisikan di dalam kelas state dan bersifat dinamis, seperti variabel yang merepresentasikan data UI atau status sementara. Contohnya meliputi variabel yang menyimpan teks, nilai checkbox, posisi slider, atau data item dalam daftar yang mungkin berubah karena interaksi pengguna. Dengan `setState()`, perubahan pada variabel-variabel ini langsung terlihat pada antarmuka pengguna tanpa perlu merender ulang seluruh aplikasi.

#### Jelaskan perbedaan antara `const` dengan `final`. ####

* `const`: Menandakan bahwa nilai suatu variabel bersifat konstan dan harus ditentukan saat kompilasi. Nilai `const` tidak dapat diubah dan berlaku secara tetap di seluruh siklus hidup program. const umumnya digunakan untuk objek atau nilai yang tidak akan pernah berubah dan sudah diketahui sebelum runtime, seperti `const pi = 3.14`.

* `final`: Menandakan bahwa nilai variabel bersifat final, yaitu hanya dapat diinisialisasi sekali. Namun, nilai `final` bisa ditentukan pada saat runtime, bukan hanya saat kompilasi. Misalnya, `final currentTime = DateTime.now();` valid karena nilainya baru dihasilkan ketika program berjalan.

#### Implementasi checklist step by step ####

1) Membuat project Flutter baru dengan tema E-commerce, kemudian melakukan run. Cara melakukannya adalah sebagai berikut:
   ```
   flutter create fresh_bite
   cd fresh_bite
   flutter run
   ```

2) Membuat file `menu.dart` pada direktori yang sama dengan `main.dart` dengan memindahkan sebagian besar kode dari `main.dart`ke `menu.dart`, dan meng-import `menu.dart` pada `main.dart`

3) Menambahkan beberapa class pada `menu.dart`, seperti `ItemHomepage` dan `Itemcard` yang bertujuan untuk men-display 3 objek.

4) Mengimplementasikan warna yang berbeda pada setiap tombol yang ada. Saya menggunakan tema yang sama seperti "Subway" (brand sandwich) dan mendapatkan referensi color pallete dari internet.

5) Memunculkan snackbar dengan tulisan:
   * "Kamu telah menekan tombol Lihat Daftar Produk" ketika tombol `Lihat Daftar Produk` ditekan.
   * "Kamu telah menekan tombol Tambah Produk" ketika tombol `Tambah Produk` ditekan.
   * "Kamu telah menekan tombol Logout" ketika tombol `Logout` ditekan.

   Caranya adalah dengan menambahkan:
   ```
   child: InkWell(
    // Aksi ketika kartu ditekan.
    onTap: () {
        // Menampilkan pesan SnackBar saat kartu ditekan.
        ScaffoldMessenger.of(context)
        ..hideCurrentSnackBar()
        ..showSnackBar(
            SnackBar(content: Text("Kamu telah menekan tombol ${item.name}!"))
        );
    },
    ....
    ```

# Tugas Individu 8 #

#### Kegunaan dan keuntungan `const` pada Flutter serta waktu ketika sebaiknya digunakan dan tidak digunakan. ####
Pada Flutter, `const` digunakan untuk mendefinisikan content atau widget yang bersifat immutable (tidak dapat berubah) dan diinisialisasi saat compile time.  Artinya, nilai yang dideklarasikan dengan const tidak akan berubah selama aplikasi berjalan. Hal ini akan berpengaruh pada optimisasi memori, performa, dan keamanan terhadap perubahan.

Kapan menggunakan `const` pada Flutter:
* Untuk widget yang statis: Apabila kita memiliki widget yang isinya tidak akan berubah selama siklus hidup aplikasi, gunakan const. Contohnya adalah `Text`, `Icon`, atau `Container` yang memiliki warna atau ukuran tetap.
* Saat menggunakan nilai konstan: Jika nilai dalam widget bersifat tetap, misalnya teks atau ukuran, maka mendeklarasikannya dengan `const` lebih baik untuk kinerja dan memori.
* Reusable components: Kita sebaiknya menggunakan const untuk widget atau nilai konstan yang sering digunakan kembali di banyak tempat dalam aplikasi. Misalnya, warna tema aplikasi atau standard padding.

Kapan tidak menggunakan `const` pada Flutter:
* Untuk Widget Dinamis: Kita sebaiknya menghindari penggunaan `const` jika nilai widget bisa berubah berdasarkan keadaan atau interaksi pengguna, misal hasil dari API atau input pengguna. 
* Apabila menggunakan object variable yang nilainya bisa berubah-ubah.

#### Penggunaan `Column` dan `Row` pada Flutter, serta contoh implementasinya. ####
Di Flutter, `Column` dan `Row` adalah widget layout yang digunakan untuk mengatur posisi dan susunan widget child di layar. Column mengatur widget secara vertikal (dari atas ke bawah), sedangkan Row mengatur widget secara horizontal (dari kiri ke kanan).

Properti utama `column`:
* `mainAxisAlignment`: Mengatur posisi child pada main axis (sumbu utama) Column, yaitu vertikal.
* `crossAxisAlignment`: Mengatur posisi child pada cross axis (sumbu silang), yaitu horizontal.
* `children`: Daftar widget child yang ingin disusun secara vertikal.

Implementasinya:
```
Column(
  mainAxisAlignment: MainAxisAlignment.center, // Align secara vertikal, disusun di tengah, widget tersusun dari atas ke bawah
  crossAxisAlignment: CrossAxisAlignment.start, // Align secara horizontal, disusun mulai dari kiri
  children: [
    Text('Hello, Flutter!'),
    SizedBox(height: 10), // Jarak antar widget
    Icon(Icons.star, color: Colors.amber),
    ElevatedButton(onPressed: () {}, child: Text('Click Me'))
  ],
)
```

Properti utama `row`:
* `mainAxisAlignment`: Mengatur posisi child pada main axis Row, yaitu horizontal.
* `crossAxisAlignment`: Mengatur posisi child pada cross axis, yaitu vertikal.
* `children`: Daftar widget child yang ingin disusun secara horizontal.

Implementasi:
```
Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround, // Sebar widget secara merata, widget tersusun dari kiri ke kanan
  crossAxisAlignment: CrossAxisAlignment.center, // Align widget di tengah secara vertikal
  children: [
    Icon(Icons.home, color: Colors.blue),
    Icon(Icons.search, color: Colors.green),
    Icon(Icons.settings, color: Colors.grey),
  ],
)
```

#### Elemen input yang digunakan pada halaman form yang dibuat pada tugas kali ini. ####
Elemen input yang digunakan:
1) `TextFormField`yang digunakan pada `Nama Produk`, `Harga`, serta `Deskripsi` dengan validasi harus terdapat input (input tidak boleh kosong). Khusus untuk `Harga`, terdapat tambahan validasi bahwa inputnya harus berupa angka.

Elemen input lainnya yang tidak digunakan:
1) TextField: Memungkinkan pengguna mengetik teks bebas, biasanya untuk mengisi formulir atau kolom pencarian.
2) Checkbox: Untuk memilih beberapa opsi secara bersamaan dari daftar pilihan yang ada.
3) Radio: Untuk memilih satu opsi dari sekumpulan pilihan yang saling eksklusif.
4) Switch: Memungkinkan pengguna mengaktifkan atau menonaktifkan opsi tertentu.
5) Slider: Elemen input berbentuk penggeser untuk memilih nilai dalam rentang tertentu, seperti volume atau brightness.
6) DropdownButton: Menu pilihan tarik-turun yang memungkinkan pengguna memilih satu opsi dari daftar yang tersedia.
7) DatePicker: Widget untuk memilih tanggal dari kalender.
8) TimePicker: Widget untuk memilih waktu, baik dalam format jam maupun menit.

#### Cara mengatur tema (theme) dalam aplikasi Flutter agar aplikasi yang dibuat konsisten. ####
Untuk kasus kali ini, saya memilih untuk menggunakan warna yang berbeda-beda dalam theme saya. Karena itu, saya tidak menggunakan primary dan secondary color dari `swatch`. Saya memutuskan untuk meng-assign warna nya satu per satu sehingga saya mempunyai kontrol yang bebas terhadap warna yang ingin saya gunakan.

Namun, sebenarnya Flutter mempunyai fitur tersendiri apabila kita ingin menggunakan warna yang sama untuk banyak bagian, yaitu menggunakan `swatch` yang diajarkan pada tutorial. Contohnya adalah sebagai berikut:
```
theme: ThemeData(
    colorScheme: ColorScheme.fromSwatch(
          primarySwatch: Colors.deepPurple,
    ).copyWith(secondary: Colors.deepPurple[400]),
  ),
```
`primarySwatch` akan menentukan warna utama / tema (theme) aplikasi yang digunakan di berbagai komponen penting, seperti `AppBar`, `FloatingActionButton`, dan lainnya. Sedangkan, secondary colornya akan digunakan untuk elemen-elemen kecil tambahan seperti `button`, `icon`, dan lain-lain. Dengan menggunakan fitur tersebut, pengguna dapat memastikan bahwa setiap perubahan yang dilakukan akan mengikuti theme yang sudah ditentukan.

#### Cara menangani navigasi dalam aplikasi dengan banyak halaman pada Flutter. ####
Untuk menangani navigasi di aplikasi Flutter dengan banyak halaman, teknik nested navigation digunakan, dengan bantuan Navigator dan MaterialPageRoute untuk memudahkan perpindahan halaman.

Navigator bekerja dengan sistem tumpukan (stack) di mana:

push() menambahkan route baru ke atas stack sehingga halaman baru ditampilkan,
pop() menghapus route di posisi teratas untuk kembali ke halaman sebelumnya, dan
pushReplacement() mengganti route teratas dengan route baru tanpa mengubah posisi stack di bawahnya.
Dengan MaterialPageRoute, kita dapat menentukan halaman tujuan dan menambah transisi antar halaman, memungkinkan navigasi sederhana seperti membuka halaman baru dengan Navigator.push() atau kembali ke halaman sebelumnya dengan Navigator.pop().