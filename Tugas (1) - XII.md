# PENJELASAN OOP + HUBUNGANNYA KE LARAVEL — BAHASA AWAM & ANALOGI
## Pendamping Tugas Praktik PBO Kelas XII — Sistem Manajemen Karyawan

> Dokumen ini dibuat supaya kalian **paham konsepnya dulu**, termasuk kenapa OOP yang dipelajari di PHP Native ini nantinya "nyambung" ke Laravel. Kalau langsung ngoding tanpa paham analoginya, biasanya cuma jadi hafalan syntax yang cepat lupa.

---

## 🧠 Cara Baca Dokumen Ini

Setiap konsep dijelaskan dengan urutan:

1. **Analogi dulu** (cerita sehari-hari)
2. **Terjemahan ke istilah OOP**
3. **Kaitannya ke tugas kalian** (kasus Sistem Karyawan)
4. **Kode singkat** biar kebayang

Di bagian akhir, ada penjelasan khusus **kenapa dan bagaimana** konsep ini nyambung ke Laravel.

---

## 1. Class & Object — "Formulir Data Karyawan vs Karyawan Sungguhan"

### Analogi
Bayangkan HRD punya **satu formulir kosong** bernama "Formulir Data Karyawan". Formulir itu sendiri bukan karyawan — dia cuma template kosong berisi kolom "Nama", "Gaji Pokok", dll.

Begitu formulir itu **diisi** untuk si Budi, formulir itu jadi **data karyawan Budi yang sungguhan**. HRD bisa mengisi formulir yang sama berkali-kali untuk Sari, Andi, Rina — masing-masing jadi **data karyawan yang berbeda**, meskipun bentuk formulirnya sama.

- **Formulir kosong** = `class`
- **Formulir yang sudah diisi untuk satu orang** = `object`

### Kaitan ke Tugas
```php
class Karyawan { ... }              // formulir kosongnya

$karyawan1 = new Karyawan("Budi", 4000000); // formulir yang sudah diisi untuk Budi
```

---

## 2. Property & Method — "Data di Formulir vs Yang Bisa Dilakukan Sistem"

### Analogi
- **Property** = kolom-kolom yang diisi di formulir (nama, gaji pokok)
- **Method** = "tombol aksi" yang bisa dipencet sistem HRD, misalnya "Hitung Gaji" atau "Tampilkan Info Karyawan"

### Kaitan ke Tugas
```php
class Karyawan
{
    private $nama;       // kolom formulir
    private $gajiPokok;  // kolom formulir

    public function hitungGaji()  // tombol aksi "hitung gaji"
    {
        return $this->gajiPokok;
    }
}
```

---

## 3. `$this` — "Kata Ganti 'Berkas Ini'"

### Analogi
Bayangkan HRD punya **banyak berkas karyawan** menumpuk di meja. Waktu HRD sedang mengisi satu berkas, dia bilang: *"Tulis nama di berkas **ini**."* Kata **"ini"** merujuk ke berkas yang sedang dipegang saat itu — bukan berkas karyawan lain yang ada di tumpukan.

`$this` bekerja seperti itu: dia merujuk ke **object yang sedang "dipegang"/diproses saat itu**.

### Kaitan ke Tugas
```php
public function __construct($nama, $gajiPokok)
{
    $this->nama = $nama; // "nama di berkas INI (object ini)"
}

$karyawan1 = new Karyawan("Budi", 4000000);
$manager1 = new Manager("Sari", 6000000, 2000000);
```
Waktu `$karyawan1` dibuat, `$this` artinya `$karyawan1`. Waktu `$manager1` dibuat, `$this` artinya `$manager1`. Tidak akan tertukar.

---

## 4. Constructor — "Proses Onboarding Otomatis Karyawan Baru"

### Analogi
Setiap karyawan baru masuk, biasanya ada **proses onboarding otomatis**: langsung dibuatkan ID karyawan, langsung dicatat nama dan gaji pokoknya di sistem — tanpa HRD harus mengetik ulang satu-satu secara manual setelah orangnya "resmi terdaftar".

