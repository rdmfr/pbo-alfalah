# BAB 1: Dasar-Dasar Pemrograman Berorientasi Objek (PBO) & Setup Laravel

Selamat datang di repository pembelajaran **Pemrograman Berorientasi Objek (PBO)** untuk **Kelas XI PPLG/RPL**.

Pada bab ini, kita akan mempelajari konsep dasar **Pemrograman Berorientasi Objek (Object-Oriented Programming/OOP)** serta menerapkannya secara langsung menggunakan framework **Laravel**.

---

# 📋 Daftar Isi

1. Penjelasan PBO dengan Bahasa Awam
2. Perbandingan: Pemrograman Prosedural vs PBO
3. Empat Komponen Utama PBO di Laravel
4. Empat Pilar PBO
5. Panduan Praktikum: Setup Environment & Instalasi Laravel
6. Praktikum: Menerapkan Class, Property, dan Method
7. Rangkuman
8. Tugas Mandiri

---

# 1. Penjelasan PBO dengan Bahasa Awam

## Apa itu PBO (Object-Oriented Programming)?

Pernahkah kalian bermain game seperti **Mobile Legends**, **Free Fire**, **PUBG**, atau **GTA V**?

Di dalam game terdapat banyak objek, misalnya:

- Hero
- Monster
- Mobil
- Senjata
- NPC
- Item

Semua benda tersebut disebut **Object (Objek)**.

**Pemrograman Berorientasi Objek (PBO/OOP)** adalah metode membuat program dengan cara mengelompokkan kode berdasarkan **objek di dunia nyata**, sehingga kode menjadi lebih rapi, mudah dipahami, dan mudah dikembangkan.

Setiap objek memiliki dua bagian utama.

### Atribut (Property)

Merupakan data atau ciri-ciri suatu objek.

Contoh Hero Mobile Legends:

- Nama
- HP
- Mana
- Level
- Role

### Perilaku (Method)

Merupakan aksi yang dapat dilakukan objek.

Contoh:

- Berjalan
- Menyerang
- Menggunakan Skill
- Recall

---

# 2. Perbandingan: Pemrograman Prosedural vs PBO

## Pemrograman Prosedural

Bayangkan kalian memiliki sebuah bengkel motor.

Semua data dicatat dalam **satu buku besar** mulai halaman pertama sampai terakhir.

Isi buku tersebut antara lain:

- Data pelanggan
- Data mekanik
- Data transaksi
- Data sparepart
- Data pembayaran

Semuanya bercampur menjadi satu sehingga ketika data semakin banyak akan sulit dicari.

Inilah yang sering disebut **Spaghetti Code**.

---

## Pemrograman Berorientasi Objek (PBO)

Pada PBO, setiap data dipisahkan sesuai fungsinya.

Misalnya:

- Data Motor
- Data Pelanggan
- Data Mekanik
- Data Transaksi
- Data Pembayaran

Setiap bagian mempunyai tempatnya masing-masing sehingga kode menjadi:

- Lebih rapi
- Mudah diperbaiki
- Mudah dikembangkan
- Tidak saling mengganggu

---

# 3. Empat Komponen Utama PBO di Laravel

Laravel dibangun menggunakan konsep **Object-Oriented Programming**.

Komponen utamanya adalah sebagai berikut.

| Komponen | Laravel | Penjelasan |
|----------|----------|------------|
| **Class** | Controller, Model | Cetakan (Blueprint) suatu objek. |
| **Object** | Instance dari Class | Hasil nyata yang dibuat dari Class. |
| **Property** | Variabel di dalam Class | Menyimpan data atau ciri-ciri objek. |
| **Method** | Function di dalam Class | Menyimpan aksi atau perilaku objek. |

## Contoh sederhana

Class:

```php
class Mobil
{

}
```

Property:

```php
public $merk = "Toyota";
```

Method:

```php
public function jalan()
{

}
```

Object:

```php
$mobil = new Mobil();
```

---

# 4. Empat Pilar PBO

## 1. Inheritance (Pewarisan)

Class dapat mewarisi sifat dari Class lain.

Contoh di Laravel:

```php
class MobilController extends Controller
```

Artinya:

MobilController memiliki seluruh kemampuan dasar dari Controller.

---

## 2. Encapsulation (Pembungkusan Data)

Data dapat dilindungi menggunakan keyword:

```php
public
protected
private
```

Tujuannya agar data tidak bisa diakses sembarangan.

---

## 3. Abstraction (Penyederhanaan)

Pengguna cukup memakai fungsi tanpa mengetahui proses di dalamnya.

Contoh:

```php
Siswa::all();
```

Kita cukup memanggil satu perintah tanpa perlu menulis query SQL secara manual.

