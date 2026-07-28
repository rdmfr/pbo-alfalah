# BAB 1

# DASAR-DASAR PEMROGRAMAN BERORIENTASI OBJEK (PBO) DALAM FRAMEWORK LARAVEL

---

# A. Identitas Materi

**Mata Pelajaran:** Pemrograman Berbasis Objek (PBO)
**Framework:** Laravel
**Bahasa Pemrograman:** PHP
**Tingkat:** SMK
**Materi:** Konsep Dasar Object Oriented Programming (OOP)

---

# B. Tujuan Pembelajaran

Setelah mempelajari bab ini, peserta didik diharapkan mampu:

1. Menjelaskan konsep dasar Pemrograman Berorientasi Objek (PBO/OOP).
2. Memahami perbedaan pemrograman prosedural dan pemrograman berbasis objek.
3. Menjelaskan hubungan antara Class, Object, Property, dan Method.
4. Memahami penerapan konsep PBO pada framework Laravel.
5. Membuat Controller Laravel sederhana menggunakan konsep Class, Property, dan Method.
6. Menghubungkan Controller dengan Route Laravel.

---

# C. Apersepsi

Pernahkah kalian bermain game seperti **Mobile Legends, Free Fire, Minecraft, atau GTA?**

Di dalam sebuah game terdapat berbagai macam karakter dan benda seperti:

* Hero
* Senjata
* Kendaraan
* Monster
* Item

Setiap benda tersebut memiliki ciri dan kemampuan masing-masing.

Contohnya sebuah karakter Hero dalam game:

| Komponen   | Contoh                       |
| ---------- | ---------------------------- |
| Nama       | Alucard                      |
| Level      | 15                           |
| Darah (HP) | 5000                         |
| Role       | Fighter                      |
| Kemampuan  | Menyerang, menggunakan skill |

Dalam dunia pemrograman, karakter atau benda tersebut disebut sebagai **Object (Objek)**.

Konsep inilah yang menjadi dasar dari **Pemrograman Berorientasi Objek (PBO)** atau **Object-Oriented Programming (OOP)**.

---

# 1. PENGENALAN KONSEP PBO (OOP)

## A. Apa Itu PBO / OOP?

**Pemrograman Berorientasi Objek (PBO)** atau **Object-Oriented Programming (OOP)** adalah metode pemrograman yang menyusun program berdasarkan objek.

Berbeda dengan pemrograman biasa yang hanya berisi kumpulan perintah dari atas ke bawah, PBO mengelompokkan data dan fungsi berdasarkan objek tertentu.

Sederhananya:

> PBO adalah cara membuat program dengan meniru konsep benda yang ada di dunia nyata.

Contoh:

Dalam aplikasi sekolah terdapat objek:

```
Siswa
Guru
Kelas
Nilai
Mata Pelajaran
```

Setiap objek memiliki:

1. **Atribut (Data/Ciri-ciri)**
2. **Method (Perilaku/Aksi)**

---

# B. Komponen Dalam Sebuah Object

## 1. Atribut / Property

Property adalah data atau ciri yang dimiliki sebuah objek.

Contoh objek:

```
Objek: Laptop
```

Property:

```
- Merk
- RAM
- Processor
- Harga
```

Dalam PHP:

```php
public $merk = "Asus";
public $ram = "16GB";
```

---

## 2. Method

Method adalah fungsi atau kemampuan yang dapat dilakukan oleh sebuah objek.

Contoh:

Objek:

```
Laptop
```

Method:

```
- Menyalakan()
- Shutdown()
- MenjalankanProgram()
```

Dalam PHP:

```php
public function nyalakan()
{
    return "Laptop menyala";
}
```

---

# 2. PERBANDINGAN PEMROGRAMAN PROSEDURAL DAN PBO

## A. Pemrograman Prosedural

Pemrograman prosedural adalah cara membuat program dengan menulis perintah secara berurutan.

Contoh sederhana:

```
Input data siswa
↓
Simpan data
↓
Hitung nilai
↓
Tampilkan hasil
```

Pada program kecil cara ini masih mudah digunakan.

Namun ketika aplikasi semakin besar, kode dapat menjadi sulit dikelola.

Masalah yang sering muncul:

* Kode terlalu panjang.
* Sulit mencari kesalahan.
* Banyak fungsi saling bergantung.
* Terjadi spaghetti code.

---

## B. Pemrograman Berorientasi Objek

Dalam PBO, program dibagi berdasarkan objek.

Contoh aplikasi sekolah:

```
Class Siswa

Class Guru

Class Nilai

Class Jadwal
```

Setiap class memiliki tanggung jawab masing-masing.

