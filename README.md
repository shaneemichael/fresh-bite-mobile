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

* `const`: Menandakan bahwa nilai suatu variabel bersifat konstan dan harus ditentukan saat kompilasi. Nilai `const` tidak dapat diubah dan berlaku secara tetap di seluruh siklus hidup program. const umumnya digunakan untuk objek atau nilai yang tidak akan pernah berubah dan sudah diketahui sebelum runtime, seperti `const` pi = 3.14.

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