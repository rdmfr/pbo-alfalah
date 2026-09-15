# MODUL AJAR
## PEMROGRAMAN BERORIENTASI OBJEK (PBO)
### BAB 1 — Dasar-Dasar PBO & Setup Laravel

*Fase F — Kelas XI, Konsentrasi Pengembangan Perangkat Lunak dan Gim (PPLG)*
*Kurikulum Merdeka*

---

## A. INFORMASI UMUM

### 1. Identitas Modul

| Komponen | Keterangan |
|---|---|
| Mata Pelajaran | Pemrograman Berorientasi Objek (PBO) |
| Fase / Kelas | F / XI PPLG |
| Alokasi Waktu | 3 x pertemuan (@ 6 JP, 1 JP = 45 menit) |
| Elemen | Berpikir Komputasional & Pemrograman Berbasis Objek |
| Model Pembelajaran | Discovery Learning & Project Based Learning (PjBL) |
| Moda | Tatap muka / Blended Learning (Laboratorium Komputer) |

### 2. Capaian Pembelajaran (CP)

Pada akhir fase F, peserta didik mampu memahami konsep dasar pemrograman berorientasi objek (Class, Object, Property, Method) serta menerapkan empat pilar PBO (Abstraction, Encapsulation, Inheritance, Polymorphism) dalam bahasa pemrograman PHP dan framework Laravel untuk membangun aplikasi berbasis MVC secara terstruktur.

### 3. Tujuan Pembelajaran (TP)

1. Peserta didik dapat menjelaskan konsep dan perbedaan antara pemrograman prosedural dan pemrograman berorientasi objek dengan tepat.
2. Peserta didik dapat mengidentifikasi komponen utama PBO (Class, Object, Property, Method) dan menganalogikannya dengan contoh kehidupan sehari-hari.
3. Peserta didik dapat menjelaskan dan memberi contoh empat pilar PBO (Abstraction, Encapsulation, Inheritance, Polymorphism).
4. Peserta didik dapat menuliskan kode PBO sederhana menggunakan PHP native (membuat class, object, property, dan method).
5. Peserta didik dapat melakukan instalasi framework Laravel dan menjalankan server lokal.
6. Peserta didik dapat menghubungkan konsep PBO dengan komponen Model dan Controller pada arsitektur MVC di Laravel.

### 4. Profil Pelajar Pancasila

- **Bernalar Kritis** — menganalisis perbedaan pendekatan prosedural dan PBO serta memilih solusi pemrograman yang tepat.
- **Mandiri** — melakukan instalasi environment dan eksplorasi kode secara mandiri sesuai instruksi praktikum.
- **Kreatif** — merancang class dan object baru (tugas mandiri Laptop) dengan variasi property dan method sendiri.
- **Gotong Royong** — berdiskusi dan saling membantu memecahkan error saat instalasi Laravel di laboratorium.

### 5. Sarana, Prasarana, dan Target Peserta Didik

| Aspek | Keterangan |
|---|---|
| Sarana | Laptop/PC, koneksi internet, text editor/VS Code, XAMPP, Composer, browser |
| Prasarana | Modul ajar, LKPD, proyektor, Laboratorium Komputer |
| Target Peserta Didik | Reguler (tidak ada kesulitan dalam mencerna materi ajar) |
| Jumlah Peserta Didik | Maksimal 36 peserta didik per rombel |

### 6. Pemahaman Bermakna

Peserta didik menyadari bahwa hampir seluruh aplikasi digital yang mereka gunakan sehari-hari — mulai dari aplikasi belanja online, transportasi online, hingga mobile banking — dibangun menggunakan konsep PBO. Memahami PBO berarti memahami "cara berpikir" di balik aplikasi-aplikasi tersebut.

### 7. Pertanyaan Pemantik

- Pernahkah kalian membuka aplikasi Gojek, Shopee, atau mobile banking? Menurut kalian, bagaimana programmer mengatur ribuan data pengguna, driver, dan transaksi agar tetap rapi?
- Apa perbedaan antara "cetakan kue" dan "kue yang sudah jadi"? Menurut kalian, apa hubungannya dengan istilah Class dan Object dalam pemrograman?

---

## B. KEGIATAN PEMBELAJARAN

### Pertemuan 1 — Konsep Dasar PBO (6 JP)

**Kegiatan Pendahuluan (15 menit)**
- Guru membuka kelas, menyapa, dan mengecek kehadiran peserta didik.
- Guru menyampaikan tujuan pembelajaran dan mengajukan pertanyaan pemantik.
- Apersepsi: guru menampilkan tampilan aplikasi Gojek/Shopee di layar proyektor sebagai pemantik diskusi.