Keuntungan:

✅ Kode lebih rapi
✅ Mudah dikembangkan
✅ Mudah diperbaiki
✅ Dapat digunakan kembali (reusable)

---

# 3. KOMPONEN UTAMA PBO DALAM LARAVEL

Framework Laravel dibuat menggunakan konsep PBO modern.

Hampir seluruh bagian Laravel menggunakan Class dan Object.

Contohnya:

```
Controller
Model
Middleware
Request
Service
```

Semua komponen tersebut merupakan object yang saling bekerja sama.

---

# Analogi Class dan Object

Bayangkan membuat sebuah kue.

```
CLASS
(Cetakan Kue)

        |
        |
        ↓

OBJECT
(Kue yang sudah jadi)
```

Class adalah rancangan.

Object adalah hasil dari rancangan tersebut.

---

## Class (Blueprint / Cetakan)

Class adalah template atau rancangan untuk membuat object.

Contoh:

Class:

```
Mobil
```

Memiliki:

Property:

```
- Merk
- Warna
- Kecepatan
```

Method:

```
- Jalan()
- Rem()
```

Dalam Laravel:

Contoh Class:

```
MobilController.php
Siswa.php
Produk.php
```

---

## Object (Instansi)

Object adalah hasil nyata dari sebuah class.

Contoh:

Dari class:

```
Mobil
```

Dapat dibuat object:

```
Toyota Supra
Honda Civic
BMW M4
```

Setiap object memiliki data berbeda.

---

## Property

Property adalah variabel yang berada di dalam class.

Contoh:

```php
class Mobil
{
    public $warna = "Merah";
}
```

Property:

```
$warna
```

berisi data:

```
Merah
```

---

## Method

Method adalah fungsi yang berada dalam class.

Contoh:

```php
class Mobil
{
    public function jalan()
    {
        return "Mobil berjalan";
    }
}
```

Method:

```
jalan()
```

berfungsi menjalankan aksi.

---

# Hubungan PBO Dengan Laravel

Pada Laravel:

| Konsep PBO | Implementasi Laravel         |
| ---------- | ---------------------------- |
| Class      | Controller, Model            |
| Object     | Data hasil pemanggilan class |
| Property   | Variabel dalam class         |
| Method     | Function dalam class         |

Contoh:

```php
class SiswaController extends Controller
{

    public $nama = "Budi";


    public function tampil()
    {
        return $this->nama;
    }

}
```

Pada kode tersebut:

* `SiswaController` → Class
* `$nama` → Property
* `tampil()` → Method
* `$this` → Mengakses isi class sendiri

---
Berikut **lanjutan BAB 1 bagian 2**. Bagian ini melanjutkan dari **Komponen Utama PBO Laravel** menuju **4 Pilar PBO, Praktikum Laravel, Rangkuman, dan Tugas Mandiri**.

Simpan sebagai lanjutan file:

```text
BAB-1/dasar-pbo-laravel.md
```

---

# 4. EMPAT PILAR UTAMA PBO DALAM LARAVEL

Dalam Pemrograman Berorientasi Objek terdapat empat konsep utama yang menjadi dasar pengembangan aplikasi modern.

Keempat konsep tersebut disebut sebagai **4 Pilar PBO**, yaitu:

```text
+--------------------------------+
|        4 PILAR UTAMA PBO       |
+--------------------------------+

          PBO / OOP

     /       |        |        \

Inheritance Encapsulation Abstraction Polymorphism

(Pewarisan) (Keamanan) (Penyederhanaan) (Banyak Bentuk)
```

Keempat konsep ini digunakan secara langsung dalam framework Laravel.

---

# A. Inheritance (Pewarisan)

## Pengertian

Inheritance adalah konsep PBO yang memungkinkan sebuah class mewarisi sifat dan kemampuan dari class lainnya.

Sederhananya:

> Sebuah class anak dapat menggunakan fitur yang dimiliki oleh class induknya tanpa harus membuat ulang kode tersebut.

Contoh dalam kehidupan nyata:

Seorang anak mendapatkan sifat dari orang tuanya.

Misalnya:

Orang tua:

```
Memiliki:
- Rambut hitam
- Mata coklat
- Tinggi badan
```

Anak:

```
Mewarisi:
- Rambut hitam
- Mata coklat
```

---

## Implementasi Inheritance Pada Laravel

Dalam Laravel, konsep inheritance sering digunakan pada Controller.

Contoh:

```php
class MobilController extends Controller
{

}
```

Perhatikan:

```php
extends Controller
```

Artinya:

`MobilController` mewarisi kemampuan dari class `Controller` bawaan Laravel.

