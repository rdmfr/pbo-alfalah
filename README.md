BAB 1: Dasar-Dasar Pemrograman Berorientasi Objek (PBO) & Setup Laravel

Selamat datang di repository pembelajaran **Pemrograman Berorientasi Objek (PBO)** untuk Kelas XI PPLG / RPL. Pada bab ini, kita akan mempelajari konsep dasar PBO secara langsung menggunakan framework **Laravel**.

---

## 📋 Daftar Isi
1. [Penjelasan PBO dengan Bahasa Awam](#1-penjelasan-pbo-dengan-bahasa-awam)
2. [Perbandingan: Cara Lama (Prosedural) vs PBO](#2-perbandingan-cara-lama-prosedural-vs-pbo)
3. [Empat Komponen Utama PBO di Laravel](#3-empat-komponen-utama-pbo-di-laravel)
4. [Empat Pilar Utama PBO di Laravel](#4-empat-pilar-utama-pbo-di-laravel)
5. [Panduan Praktikum: Setup Environment & Installasi Laravel](#5-panduan-praktikum-setup-environment--installasi-laravel)
6. [Praktikum: Menerapkan Class, Property, & Method pada Controller](#6-praktikum-menerapkan-class-property--method-pada-controller)
7. [Rangkuman Bab 1](#7-rangkuman-bab-1)
8. [Tugas Mandiri](#8-tugas-mandiri)

---

## 1. Penjelasan PBO dengan Bahasa Awam

### Apa itu PBO / OOP?
Pernahkah kamu bermain game seperti **Mobile Legends**, **Free Fire**, atau **GTA**?
Di dalam game tersebut, terdapat berbagai macam elemen seperti **Hero**, **Monster**, **Mobil**, atau **Senjata**. Di dalam dunia pemrograman, semua elemen itu disebut sebagai **OBJECT (OBJEK)**.

**PBO (Pemrograman Berorientasi Objek)** atau *Object-Oriented Programming (OOP)* adalah cara membuat program dengan mengelompokkan kode berdasarkan "Benda/Objek" di dunia nyata, bukan sekadar menulis deretan perintah dari atas ke bawah.

Setiap objek di dalam program memiliki 2 komponen utama:
1. **Atribut / Data (Ciri-cirinya):** Contoh pada Hero ML $\rightarrow$ *Nama*, *Darah (HP)*, *Level*, dan *Role*.
2. **Perilaku / Aksi (Yang bisa dia lakukan):** Contoh pada Hero ML $\rightarrow$ *Berjalan*, *Menyerang*, dan *Menggunakan Skill*.

---

## 2. Perbandingan: Cara Lama (Prosedural) vs PBO

Bayangkan kamu sedang mengelola sebuah **Bengkel Motor**:

* **Cara Lama (Prosedural):**
  Kamu mencatat semua stok barang, data mekanik, transaksi pembeli, dan keuangan di **satu buku catatan panjang** dari halaman 1 sampai akhir. Jika bengkel makin besar dan catatan makin tebal, kamu akan sangat pusing mencari data tertentu dan rentan salah coret (*Spaghetti Code*).

* **Cara PBO (Berorientasi Objek):**
  Kamu membuat **Formulir khusus Motor**, **Formulir khusus Transaksi**, dan **Formulir khusus Pembeli**. Kodenya terpisah-pisah secara rapi sesuai dengan fungsi dan wujud fisiknya. Jika ada masalah pada transaksi, kamu cukup membuka Formulir Transaksi tanpa mengganggu data lainnya.

---


## 3. Empat Komponen Utama PBO di Laravel

Laravel dibangun 100% menggunakan konsep PBO modern. Seluruh aplikasi Laravel dijalankan oleh 4 komponen utama berikut:

| Komponen PBO | Istilah di Laravel | Penjelasan Bahasa Awam & Contoh |
| :--- | :--- | :--- |
| **Class** | `Controller`, `Model` | **Cetakan / Blueprint.** Seperti cetakan kue atau gambar teknik pabrik. Cetakan sendiri belum bisa dimakan, tapi berfungsi sebagai aturan pembuatan. <br> *Contoh:* `SiswaController.php`, `MobilController.php`. |
| **Object** | `$siswa`, `$mobil` | **Wujud Nyata / Hasil.** Seperti kue fisik yang sudah jadi dari cetakan. Dari 1 cetakan, kita bisa membuat puluhan kue nyata. <br> *Contoh:* Data nyata hasil query database. |
| **Property** | Variabel di Class | **Ciri-ciri / Identitas Objek.** Pada HP: *Merk*, *RAM*, dan *Harga*. <br> *Contoh di Laravel:* `public $namaSekolah = "SMK Negeri 1";` |
| **Method** | Fungsi di Class | **Aksi / Tombol Fungsi.** Pada HP: *ambilFoto()* dan *casBaterai()*. <br> *Contoh di Laravel:* `public function index() { ... }` |

---

## 4. Empat Pilar Utama PBO di Laravel

 Empat pilar ini adalah "aturan main" utama dalam dunia PBO yang diterapkan langsung oleh framework Laravel:

1. **Inheritance (Pewarisan Sifat):**
   * *Bahasa Awam:* Seperti sifat seorang anak yang diturunkan dari orang tuanya. Anak otomatis punya warna kulit atau bentuk rambut orang tuanya tanpa perlu dibuat dari awal.
   * *Di Laravel:* Terlihat pada sintaks `class MobilController extends Controller`. Artinya, `MobilController` otomatis mewarisi semua fitur bawaan `Controller` milik Laravel.
2. **Encapsulation (Pembungkusan / Keamanan Data):**
   * *Bahasa Awam:* Seperti kapsul obat atau casing HP. Komponen mesin dan kabel HP yang rumit dibungkus di dalam casing agar aman dan tidak bisa asal dicolok dari luar.
   * *Di Laravel:* Penggunaan kata kunci `public`, `protected`, atau `private` pada variabel agar data penting aplikasi tidak diubah sembarangan.
3. **Abstraction (Penyederhanaan):**
   * *Bahasa Awam:* Saat kamu menyalakan TV, kamu hanya perlu menekan **Tombol Power** pada remote. Kamu tidak perlu tahu bagaimana arus listrik dan gelombang sinyal bekerja di dalam mesin TV.
   * *Di Laravel:* Kamu cukup mengetik `Siswa::all()` untuk mengambil seluruh data siswa dari database, tanpa harus pusing menulis perintah SQL yang panjang dan rumit.
4. **Polymorphism (Banyak Bentuk):**
   * *Bahasa Awam:* Perintahnya sama, tetapi cara kerjanya berbeda. Contoh perintah "Bergerak!". Jika diberikan ke *Burung* ia akan *terbang*, jika ke *Ikan* ia akan *berenang*.

---

## 5. Panduan Praktikum: Setup Environment & Installasi Laravel

Sebelum mulai coding PBO di Laravel, kita perlu menyiapkan tools dan menginstal framework Laravel di komputer/laptop laboratorium.

### A. Persiapan Tools (Bahan-Bahan)
Pastikan komputer kalian sudah terpasang 3 aplikasi utama ini:
1. **PHP (via XAMPP):** Mesin utama untuk menjalankan bahasa pemrograman PHP (minimal versi 8.2).
2. **Composer:** Aplikasi pengunduh otomatis (*dependency manager*) untuk PHP yang bertugas mengunduh framework Laravel dari internet.
3. **VS Code (Visual Studio Code):** Code editor tempat kita menuliskankan kode program.

---

### B. Langkah-Langkah Install Project Laravel (Step-by-Step)

#### Langkah 1: Cek Tools
Buka **Terminal** (Mac/Linux) atau **Command Prompt (CMD) / Git Bash** (Windows), lalu ketik perintah berikut satu per satu untuk memastikan alat utama sudah terpasang:
```bash
php -v
composer -v

---

Langkah 2: Masuk ke Folder Kerja
Pindahkan direktori terminal ke folder penyimpanan projek kalian (misalnya folder htdocs di dalam XAMPP):

Bash
cd C:/xampp/htdocs
Langkah 3: Install Project Laravel Baru
Jalankan perintah berikut untuk menyuruh Composer mengunduh dan membuatkan folder project Laravel baru bernama pbo-laravel:

Bash
composer create-project laravel/laravel pbo-laravel
Tunggu proses download beberapa menit hingga muncul teks "Application key set successfully."

Langkah 4: Buka Project di VS Code
Masuk ke dalam folder project yang baru saja dibuat, lalu buka folder tersebut di Visual Studio Code:

Bash
cd pbo-laravel
code .
Langkah 5: Jalankan Server Lokal
Di dalam VS Code, buka Terminal baru (Ctrl + ~ atau menu Terminal -> New Terminal), lalu jalankan perintah server bawaan Laravel:

Bash
php artisan serve
Buka browser (Google Chrome / Edge) dan ketik alamat: http://127.0.0.1:8000 atau http://localhost:8000. Jika muncul halaman selamat datang berlogo Laravel, instalasi BERHASIL.

6. Praktikum: Menerapkan Class, Property, & Method pada Controller
Mari kita buat sebuah Controller untuk mempraktikkan komponen PBO secara langsung.

Langkah 1: Membuat Controller (Class)
Buka Terminal di VS Code, lalu jalankan perintah Artisan berikut:

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
        // Keyword '$this' digunakan untuk mengakses property milik Class ini sendiri$this->kecepatan += 50;

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

http://127.0.0.1:8000/mobil/gas

http://127.0.0.1:8000/mobil/rem

7. Rangkuman Bab 1
PBO (OOP) adalah metode pemrograman berbasis objek yang mengelompokkan data (property) dan aksi (method).

Class adalah cetakannya (blueprint), sedangkan Object adalah wujud nyatanya.

Seluruh file Controller dan Model di Laravel berbentuk Class yang saling terhubung.

Tanda -> digunakan untuk mengakses Property atau Method di dalam Laravel, dan variabel $this digunakan untuk merujuk ke isi Class itu sendiri.

8. Tugas Mandiri
Kerjakan latihan berikut pada project Laravel masing-masing:

Buatlah sebuah Controller baru bernama LaptopController melalui terminal Artisan!

Buatlah 3 Property di dalam LaptopController:

$merk (isi dengan merk laptop pilihanmu, contoh: "Asus ROG")

$ram (isi dengan kapasitas RAM, contoh: "16 GB")

$prosesor (isi dengan tipe prosesor, contoh: "Intel Core i7")

Buatlah 1 Method bernama spesifikasi() yang mengembalikan teks kalimat gabungan dari seluruh property di atas menggunakan variabel $this!

Hubungkan Controller tersebut ke file routes/web.php dengan jalur URL /laptop!

Buka http://127.0.0.1:8000/laptop di browser dan pastikan output spesifikasi laptop tampil dengan benar!

Tips Saat Koding:

Jika di browser muncul error "Class Not Found", periksa apakah kamu sudah menulis baris use App\Http\Controllers\LaptopController; di file routes/web.php.

Jangan lupa selalu akhiri setiap baris kode PHP dengan tanda titik koma (;).