**Kegiatan Inti (240 menit)**
- Peserta didik menyimak penjelasan guru mengenai konsep PBO, perbandingan Prosedural vs PBO, serta komponen utama PBO (materi bagian 1-2).
- Peserta didik berdiskusi kelompok kecil mencari 3 contoh Class dan Object dari aplikasi/benda di sekitar mereka (LKPD 1).
- Peserta didik menyimak penjelasan empat pilar PBO beserta analogi kehidupan sehari-hari (materi bagian 3).
- Peserta didik mempraktikkan kode `dasar_pbo.php` secara mandiri di laboratorium komputer (materi bagian 4).

**Kegiatan Penutup (15 menit)**
- Peserta didik menyimpulkan materi bersama guru.
- Guru memberikan pertanyaan refleksi dan menutup pelajaran.

### Pertemuan 2 — Setup Environment & Instalasi Laravel (6 JP)

**Kegiatan Inti**
- Peserta didik melakukan praktikum instalasi Laravel secara berurutan (materi bagian 5) dengan pendampingan guru.
- Peserta didik menjalankan server lokal dan memverifikasi tampilan halaman utama Laravel.
- Guru berkeliling memfasilitasi peserta didik yang mengalami kendala instalasi (troubleshooting).

### Pertemuan 3 — Penerapan PBO pada Laravel (MVC) (6 JP)

**Kegiatan Inti**
- Peserta didik menyimak penjelasan penerapan Inheritance pada Model dan logika pemrograman pada Controller (materi bagian 6).
- Peserta didik mempraktikkan pembuatan SiswaController beserta routing-nya.
- Peserta didik mengerjakan Tugas Mandiri (materi bagian 7) sebagai asesmen sumatif.

---

## C. MATERI PEMBELAJARAN

## BAB 1: Dasar-Dasar Pemrograman Berorientasi Objek (PBO) & Setup Laravel

### 1. Identifikasi & Konsep Pemrograman Berorientasi Objek (PBO)

#### A. Apa itu PBO / OOP?

**Pemrograman Berorientasi Objek (Object-Oriented Programming / OOP)** adalah paradigma atau tata cara pembuatan program menggunakan konsep **Object**. Objek ini memiliki data (*property/attribute*) dan prosedur/fungsi (*method*).

> 🌍 **Analogi Kehidupan Sehari-hari**
> Bayangkan kalian sedang membuka aplikasi ojek online seperti Gojek atau Grab. Di dalam aplikasi tersebut ada banyak "objek" seperti Driver, Penumpang, dan Pesanan. Setiap Driver punya data (nama, plat nomor, rating) dan bisa melakukan aksi (menerima order, mengantar penumpang). Itulah cara berpikir PBO — semua hal di dunia nyata direpresentasikan sebagai objek yang punya data dan aksi.

#### B. Perbandingan: Prosedural vs PBO

- **Pemrograman Prosedural:** Berfokus pada langkah-langkah linier dari atas ke bawah. Ketika aplikasi membesar, kode menjadi sulit dikelola dan rentan berantakan (*spaghetti code*).
- **Pemrograman Berorientasi Objek (PBO):** Mengorganisasikan program ke dalam **Class** dan **Object** yang saling berinteraksi secara modular, sehingga kode lebih rapi, reusable, dan mudah dikembangkan.

> 🌍 **Analogi**
> Prosedural itu seperti resep masakan yang ditulis sebagai daftar langkah panjang dari awal sampai akhir dalam satu kertas. Kalau ingin membuat 10 masakan berbeda, kalian harus menulis 10 kertas resep terpisah, walaupun ada langkah yang sama (misalnya "potong bawang"). PBO itu seperti dapur profesional: setiap koki (object) punya tugas dan peralatan masing-masing (property & method), dan bisa dipanggil kapan saja tanpa menulis ulang instruksi dari nol.

#### C. Penggunaan PBO

PBO digunakan secara luas dalam bahasa seperti PHP, Java, C#, Python, dan C++. Pada ekosistem PHP modern, framework seperti **Laravel** dibangun 100% menggunakan paradigma PBO. Contoh nyata aplikasi berbasis PBO yang sering digunakan siswa: aplikasi e-commerce (Shopee, Tokopedia), aplikasi perbankan digital, aplikasi presensi sekolah, dan sistem informasi akademik.

---