`__construct()` adalah "proses onboarding otomatis" itu. Begitu ada `new Karyawan(...)`, PHP otomatis menjalankan `__construct()` untuk mengisi data awal.

### Kaitan ke Tugas
```php
class Karyawan
{
    private $nama;
    private $gajiPokok;

    public function __construct($nama, $gajiPokok)
    {
        $this->nama = $nama;
        $this->gajiPokok = $gajiPokok;
    }
}

$karyawan1 = new Karyawan("Budi", 4000000);
// __construct() otomatis jalan begitu baris ini dieksekusi
```

---

## 5. Encapsulation — "Data Gaji yang Rahasia, Harus Lewat HRD"

### Analogi
Data gaji karyawan itu **rahasia dan sensitif**. Orang lain (misalnya rekan kerja) tidak boleh asal buka database dan lihat gaji siapa saja secara langsung. Kalau mau tahu, mereka harus **minta secara resmi lewat HRD**, dan HRD yang menentukan informasi apa yang boleh dibagikan.

- **Data asli (gaji, nama) yang disimpan rapat** = property `private`
- **HRD sebagai perantara resmi** = method `public` seperti `getNama()`, `getGajiPokok()`

### Kaitan ke Tugas
```php
class Karyawan
{
    private $nama; // data rahasia, tidak bisa diakses langsung

    public function getNama() // "lewat HRD" - cara resmi untuk ambil data
    {
        return $this->nama;
    }
}

$manager1 = new Manager("Sari", 6000000, 2000000);

echo $manager1->nama;       // ❌ ERROR! Seperti coba lihat gaji orang tanpa lewat HRD
echo $manager1->getNama();  // ✅ BENAR! Ini lewat "loket resmi" HRD
```

> 💡 Ini kenapa di tugas kalian diminta coba `echo $manager1->nama;` dulu (harus error), baru pakai `getNama()` (harus berhasil) — biar kebukti encapsulation-nya beneran jalan.

---

## 6. Inheritance — "Jabatan Baru yang Tetap Berstatus Karyawan"

### Analogi
Semua orang di perusahaan — apapun jabatannya (Manager, Programmer, Designer) — **tetap seorang karyawan**. Mereka semua otomatis punya hal-hal dasar yang dimiliki setiap karyawan: nama, gaji pokok, hak cuti, dll. Tapi masing-masing jabatan punya **tambahan khusus**: Manager punya tunjangan jabatan, Programmer punya bonus project.

- **"Karyawan" secara umum** = Parent Class (`Karyawan`)
- **Jabatan spesifik (Manager, Programmer)** = Child Class
- **Hal dasar yang otomatis dimiliki semua jabatan** = property/method yang diwarisi
- **Tambahan khusus per jabatan** = property/method baru di Child Class

### Kaitan ke Tugas
```php
class Karyawan
{
    public function infoKaryawan()
    {
        return "Data karyawan umum";
    }
}

class Manager extends Karyawan // "jabatan Manager" tetap otomatis berstatus karyawan
{
    private $tunjanganJabatan; // tambahan khusus milik Manager
}
```
`Manager` **otomatis mewarisi** semua yang dimiliki `Karyawan` — HRD tidak perlu menulis ulang dari nol semua hal dasar untuk setiap jabatan baru.

### Kenapa Perlu `parent::__construct()`?
Analoginya: waktu Manager baru "didaftarkan" ke sistem, data dasarnya (nama, gaji pokok) **tetap harus diproses seperti karyawan biasa** — baru setelah itu ditambahkan data khusus Manager (tunjangan jabatan). `parent::__construct()` artinya *"jalankan dulu proses pendaftaran standar milik Karyawan, baru tambahkan data khusus Manager."*

```php
class Manager extends Karyawan
{
    private $tunjanganJabatan;

    public function __construct($nama, $gajiPokok, $tunjanganJabatan)
    {
        parent::__construct($nama, $gajiPokok);       // proses standar dulu
        $this->tunjanganJabatan = $tunjanganJabatan;   // baru data khusus Manager
    }
}
```

