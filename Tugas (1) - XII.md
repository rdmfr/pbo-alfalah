# TUGAS PRAKTIK PBO KELAS XII

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

---

# 📚 Pengingat Materi

## 1. Constructor

**Constructor** adalah method khusus yang otomatis dijalankan ketika object dibuat menggunakan `new`.

Dalam PHP ditulis:

```php
__construct()
```

Constructor biasanya digunakan untuk mengisi nilai awal property.

```php
class Karyawan
{
    private $nama;

    public function __construct($nama)
    {
        $this->nama = $nama;
    }
}

$karyawan = new Karyawan("Budi");
```

Ketika `new Karyawan("Budi")` dijalankan, constructor otomatis dipanggil.

---

## 2. Encapsulation

**Encapsulation** adalah konsep membatasi akses langsung terhadap data di dalam class.

Dalam tugas ini gunakan:

- `private` untuk data yang tidak boleh diakses langsung dari luar class.
- Getter untuk mengambil data yang bersifat `private`.

Contoh:

```php
class Karyawan
{
    private $nama;

    public function getNama()
    {
        return $this->nama;
    }
}
```

Data `$nama` tidak boleh diakses langsung dari luar class.

---

## 3. Inheritance

**Inheritance** adalah kemampuan sebuah Child Class untuk mewarisi property dan method dari Parent Class.

Dalam PHP menggunakan:

```php
extends
```

Contoh:

```php
class Karyawan
{
    public function info()
    {
        return "Data karyawan";
    }
}

class Manager extends Karyawan
{
}
```

`Manager` merupakan Child Class dari `Karyawan`.

---

## 4. Method Overriding

**Method overriding** terjadi ketika Child Class membuat kembali method yang sudah dimiliki Parent Class.

Nama method tetap sama, tetapi perilakunya dapat dibuat berbeda.

```php
class Karyawan
{
    public function hitungGaji()
    {
        return 4000000;
    }
}

class Manager extends Karyawan
{
    public function hitungGaji()
    {
        return 7000000;
    }
}
```

Child Class dapat tetap memanfaatkan method Parent menggunakan:

```php
parent::namaMethod()
```

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

# 2. Child Class `Manager`

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

# 3. Child Class `Programmer`

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

# 4. Membuat Object

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
