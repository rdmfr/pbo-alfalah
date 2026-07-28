# BAB 1: DASAR-DASAR PEMROGRAMAN BERORIENTASI OBJEK (PBO) & SETUP LARAVEL

## 1. IDENTIFIKASI & KONSEP PEMROGRAMAN BERORIENTASI OBJEK (PBO)

### A. Apa itu PBO / OOP?

**Pemrograman Berorientasi Objek (Object-Oriented Programming / OOP)** adalah paradigma atau tata cara pembuatan program menggunakan konsep **Object**. Objek ini memiliki data (*property/attribute*) dan prosedur/fungsi (*method*).

### B. Perbandingan: Prosedural vs PBO

* **Pemrograman Prosedural:** Berfokus pada langkah-langkah linier dari atas ke bawah. Ketika aplikasi membesar, kode menjadi sulit dikelola dan rentan berantakan (*spaghetti code*).
* **Pemrograman Berorientasi Objek (PBO):** Mengorganisasikan program ke dalam **Class** dan **Object** yang saling berinteraksi secara modular, sehingga kode lebih rapi, reusable, dan mudah dikembangkan.

### C. Penggunaan PBO

PBO digunakan secara luas dalam bahasa seperti PHP, Java, C#, Python, dan C++. Pada ekosistem PHP modern, framework seperti **Laravel** dibangun 100% menggunakan paradigma PBO.

---

## 2. KOMPONEN UTAMA PBO

| Komponen | Penjelasan | Contoh Dunia Nyata |
| --- | --- | --- |
| **Class** | Draf, rancangan, atau *blueprint* yang mendeskripsikan struktur dan perilaku objek. | Cetakan / Gambar teknik mobil |
| **Object** | Wujud nyata (*instansiasi*) yang dibuat dari sebuah Class. | Mobil fisik hasil cetakan (Toyota, Honda) |
| **Property / Attribute** | Variabel di dalam class yang menyimpan data/karakteristik objek. | Warna, Merk, Kecepatan Maksimum |
| **Method / Function** | Fungsi di dalam class yang mendeskripsikan aksi/perilaku objek. | `tambahKecepatan()`, `mengeram()` |

---

## 3. EMPAT PILAR UTAMA PBO

### a. Abstraction (Abstraksi)

* **Pengertian:** Proses menentukan data dan method yang dimiliki oleh suatu class dengan melihat objek dalam bentuk yang lebih umum/sederhana.
* **Fungsi:** Menyederhanakan sistem kompleks menjadi kumpulan subsistem yang mudah dipahami.
* **Contoh:** Class `Hewan` membawahi subsistem spesifik seperti `Sapi`, `Kambing`, dan `Kucing`.

### b. Encapsulation (Enkapsulasi)

* **Pengertian:** Proses penyatuan data bersama method-nya ke dalam satu wadah (class).
* **Fungsi:** Menyembunyikan rincian internal dan menjaga data agar tidak diakses secara sembarangan.

### c. Inheritance (Pewarisan)

* **Pengertian:** Konsep mewariskan property dan method milik class induk (*super class*) kepada class turunannya (*child class*).
* **Fungsi:** Efisiensi kode—class turunan tidak perlu menulis ulang kode yang sudah ada pada class induk.
* **Contoh:** Class `Kakek` $\rightarrow$ `Ayah` $\rightarrow$ `Anak`.

### d. Polymorphism (Polimorfisme)

* **Pengertian:** Memungkinkan penggunaan nama interface/method yang sama pada objek berbeda, namun dengan cara kerja yang disesuaikan.
* **Contoh:** Class `Mobil` dan Class `Motor` sama-sama memiliki method `melaju()`, namun mekanisme mesin internalnya berbeda.

---

## 4. IMPLEMENTASI KODE PBO PADA PHP NATIVE

Buat file baru bernama `dasar_pbo.php` di text editor kalian, lalu ketik kode berikut:

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
        $this->kecepatan += $tambahan;
        return "Mobil " . $this->merk . " berwarna " . $this->warna . " sedang melaju " . $this->kecepatan . " km/jam!";
    }

    public function mengeram() {
        return "Mobil " . $this->merk . " sedang mengeram.";
    }
}

// 2. MEMBUAT OBJECT (Instansiasi dengan keyword 'new')
$mobilSatu = new Mobil();
$mobilSatu->merk = "Toyota Supra";
$mobilSatu->warna = "Merah";

$mobilDua = new Mobil();
$mobilDua->merk = "Honda Civic";
$mobilDua->warna = "Hitam";

