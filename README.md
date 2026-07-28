Markdown
# BAB 1: Dasar-Dasar Pemrograman Berorientasi Objek (PBO) & Setup Laravel

Selamat datang di repository pembelajaran **Pemrograman Berorientasi Objek (PBO)** untuk Kelas XI PPLG / RPL. Repository ini berisi materi teori, contoh kode PHP Native, serta panduan praktikum penginstalan framework Laravel dari awal.

---

## 📋 Daftar Isi
1. [Identifikasi & Konsep PBO](#1-identifikasi--konsep-pbo)
2. [Komponen Utama PBO](#2-komponen-utama-pbo)
3. [Empat Pilar Utama PBO](#3-empat-pilar-utama-pbo)
4. [Implementasi Kode PHP Native](#4-implementasi-kode-php-native)
5. [Panduan Praktikum: Setup Environment & Installasi Laravel](#5-panduan-praktikum-setup-environment--installasi-laravel)
6. [Penerapan PBO pada Framework Laravel](#6-penerapan-pbo-pada-framework-laravel)
7. [Tugas Mandiri](#7-tugas-mandiri)

---

## 1. Identifikasi & Konsep PBO

### A. Apa itu PBO / OOP?
**Pemrograman Berorientasi Objek (Object-Oriented Programming / OOP)** adalah paradigma atau tata cara pembuatan program menggunakan konsep **Object**. Objek ini memiliki data (*property/attribute*) dan prosedur/fungsi (*method*).

### B. Perbandingan: Prosedural vs PBO
* **Pemrograman Prosedural:** Berfokus pada langkah-langkah linier dari atas ke bawah. Ketika aplikasi membesar, kode menjadi sulit dikelola dan rentan berantakan (*spaghetti code*).
* **Pemrograman Berorientasi Objek (PBO):** Mengorganisasikan program ke dalam **Class** dan **Object** yang saling berinteraksi secara modular, sehingga kode lebih rapi, reusable, dan mudah dikembangkan.

### C. Penggunaan PBO
PBO digunakan secara luas dalam bahasa seperti PHP, Java, C#, Python, dan C++. Pada ekosistem PHP modern, framework seperti **Laravel** dibangun 100% menggunakan paradigma PBO.

---

## 2. Komponen Utama PBO

| Komponen | Penjelasan | Contoh Dunia Nyata |
| :--- | :--- | :--- |
| **Class** | Draf, rancangan, atau *blueprint* yang mendeskripsikan struktur dan perilaku objek. | Cetakan / Gambar teknik mobil |
| **Object** | Wujud nyata (*instansiasi*) yang dibuat dari sebuah Class. | Mobil fisik hasil cetakan (Toyota, Honda) |
| **Property / Attribute** | Variabel di dalam class yang menyimpan data/karakteristik objek. | Warna, Merk, Kecepatan Maksimum |
| **Method / Function** | Fungsi di dalam class yang mendeskripsikan aksi/perilaku objek. | `tambahKecepatan()`, `mengeram()` |

---

## 3. Empat Pilar Utama PBO

1. **Abstraction (Abstraksi):** Proses menentukan data dan method yang dimiliki oleh suatu class dengan melihat objek dalam bentuk yang lebih umum/sederhana.
2. **Encapsulation (Enkapsulasi):** Proses penyatuan data bersama method-nya ke dalam satu wadah (class) untuk menjaga keamanan data agar tidak diakses secara sembarangan.
3. **Inheritance (Pewarisan):** Konsep mewariskan property dan method milik class induk (*super class*) kepada class turunannya (*child class*).
4. **Polymorphism (Polimorfisme):** Memungkinkan penggunaan nama interface/method yang sama pada objek berbeda, namun dengan mekanisme kerja internal yang disesuaikan.

---

## 4. Implementasi Kode PHP Native

File contoh kode dapat kalian lihat dan jalankan di folder [`01-php-native/dasar_pbo.php`](01-php-native/dasar_pbo.php).

```php
<?php

// 1. MEMBUAT CLASS (Blueprint / Cetakan)
class Mobil {
    // Property (Attribute / Data)
    public $merk;
    public $warna;
    public $kecepatan = 0;

    // Method (Aksi / Perilaku)
    public function tambahKecepatan($tambahan) {
        // Keyword '$this' merujuk pada objek yang sedang aktif
        $this->kecepatan +=$tambahan;
        return "Mobil " . $this->merk . " berwarna " . $this->warna . " sedang melaju " . $this->kecepatan . " km/jam!";
    }

    public function mengeram() {
        return "Mobil " . $this->merk . " sedang mengeram.";
    }
}

// 2. MEMBUAT OBJECT (Instansiasi dengan keyword 'new')
$mobilSatu = new Mobil();$mobilSatu->merk = "Toyota Supra";
$mobilSatu->warna = "Merah";

$mobilDua = new Mobil();$mobilDua->merk = "Honda Civic";
$mobilDua->warna = "Hitam";

// 3. MEMANGGIL METHOD MENGGUNAKAN OPERATOR '->'
echo $mobilSatu->tambahKecepatan(80); 
// Output: Mobil Toyota Supra berwarna Merah sedang melaju 80 km/jam!

echo "<br>";

echo $mobilDua->mengeram();
// Output: Mobil Honda Civic sedang mengeram.

?>
Simbol Penting dalam PHP PBO:
new : Perintah untuk membuat Object baru dari sebuah Class.

-> : Operator untuk mengakses Property atau Method milik objek.

$this : Variabel khusus yang merujuk pada objek yang sedang dieksekusi di dalam Class.

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
Jalankan perintah berikut untuk mengunduh dan membuat project Laravel bernama pbo-laravel:

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

6. Penerapan PBO pada Framework Laravel
Di dalam Laravel, konsep PBO terimplementasi penuh pada arsitektur MVC (Model-View-Controller).

A. Model (Representasi Database & Inheritance)
Di Laravel, setiap tabel database diwakili oleh Class Model yang mewarisi sifat dari Class Model bawaan Laravel (extends):

PHP
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

// Class 'Siswa' mewarisi (Inheritance) fungsi dari Class Model bawaan
class Siswa extends Model {
    protected $table = 'siswa';
}
B. Controller (Logika Aplikasi)
Controller di Laravel berfungsi mengatur logika program dengan menggunakan Class dan Method.

Langkah Praktikum Controller:

Buka terminal di VS Code, ketik perintah Artisan berikut:

Bash
php artisan make:controller SiswaController
Buka file app/Http/Controllers/SiswaController.php, lalu sesuaikan kodenya:

PHP
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class SiswaController extends Controller 
{
    public $sekolah = "SMK Negeri 1";

    public function index() 
    {
        $namaSiswa = "Ahmad";
        $kelas = "XI PPLG 1";

        return "Halo! Nama saya " . $namaSiswa . " (" . $kelas . ") dari " . $this->sekolah;
    }
}
Daftarkan Controller pada file routes/web.php:

PHP
use App\Http\Controllers\SiswaController;

Route::get('/siswa', [SiswaController::class, 'index']);
Akses melalui browser pada alamat: http://127.0.0.1:8000/siswa.

7. Tugas Mandiri
Buatlah sebuah class baru bernama Laptop (bisa di PHP native atau buat LaptopController di Laravel) dengan ketentuan:

Property: $merk, $ram, dan $prosesor.

Method: tampilkanSpesifikasi() yang mengembalikan deskripsi laptop tersebut.

Buat 2 Object laptop yang berbeda (contoh: ASUS dan Lenovo), lalu tampilkan hasilnya di browser!

Catatan: Kerjakan tugas mandiri di komputer masing-masing. Jika ada kendala error, silakan tanyakan langsung saat jam praktikum berlangsung.


<ElicitationsGroup message="Pilih langkah lanjutan yang ingin Anda ketahui:">
  <Elicitation label="Berikan panduan langkah-langkah mengunggah file ini ke GitHub via Git CLI" query="Bagaimana cara mengunggah file README.md dan materi Bab 1 dari komputer ke repository GitHub menggunakan perintah Git CLI?"/>
  <Elicitation label="Buatkan template struktur folder repository yang rapi untuk kelas PBO" query="Berikan saran struktur folder repository GitHub yang ideal untuk menampung seluruh materi PBO dari Bab 1 sampai akhir semester."/>
</ElicitationsGroup>
