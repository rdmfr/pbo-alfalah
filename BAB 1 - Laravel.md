BAB 1: DASAR-DASAR PEMROGRAMAN BERORIENTASI OBJEK (PBO) DALAM FRAMEWORK LARAVEL
1. PENGENALAN KONSEP PBO (OOP) DENGAN BAHASA AWAM
A. Apa itu PBO / OOP?
Pernahkah kamu bermain game seperti Mobile Legends, Free Fire, atau GTA?
Di dalam game tersebut, terdapat berbagai macam elemen seperti Hero, Monster, Mobil, atau Senjata. Di dalam dunia pemrograman, semua elemen itu disebut sebagai OBJECT (OBJEK).

Pemrograman Berorientasi Objek (PBO) atau Object-Oriented Programming (OOP) adalah cara membuat program dengan mengelompokkan kode berdasarkan "Benda/Objek" di dunia nyata, bukan sekadar menulis deretan perintah dari atas ke bawah.

Setiap objek di dalam program memiliki 2 komponen utama:

Atribut / Data (Ciri-cirinya): Contoh pada Hero ML → Nama, Darah (HP), Level, dan Role.

Perilaku / Aksi (Yang bisa dia lakukan): Contoh pada Hero ML → Berjalan, Menyerang, dan Menggunakan Skill.

B. Perbandingan: Cara Lama (Prosedural) vs Cara PBO
Bayangkan kamu sedang mengelola sebuah Bengkel Motor:

Cara Lama (Prosedural):
Kamu mencatat semua stok barang, data mekanik, transaksi pembeli, dan keuangan di satu buku catatan panjang dari halaman 1 sampai akhir. Jika bengkel makin besar dan catatan makin tebal, kamu akan sangat pusing mencari data tertentu dan rentan salah coret (Spaghetti Code).

Cara PBO (Berorientasi Objek):
Kamu membuat Formulir khusus Motor, Formulir khusus Transaksi, dan Formulir khusus Pembeli. Kodenya terpisah-pisah secara rapi sesuai dengan fungsi dan wujud fisiknya. Jika ada masalah pada transaksi, kamu cukup membuka Formulir Transaksi tanpa mengganggu data lainnya.

2. KOMPONEN UTAMA PBO DI LARAVEL
Laravel dibangun 100% menggunakan konsep PBO modern. Seluruh aplikasi Laravel dijalankan oleh 4 komponen utama berikut.

Analogi Sederhana: Cetakan Kue vs Kue Nyata

Class (Cetakan Kue)⟶Dibuat Menjadi⟶Object (Kue Nyata)

Plaintext
+-----------------------------------+       +-----------------------------------+
|              CLASS                |       |              OBJECT               |
|      (Cetakan / Blueprint)        | ----> |       (Hasil Wujud Nyata)         |
|  - Property : $rasa, $warna       |       |  - Property : "Cokelat", "Merah"  |
|  - Method   : panggang()          |       |  - Method   : Siap Dimakan!       |
+-----------------------------------+       +-----------------------------------+
Penjelasan 4 Komponen:
Class (Cetakan / Blueprint):

Penjelasan: Rancangan atau cetakan utama. Cetakan kue sendiri belum bisa dimakan, tetapi berfungsi sebagai patokan bentuk dan aturan pembuatan kue.

Di Laravel: Berupa file Controller (contoh: SiswaController.php) atau file Model (contoh: Siswa.php).

Object (Bentuk Nyata / Instansiasi):

Penjelasan: Kue fisik yang sudah jadi dari cetakan tersebut. Dari 1 cetakan, kita bisa membuat puluhan kue nyata dengan variasi warna atau rasa yang berbeda.

Di Laravel: Data nyata yang diambil dari database atau variabel hasil pemanggilan class.

Property (Variabel di dalam Class):

Penjelasan: Ciri-ciri, identitas, atau data yang ditempelkan pada objek.

Contoh: HP memiliki property $merk, $ram, dan $harga.

Di Laravel: Variabel yang ditulis di dalam class, contoh: public $namaSekolah = "SMK Negeri 1";.

Method (Fungsi di dalam Class):

Penjelasan: Perilaku, aksi, atau tombol fungsi yang bisa dijalankan oleh objek.

Contoh: HP memiliki method ambilFoto() dan casBaterai().

Di Laravel: Fungsi yang ditulis di dalam class, contoh: public function tampilkanProfil() { ... }.

3. EMPAT PILAR UTAMA PBO DALAM LARAVEL
Di dalam dunia PBO, terdapat 4 aturan/prinsip utama yang diterapkan langsung oleh framework Laravel:

Plaintext
                  +-----------------------------------+
                  |        4 PILAR UTAMA PBO          |
                  +-----------------------------------+
                    /          |         |          \
                   /           |         |           \
        Inheritance      Encapsulation  Abstraction   Polymorphism
       (Pewarisan)       (Keamanan)   (Penyederhanaan) (Banyak Bentuk)
Inheritance (Pewarisan Sifat):

Bahasa Awam: Seperti sifat seorang anak yang diturunkan dari orang tuanya. Sang anak otomatis memiliki warna kulit atau bentuk rambut dari orang tuanya tanpa perlu dibuat dari awal.

