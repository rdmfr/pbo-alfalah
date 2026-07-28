[dasar-pbo-laravel.md](https://github.com/user-attachments/files/30468814/dasar-pbo-laravel.md)
# BAB 1
# DASAR-DASAR PEMROGRAMAN BERORIENTASI OBJEK (PBO) DALAM FRAMEWORK LARAVEL

---

# A. Identitas Materi

**Mata Pelajaran:** Pemrograman Berbasis Objek (PBO)
**Framework:** Laravel
**Bahasa Pemrograman:** PHP
**Tingkat:** SMK
**Materi:** Konsep Dasar Object Oriented Programming (OOP)
**Alokasi Waktu:** 4 x 45 menit (2 pertemuan)

---

# B. Tujuan Pembelajaran

Setelah mempelajari bab ini, peserta didik diharapkan mampu:

1. Menjelaskan konsep dasar Pemrograman Berorientasi Objek (PBO/OOP) dengan bahasa sendiri.
2. Memahami perbedaan pemrograman prosedural dan pemrograman berbasis objek, lengkap dengan kelebihan dan kekurangannya.
3. Menjelaskan hubungan antara Class, Object, Property, dan Method beserta contohnya.
4. Menginstal dan menyiapkan project Laravel dari nol menggunakan Composer.
5. Memahami penerapan konsep PBO (Class, Object, Property, Method) pada struktur framework Laravel.
6. Membuat Controller Laravel sederhana menggunakan konsep Class, Property, dan Method.
7. Menghubungkan Controller dengan Route Laravel dan menampilkan hasilnya di browser.
8. Menjelaskan dan memberi contoh penerapan 4 pilar PBO (Inheritance, Encapsulation, Abstraction, Polymorphism) di dalam Laravel.

---

# C. Apersepsi

Pernahkah kalian bermain game seperti **Mobile Legends, Free Fire, Minecraft, atau GTA?**

Di dalam sebuah game terdapat berbagai macam karakter dan benda, misalnya:

* Hero
* Senjata
* Kendaraan
* Monster
* Item

Setiap benda tersebut memiliki ciri dan kemampuan masing-masing yang berbeda satu sama lain. Walaupun berasal dari "jenis" yang sama (misalnya sama-sama Hero), setiap karakter punya data dan kemampuan sendiri.

Contohnya sebuah karakter Hero dalam game:

| Komponen   | Contoh                       |
| ---------- | ---------------------------- |
| Nama       | Alucard                      |
| Level      | 15                           |
| Darah (HP) | 5000                         |
| Role       | Fighter                      |
| Kemampuan  | Menyerang, menggunakan skill |

Bandingkan dengan Hero lain:

| Komponen   | Contoh                       |
| ---------- | ---------------------------- |
| Nama       | Miya                         |
| Level      | 10                           |
| Darah (HP) | 3200                         |
| Role       | Marksman                     |
| Kemampuan  | Menembak, memanggil bulan    |

Perhatikan bahwa **keduanya adalah "Hero"**, tapi datanya berbeda-beda. Ini karena keduanya dibuat dari **rancangan (cetakan) yang sama**, yaitu rancangan "Hero", namun diisi dengan data masing-masing.

Dalam dunia pemrograman:

* Rancangan "Hero" tersebut disebut **Class**.
* Setiap karakter hasil dari rancangan itu (Alucard, Miya, dst) disebut **Object (Objek)**.

Konsep inilah yang menjadi dasar dari **Pemrograman Berorientasi Objek (PBO)** atau **Object-Oriented Programming (OOP)**.

> Intinya: PBO adalah cara berpikir dalam membuat program dengan meniru cara benda-benda di dunia nyata bekerja — setiap benda punya **data** (ciri-ciri) dan **kemampuan** (aksi yang bisa dilakukan).

---

# 1. PENGENALAN KONSEP PBO (OOP)

## A. Apa Itu PBO / OOP?

**Pemrograman Berorientasi Objek (PBO)** atau **Object-Oriented Programming (OOP)** adalah metode/paradigma pemrograman yang menyusun program berdasarkan **objek**, bukan berdasarkan urutan perintah semata.

Berbeda dengan pemrograman prosedural yang hanya berisi kumpulan perintah dari atas ke bawah, PBO mengelompokkan **data** dan **fungsi** yang berhubungan ke dalam satu wadah yang disebut **objek**.

Sederhananya:

> PBO adalah cara membuat program dengan meniru konsep benda yang ada di dunia nyata: setiap benda memiliki data (ciri-ciri) dan perilaku (hal yang bisa ia lakukan).

### Mengapa PBO penting dipelajari?

1. **Struktur program lebih rapi** — kode dikelompokkan berdasarkan tanggung jawabnya masing-masing.
2. **Mudah dikembangkan** — jika ingin menambah fitur baru, kita cukup menambah class baru tanpa mengubah seluruh program.
3. **Mudah dipelihara (maintenance)** — kesalahan pada satu bagian tidak langsung merusak bagian lain.
4. **Dipakai oleh hampir semua framework modern** — termasuk Laravel, sehingga wajib dikuasai sebelum belajar Laravel lebih dalam.

### Contoh Kasus Nyata

Dalam aplikasi sekolah terdapat beberapa "benda" atau entitas, misalnya:

```
Siswa
Guru
Kelas
Nilai
Mata Pelajaran
```

Setiap objek/entitas tersebut memiliki dua bagian penting:

1. **Atribut (Data/Ciri-ciri)** — sesuatu yang **dimiliki** oleh objek.
2. **Method (Perilaku/Aksi)** — sesuatu yang **bisa dilakukan** oleh objek.

Misalnya untuk objek `Siswa`:

| Jenis     | Contoh                                      |
| --------- | -------------------------------------------- |
| Atribut   | nama, NIS, kelas, alamat, nilai              |
| Method    | absen(), mengerjakanTugas(), lihatNilai()    |

---

## B. Komponen Dalam Sebuah Object

### 1. Atribut / Property

**Property** adalah data atau ciri yang dimiliki sebuah objek. Anggap saja property adalah "kata benda" yang menjelaskan objek tersebut — seperti mengisi biodata.

Contoh objek:

```
Objek: Laptop
```

Property (ciri-ciri) yang dimiliki:

```
- Merk
- RAM
- Processor
- Harga
```

Dalam kode PHP, property ditulis di dalam class menggunakan tanda `$` (variabel):

```php
class Laptop
{
    public $merk = "Asus";
    public $ram = "16GB";
    public $processor = "Intel Core i7";
    public $harga = 12000000;
}
```

**Penjelasan baris per baris:**

* `class Laptop { ... }` → membuat sebuah class bernama `Laptop`.
* `public` → jenis akses yang menentukan siapa saja yang boleh mengakses property ini (akan dibahas lebih lanjut di bagian Encapsulation).
* `$merk`, `$ram`, `$processor`, `$harga` → nama-nama property (variabel) milik class.
* Tanda `=` diikuti nilai → nilai awal (default) dari property tersebut.

### 2. Method

**Method** adalah fungsi atau kemampuan yang dapat dilakukan oleh sebuah objek. Kalau property adalah "kata benda", maka method adalah "kata kerja" — sesuatu yang **dilakukan** oleh objek.

Contoh:

Objek:

```
Laptop
```

Method (kemampuan) yang dimiliki:

```
- Menyalakan()
- Shutdown()
- MenjalankanProgram()
```

Dalam kode PHP, method ditulis seperti fungsi biasa tetapi berada **di dalam class**:

```php
class Laptop
{
    public $merk = "Asus";

    public function nyalakan()
    {
        return "Laptop $this->merk menyala";
    }

    public function shutdown()
    {
        return "Laptop $this->merk dimatikan";
    }
}
```

**Penjelasan:**

* `public function nyalakan() { ... }` → mendefinisikan method bernama `nyalakan`.
* `return "..."` → mengembalikan/menghasilkan sebuah nilai (dalam contoh ini berupa teks/string).
* `$this->merk` → cara method mengakses property yang dimiliki oleh objek yang sama (akan dijelaskan lebih detail pada bagian keyword `$this`).

### Ringkasan Perbedaan Property vs Method

| Aspek     | Property                     | Method                          |
| --------- | ----------------------------- | -------------------------------- |
| Jenis     | Data / variabel               | Fungsi / aksi                    |
| Analogi   | Kata benda (ciri-ciri)         | Kata kerja (kemampuan)            |
| Contoh    | `$merk`, `$harga`             | `nyalakan()`, `bayar()`           |
| Ditulis   | `public $nama = nilai;`       | `public function nama() { ... }` |

---

# 2. PERBANDINGAN PEMROGRAMAN PROSEDURAL DAN PBO

## A. Pemrograman Prosedural

Pemrograman prosedural adalah cara membuat program dengan menulis perintah secara berurutan dari atas ke bawah, biasanya berbasis fungsi-fungsi yang berdiri sendiri.

Contoh alur sederhana:

```
Input data siswa
   ↓
Simpan data
   ↓
Hitung nilai
   ↓
Tampilkan hasil
```

Contoh kode prosedural (tanpa class):

```php
function inputSiswa($nama, $nilai) {
    return ["nama" => $nama, "nilai" => $nilai];
}

function hitungRataRata($nilai1, $nilai2, $nilai3) {
    return ($nilai1 + $nilai2 + $nilai3) / 3;
}

$siswa = inputSiswa("Budi", 80);
$rata = hitungRataRata(80, 90, 70);

echo "Nama: " . $siswa['nama'] . ", Rata-rata: " . $rata;
```

Pada program kecil, cara ini masih mudah digunakan dan cukup cepat ditulis. Namun ketika aplikasi semakin besar (ratusan atau ribuan baris kode), kode dapat menjadi sulit dikelola.

### Masalah yang sering muncul pada pemrograman prosedural:

* Kode terlalu panjang dan bertumpuk dalam satu file.
* Sulit mencari letak kesalahan (bug) karena semua fungsi saling terkait secara acak.
* Banyak fungsi saling bergantung satu sama lain sehingga mengubah satu fungsi bisa merusak fungsi lain.
* Sulit digunakan ulang (reuse) di bagian program lain.
* Terjadi **spaghetti code** — kode yang alurnya rumit seperti mie spageti yang saling melilit.

---

## B. Pemrograman Berorientasi Objek

Dalam PBO, program dibagi berdasarkan **objek/entitas**, bukan sekadar fungsi.

Contoh aplikasi sekolah dipecah menjadi beberapa class:

```
Class Siswa
Class Guru
Class Nilai
Class Jadwal
```

Contoh kode yang sama dengan pendekatan PBO:

```php
class Siswa
{
    public $nama;
    public $nilai = [];

    public function __construct($nama)
    {
        $this->nama = $nama;
    }

    public function tambahNilai($nilai)
    {
        $this->nilai[] = $nilai;
    }

    public function hitungRataRata()
    {
        return array_sum($this->nilai) / count($this->nilai);
    }
}

$budi = new Siswa("Budi");
$budi->tambahNilai(80);
$budi->tambahNilai(90);
$budi->tambahNilai(70);

echo "Nama: " . $budi->nama . ", Rata-rata: " . $budi->hitungRataRata();
```

Setiap class memiliki tanggung jawab masing-masing: `Siswa` mengurus data dan perilaku yang berkaitan dengan siswa saja, tidak bercampur dengan urusan lain.

### Keuntungan PBO dibanding Prosedural:

✅ Kode lebih rapi dan terorganisir per objek/entitas
✅ Mudah dikembangkan — tinggal menambah class atau method baru
✅ Mudah diperbaiki — kesalahan biasanya terlokalisasi pada satu class
✅ Dapat digunakan kembali (reusable) — satu class bisa dipakai di banyak tempat
✅ Lebih mudah dipahami tim karena struktur mengikuti dunia nyata

### Tabel Perbandingan Ringkas

| Aspek                  | Prosedural                         | PBO (OOP)                              |
| ---------------------- | ----------------------------------- | ---------------------------------------- |
| Fokus utama            | Fungsi/prosedur                     | Objek (data + fungsi jadi satu)          |
| Struktur kode          | Berurutan, atas ke bawah            | Dikelompokkan dalam class                |
| Reusability            | Rendah - Sedang                     | Tinggi                                    |
| Cocok untuk             | Program kecil/sederhana             | Program besar dan kompleks               |
| Contoh penerapan        | Script kalkulator sederhana          | Aplikasi web seperti Laravel             |

---

# 3. KOMPONEN UTAMA PBO DALAM LARAVEL

Framework Laravel dibuat menggunakan konsep PBO modern dari PHP. Hampir seluruh bagian Laravel menggunakan **Class** dan **Object**.

Contohnya:

```
Controller   → mengatur alur/logika aplikasi
Model        → mengatur data dan interaksi dengan database
Middleware   → menyaring/memfilter request sebelum diproses
Request      → menampung data yang dikirim oleh pengguna
Service      → menyimpan logika bisnis yang bisa dipakai ulang
```

Semua komponen tersebut merupakan **object** yang saling bekerja sama untuk menjalankan aplikasi.

---

# 3.1 PERSIAPAN & SETUP PROJECT LARAVEL

Sebelum praktik membuat Controller, kita perlu menyiapkan project Laravel terlebih dahulu di komputer. Berikut langkah-langkah lengkapnya.

## A. Kebutuhan Sistem (Requirements)

Sebelum instalasi, pastikan komputer sudah memiliki:

| Kebutuhan  | Keterangan                                             |
| ----------- | ------------------------------------------------------- |
| PHP         | Minimal versi 8.1 (disarankan versi terbaru yang stabil, misalnya 8.2/8.3) |
| Composer    | Dependency manager untuk PHP, digunakan untuk menginstal Laravel dan library-nya |
| Node.js & NPM | Digunakan untuk mengelola aset front-end (CSS/JS) — opsional di awal, tapi disarankan ada |
| Database    | MySQL / MariaDB / SQLite (bisa dipilih sesuai kebutuhan) |
| Text Editor / IDE | Disarankan Visual Studio Code, atau bisa juga PHPStorm/Sublime Text |
| XAMPP / Laragon | Alat bantu (opsional) yang menyediakan PHP, MySQL, dan Apache sekaligus dalam satu paket, memudahkan pemula |

> 💡 **Tips untuk pemula:** Jika belum familiar dengan instalasi PHP dan Composer secara manual, disarankan menginstal **Laragon** (Windows) atau **XAMPP**, karena keduanya sudah menyediakan PHP dan database secara otomatis.

## B. Mengecek Instalasi PHP dan Composer

Buka **terminal / command prompt**, lalu jalankan perintah berikut untuk memastikan PHP sudah terpasang:

```bash
php -v
```

Jika berhasil, akan muncul versi PHP, misalnya:

```
PHP 8.2.12 (cli) (built: ...)
```

Kemudian cek juga Composer:

```bash
composer -v
```

Jika berhasil, akan muncul versi Composer, misalnya:

```
Composer version 2.7.1
```

Jika muncul pesan error seperti `command not found`, berarti PHP atau Composer belum terpasang / belum terdaftar di PATH sistem, dan perlu diinstal terlebih dahulu dari situs resminya:

* PHP: https://www.php.net/downloads
* Composer: https://getcomposer.org/download/

## C. Membuat Project Laravel Baru

Ada dua cara umum untuk membuat project Laravel baru. Pilih salah satu.

### Cara 1 — Menggunakan Composer (paling umum & direkomendasikan)

Jalankan perintah berikut di terminal, di dalam folder tempat kalian ingin menyimpan project (misalnya folder `htdocs` atau `www`):

```bash
composer create-project laravel/laravel nama-project
```

Contoh:

```bash
composer create-project laravel/laravel aplikasi-mobil
```

Perintah ini akan:

1. Mengunduh Laravel beserta seluruh dependency (library pendukung) yang dibutuhkan.
2. Membuat folder baru bernama `aplikasi-mobil` yang sudah berisi struktur project Laravel lengkap.

Proses ini membutuhkan koneksi internet dan bisa memakan waktu beberapa menit tergantung kecepatan internet.

### Cara 2 — Menggunakan Laravel Installer

Jika Laravel Installer sudah terpasang secara global melalui Composer:

```bash
composer global require laravel/installer
```

Setelah itu, project baru bisa dibuat dengan perintah singkat:

```bash
laravel new nama-project
```

Contoh:

```bash
laravel new aplikasi-mobil
```

Nantinya akan muncul beberapa pertanyaan interaktif (misalnya memilih starter kit, database, dsb) yang bisa dijawab sesuai kebutuhan, atau langsung tekan Enter untuk memakai pengaturan default.

## D. Struktur Folder Project Laravel

Setelah project berhasil dibuat, masuk ke dalam foldernya:

```bash
cd aplikasi-mobil
```

Struktur folder penting yang perlu diketahui pemula:

```
aplikasi-mobil/
├── app/
│   ├── Http/
│   │   └── Controllers/     ← tempat semua Controller dibuat
│   └── Models/               ← tempat semua Model dibuat
├── bootstrap/
├── config/                   ← file-file konfigurasi aplikasi
├── database/
│   └── migrations/           ← struktur tabel database
├── public/                    ← folder yang diakses oleh web server
├── resources/
│   └── views/                 ← file tampilan (Blade template)
├── routes/
│   ├── web.php                ← tempat mendaftarkan route/URL aplikasi
│   └── api.php
├── storage/
├── .env                        ← file konfigurasi environment (database, dll)
├── artisan                     ← file untuk menjalankan perintah Laravel (CLI)
└── composer.json
```

Yang paling sering digunakan pada bab ini adalah:

* `app/Http/Controllers/` → tempat membuat Controller.
* `routes/web.php` → tempat mendaftarkan alamat URL (route).

## E. Mengatur File .env (Opsional untuk Praktikum Ini)

File `.env` berisi konfigurasi environment aplikasi, termasuk koneksi database. Untuk praktikum pada bab ini (yang belum menggunakan database), file `.env` bisa dibiarkan dengan pengaturan default.

Contoh isi `.env` bagian database (akan digunakan pada bab-bab selanjutnya saat mempelajari Model dan Eloquent):

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nama_database
DB_USERNAME=root
DB_PASSWORD=
```

> Setiap kali file `.env` diubah, sebaiknya jalankan perintah berikut agar Laravel membaca ulang konfigurasi:
> ```bash
> php artisan config:clear
> ```

## F. Menjalankan Project Laravel untuk Pertama Kali

Masuk ke folder project (jika belum), lalu jalankan:

```bash
php artisan serve
```

Jika berhasil, akan muncul tampilan seperti berikut:

```
INFO  Server running on [http://127.0.0.1:8000].

Press Ctrl+C to stop the server
```

Buka browser dan akses:

```
http://127.0.0.1:8000
```

Jika muncul halaman selamat datang Laravel (Laravel welcome page), berarti instalasi berhasil dan project siap digunakan untuk praktikum. 🎉

> ⚠️ **Catatan:** Perintah `php artisan serve` harus tetap berjalan (jangan ditutup terminalnya) selama ingin mengakses aplikasi melalui browser. Untuk menghentikan server, tekan `Ctrl + C` pada terminal.

---

# Analogi Class dan Object

Bayangkan membuat sebuah kue menggunakan cetakan:

```
CLASS
(Cetakan Kue)
        |
        ↓
OBJECT
(Kue yang sudah jadi)
```

* **Class** adalah rancangan/cetakan — hanya ada satu, dibuat sekali.
* **Object** adalah hasil dari rancangan tersebut — bisa dibuat berkali-kali, dan setiap hasilnya bisa memiliki "isi" atau data yang berbeda (misalnya kue rasa coklat, kue rasa vanila — tapi bentuknya tetap sama karena dari cetakan yang sama).

---

## Class (Blueprint / Cetakan)

**Class** adalah template atau rancangan untuk membuat object. Class sendiri **belum berupa data nyata**, ia hanya berupa aturan/struktur.

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

Ditulis dalam PHP:

```php
class Mobil
{
    public $merk;
    public $warna;
    public $kecepatan = 0;

    public function jalan()
    {
        return "Mobil sedang berjalan";
    }

    public function rem()
    {
        return "Mobil sedang direm";
    }
}
```

Dalam Laravel, contoh nama file class biasanya berbentuk:

```
MobilController.php
Siswa.php
Produk.php
```

---

## Object (Instansi)

**Object** adalah hasil nyata (instansiasi) dari sebuah class. Proses membuat object dari class disebut **instansiasi**, menggunakan kata kunci `new`.

Contoh:

Dari class:

```
Mobil
```

Dapat dibuat beberapa object:

```php
$mobil1 = new Mobil();
$mobil1->merk = "Toyota Supra";
$mobil1->warna = "Merah";

$mobil2 = new Mobil();
$mobil2->merk = "Honda Civic";
$mobil2->warna = "Hitam";
```

Setiap object (`$mobil1`, `$mobil2`) berasal dari class yang **sama** (`Mobil`), tetapi memiliki **data yang berbeda**. Inilah inti dari konsep object: satu cetakan, banyak variasi hasil.

---

## Property

**Property** adalah variabel yang berada di dalam class, digunakan untuk menyimpan data/ciri-ciri milik object.

Contoh:

```php
class Mobil
{
    public $warna = "Merah";
}
```

Property `$warna` berisi data `"Merah"`. Untuk mengakses property dari luar class (setelah object dibuat), gunakan tanda panah `->`:

```php
$mobil = new Mobil();
echo $mobil->warna; // Output: Merah
```

---

## Method

**Method** adalah fungsi yang berada dalam class, digunakan untuk mendefinisikan aksi/perilaku yang bisa dilakukan object.

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

Method `jalan()` berfungsi menjalankan sebuah aksi. Cara memanggilnya sama seperti property, menggunakan tanda panah `->`, tetapi diikuti tanda kurung `()`:

```php
$mobil = new Mobil();
echo $mobil->jalan(); // Output: Mobil berjalan
```

---

# Hubungan PBO Dengan Laravel

Pada Laravel, konsep PBO diterapkan sebagai berikut:

| Konsep PBO | Implementasi Laravel                  |
| ---------- | --------------------------------------- |
| Class      | Controller, Model, Middleware, dll      |
| Object     | Data hasil pemanggilan/instansiasi class |
| Property   | Variabel yang didefinisikan dalam class |
| Method     | Function yang didefinisikan dalam class |

Contoh Controller sederhana yang menerapkan konsep PBO:

```php
<?php

namespace App\Http\Controllers;

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

* `SiswaController` → **Class**
* `$nama` → **Property**
* `tampil()` → **Method**
* `$this` → digunakan untuk **mengakses property/method milik class itu sendiri**

### Memahami Keyword `$this` Lebih Dalam

`$this` hanya bisa digunakan **di dalam class**, dan artinya adalah "objek yang sedang aktif memanggil method ini". Jika ada 2 object berbeda dari class yang sama, `$this` akan selalu merujuk ke object yang sedang digunakan saat itu, bukan object lainnya.

Contoh ilustrasi:

```php
$siswa1 = new SiswaController();
$siswa1->nama = "Budi";
echo $siswa1->tampil(); // Output: Budi -> $this merujuk ke $siswa1

$siswa2 = new SiswaController();
$siswa2->nama = "Ani";
echo $siswa2->tampil(); // Output: Ani -> $this merujuk ke $siswa2
```

---

# 4. EMPAT PILAR UTAMA PBO DALAM LARAVEL

Dalam Pemrograman Berorientasi Objek terdapat empat konsep utama yang menjadi dasar pengembangan aplikasi modern.

Keempat konsep tersebut disebut sebagai **4 Pilar PBO**, yaitu:

```
                    4 PILAR UTAMA PBO

                       PBO / OOP
           ┌───────────────┼───────────────┐
           |               |               |               |
   Inheritance     Encapsulation    Abstraction     Polymorphism
   (Pewarisan)      (Keamanan)     (Penyederhanaan)  (Banyak Bentuk)
```

Keempat konsep ini digunakan secara langsung dalam framework Laravel.

---

# A. Inheritance (Pewarisan)

## Pengertian

**Inheritance** adalah konsep PBO yang memungkinkan sebuah class (disebut **class anak / child class**) mewarisi sifat dan kemampuan dari class lain (disebut **class induk / parent class**).

Sederhananya:

> Sebuah class anak dapat menggunakan property dan method yang dimiliki oleh class induknya, tanpa harus menuliskan ulang kode tersebut.

## Analogi Kehidupan Nyata

Seorang anak mendapatkan sifat dari orang tuanya.

Orang tua memiliki:

```
- Rambut hitam
- Mata coklat
- Tinggi badan
```

Anak mewarisi:

```
- Rambut hitam
- Mata coklat
```

Tapi anak juga bisa memiliki ciri tambahan yang tidak dimiliki orang tuanya (misalnya lesung pipi).

## Contoh Kode Inheritance (Umum)

```php
class Kendaraan
{
    public $merk;

    public function jalan()
    {
        return "$this->merk sedang berjalan";
    }
}

class Mobil extends Kendaraan
{
    public function klakson()
    {
        return "Mobil membunyikan klakson";
    }
}

$mobil = new Mobil();
$mobil->merk = "Toyota";

echo $mobil->jalan();   // Diwarisi dari Kendaraan -> "Toyota sedang berjalan"
echo $mobil->klakson(); // Method sendiri -> "Mobil membunyikan klakson"
```

Perhatikan bahwa class `Mobil` **tidak perlu menulis ulang** method `jalan()`, karena sudah otomatis diwarisi dari class `Kendaraan`.

## Implementasi Inheritance Pada Laravel

Dalam Laravel, konsep inheritance sering digunakan pada Controller.

Contoh:

```php
class MobilController extends Controller
{

}
```

Perhatikan bagian:

```php
extends Controller
```

Artinya:

`MobilController` mewarisi kemampuan dari class `Controller` bawaan Laravel (yang berada di `app/Http/Controllers/Controller.php`).

Sehingga `MobilController` dapat langsung menggunakan fitur-fitur bawaan yang sudah disediakan Laravel di dalam class `Controller`, seperti method untuk validasi, autorisasi, dan lainnya, tanpa perlu menulis ulang.

---

# B. Encapsulation (Pembungkusan Data)

## Pengertian

**Encapsulation** adalah konsep untuk membungkus/melindungi data (property) dan method di dalam sebuah class, agar data tersebut tidak dapat diubah secara sembarangan dari luar class.

## Analogi Sederhana

Bayangkan sebuah smartphone.

Pengguna hanya melihat dan menggunakan bagian luar:

```
Tombol Power
Layar
Aplikasi
```

Tetapi tidak bisa mengutak-atik langsung bagian dalam:

```
Kabel
Komponen mesin
Sistem elektronik
```

Bagian dalam smartphone tersebut **terlindungi** dari pengguna biasa — hanya teknisi (dari dalam class itu sendiri) yang bisa mengaksesnya secara langsung.

## Access Modifier Pada PHP

PHP memiliki tiga tingkat akses (access modifier) yang digunakan untuk mengatur encapsulation:

| Modifier    | Fungsi                                              | Bisa diakses dari                       |
| ----------- | ---------------------------------------------------- | ----------------------------------------- |
| `public`    | Bisa diakses dari mana saja                          | Dalam class, class turunan, dan luar class |
| `protected` | Hanya class itu sendiri dan class turunannya         | Dalam class dan class turunan (tidak dari luar) |
| `private`   | Hanya bisa digunakan/dipanggil di dalam class itu sendiri | Hanya di dalam class itu sendiri       |

## Contoh Kode

```php
class Siswa
{
    private $password;
    public $nama;

    public function setPassword($passwordBaru)
    {
        $this->password = $passwordBaru;
    }

    public function cekPassword($input)
    {
        return $input === $this->password;
    }
}

$siswa = new Siswa();
$siswa->nama = "Budi";        // ✅ Boleh, karena public
$siswa->setPassword("12345"); // ✅ Boleh, lewat method public

// $siswa->password = "abc";  // ❌ ERROR! karena $password bersifat private,
                               // tidak bisa diakses langsung dari luar class
```

Pada contoh tersebut, `$password` **tidak dapat diakses langsung dari luar class** karena bersifat `private`. Untuk mengubah atau membaca nilainya, harus melalui method yang disediakan class (misalnya `setPassword()` dan `cekPassword()`). Inilah tujuan encapsulation: **melindungi data penting agar tidak sembarangan diubah**.

---

# C. Abstraction (Penyederhanaan)

## Pengertian

**Abstraction** adalah konsep menyembunyikan proses yang rumit/kompleks di balik layar, dan hanya menampilkan bagian yang perlu digunakan oleh pemakainya.

## Analogi Kehidupan Nyata

Ketika menggunakan motor, pengendara cukup:

```
Putar kunci
Tarik gas
Tekan rem
```

Tanpa perlu memahami secara detail:

```
Cara mesin bekerja
Proses pembakaran bahan bakar
Sistem transmisi gigi
```

Semua proses rumit tersebut **disembunyikan**, pengendara hanya berinteraksi dengan bagian yang sederhana (kunci, gas, rem).

## Abstraction Dalam Laravel

Laravel banyak menggunakan konsep abstraction, terutama pada fitur **Eloquent ORM** (Object Relational Mapping) — fitur yang menjembatani PHP dengan database.

Contoh:

```php
Siswa::all();
```

Perintah tersebut digunakan untuk mengambil **semua data siswa** dari database. Kita tidak perlu menulis query SQL secara manual seperti:

```sql
SELECT * FROM siswa;
```

Laravel sudah menyembunyikan proses koneksi database, penyusunan query, dan pengambilan data melalui satu baris perintah sederhana. Inilah contoh nyata abstraction — proses rumit di balik layar, hanya menyisakan perintah yang mudah dipahami.

Contoh abstraction lain di Laravel:

```php
Siswa::find(1);          // Mengambil siswa dengan id = 1
Siswa::where('kelas', 'XII')->get(); // Mengambil siswa dari kelas XII
```

---

# D. Polymorphism (Banyak Bentuk)

## Pengertian

Polymorphism berasal dari kata:

```
Poly  = Banyak
Morph = Bentuk
```

Artinya, sebuah fungsi/method dengan **nama yang sama** dapat memiliki **perilaku yang berbeda-beda**, tergantung dari objek mana ia dipanggil.

## Contoh Sederhana

Perintah:

```
bergerak()
```

Jika diberikan kepada objek yang berbeda, hasilnya juga berbeda:

* Burung → `Terbang`
* Ikan → `Berenang`
* Kucing → `Berjalan`

Perintah/nama method sama (`bergerak()`), tetapi hasil/perilakunya berbeda tergantung objeknya.

## Contoh Kode Polymorphism

```php
class Hewan
{
    public function bergerak()
    {
        return "Hewan bergerak";
    }
}

class Burung extends Hewan
{
    public function bergerak()
    {
        return "Burung terbang di udara";
    }
}

class Ikan extends Hewan
{
    public function bergerak()
    {
        return "Ikan berenang di air";
    }
}

$hewan = [new Burung(), new Ikan()];

foreach ($hewan as $item) {
    echo $item->bergerak() . "\n";
}

// Output:
// Burung terbang di udara
// Ikan berenang di air
```

Perhatikan bahwa method `bergerak()` dipanggil dengan cara yang **sama persis**, tetapi hasilnya berbeda karena masing-masing class (`Burung` dan `Ikan`) memiliki implementasi (isi) method-nya sendiri. Proses menimpa/menulis ulang method dari class induk seperti ini disebut **method overriding**.

## Polymorphism Dalam Laravel

Laravel menggunakan polymorphism pada berbagai fitur, seperti:

* **Eloquent Relationship** (contoh: *Polymorphic Relationship*, di mana satu Model bisa berelasi dengan beberapa Model lain menggunakan struktur yang sama).
* **Middleware** — setiap middleware memiliki method `handle()` dengan nama sama, tetapi isi/perilakunya berbeda-beda sesuai fungsi middleware tersebut.
* **Service Container** — Laravel bisa memanggil implementasi berbeda dari satu interface yang sama, tergantung konfigurasi aplikasi.

Contoh sederhana: satu method di Laravel dapat bekerja dengan beberapa jenis object yang berbeda, selama object tersebut memiliki method dengan nama yang sesuai (mengikuti aturan/kontrak yang sama).

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

> 📌 **Catatan:** Pastikan kalian sudah menyiapkan project Laravel terlebih dahulu mengikuti langkah pada bagian **3.1 Persiapan & Setup Project Laravel** di atas, sebelum melanjutkan praktikum ini.

---

# Langkah 1 - Membuat Controller

Buka terminal, arahkan ke folder project Laravel yang sudah dibuat sebelumnya:

```bash
cd aplikasi-mobil
```

Kemudian jalankan perintah artisan untuk membuat Controller baru:

```bash
php artisan make:controller MobilController
```

Jika berhasil, akan muncul pesan seperti:

```
Controller [app/Http/Controllers/MobilController.php] created successfully.
```

Dan Laravel akan membuat file baru pada:

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

Kemudian ubah isinya menjadi:

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

Menunjukkan bahwa `MobilController` adalah sebuah **class**, dan menggunakan **inheritance** dari class bawaan Laravel:

```php
Controller
```

## 2. Property

```php
public $merk = "Toyota Supra";
```

Merupakan data yang dimiliki object dari class ini. Property lainnya yang digunakan:

```php
$warna
$kecepatan
```

## 3. Method

Method:

```php
tambahKecepatan()
```

digunakan untuk menambah nilai kecepatan sebanyak 50 setiap kali dipanggil, lalu menampilkan pesan status mobil.

Method:

```php
mengerem()
```

digunakan untuk memberikan aksi/pesan pengereman.

## 4. Keyword $this

Pada kode:

```php
$this->merk
```

berarti:

> "Ambil property `$merk` milik object dari class ini sendiri."

Contoh lainnya:

```php
$this->warna
```

mengakses property:

```php
public $warna
```

yang berada di class yang sama.

---

# Langkah 3 - Membuat Route Laravel

Buka file:

```
routes/web.php
```

Tambahkan kode berikut (letakkan di bagian bawah file, sebelum baris paling akhir):

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

berarti memanggil (mereferensikan) class:

```
MobilController
```

Sedangkan:

```php
'tambahKecepatan'
```

berarti method yang akan dijalankan ketika alamat/route tersebut diakses, dalam contoh ini adalah method:

```
tambahKecepatan()
```

Jadi, ketika seseorang mengakses alamat `/mobil/gas` di browser, Laravel akan:

1. Membuat object dari `MobilController`.
2. Memanggil method `tambahKecepatan()` dari object tersebut.
3. Menampilkan hasil `return` dari method tersebut ke layar browser.

---

# Langkah 4 - Menjalankan Laravel

Jalankan perintah berikut di terminal (pastikan berada di dalam folder project):

```bash
php artisan serve
```

Jika berhasil, akan muncul pesan:

```
INFO  Server running on [http://127.0.0.1:8000].
```

---

# Langkah 5 - Pengujian

Buka browser, lalu coba akses alamat berikut satu per satu.

## Menguji Gas Mobil

Akses:

```
http://127.0.0.1:8000/mobil/gas
```

Output yang muncul di browser:

```
Mobil Toyota Supra warna Merah berjalan dengan kecepatan 50 km/jam
```

> 💡 Coba refresh (F5) halaman tersebut beberapa kali. Perhatikan bahwa nilai kecepatan **akan selalu kembali ke 50**, bukan bertambah menjadi 100, 150, dst. Ini karena setiap request baru ke Laravel akan membuat **object baru** dari `MobilController`, sehingga nilai property `$kecepatan` selalu diatur ulang ke 0 lalu ditambah 50. Ini contoh nyata bahwa setiap object memiliki data sendiri yang terpisah, dan tidak disimpan permanen kecuali disimpan ke database.

## Menguji Rem Mobil

Akses:

```
http://127.0.0.1:8000/mobil/rem
```

Output yang muncul di browser:

```
Mobil Toyota Supra sedang melakukan pengereman
```

---

# 6. RANGKUMAN BAB 1

Setelah mempelajari bab ini, dapat disimpulkan bahwa:

1. **PBO (OOP)** adalah metode pemrograman yang menggunakan **objek** sebagai dasar pembuatan program, meniru konsep benda di dunia nyata.

2. Object memiliki dua bagian utama:
   * **Property** → data atau ciri-ciri yang dimiliki objek (kata benda).
   * **Method** → aksi atau kemampuan yang bisa dilakukan objek (kata kerja).

3. **Class** merupakan blueprint/cetakan untuk membuat object, sedangkan **Object** adalah hasil nyata dari class tersebut (proses ini disebut instansiasi, menggunakan kata kunci `new`).

4. Sebelum praktik dengan Laravel, kita perlu menyiapkan project terlebih dahulu menggunakan **Composer** (`composer create-project laravel/laravel nama-project`) dan menjalankannya dengan **`php artisan serve`**.

5. Laravel menggunakan konsep PBO hampir di seluruh bagian framework-nya, seperti Controller, Model, Middleware, dan Request.

6. Empat pilar utama PBO adalah:
   * **Inheritance (Pewarisan)** — class anak mewarisi property/method dari class induk (`extends`).
   * **Encapsulation (Pembungkusan)** — melindungi data menggunakan access modifier (`public`, `protected`, `private`).
   * **Abstraction (Penyederhanaan)** — menyembunyikan proses rumit, hanya menampilkan yang penting (contoh: Eloquent `Siswa::all()`).
   * **Polymorphism (Banyak Bentuk)** — method dengan nama sama tapi perilaku berbeda tergantung objeknya.

7. **Controller Laravel** merupakan contoh nyata penerapan class dalam PBO, yang dihubungkan dengan **Route** agar bisa diakses melalui browser.

8. Keyword `$this` digunakan untuk mengakses property dan method milik object yang sama di dalam class.

---

# Glosarium Istilah Penting

| Istilah        | Arti Singkat                                                          |
| -------------- | ----------------------------------------------------------------------- |
| Class          | Rancangan/cetakan untuk membuat object                                  |
| Object         | Hasil nyata (instansiasi) dari sebuah class                             |
| Property       | Variabel/data yang dimiliki oleh class atau object                      |
| Method         | Fungsi/aksi yang dimiliki oleh class atau object                        |
| Instansiasi    | Proses membuat object baru dari sebuah class menggunakan `new`          |
| `$this`        | Kata kunci untuk mengakses property/method milik object yang sama       |
| `extends`      | Kata kunci untuk mewarisi (inheritance) class lain                      |
| Access Modifier| Pengatur hak akses property/method: `public`, `protected`, `private`    |
| Overriding     | Menulis ulang isi method dari class induk di dalam class anak           |
| Controller     | Class di Laravel yang mengatur logika/alur aplikasi                     |
| Route          | Pemetaan alamat URL ke Controller/method tertentu di Laravel            |
| Artisan        | Command line tool bawaan Laravel untuk berbagai perintah (`php artisan ...`) |
| Composer       | Aplikasi pengelola dependency/library untuk PHP                         |

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

Buat 3 property berikut di dalam `LaptopController`:

### 1. Merk Laptop

```php
public $merk = "Asus ROG";
```

### 2. RAM

```php
public $ram = "16 GB";
```

### 3. Processor

```php
public $prosesor = "Intel Core i7";
```

---

Buat sebuah method:

```php
spesifikasi()
```

Method tersebut harus menampilkan hasil seperti berikut ketika diakses:

```
Laptop Asus ROG
RAM 16 GB
Processor Intel Core i7
```

**Ketentuan tambahan:**

* Gunakan keyword `$this` untuk memanggil property di dalam method.
* Gunakan tanda `"\n"` atau tag HTML `<br>` agar tampilan menjadi 3 baris terpisah.

---

## Routing

Tambahkan route berikut pada `routes/web.php`:

```php
use App\Http\Controllers\LaptopController;

Route::get('/laptop',
[LaptopController::class, 'spesifikasi']);
```

---

## Pengujian

Jalankan server:

```bash
php artisan serve
```

Kemudian buka browser dan akses:

```
http://127.0.0.1:8000/laptop
```

Pastikan informasi laptop muncul dengan format yang benar dan sesuai ketentuan.

---

## Tugas Tambahan (Opsional, untuk Pengayaan)

1. Tambahkan method baru bernama `upgradeRam()` yang mengubah nilai `$ram` menjadi `"32 GB"`, kemudian tampilkan pesan "RAM berhasil diupgrade menjadi 32 GB". Daftarkan route baru untuk method ini.
2. Buatlah class `Laptop` **terpisah** (bukan Controller) yang menerapkan **encapsulation**, di mana property harga bersifat `private`, dan sediakan method `getHarga()` serta `setHarga()`.
3. Buatlah 2 class turunan dari `LaptopController`-mu (misalnya `LaptopGamingController` dan `LaptopKantorController`) yang masing-masing meng-override method `spesifikasi()` agar menampilkan hasil yang berbeda — ini adalah latihan penerapan **polymorphism**.

---

# Refleksi Pembelajaran

Jawablah pertanyaan berikut untuk menguji pemahaman kalian:

1. Apa perbedaan Class dan Object? Berikan contoh dari kehidupan sehari-hari selain yang ada di modul ini.
2. Mengapa Laravel menggunakan konsep PBO, dan apa manfaatnya dibanding pemrograman prosedural?
3. Apa fungsi keyword `$this`? Jelaskan dengan contoh kode sendiri.
4. Sebutkan dan jelaskan 4 pilar utama PBO beserta contoh penerapannya masing-masing di Laravel!
5. Mengapa penggunaan PBO membuat program lebih mudah dikembangkan dan dipelihara?
6. Jelaskan langkah-langkah membuat project Laravel baru menggunakan Composer, mulai dari nol!
7. Apa perbedaan access modifier `public`, `protected`, dan `private`? Berikan contoh masing-masing.

---