### 2. Komponen Utama PBO

| Komponen | Penjelasan | Contoh Dunia Nyata |
| --- | --- | --- |
| **Class** | Draf, rancangan, atau *blueprint* yang mendeskripsikan struktur dan perilaku objek. | Formulir pendaftaran siswa baru (formatnya sama untuk semua siswa) |
| **Object** | Wujud nyata (*instansiasi*) yang dibuat dari sebuah Class. | Formulir yang sudah diisi data siswa bernama Ahmad |
| **Property / Attribute** | Variabel di dalam class yang menyimpan data/karakteristik objek. | Nama, NIS, Kelas, Alamat siswa |
| **Method / Function** | Fungsi di dalam class yang mendeskripsikan aksi/perilaku objek. | `daftarUlang()`, `lihatNilai()`, `absen()` |

> 🌍 **Analogi Tambahan: Aplikasi Sekolah**
> Class `Siswa` adalah "format data siswa" yang berlaku untuk seluruh siswa di sekolah. Ketika kalian mendaftar dan data kalian dimasukkan ke sistem, sistem membuat satu Object baru dari Class `Siswa`, yaitu "kalian sendiri" dengan nama, NIS, dan kelas masing-masing. Setiap siswa (object) berbeda datanya, tetapi strukturnya (property & method) tetap sama karena berasal dari Class yang sama.

---

### 3. Empat Pilar Utama PBO

#### a. Abstraction (Abstraksi)

- **Pengertian:** Proses menentukan data dan method yang dimiliki oleh suatu class dengan melihat objek dalam bentuk yang lebih umum/sederhana.
- **Fungsi:** Menyederhanakan sistem kompleks menjadi kumpulan subsistem yang mudah dipahami.
- **Contoh:** Class `Hewan` membawahi subsistem spesifik seperti `Sapi`, `Kambing`, dan `Kucing`.

> 🌍 **Analogi**
> Saat kalian mengendarai motor, kalian cukup tahu cara "tarik gas" dan "tekan rem" untuk berjalan atau berhenti. Kalian tidak perlu tahu detail rumit di dalam mesin (pembakaran bahan bakar, kerja piston, dsb). Itulah abstraksi — pengguna hanya melihat fitur penting (method) tanpa perlu tahu cara kerja rinci di baliknya. Begitu juga aplikasi e-wallet: pengguna cukup tekan tombol "Bayar", tanpa perlu tahu proses enkripsi dan verifikasi bank di belakang layar.

#### b. Encapsulation (Enkapsulasi)

- **Pengertian:** Proses penyatuan data bersama method-nya ke dalam satu wadah (class).
- **Fungsi:** Menyembunyikan rincian internal dan menjaga data agar tidak diakses secara sembarangan.

> 🌍 **Analogi**
> Bayangkan kartu ATM kalian. Saldo di rekening tidak bisa diubah langsung oleh siapa pun secara sembarangan — harus melalui "pintu" tertentu, yaitu memasukkan PIN lalu memilih menu tarik tunai/transfer. Saldo (property) disembunyikan dan hanya bisa diakses/diubah melalui method resmi (verifikasi PIN, transaksi). Itulah enkapsulasi: melindungi data penting agar tidak diubah secara sembarangan dari luar.

#### c. Inheritance (Pewarisan)

- **Pengertian:** Konsep mewariskan property dan method milik class induk (*super class*) kepada class turunannya (*child class*).
- **Fungsi:** Efisiensi kode—class turunan tidak perlu menulis ulang kode yang sudah ada pada class induk.
- **Contoh:** Class `Kakek` → `Ayah` → `Anak`.

> 🌍 **Analogi**
> Class `Kendaraan` punya property seperti kecepatan dan method seperti `jalan()` dan `berhenti()`. Class `Mobil` dan Class `Motor` bisa mewarisi (`extends`) semua itu dari Class `Kendaraan`, sehingga tidak perlu menulis ulang kode `jalan()` dan `berhenti()` dari nol — mereka tinggal menambahkan hal khusus, misalnya `Mobil` punya `bukaBagasi()` dan `Motor` punya `standarSamping()`. Persis seperti anak yang mewarisi sifat dari orang tuanya, tetapi tetap punya keunikan sendiri.

#### d. Polymorphism (Polimorfisme)

- **Pengertian:** Memungkinkan penggunaan nama interface/method yang sama pada objek berbeda, namun dengan cara kerja yang disesuaikan.
- **Contoh:** Class `Mobil` dan Class `Motor` sama-sama memiliki method `melaju()`, namun mekanisme mesin internalnya berbeda.

