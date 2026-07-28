# BAB 1: Dasar-Dasar Pemrograman Berorientasi Objek (PBO) dalam Framework Laravel

Selamat datang di repository pembelajaran **Pemrograman Berorientasi Objek (PBO)** untuk Kelas XI PPLG / RPL. Pada bab ini, kita akan mempelajari konsep dasar PBO secara langsung menggunakan framework **Laravel**.

---

## 📋 Daftar Isi
1. [Penjelasan PBO dengan Bahasa Awam](#1-penjelasan-pbo-dengan-bahasa-awam)
2. [Perbandingan: Cara Lama (Prosedural) vs PBO](#2-perbandingan-cara-lama-prosedural-vs-pbo)
3. [Empat Komponen Utama PBO di Laravel](#3-empat-komponen-utama-pbo-di-laravel)
4. [Empat Pilar Utama PBO di Laravel](#4-empat-pilar-utama-pbo-di-laravel)
5. [Panduan Praktikum: Setup Environment & Installasi Laravel](#5-panduan-praktikum-setup-environment--installasi-laravel)
6. [Praktikum: Menerapkan Class, Property, & Method pada Controller](#6-praktikum-menerapkan-class-property--method-pada-controller)
7. [Tugas Mandiri](#7-tugas-mandiri)

---

## 1. Penjelasan PBO dengan Bahasa Awam

### Apa itu PBO / OOP?
Bayangkan kamu sedang bermain game seperti **Mobile Legends** atau **GTA**. 
* Di dalam game tersebut, ada karakter **Hero**, **Siput/Monster**, **Mobil**, dan **Senjata**.
* Semua hal di dalam game itu disebut sebagai **OBJEC / OBJEK**.

**PBO (Pemrograman Berorientasi Objek)** adalah cara membuat program dengan mengelompokkan kode berdasarkan "Benda/Objek" nyata, bukan sekadar kumpulan perintah dari atas ke bawah. Setiap objek di dalam program punya dua hal:
1. **Atribut / Data (Ciri-cirinya):** Misal Hero punya *Darah (HP)*, *Nama*, dan *Level*.
2. **Perilaku / Aksi (Yang bisa dia lakukan):** Misal Hero bisa *Jalan*, *Pukul*, atau *Gunakan Skill*.

---

## 2. Perbandingan: Cara Lama (Prosedural) vs PBO

Bayangkan kamu mengelola toko sepeda motor:

* **Cara Lama (Prosedural):**
  Kamu mencatat semua transaksi, stok, data pembeli, dan harga di **satu buku catatan panjang** dari halaman 1 sampai selesai. Kalau catatan makin tebal, kamu bakal pusing mencari data dan rentan salah coret (*spaghetti code*).

* **Cara PBO (Berorientasi Objek):**
  Kamu membuat **Formulir khusus Motor** dan **Formulir khusus Pembeli**. Setiap ada motor baru, kamu tinggal isi formulirnya. Kodenya terpisah-pisah secara rapi sesuai bentuk fisiknya, sehingga gampang dicari, diperbaiki, dan diperbanyak.

---

## 3. Empat Komponen Utama PBO di Laravel

Dalam framework Laravel, seluruh program disusun menggunakan 4 komponen ini. Supaya cepat paham, mari kita gunakan analogi **Cetakan Kue dan Kue Nyata**:

```text
[ CLASS / CETAKAN ]   ---> Dibuat jadi --->   [ OBJECT / KUE NYATA ]
  • Property : Rasa, Warna                      • Property : Cokelat, Merah
  • Method   : Dipanggang()                     • Method   : Siap Dimakan!
Penjelasan Sederhana:
Class (Cetakan / Blueprint):

Bahasa Awam: Cetakan kue atau gambar teknik pabrik. Cetakan ini belum bisa dimakan atau dinaiki, tapi berfungsi sebagai aturan/patokan pembuatan.

Di Laravel: File Controller (SiswaController.php) atau Model (Siswa.php).

Object (Bentuk Nyata / Instansiasi):

Bahasa Awam: Kue yang sudah jadi atau Mobil nyata yang sudah keluar dari pabrik. Dari 1 cetakan, kita bisa bikin ratusan kue/mobil nyata.

Di Laravel: Data nyata yang dipanggil dari database atau hasil dari new ClassName().

Property (Variabel di dalam Class):

Bahasa Awam: Ciri-ciri atau identitas objek. Contoh pada HP: Merk, Warna, Kapasitas Baterai.

Di Laravel: Variabel seperti public $nama; atau protected $table = 'siswa';.

Method (Fungsi di dalam Class):

Bahasa Awam: Aksi atau tombol fungsi yang bisa ditekan. Contoh pada HP: casBaterai(), ambilFoto().

Di Laravel: Fungsi seperti public function index().

4. Empat Pilar Utama PBO di Laravel
Empat pilar ini adalah "aturan main" utama dalam dunia PBO:

Inheritance (Pewarisan Sifat):

Bahasa Awam: Seperti sifat anak yang diturunkan dari orang tuanya. Anak otomatis punya warna kulit atau gaya rambut orang tuanya tanpa perlu dibuat dari nol.

Di Laravel: class MobilController extends Controller artinya MobilController otomatis mewarisi semua kemampuan canggih bawaan Class Controller milik Laravel.

Encapsulation (Pembungkusan / Keamanan):

Bahasa Awam: Seperti kapsul obat atau casing HP. Komponen mesin HP yang rumit dibungkus di dalam casing supaya aman dan pengguna tidak asal mencolok kabel mesin.

Di Laravel: Menggunakan kata kunci public, protected, atau private pada variabel agar data penting tidak diubah sembarangan dari luar.

Abstraction (Penyederhanaan):

Bahasa Awam: Saat kamu menyalakan TV, kamu cuma perlu menekan Tombol Power di remote. Kamu tidak perlu tahu bagaimana gelombang listrik bergerak di dalam mesin TV.

Di Laravel: Kamu cukup mengetik Siswa::all() untuk mengambil semua data siswa, tanpa perlu pusing menulis perintah SQL yang rumit.

Polymorphism (Banyak Bentuk):

Bahasa Awam: Perintahnya sama, tapi hasilnya beda. Contoh: Perintah "Bergerak". Jika diberikan ke Burung, dia akan terbang. Jika diberikan ke Ikan, dia akan berenang.

5. Panduan Praktikum: Setup Environment & Installasi Laravel
Ikuti langkah-langkah praktikum berikut di komputer lab/laptop masing-masing:

Langkah 1: Cek Tools
Buka Terminal / Git Bash / CMD, lalu jalankan perintah berikut untuk memastikan PHP dan Composer siap:

Bash
php -v
composer -v
Langkah 2: Masuk ke Folder Kerja
Pindahkan direktori terminal ke folder penyimpanan projek kalian (misalnya folder htdocs di XAMPP):

Bash
cd C:/xampp/htdocs
Langkah 3: Install Project Laravel Baru
Jalankan perintah berikut untuk mengunduh dan membuat project Laravel baru bernama pbo-laravel:

Bash
composer create-project laravel/laravel pbo-laravel
Langkah 4: Buka Project di VS Code
Masuk ke folder project yang telah dibuat, lalu buka di Visual Studio Code:

Bash
cd pbo-laravel
code .
Langkah 5: Jalankan Server Lokal
Nyalakan server bawaan Laravel dengan menjalankan perintah Artisan berikut di terminal VS Code:

Bash
php artisan serve
Buka browser dan akses alamat http://127.0.0.1:8000. Jika halaman utama Laravel tampil, maka instalasi berhasil.

6. Praktikum: Menerapkan Class, Property, & Method pada Controller
Mari kita buat sebuah Controller untuk mempraktikkan komponen PBO langsung di Laravel.

Langkah 1: Membuat Controller (Cetakan)
Buka Terminal di VS Code, lalu jalankan perintah Artisan berikut:

Bash
php artisan make:controller MobilController
Langkah 2: Menulis Kode PBO pada Controller
Buka file app/Http/Controllers/MobilController.php, lalu ubah kode di dalamnya menjadi seperti berikut:

PHP
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

// 1. CLASS (Cetakan Utama): Mewarisi sifat dari Controller bawaan Laravel
class MobilController extends Controller
{
    // 2. PROPERTY (Ciri-ciri/Data):
    public $merk = "Toyota Supra";
    public $warna = "Merah";
    public $kecepatan = 0;

    // 3. METHOD (Aksi/Perilaku):
    public function tambahKecepatan()
    {
        // Keyword '$this' artinya: "Ambil variabel milik Class SAYA SENDIRI"
        $this->kecepatan += 50;

        return "Mobil " . $this->merk . " berwarna " . $this->warna . " melaju dengan kecepatan " . $this->kecepatan . " km/jam.";
    }

    public function mengeram()
    {
        return "Mobil " . $this->merk . " sedang mengeram (mengerem).";
    }
}
Langkah 3: Menghubungkan ke Route (Jalur Web)
Buka file routes/web.php, tambahkan Route berikut di bagian paling bawah untuk memanggil method yang ada di Controller:

PHP
use App\Http\Controllers\MobilController;

// Jalur 1: Memanggil method 'tambahKecepatan'
Route::get('/mobil/gas', [MobilController::class, 'tambahKecepatan']);

// Jalur 2: Memanggil method 'mengeram'
Route::get('/mobil/rem', [MobilController::class, 'mengeram']);
Langkah 4: Uji Coba di Browser
Pastikan server php artisan serve tetap berjalan, lalu buka browser dan akses URL berikut:

http://127.0.0.1:8000/mobil/gas

http://127.0.0.1:8000/mobil/rem

7. Tugas Mandiri
Buatlah sebuah Controller baru di Laravel untuk menerapkan konsep PBO secara mandiri dengan ketentuan sebagai berikut:

Buat Controller bernama LaptopController menggunakan perintah Artisan di terminal:

Bash
php artisan make:controller LaptopController
Buatlah 3 Property (variabel) di dalam LaptopController:

$merk (misal: "Asus ROG")

$ram (misal: "16 GB")

$prosesor (misal: "Intel Core i7")

Buatlah 1 Method bernama spesifikasi() yang mengembalikan kalimat deskripsi gabungan dari seluruh property tersebut menggunakan keyword $this.

Daftarkan Controller ke dalam file routes/web.php dengan alur route /laptop.

Buka http://127.0.0.1:8000/laptop di browser dan pastikan output spesifikasi laptop tampil dengan benar!

Tips Saat Koding:

Jika di browser muncul error "Class Not Found", periksa apakah kamu sudah menulis baris use App\Http\Controllers\LaptopController; di file routes/web.php.

Jangan lupa selalu akhiri setiap baris kode PHP dengan tanda titik koma (;).


<ElicitationsGroup message="Pilih opsi lanjutan yang Anda perlukan untuk persiapan kelas:">
  <Elicitation label="Buatkan cheatsheet perintah Git CLI untuk upload file ini ke GitHub" query="Berikan ringkasan perintah Git CLI untuk mengunggah file README.md ini ke repository GitHub dari awal."/>
  <Elicitation label="Lanjutkan ke materi Bab 2: Constructor (__construct) dan Access Modifiers" query="Buatkan materi kelanjutan Bab 2 full Laravel mengenai Constructor (__construct) dan Access Modifiers (Public, Protected, Private) dalam format README.md."/>
</ElicitationsGroup>