---

## 7. Method Overriding — "Rumus Gaji yang Beda-Beda Tiap Jabatan"

### Analogi
Semua karyawan punya cara "hitung gaji", tapi **rumusnya beda-beda tergantung jabatan**:
- Karyawan biasa: gaji = gaji pokok saja
- Manager: gaji = gaji pokok + tunjangan jabatan
- Programmer: gaji = gaji pokok + bonus project

Manager dan Programmer **tidak menghapus** cara hitung gaji dasar — mereka **menulis ulang rumusnya sendiri**, tapi tetap **memanfaatkan** angka gaji pokok dari perhitungan dasar.

- **Menulis ulang rumus** = Method Overriding
- **Memanfaatkan angka dari rumus dasar** = `parent::hitungGaji()`

### Kaitan ke Tugas
```php
class Karyawan
{
    public function hitungGaji()
    {
        return $this->gajiPokok;
    }
}

class Manager extends Karyawan
{
    private $tunjanganJabatan;

    public function hitungGaji() // override — rumus baru khusus Manager
    {
        $gajiDasar = parent::hitungGaji(); // "pinjam" hasil rumus dasar dulu
        return $gajiDasar + $this->tunjanganJabatan; // baru ditambah tunjangan
    }
}
```

---

## 🔗 Menghubungkan Semua Konsep dalam Satu Cerita

Bayangkan kalian membangun **sistem HRD mini**:

1. Ada **formulir kosong "Karyawan"** (`class Karyawan`) sebagai template dasar.
2. Setiap kali ada karyawan baru, dibuat **data baru** (`new Karyawan(...)`) — ini object.
3. Begitu data dibuat, ada **proses onboarding otomatis** (`__construct()`) yang mencatat nama dan gaji pokok.
4. Data gaji dan nama **disimpan rapat**, orang lain harus lewat **HRD sebagai perantara resmi** (`getNama()`, `getGajiPokok()`) — ini encapsulation.
5. Untuk jabatan Manager dan Programmer, dibuat **jenis karyawan turunan** (`extends`) yang otomatis punya semua hal dasar karyawan, **plus** data tambahan sesuai jabatannya — ini inheritance.
6. Karena tiap jabatan punya rumus gaji sendiri, dibuat **rumus hitung gaji versi masing-masing** (`hitungGaji()` di-override), tapi tetap **memanfaatkan** rumus dasar dari `Karyawan` (`parent::hitungGaji()`).

Kalau kalian bisa menceritakan ulang alur ini pakai kata-kata sendiri, berarti kalian sudah paham konsepnya — bukan cuma hafal syntax.

---

## 🚀 Sekarang, Kenapa Ini Semua Nyambung ke Laravel?

### Analogi Besarnya
Bayangkan kalian sudah belajar **cara menulis surat resmi** dengan tangan — tahu strukturnya, tahu bagian kop, tahu bagian isi, tahu bagian penutup. Nah, Laravel itu seperti **mesin cetak surat otomatis** yang canggih: dia tetap punya kop, isi, dan penutup surat — tapi karena kalian sudah paham strukturnya, kalian jadi lebih cepat ngerti kenapa mesin itu dirancang seperti itu.

Laravel **bukan bahasa baru**. Laravel adalah **kumpulan class-class siap pakai** yang ditulis oleh developer lain, dan kalian tinggal **memanfaatkan / memperluasnya** — persis seperti kalian memanfaatkan/memperluas `class Karyawan` di tugas ini.

### 1. `extends Model` = Inheritance yang Sama Persis

Ingat analogi "jabatan baru yang tetap berstatus karyawan"? Di Laravel:

```php
class Karyawan extends Model
{
    protected $table = 'karyawan';
}
```

`class Karyawan` di sini **mewarisi** semua kemampuan dari `Model` — seperti kemampuan menyimpan data ke database, mengambil semua data (`all()`), mencari data (`find()`), dan lainnya. Kalian **tidak perlu menulis ulang** kemampuan-kemampuan itu dari nol, sama seperti `Manager` tidak perlu menulis ulang property `$nama` dan `$gajiPokok` — karena sudah otomatis diwarisi dari `Karyawan`.