> 🌍 **Analogi**
> Coba perhatikan berbagai aplikasi pembayaran digital seperti GoPay, OVO, dan DANA. Ketiganya memiliki method yang sama yaitu `bayar()`, tetapi proses di baliknya berbeda-beda (beda server, beda cara verifikasi). Contoh lain: Class `Kucing` dan Class `Bebek` sama-sama punya method `bersuara()`, tapi hasilnya berbeda — kucing mengeong, bebek berkwek. Satu "nama perintah" yang sama, hasil kerja yang berbeda sesuai objeknya — itulah polimorfisme.

---

### 4. Implementasi Kode PBO pada PHP Native

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

#### Simbol Penting dalam PHP PBO

| Simbol | Fungsi |
|---|---|
| `new` | Perintah untuk membuat Object baru dari sebuah Class. |
| `->` | Operator untuk mengakses Property atau Method milik objek. |
| `$this` | Variabel khusus yang merujuk pada objek yang sedang dieksekusi di dalam Class. |

---

### 5. Panduan Praktikum: Setup Environment & Instalasi Laravel

Ikuti langkah-langkah praktikum berikut untuk menginstal dan menjalankan framework Laravel di komputer lab/laptop masing-masing:

**Langkah 1: Cek Tools**

Buka **Terminal** / **Git Bash** / **CMD**, lalu jalankan perintah berikut untuk memastikan PHP dan Composer siap:

```bash
php -v
composer -v
```

**Langkah 2: Masuk ke Folder Kerja**

Pindahkan direktori terminal ke folder penyimpanan projek kalian (misalnya folder `htdocs` di XAMPP):

```bash
cd C:/xampp/htdocs
```

**Langkah 3: Install Project Laravel Baru**

Jalankan perintah berikut untuk mengunduh dan membuat project Laravel bernama `pbo-laravel`:

```bash
composer create-project laravel/laravel pbo-laravel
```

*Tunggu proses download hingga muncul tulisan **"Application key set successfully."***

**Langkah 4: Buka Project di VS Code**

Masuk ke folder project yang telah dibuat, lalu buka di Visual Studio Code:

```bash
cd pbo-laravel
code .
```

**Langkah 5: Jalankan Server Lokal**

Nyalakan server bawaan Laravel dengan menjalankan perintah Artisan berikut di terminal VS Code:

```bash
php artisan serve
```

Buka browser dan akses alamat `http://127.0.0.1:8000`. Jika halaman utama Laravel tampil, maka instalasi **berhasil**.

> 💡 **Tips Troubleshooting**
> - Jika muncul pesan error 'php is not recognized', pastikan folder PHP sudah ditambahkan ke Environment Variables (PATH) di komputer kalian.
> - Jika `composer create-project` gagal, periksa kembali koneksi internet karena Composer mengunduh paket dari server.

---

### 6. Penerapan PBO pada Framework Laravel

Di dalam Laravel, konsep PBO terimplementasi penuh pada arsitektur **MVC (Model-View-Controller)**.

> 🌍 **Analogi MVC**
> Bayangkan restoran cepat saji. **Model** adalah gudang bahan baku (mengurus data mentah dari database). **Controller** adalah koki (mengolah data sesuai pesanan/logika). **View** adalah tampilan makanan yang disajikan ke pelanggan (tampilan yang dilihat pengguna di browser). Ketiganya bekerja sama namun punya tugas terpisah, sehingga dapur (aplikasi) tetap rapi walau pesanan (fitur) semakin banyak.

#### A. Model (Representasi Database & Inheritance)

Di Laravel, setiap tabel database diwakili oleh Class Model yang mewarisi sifat dari Class `Model` bawaan Laravel (`extends`):

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

// Class 'Siswa' mewarisi (Inheritance) fungsi dari Class Model bawaan
class Siswa extends Model {
    protected $table = 'siswa'; // Property internal
}
```

#### B. Controller (Logika Aplikasi)

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

4. Akses melalui browser pada alamat: `http://127.0.0.1:8000/siswa`.

---

## D. ASESMEN

### 1. Asesmen Formatif (Diagnostik Awal & Proses)

Dilakukan melalui tanya jawab lisan saat apersepsi dan pengamatan keaktifan diskusi kelompok (LKPD 1) mengenai contoh Class/Object di sekitar peserta didik.

**Contoh Soal Latihan Lisan/Kuis Singkat**