// 3. MEMANGGIL METHOD MENGGUNAKAN OPERATOR '->'
echo $mobilSatu->tambahKecepatan(80); 
// Output: Mobil Toyota Supra berwarna Merah sedang melaju 80 km/jam!

echo "<br>";

echo $mobilDua->mengeram();
// Output: Mobil Honda Civic sedang mengeram.

?>

```

### Simbol Penting dalam PHP PBO:

* **`new`** : Perintah untuk membuat Object baru dari sebuah Class.
* **`->`** : Operator untuk mengakses Property atau Method milik objek.
* **`$this`** : Variabel khusus yang merujuk pada objek yang sedang dieksekusi di dalam Class.

---

## 5. PANDUAN PRAKTIKUM: SETUP ENVIRONMENT & INSTALLASI LARAVEL

Ikuti langkah-langkah praktikum berikut untuk menginstal dan menjalankan framework Laravel di komputer lab/laptop masing-masing:

### Langkah 1: Cek Tools

Buka **Terminal** / **Git Bash** / **CMD**, lalu jalankan perintah berikut untuk memastikan PHP dan Composer siap:

```bash
php -v
composer -v

```

### Langkah 2: Masuk ke Folder Kerja

Pindahkan direktori terminal ke folder penyimpanan projek kalian (misalnya folder `htdocs` di XAMPP):

```bash
cd C:/xampp/htdocs

```

### Langkah 3: Install Project Laravel Baru

Jalankan perintah berikut untuk mengunduh dan membuat project Laravel bernama `pbo-laravel`:

```bash
composer create-project laravel/laravel pbo-laravel

```

*Tunggu proses download hingga muncul tulisan **"Application key set successfully."***

### Langkah 4: Buka Project di VS Code

Masuk ke folder project yang telah dibuat, lalu buka di Visual Studio Code:

```bash
cd pbo-laravel
code .

```

### Langkah 5: Jalankan Server Lokal

Nyalakan server bawaan Laravel dengan menjalankan perintah Artisan berikut di terminal VS Code:

```bash
php artisan serve

```

Buka browser dan akses alamat `[http://127.0.0.1:8000](http://127.0.0.1:8000)`. Jika halaman utama Laravel tampil, maka instalasi **berhasil**.

---

## 6. PENERAPAN PBO PADA FRAMEWORK LARAVEL

Di dalam Laravel, konsep PBO terimplementasi penuh pada arsitektur **MVC (Model-View-Controller)**.

### A. Model (Representasi Database & Inheritance)

Di Laravel, setiap tabel database diwakili oleh Class Model yang mewarisi sifat dari Class `Model` bawaan Laravel (`extends`):

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

// Class 'Siswa' mewarisi (Inheritance) fungsi dari Class Model bawaan
class Siswa extends Model {
    protected $table = 'siswa'; // Property internal
}

```

### B. Controller (Logika Aplikasi)

Controller di Laravel berfungsi mengatur logika program dengan menggunakan Class dan Method.

**Praktikum Siswa (Membuat Controller):**

1. Buka terminal di VS Code, ketik perintah Artisan berikut:
```bash
php artisan make:controller SiswaController

```


2. Buka file `app/Http/Controllers/SiswaController.php`, lalu sesuaikan kodenya:
```php
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

```


3. Daftarkan Controller pada file `routes/web.php`:
```php
use App\Http\Controllers\SiswaController;

Route::get('/siswa', [SiswaController::class, 'index']);

```


4. Akses melalui browser pada alamat: `[http://127.0.0.1:8000/siswa](http://127.0.0.1:8000/siswa)`.

---

## 7. TUGAS MANDIRI

1. Buatlah sebuah class baru bernama `Laptop` (bisa di PHP native atau buat `LaptopController` di Laravel) dengan ketentuan:
* **Property:** `$merk`, `$ram`, dan `$prosesor`.
* **Method:** `tampilkanSpesifikasi()` yang mengembalikan deskripsi laptop tersebut.


2. Buat **2 Object laptop yang berbeda** (contoh: ASUS dan Lenovo), lalu tampilkan hasilnya di browser!

---

## RANGKUMAN BAB 1

* PBO berfokus pada pengorganisasian data (*property*) dan fungsi (*method*) ke dalam **Object**.
* **Class** adalah cetakannya (*blueprint*), sedangkan **Object** adalah hasil wujud nyatanya (*instance*).
* Empat pilar utama PBO: **Abstraction**, **Encapsulation**, **Inheritance**, dan **Polymorphism**.
* Laravel dibangun 100% menggunakan paradigma PBO, yang terlihat jelas pada struktur **Model** dan **Controller**.