**Bedanya cuma siapa "orang tua"-nya**: di tugas kalian orang tuanya adalah class `Karyawan` yang kalian buat sendiri. Di Laravel, orang tuanya adalah class `Model` yang sudah disiapkan oleh Laravel.

### 2. Controller = Class yang Punya "Tombol Aksi" (Method)

Ingat analogi "tombol aksi yang bisa dipencet sistem HRD"? Controller di Laravel persis seperti itu, hanya lebih besar skalanya:

```php
class KaryawanController extends Controller
{
    public function index()
    {
        $karyawan = Karyawan::all();

        return view('karyawan.index', [
            'karyawan' => $karyawan
        ]);
    }
}
```

`index()` di sini adalah **method** — sama seperti `hitungGaji()` di tugas kalian. Bedanya, method ini "dipencet" otomatis ketika ada orang membuka halaman tertentu di website, bukan dipanggil manual dari kode.

### 3. `Karyawan::all()` = Memanggil Kemampuan yang Diwarisi

Ingat, `Manager` otomatis punya `infoKaryawan()` walau tidak menulis ulang, karena diwarisi dari `Karyawan`? Nah:

```php
Karyawan::all();
```

`all()` **bukan method yang ditulis di class `Karyawan` kalian** — dia diwarisi dari `Model`. Karena `Karyawan extends Model`, otomatis class `Karyawan` "mewarisi" kemampuan `all()` untuk mengambil semua data karyawan dari database. Sama seperti `Manager` mewarisi `infoKaryawan()` dari `Karyawan` tanpa perlu menulis ulang.

### 4. Constructor, `$this`, dan Encapsulation Tetap Berlaku

Di balik semua "kecanggihan" Laravel, mesinnya tetap PHP OOP biasa:
- Laravel tetap punya `__construct()` di banyak class-nya untuk inisialisasi.
- Laravel tetap pakai `$this` di dalam method-nya untuk merujuk ke object yang sedang berjalan.
- Laravel tetap menerapkan encapsulation — banyak property di class Laravel dibuat `protected` (mirip `private`, tapi bisa diakses Child Class) supaya tidak bisa diubah sembarangan dari luar.

### Kesimpulan Analogi

| Yang kalian pelajari di tugas ini | Muncul lagi di Laravel sebagai |
|---|---|
| `class Karyawan` (formulir kosong) | `class Karyawan extends Model` |
| `class Manager extends Karyawan` (jabatan yang tetap karyawan) | `class KaryawanController extends Controller` |
| Method yang diwarisi otomatis (`infoKaryawan()`) | Method yang diwarisi dari `Model` (`all()`, `find()`, dll) |
| `parent::__construct()` (proses standar dulu) | Mekanisme constructor yang sama di class Laravel |
| Property `private` (data rahasia gaji) | Property `protected` di banyak class Laravel |

**Intinya:** Laravel itu bukan "dunia baru yang asing". Laravel adalah **taman bermain yang jauh lebih besar**, tapi aturan mainnya (class, object, extends, constructor, encapsulation) **sama persis** dengan yang kalian pelajari dan praktikkan lewat PHP Native di tugas ini. Karena itu, tugas ini sengaja dibuat pakai PHP Native dulu — supaya waktu kalian ketemu Laravel nanti, kalian tidak kaget dengan konsepnya, cuma perlu belajar "kosakata" dan tools baru di atas fondasi yang sudah kalian kuasai.

---

## ✅ Checklist Pemahaman Diri (Sebelum Ngoding)

Coba jawab dulu tanpa buka kode:

- [ ] Bisa jelaskan bedanya `class` dan `object` pakai analogi sendiri?
- [ ] Ngerti kenapa `$this` bisa merujuk ke object yang berbeda-beda?
- [ ] Ngerti kenapa constructor jalan otomatis tanpa dipanggil manual?
- [ ] Bisa jelaskan kenapa data gaji harus `private`, bukan cuma aturan formal?
- [ ] Ngerti kenapa `Manager` dan `Programmer` butuh `parent::__construct()`?
- [ ] Ngerti bedanya "mewarisi method" vs "override method" pada `hitungGaji()`?
- [ ] Bisa jelaskan kenapa `class Karyawan extends Model` di Laravel itu konsepnya sama dengan `class Manager extends Karyawan` di tugas ini?

Kalau semua sudah dicentang, kalian siap lanjut ke pengerjaan tugas di bawah ini. Selamat mengerjakan! 🚀

---
---

# 📝 TUGAS PRAKTIK PBO KELAS XII
## Membuat Sistem Manajemen Karyawan dengan OOP PHP

### 🎯 Tujuan Pembelajaran

Melalui tugas ini, siswa diharapkan mampu menerapkan konsep:

- Class & Object
- Property & Method
- `$this`
- Constructor
- Encapsulation
- Inheritance
- Method Overriding

Selain itu, siswa diharapkan mulai memahami bagaimana konsep OOP PHP yang dipelajari dapat diterapkan ketika menggunakan **Laravel**.

> 💡 Kalau masih bingung dengan istilah-istilah di atas atau hubungannya ke Laravel, baca lagi bagian **Penjelasan dengan Bahasa Awam + Analogi** di awal dokumen ini sebelum mulai ngoding.

---

# 🧩 STUDI KASUS

Sebuah perusahaan ingin memiliki program sederhana untuk mengelola data karyawan.

Perusahaan memiliki beberapa jenis karyawan:

- Karyawan biasa
- Manager
- Programmer

Buatlah sistem sederhana menggunakan OOP PHP.

Gunakan:

```text
Karyawan
├── Manager
└── Programmer
```

`Karyawan` menjadi **Parent Class**, sedangkan `Manager` dan `Programmer` menjadi **Child Class**.

---

# 📌 KETENTUAN PROGRAM

## 1. Parent Class `Karyawan`

Buat class:

```text
Karyawan
```

Wajib memiliki:

### Property

```text
$nama
$gajiPokok
```

Keduanya harus menggunakan:

```php
private
```

### Constructor

Buat:

```php
__construct($nama, $gajiPokok)
```

Constructor harus menggunakan `$this` untuk mengisi property.

### Getter

Buat minimal:

```text
getNama()
getGajiPokok()
```

### Method

Buat:

```text
hitungGaji()
```

Untuk Karyawan biasa:

```text
gaji = gaji pokok
```

Buat juga:

```text
infoKaryawan()
```

yang menampilkan informasi karyawan.

---

## 2. Child Class `Manager`

Buat:

```text
Manager extends Karyawan
```

Tambahkan property:

```text
$tunjanganJabatan
```

Property harus menggunakan `private`.

Buat constructor:

```php
__construct($nama, $gajiPokok, $tunjanganJabatan)
```

Constructor wajib memanggil:

```php
parent::__construct(...)
```

Kemudian override:

```text
hitungGaji()
```

Perhitungannya:

```text
Gaji Manager =
Gaji Pokok + Tunjangan Jabatan
```

Di dalam method tersebut wajib menggunakan:

```php
parent::hitungGaji()
```

---

## 3. Child Class `Programmer`

Buat:

```text
Programmer extends Karyawan
```

Tambahkan property:

```text
$bonusProject
```

Property harus menggunakan `private`.

Buat constructor:

```php
__construct($nama, $gajiPokok, $bonusProject)
```

Constructor wajib memanggil:

```php
parent::__construct(...)
```

Kemudian override:

```text
hitungGaji()
```

Perhitungannya:

```text
Gaji Programmer =
Gaji Pokok + Bonus Project
```

Method wajib menggunakan:

```php
parent::hitungGaji()
```

---

## 4. Membuat Object

Buat minimal **4 object**:

- 1 object Karyawan
- 1 object Manager
- 2 object Programmer

Contoh:

```php
$karyawan1 = new Karyawan(...);

$manager1 = new Manager(...);

$programmer1 = new Programmer(...);
$programmer2 = new Programmer(...);
```