1. Sebutkan 3 contoh Class dan Object dari aplikasi yang kalian gunakan sehari-hari!
2. Mengapa saldo pada aplikasi mobile banking tidak bisa diubah langsung oleh pengguna? Pilar PBO apa yang berkaitan dengan hal ini?
3. Jelaskan perbedaan antara Class `Kendaraan` dengan Object "motor Ahmad bernomor plat B 1234 XYZ".

### 2. Asesmen Sumatif — Tugas Mandiri

Kerjakan tugas berikut secara individu, lalu kumpulkan file kode dan tangkapan layar (screenshot) hasil output di browser.

1. Buatlah sebuah class baru bernama `Laptop` (bisa di PHP native atau buat `LaptopController` di Laravel) dengan ketentuan:
   - Property: `$merk`, `$ram`, dan `$prosesor`.
   - Method: `tampilkanSpesifikasi()` yang mengembalikan deskripsi laptop tersebut.
2. Buat **2 Object laptop yang berbeda** (contoh: ASUS dan Lenovo), lalu tampilkan hasilnya di browser!
3. *(Tantangan tambahan)* Tambahkan method `hitungTotalHarga($diskon)` yang menghitung harga laptop setelah diskon, untuk melatih pemahaman kalian tentang method dengan parameter.

**Rubrik Penilaian Tugas Mandiri**

| Aspek Penilaian | Skor 4 (Sangat Baik) | Skor 3 (Baik) | Skor 2 (Cukup) | Skor 1 (Perlu Bimbingan) |
|---|---|---|---|---|
| Struktur Class & Property | Class dan seluruh property benar & sesuai ketentuan | Class benar, 1 property kurang tepat | Class benar, lebih dari 1 property kurang tepat | Class tidak terbentuk dengan benar |
| Method & Logika | Method berjalan sempurna dan menghasilkan output sesuai | Method berjalan, output kurang lengkap | Method ada namun terdapat error kecil | Method tidak berhasil dijalankan |
| Object (Instansiasi) | 2 object dibuat dengan data berbeda & benar | 2 object dibuat, sedikit kesalahan data | Hanya 1 object berhasil dibuat | Belum berhasil membuat object |
| Kerapian & Penamaan Kode | Penamaan variabel/method jelas, indentasi rapi | Cukup rapi, ada sedikit inkonsistensi | Kurang rapi namun tetap terbaca | Tidak rapi dan sulit dibaca |

### 3. Refleksi Peserta Didik

- Bagian materi PBO mana yang menurut kalian paling mudah dipahami? Mengapa?
- Bagian materi PBO mana yang masih terasa sulit? Apa yang akan kalian lakukan untuk memahaminya lebih lanjut?
- Setelah mempelajari bab ini, coba sebutkan satu aplikasi baru (selain yang dicontohkan) beserta kemungkinan Class dan Object di dalamnya!

### 4. Refleksi Guru

- Apakah seluruh peserta didik berhasil menginstal Laravel dengan lancar? Kendala apa yang paling sering muncul?
- Apakah analogi kehidupan sehari-hari membantu peserta didik memahami empat pilar PBO?
- Perlukah alokasi waktu tambahan untuk sesi praktikum instalasi pada pertemuan berikutnya?

---

## E. GLOSARIUM

| Istilah | Arti |
|---|---|
| Class | Blueprint/rancangan yang mendefinisikan struktur dan perilaku objek. |
| Object | Instansiasi/wujud nyata dari sebuah class. |
| Property | Variabel yang menyimpan data/karakteristik suatu objek. |
| Method | Fungsi di dalam class yang mendeskripsikan perilaku/aksi objek. |
| Instansiasi | Proses membuat object baru dari sebuah class menggunakan keyword `new`. |
| Inheritance | Pewarisan property dan method dari class induk ke class turunan. |
| Encapsulation | Penyatuan data & method serta pembatasan akses langsung terhadap data. |
| Polymorphism | Kemampuan method dengan nama sama bekerja berbeda pada objek berbeda. |
| MVC | Model-View-Controller, pola arsitektur pemisahan data, logika, dan tampilan. |
| Artisan | Command Line Interface (CLI) bawaan Laravel untuk mempercepat pengembangan. |

---

## F. DAFTAR PUSTAKA

- Laravel Documentation. https://laravel.com/docs
- PHP Manual — Object-Oriented Programming. https://www.php.net/manual/en/language.oop5.php
- Modul Pembelajaran Informatika/RPL Kurikulum Merdeka, Kemendikbudristek.