Di Laravel: Terlihat pada sintaks class MobilController extends Controller. Artinya, MobilController otomatis mewarisi semua fitur dan kemampuan canggih bawaan Controller milik Laravel.

Encapsulation (Pembungkusan / Keamanan Data):

Bahasa Awam: Seperti kapsul obat atau casing HP. Mesin dan kabel HP yang rumit dibungkus rapat di dalam casing agar aman dan pengguna tidak asal mencolok komponen internal.

Di Laravel: Penggunaan kata kunci public, protected, atau private pada variabel agar data penting aplikasi tidak diubah sembarangan dari luar.

Abstraction (Penyederhanaan):

Bahasa Awam: Saat kamu menyalakan TV, kamu hanya perlu menekan Tombol Power pada remote. Kamu tidak perlu tahu bagaimana arus listrik dan gelombang sinyal bekerja di dalam mesin TV.

Di Laravel: Kamu cukup mengetik Siswa::all() untuk mengambil seluruh data siswa dari database, tanpa harus pusing menulis perintah SQL yang panjang dan rumit.

Polymorphism (Banyak Bentuk):

Bahasa Awam: Perintahnya sama, tetapi cara kerjanya berbeda. Contoh perintah: "Bergerak!". Jika diberikan ke Burung ia akan terbang, jika ke Ikan ia akan berenang.

4. PRAKTIKUM: IMPLEMENTASI PBO PADA CONTROLLER LARAVEL
Mari kita praktikkkan konsep Class, Property, dan Method secara langsung pada Controller Laravel.

Langkah 1: Membuat Controller (Class)
Buka Terminal / Command Prompt pada VS Code project Laravel kalian, lalu jalankan perintah berikut:

Bash
php artisan make:controller MobilController
Langkah 2: Menulis Kode PBO pada Controller
Buka file app/Http/Controllers/MobilController.php, lalu ubah isi kodenya menjadi seperti berikut:

PHP
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

// 1. CLASS: MobilController mewarisi (extends) sifat dari Class Controller bawaan Laravel
class MobilController extends Controller
{
    // 2. PROPERTY: Identitas / Data dari objek
    public $merk = "Toyota Supra";
    public $warna = "Merah";
    public $kecepatan = 0;

    // 3. METHOD 1: Aksi untuk menambah kecepatan
    public function tambahKecepatan()
    {
        // Keyword '$this' digunakan untuk mengakses property milik Class ini sendiri
        $this->kecepatan += 50;

        return "Mobil " . $this->merk . " berwarna " . $this->warna . " sedang melaju dengan kecepatan " . $this->kecepatan . " km/jam.";
    }

    // METHOD 2: Aksi untuk mengerem
    public function mengeram()
    {
        return "Mobil " . $this->merk . " sedang melakukan pengeraman.";
    }
}
Langkah 3: Menghubungkan ke Route (Routing Web)
Buka file routes/web.php, lalu tambahkan jalur panggilan berikut di baris paling bawah:

PHP
use App\Http\Controllers\MobilController;

// Jalur 1: Memanggil method 'tambahKecepatan'
Route::get('/mobil/gas', [MobilController::class, 'tambahKecepatan']);

// Jalur 2: Memanggil method 'mengeram'
Route::get('/mobil/rem', [MobilController::class, 'mengeram']);
Langkah 4: Pengujian pada Browser
Pastikan server lokal sudah menyala (php artisan serve).

Buka browser dan akses alamat berikut:

[http://127.0.0.1:8000/mobil/gas](http://127.0.0.1:8000/mobil/gas)

[http://127.0.0.1:8000/mobil/rem](http://127.0.0.1:8000/mobil/rem)

5. RANGKUMAN BAB 1
PBO (OOP) adalah metode pemrograman berbasis objek yang mengelompokkan data (property) dan aksi (method).

Class adalah cetakannya (blueprint), sedangkan Object adalah wujud nyatanya.

Seluruh file Controller dan Model di Laravel berbentuk Class yang saling terhubung.

Tanda -> digunakan untuk mengakses Property atau Method di dalam Laravel, dan variabel $this digunakan untuk merujuk ke isi Class itu sendiri.

6. TUGAS MANDIRI SISWA
Kerjakan latihan berikut pada project Laravel masing-masing:

Buatlah sebuah Controller baru bernama LaptopController melalui terminal Artisan!

Buatlah 3 Property di dalam LaptopController:

$merk (isi dengan merk laptop pilihanmu, contoh: "Asus ROG")

$ram (isi dengan kapasitas RAM, contoh: "16 GB")

$prosesor (isi dengan tipe prosesor, contoh: "Intel Core i7")

Buatlah 1 Method bernama spesifikasi() yang mengembalikan teks kalimat gabungan dari seluruh property di atas menggunakan variabel $this!

Hubungkan Controller tersebut ke file routes/web.php dengan jalur URL /laptop!

Buka [http://127.0.0.1:8000/laptop](http://127.0.0.1:8000/laptop) di browser dan pastikan output spesifikasi laptop tampil dengan benar!


Buatkan Lembar Kerja Peserta Didik (LKPD) / Soal Latihan untuk Bab 1 ini