---

## 4. Polymorphism (Banyak Bentuk)

Satu perintah dapat menghasilkan perilaku yang berbeda.

Contoh:

Perintah:

```
bergerak()
```

Pada Burung:

```
Terbang
```

Pada Ikan:

```
Berenang
```

---

# 5. Panduan Praktikum: Setup Environment & Instalasi Laravel

## A. Persiapan Software

Pastikan komputer telah terpasang:

- PHP 8.2 atau lebih baru (melalui XAMPP/Laragon)
- Composer
- Visual Studio Code

---

## B. Langkah 1 — Cek Instalasi

Buka Terminal atau CMD kemudian jalankan:

```bash
php -v
composer -v
```

Jika kedua versi muncul, berarti instalasi berhasil.

---

## Langkah 2 — Masuk ke Folder Kerja

Misalnya menggunakan XAMPP:

```bash
cd C:/xampp/htdocs
```

---

## Langkah 3 — Membuat Project Laravel

```bash
composer create-project laravel/laravel pbo-laravel
```

Tunggu hingga proses selesai.

Jika berhasil akan muncul pesan:

```
Application key set successfully.
```

---

## Langkah 4 — Membuka Project

```bash
cd pbo-laravel
code .
```

---

## Langkah 5 — Menjalankan Server

```bash
php artisan serve
```

Buka browser:

```
http://127.0.0.1:8000
```

Apabila muncul halaman Laravel, berarti instalasi berhasil.

---

# 6. Praktikum: Class, Property, dan Method

## Langkah 1 — Membuat Controller

```bash
php artisan make:controller MobilController
```

---

## Langkah 2 — Menulis Kode Controller

Buka file:

```
app/Http/Controllers/MobilController.php
```

Lalu isi dengan kode berikut.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class MobilController extends Controller
{
    // Property
    public $merk = "Toyota Supra";
    public $warna = "Merah";
    public $kecepatan = 0;

    // Method
    public function tambahKecepatan()
    {
        $this->kecepatan += 50;

        return "Mobil {$this->merk} berwarna {$this->warna} sedang melaju dengan kecepatan {$this->kecepatan} km/jam.";
    }

    // Method
    public function mengerem()
    {
        return "Mobil {$this->merk} sedang mengerem.";
    }
}
```

---

## Langkah 3 — Routing

Buka file:

```
routes/web.php
```

Tambahkan:

```php
use App\Http\Controllers\MobilController;

Route::get('/mobil/gas', [MobilController::class, 'tambahKecepatan']);

Route::get('/mobil/rem', [MobilController::class, 'mengerem']);
```

---

## Langkah 4 — Pengujian

Jalankan server:

```bash
php artisan serve
```

Kemudian buka:

```
http://127.0.0.1:8000/mobil/gas
```

dan

```
http://127.0.0.1:8000/mobil/rem
```

Jika berhasil maka browser akan menampilkan hasil dari method yang dipanggil.

---

# 7. Rangkuman

Pada bab ini kita telah mempelajari bahwa:

- PBO adalah metode pemrograman berbasis objek.
- Object memiliki Property dan Method.
- Class merupakan cetakan (Blueprint) dari Object.
- Laravel dibangun menggunakan konsep OOP.
- Controller dan Model merupakan contoh Class di Laravel.
- Keyword `$this` digunakan untuk mengakses Property atau Method milik Class itu sendiri.
- Operator `->` digunakan untuk mengakses Property maupun Method pada sebuah objek.

---

# 8. Tugas Mandiri

Kerjakan latihan berikut.

### 1. Buat Controller baru

```bash
php artisan make:controller LaptopController
```

---

### 2. Tambahkan Property

```php
public $merk = "Asus ROG";
public $ram = "16 GB";
public $prosesor = "Intel Core i7";
```

---

### 3. Buat Method

```php
public function spesifikasi()
{
    return "Laptop {$this->merk} memiliki RAM {$this->ram} dengan prosesor {$this->prosesor}.";
}
```

---

### 4. Tambahkan Routing

```php
use App\Http\Controllers\LaptopController;

Route::get('/laptop', [LaptopController::class, 'spesifikasi']);
```

---

### 5. Uji di Browser

```
http://127.0.0.1:8000/laptop
```

Pastikan spesifikasi laptop tampil dengan benar.

---

# 💡 Tips Saat Coding

- Jika muncul error **Class Not Found**, pastikan telah menambahkan:

```php
use App\Http\Controllers\LaptopController;
```

- Jangan lupa mengakhiri setiap baris kode PHP dengan tanda titik koma (`;`).
- Jalankan kembali server menggunakan:

```bash
php artisan serve
```

apabila server berhenti.