Data setiap object harus berbeda.

---

# 🖥️ CONTOH OUTPUT

Output kurang lebih:

```text
========================================
     SISTEM DATA KARYAWAN PERUSAHAAN
========================================

Karyawan
Nama       : Budi
Gaji Pokok : Rp4.000.000
Total Gaji : Rp4.000.000

----------------------------------------

Manager
Nama              : Sari
Gaji Pokok        : Rp6.000.000
Tunjangan Jabatan : Rp2.000.000
Total Gaji        : Rp8.000.000

----------------------------------------

Programmer
Nama          : Andi
Gaji Pokok    : Rp5.000.000
Bonus Project : Rp1.500.000
Total Gaji    : Rp6.500.000

----------------------------------------

Programmer
Nama          : Rina
Gaji Pokok    : Rp5.500.000
Bonus Project : Rp2.000.000
Total Gaji    : Rp7.500.000
```

Data di atas hanya contoh. Siswa wajib menggunakan data sendiri.

---

# 🧪 PENGUJIAN ENCAPSULATION

Setelah program selesai, coba tambahkan:

```php
echo $manager1->nama;
```

Program seharusnya menghasilkan error karena:

```php
private $nama;
```

Kemudian hapus kode tersebut agar program kembali berjalan normal.

Selanjutnya gunakan getter:

```php
echo $manager1->getNama();
```

Getter seharusnya dapat digunakan untuk mengambil nilai nama.

---

# 🚨 CHECKLIST KODE

Sebelum dikumpulkan, pastikan:

- [ ] Ada class `Karyawan`
- [ ] Ada class `Manager`
- [ ] Ada class `Programmer`
- [ ] Ada Parent Class
- [ ] Ada Child Class
- [ ] Menggunakan `extends`
- [ ] Menggunakan property
- [ ] Menggunakan method
- [ ] Menggunakan `$this`
- [ ] Menggunakan `__construct()`
- [ ] Menggunakan property `private`
- [ ] Ada getter
- [ ] Constructor Child menggunakan `parent::__construct()`
- [ ] Ada method overriding
- [ ] Menggunakan `parent::hitungGaji()`
- [ ] Minimal 4 object
- [ ] Data setiap object berbeda
- [ ] Program berjalan tanpa error
- [ ] Output sesuai dengan data

---

# 💻 PENGUJIAN PROGRAM

Program wajib dapat dijalankan menggunakan **php.io**.

Gunakan **PHP Native**.

Tidak diperbolehkan menggunakan:

- Laravel
- Database
- Composer
- Framework
- Library eksternal

Tujuan tahap ini adalah memastikan siswa benar-benar memahami konsep dasar OOP sebelum menggunakan framework.

---

# 🚀 BAGIAN LANJUTAN: HUBUNGANNYA DENGAN LARAVEL

Setelah program PHP Native selesai, perhatikan bahwa konsep yang digunakan sebenarnya merupakan dasar dari banyak bagian dalam Laravel.

Laravel menggunakan PHP dan sangat bergantung pada konsep OOP.

Sebagai contoh, kita memiliki class sederhana:

```php
class Karyawan
{
    private $nama;

    public function __construct($nama)
    {
        $this->nama = $nama;
    }

    public function getNama()
    {
        return $this->nama;
    }
}
```

Di Laravel, kita juga bekerja dengan berbagai class.

Contohnya sebuah Model:

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Karyawan extends Model
{
    protected $table = 'karyawan';
}
```

Perhatikan:

```php
class Karyawan extends Model
```

Artinya class `Karyawan` merupakan **Child Class** dari class `Model`.

Konsep:

```php
extends
```

yang kalian gunakan pada tugas PHP Native juga digunakan dalam Laravel.

---

# 🔎 Contoh Controller Laravel

Dalam Laravel, kita juga membuat class Controller:

```php
namespace App\Http\Controllers;

use App\Models\Karyawan;