Sehingga `MobilController` dapat menggunakan fitur yang sudah disediakan Laravel.

---

# B. Encapsulation (Pembungkusan Data)

## Pengertian

Encapsulation adalah konsep untuk melindungi data dalam sebuah class agar tidak dapat diubah secara sembarangan dari luar.

Analogi sederhana:

Bayangkan sebuah smartphone.

Pengguna hanya melihat:

```
Tombol Power
Layar
Aplikasi
```

Tetapi tidak melihat:

```
Kabel
Komponen mesin
Sistem elektronik
```

Bagian dalam smartphone tersebut terlindungi.

---

## Access Modifier Pada PHP

PHP memiliki tiga tingkat akses:

| Modifier  | Fungsi                                    |
| --------- | ----------------------------------------- |
| Public    | Bisa diakses dari mana saja               |
| Protected | Hanya class sendiri dan turunannya        |
| Private   | Hanya bisa digunakan dalam class tersebut |

Contoh:

```php
class Siswa
{

    private $password;

    public $nama;

}
```

Pada contoh tersebut:

`$password` tidak dapat diakses langsung dari luar class karena bersifat private.

---

# C. Abstraction (Penyederhanaan)

## Pengertian

Abstraction adalah konsep menyembunyikan proses yang rumit dan hanya menampilkan bagian yang diperlukan.

Contoh kehidupan nyata:

Ketika menggunakan motor:

Kita cukup:

```
Putar kunci
Tarik gas
Tekan rem
```

Tanpa perlu memahami:

```
Cara mesin bekerja
Proses pembakaran
Sistem transmisi
```

---

## Abstraction Dalam Laravel

Laravel banyak menggunakan konsep abstraction.

Contoh:

```php
Siswa::all();
```

Perintah tersebut digunakan untuk mengambil semua data siswa.

Kita tidak perlu menulis:

```sql
SELECT * FROM siswa;
```

Laravel sudah menyembunyikan proses tersebut melalui fitur Eloquent ORM.

---

# D. Polymorphism (Banyak Bentuk)

## Pengertian

Polymorphism berasal dari kata:

```
Poly = Banyak

Morph = Bentuk
```

Artinya sebuah fungsi dapat memiliki banyak bentuk perilaku.

Contoh sederhana:

Perintah:

```
bergerak()
```

Jika diberikan kepada:

Burung:

```
Terbang
```

Ikan:

```
Berenang
```

Kucing:

```
Berjalan
```

Perintah sama, tetapi hasil berbeda.

---

## Polymorphism Dalam Laravel

Laravel menggunakan polymorphism pada berbagai fitur seperti:

* Eloquent Relationship
* Middleware
* Service Container

Contoh:

Satu method dapat bekerja dengan beberapa jenis object yang berbeda.

---

# 5. PRAKTIKUM IMPLEMENTASI PBO PADA CONTROLLER LARAVEL

Pada praktikum ini kita akan membuat sebuah Controller Laravel yang menerapkan:

✅ Class
✅ Property
✅ Method
✅ Inheritance
✅ Routing

Studi kasus:

> Membuat sistem sederhana untuk menampilkan informasi mobil.

---

# Langkah 1 - Membuat Controller

Buka terminal pada project Laravel.

Jalankan:

```bash
php artisan make:controller MobilController
```

Jika berhasil maka Laravel membuat file:

```
app
 └── Http
     └── Controllers
          └── MobilController.php
```

---

# Langkah 2 - Membuat Class Controller

Buka file:

```
app/Http/Controllers/MobilController.php
```

Kemudian ubah menjadi:

```php
<?php

namespace App\Http\Controllers;


class MobilController extends Controller
{

    // PROPERTY
    public $merk = "Toyota Supra";

    public $warna = "Merah";

    public $kecepatan = 0;



    // METHOD
    public function tambahKecepatan()
    {

        $this->kecepatan += 50;


        return "Mobil "
        . $this->merk
        . " warna "
        . $this->warna
        . " berjalan dengan kecepatan "
        . $this->kecepatan
        . " km/jam";

    }



    public function mengerem()
    {

        return "Mobil "
        . $this->merk
        . " sedang melakukan pengereman";

    }

}
```

---

# Penjelasan Program

## 1. Class

```php
class MobilController extends Controller
```

Menunjukkan bahwa:

`MobilController` adalah sebuah class.

Dan menggunakan inheritance dari:

```php
Controller
```

---

## 2. Property

```php
public $merk = "Toyota Supra";
```

Merupakan data yang dimiliki object.

Property lainnya:

```php
$warna

$kecepatan
```

---

## 3. Method

Method:

```php
tambahKecepatan()
```

digunakan untuk menjalankan aksi.

Method:

```php
mengerem()
```

digunakan untuk memberikan aksi pengereman.

---

## 4. Keyword $this

Pada kode:

```php
$this->merk
```

berarti:

"Ambil property milik class ini sendiri."

Contoh:

```php
$this->warna
```

mengakses:

```php
public $warna
```

---

# Langkah 3 - Membuat Route Laravel

Buka file:

```
routes/web.php
```

Tambahkan:

```php
use App\Http\Controllers\MobilController;


Route::get('/mobil/gas', 
[MobilController::class, 'tambahKecepatan']);


Route::get('/mobil/rem', 
[MobilController::class, 'mengerem']);
```

---

# Penjelasan Route

Kode:

```php
MobilController::class
```

berarti memanggil class:

```
MobilController
```

Sedangkan:

```php
'tambahKecepatan'
```

memanggil method:

```
tambahKecepatan()
```

---

# Langkah 4 - Menjalankan Laravel

Jalankan:

```bash
php artisan serve
```

Jika berhasil muncul:

```
Server running on:

http://127.0.0.1:8000
```

---

# Langkah 5 - Pengujian

Buka browser:

## Menguji Gas Mobil

```
http://127.0.0.1:8000/mobil/gas
```

Output:

```
Mobil Toyota Supra warna Merah berjalan dengan kecepatan 50 km/jam
```

---

## Menguji Rem Mobil

```
http://127.0.0.1:8000/mobil/rem
```

Output:

```
Mobil Toyota Supra sedang melakukan pengereman
```

---

# 6. RANGKUMAN BAB 1

Setelah mempelajari bab ini, dapat disimpulkan bahwa:

1. PBO adalah metode pemrograman yang menggunakan objek sebagai dasar pembuatan program.

2. Object memiliki dua bagian utama:

* Property → data atau ciri objek.
* Method → aksi atau kemampuan objek.

3. Class merupakan blueprint atau cetakan untuk membuat object.

4. Laravel menggunakan konsep PBO hampir di seluruh bagian framework.

5. Empat pilar utama PBO adalah:

* Inheritance
* Encapsulation
* Abstraction
* Polymorphism

6. Controller Laravel merupakan contoh penerapan class dalam PBO.

7. Keyword:

```php
$this
```

digunakan untuk mengakses property dan method dalam class sendiri.

---

# 7. TUGAS MANDIRI SISWA

## Studi Kasus: Membuat Controller Laptop

Buatlah sebuah Controller baru dengan nama:

```
LaptopController
```

Gunakan perintah:

```bash
php artisan make:controller LaptopController
```

---

## Ketentuan Program

Buat 3 property:

### 1. Merk Laptop

Contoh:

```php
public $merk = "Asus ROG";
```

---

### 2. RAM

Contoh:

```php
public $ram = "16 GB";
```

---

### 3. Processor

Contoh:

```php
public $prosesor = "Intel Core i7";
```

---

Buat sebuah method:

```php
spesifikasi()
```

Method tersebut harus menampilkan:

```
Laptop Asus ROG
RAM 16 GB
Processor Intel Core i7
```

Gunakan konsep:

```php
$this
```

untuk memanggil property.

---

# Routing

Tambahkan route:

```php
Route::get('/laptop',
[LaptopController::class, 'spesifikasi']);
```

---

# Pengujian

Jalankan:

```bash
php artisan serve
```

Kemudian buka:

```
http://127.0.0.1:8000/laptop
```

Pastikan informasi laptop muncul dengan benar.

---

# Refleksi Pembelajaran

Jawablah pertanyaan berikut:

1. Apa perbedaan Class dan Object?
2. Mengapa Laravel menggunakan konsep PBO?
3. Apa fungsi keyword `$this`?
4. Sebutkan 4 pilar utama PBO!
5. Mengapa penggunaan PBO membuat program lebih mudah dikembangkan?

---

# Selesai BAB 1

Pada BAB berikutnya kita akan mempelajari:

**BAB 2 - CLASS, OBJECT, PROPERTY, DAN METHOD LEBIH DALAM PADA LARAVEL**

---

BAB 1 sekarang sudah memiliki alur seperti **modul ajar SMK**:

✅ Tujuan pembelajaran
✅ Apersepsi
✅ Teori konsep
✅ Contoh Laravel
✅ Praktikum
✅ Pengujian
✅ Rangkuman
✅ Tugas mandiri
✅ Refleksi

Format ini sudah siap dimasukkan ke GitHub Markdown dan nanti mudah dikembangkan menjadi website modul digital dengan MkDocs.