class KaryawanController extends Controller
{
    public function index()
    {
        $karyawan = Karyawan::all();

        return view('karyawan.index', [
            'karyawan' => $karyawan
        ]);
    }
}
```

Di sini kalian dapat melihat bahwa Laravel menggunakan konsep **class, object, method, inheritance**, dan pemanggilan object.

Contohnya:

```php
Karyawan::all();
```

digunakan untuk menjalankan method yang tersedia pada Model.

---

# 🔗 Hubungan Materi PHP Native dengan Laravel

| PHP Native yang Dipelajari | Penerapan dalam Laravel |
|---|---|
| Class | Model, Controller, Service, dan class lainnya |
| Object | Object dari Model atau class Laravel |
| Property | Data/property yang dimiliki class |
| Method | Method pada Controller, Model, Service |
| `$this` | Digunakan di dalam method class |
| Constructor | Digunakan untuk proses inisialisasi object |
| Encapsulation | Pengaturan akses property/method |
| Inheritance | `extends Model`, `extends Controller`, dll. |
| Method Overriding | Dapat digunakan ketika Child Class mengubah perilaku Parent Class |

**Catatan:** contoh Laravel di atas hanya untuk memahami hubungan konsep. Tugas utama tetap harus dibuat menggunakan PHP Native dan diuji di php.io.

---

# 🎯 TANTANGAN AKHIR

Setelah memahami hubungan PHP Native dengan Laravel, jawab pertanyaan berikut.

### Pertanyaan 1

Perhatikan:

```php
class Manager extends Karyawan
```

Apa arti `extends`?

### Pertanyaan 2

Mengapa `$nama` dibuat menggunakan:

```php
private $nama;
```

dan tidak langsung dibuat `public`?

### Pertanyaan 3

Apa fungsi:

```php
parent::__construct(...)
```

pada Child Class?

### Pertanyaan 4

Apa perbedaan method:

```php
hitungGaji()
```

pada `Karyawan`, `Manager`, dan `Programmer`?

### Pertanyaan 5

Pada Laravel terdapat:

```php
class Karyawan extends Model
```

Apa hubungan konsep tersebut dengan inheritance yang kalian pelajari?

### Pertanyaan 6

Menurut kalian, mengapa memahami OOP PHP terlebih dahulu akan membantu ketika belajar Laravel?

---

# 📊 RUBRIK PENILAIAN

| Komponen | Nilai |
|---|---:|
| Class & Object | 10 |
| Property & Method | 10 |
| `$this` | 10 |
| Constructor | 15 |
| Encapsulation | 15 |
| Inheritance | 15 |
| Method Overriding | 15 |
| Kerapihan kode & komentar | 5 |
| Program berjalan & output | 5 |
| **Total** | **100** |

---

# ⭐ BONUS

Buat Child Class tambahan:

```text
Designer extends Karyawan
```

dengan property:

```text
$bonusDesain
```

Override method:

```text
hitungGaji()
```

dengan rumus:

```text
Gaji Pokok + Bonus Desain
```

Tambahkan minimal 1 object `Designer`.

---

# 📋 KETENTUAN PENGUMPULAN

Kumpulkan:

1. File `.php`
2. Screenshot program berhasil dijalankan di **php.io**
3. Jawaban pertanyaan bagian **Tantangan Akhir**
4. Pastikan nama file menggunakan format:

```text
Nama_DataKaryawan.php
```

Contoh:

```text
Fadhil_DataKaryawan.php
```

---

# 🎓 KESIMPULAN

Tugas ini merupakan latihan untuk menggabungkan seluruh konsep dasar OOP yang telah dipelajari:

```text
Class
   ↓
Object
   ↓
Property & Method
   ↓
$this
   ↓
Constructor
   ↓
Encapsulation
   ↓
Inheritance
   ↓
Method Overriding
   ↓
Laravel
```

Sebelum menggunakan framework seperti Laravel, pastikan konsep dasar OOP tersebut benar-benar dipahami. Framework akan jauh lebih mudah dipelajari jika kalian sudah memahami cara kerja class, object, inheritance, constructor, encapsulation, dan method.
