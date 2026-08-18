# TUGAS PRAKTIK PBO KELAS XI

## Membuat Sistem Data Produk Sederhana dengan OOP PHP

### 🎯 Kompetensi yang Dinilai

Tugas ini wajib menerapkan:

| No | Materi | Wajib |
|---|---|---|
| 1 | Class & Object | ✅ |
| 2 | Property & Method | ✅ |
| 3 | `$this` | ✅ |
| 4 | Constructor | ✅ |
| 5 | Encapsulation | ✅ |
| 6 | Inheritance | ✅ |
| 7 | Method Overriding | ✅ |

---

## 📚 Penjelasan Singkat Materi

### 1. Constructor

**Constructor** adalah method khusus yang otomatis dijalankan ketika sebuah object dibuat menggunakan `new`.

Dalam PHP, constructor ditulis menggunakan:

```php
__construct()
```

Constructor biasanya digunakan untuk memberikan nilai awal pada property object.

Contoh:

```php
class Produk
{
    private $nama;

    public function __construct($nama)
    {
        $this->nama = $nama;
    }
}

$produk = new Produk("Laptop");
```

Pada contoh tersebut, `__construct()` otomatis dijalankan ketika `new Produk("Laptop")` digunakan.

---

### 2. Encapsulation

**Encapsulation** adalah konsep untuk membatasi akses langsung terhadap data yang ada di dalam sebuah class.

Salah satu cara menerapkannya adalah menggunakan:

- `private` → hanya dapat diakses dari dalam class itu sendiri.
- `protected` → dapat diakses dari class tersebut dan class turunannya.
- `public` → dapat diakses dari luar class.

Contoh:

```php
class Produk
{
    private $nama;

    public function getNama()
    {
        return $this->nama;
    }
}
```

Property `$nama` tidak dapat diakses langsung dari luar class. Untuk mengambil nilainya, digunakan method seperti `getNama()`.

---

### 3. Inheritance

**Inheritance** adalah konsep ketika sebuah class dapat mewarisi property dan method dari class lain.

Class yang diwarisi disebut **Parent Class**, sedangkan class yang mewarisi disebut **Child Class**.

Dalam PHP, inheritance menggunakan:

```php
extends
```

Contoh:

```php
class Produk
{
    public function infoProduk()
    {
        return "Ini adalah produk";
    }
}

class ProdukMakanan extends Produk
{
}
```

`ProdukMakanan` merupakan Child Class dari `Produk`.

Kita dapat menggunakan method yang diwarisi:

```php
$makanan = new ProdukMakanan();

echo $makanan->infoProduk();
```

---

### 4. Method Overriding

**Method overriding** adalah ketika Child Class membuat ulang method yang sudah dimiliki Parent Class dengan nama method yang sama.

Tujuannya adalah agar Child Class dapat memberikan perilaku atau informasi yang lebih spesifik.

Contoh:

```php
class Produk
{
    public function infoProduk()
    {
        return "Informasi produk";
    }
}

class ProdukMakanan extends Produk
{
    public function infoProduk()
    {
        return "Informasi produk makanan";
    }
}
```

Pada contoh tersebut, `ProdukMakanan` melakukan **override** terhadap method `infoProduk()` milik `Produk`.

Child Class juga dapat tetap menggunakan method milik Parent Class menggunakan:

```php
parent::infoProduk()
```

---

# 🧩 Studi Kasus

Kalian diminta membuat sebuah program **Data Produk Toko** menggunakan konsep Object-Oriented Programming (OOP).

Sebuah toko memiliki berbagai jenis produk. Untuk tugas ini, terdapat:

- **Produk** sebagai Parent Class
- **ProdukMakanan** sebagai Child Class
- **ProdukElektronik** sebagai Child Class

Setiap produk memiliki data dasar:

- Nama produk
- Harga

Sedangkan setiap jenis produk memiliki data tambahan masing-masing.

### ProdukMakanan

Memiliki tambahan:

- Tanggal kedaluwarsa

### ProdukElektronik

Memiliki tambahan:

- Masa garansi

---

# 📌 Ketentuan Program

## 1. Parent Class

Buat class:

```text
Produk
```

Class tersebut harus memiliki:

- `$nama` → `private`
- `$harga` → `private`
- Constructor
- Getter untuk nama
- Getter untuk harga
- Method `infoProduk()`

Contoh struktur:

```php
class Produk
{
    private $nama;
    private $harga;

    public function __construct($nama, $harga)
    {
        // isi property
    }

    public function getNama()
    {
        // kembalikan nama
    }

    public function getHarga()
    {
        // kembalikan harga
    }

    public function infoProduk()
    {
        // tampilkan informasi produk
    }
}
```

---

## 2. Child Class ProdukMakanan

Buat:

```text
ProdukMakanan extends Produk
```

Tambahkan property:

```text
$tanggalKadaluarsa
```

Property tambahan tersebut harus menggunakan `private`.

Class ini wajib memiliki constructor.

Constructor harus memanggil:

```php
parent::__construct(...)
```

Kemudian buat method:

```php
infoProduk()
```

yang **meng-override** method `infoProduk()` milik Parent.

Di dalam method tersebut wajib menggunakan:

```php
parent::infoProduk()
```

untuk mengambil informasi dasar produk.

---

## 3. Child Class ProdukElektronik

Buat:

```text
ProdukElektronik extends Produk
```

Tambahkan property:

```text
$masaGaransi
```

Property tambahan harus menggunakan `private`.

Class ini juga wajib memiliki constructor dan:

```php
parent::__construct(...)
```

Kemudian override:

```php
infoProduk()
```

dan wajib menggunakan:

```php
parent::infoProduk()
```

---

## 4. Object

Buat minimal **3 object**, yaitu:

- 2 object `ProdukMakanan`
- 1 object `ProdukElektronik`

Contohnya:

```php
$makanan1 = new ProdukMakanan(...);
$makanan2 = new ProdukMakanan(...);
$elektronik1 = new ProdukElektronik(...);
```

Data setiap object harus berbeda.

---

# 🖥️ Contoh Output

Jika data yang digunakan misalnya:

```text
Indomie
Rp3.500
Kadaluarsa: 2027-01-10

Roti Coklat
Rp8.000
Kadaluarsa: 2026-12-20

Headset Gaming
Rp250.000
Garansi: 1 Tahun
```

Maka output program kurang lebih:

```text
===== DATA PRODUK TOKO =====

Produk Makanan
Nama           : Indomie
Harga          : Rp3.500
Kadaluarsa     : 2027-01-10

Produk Makanan
Nama           : Roti Coklat
Harga          : Rp8.000
Kadaluarsa     : 2026-12-20

Produk Elektronik
Nama           : Headset Gaming
Harga          : Rp250.000
Garansi        : 1 Tahun
```

**Data produk bebas**, tidak harus menggunakan contoh di atas.

---

# 🚨 Ketentuan Penting

Program **tidak boleh hanya menghasilkan output yang benar**.

Guru akan mengecek kode programnya.

### Wajib ada:

- [ ] `class Produk`
- [ ] Object dibuat menggunakan `new`
- [ ] Property
- [ ] Method
- [ ] Penggunaan `$this`
- [ ] `__construct()`
- [ ] Property `private`
- [ ] Getter
- [ ] `extends`
- [ ] `parent::__construct()`
- [ ] Method overriding
- [ ] `parent::infoProduk()`
- [ ] Minimal 3 object
- [ ] Data setiap object berbeda

---

# 🧪 Pengujian Encapsulation

Setelah program selesai, coba tambahkan:

```php
echo $makanan1->nama;
```

Program **seharusnya menghasilkan error** karena `$nama` dibuat:

```php
private $nama;
```

Kemudian hapus kembali kode tersebut agar program bisa berjalan normal.

Tujuannya untuk membuktikan bahwa **Encapsulation benar-benar diterapkan**, bukan hanya ditulis di kode.

---

# 💻 Tempat Pengujian

Program harus dapat dijalankan menggunakan **php.io**.

Siswa cukup membuat satu file PHP dan menjalankannya di PHP.io.

Tidak diperbolehkan menggunakan:

- Database
- Laravel
- Composer
- Framework
- Library eksternal

**Gunakan PHP Native saja.**

---

# 📊 Rubrik Penilaian

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
| Output & program berjalan | 5 |
| **Total** | **100** |

---

# ⭐ Bonus

Buat **Child Class ketiga**:

```text
ProdukPakaian extends Produk
```

dengan property:

```text
$ukuran
```

dan override `infoProduk()`.

Bonus dapat digunakan untuk memperbaiki nilai komponen lain yang masih kurang.

---

# 📋 Ketentuan Pengumpulan

Kumpulkan:

1. File `.php`
2. Screenshot hasil program ketika berhasil dijalankan di **php.io**
3. Screenshot atau bukti bahwa program telah memenuhi ketentuan OOP
4. Pastikan nama file menggunakan format:

```text
Nama_NamaProduk.php
```

Contoh:

```text
Fadhil_DataProduk.php
```

---

## 🎯 Tujuan Tugas

Melalui tugas ini, kalian diharapkan tidak hanya menghafal syntax PHP, tetapi mampu menerapkan konsep dasar OOP secara utuh:

**Class → Object → Property → Method → `$this` → Constructor → Encapsulation → Inheritance → Method Overriding**

Setelah tugas ini selesai, kalian akan memiliki dasar yang diperlukan untuk mempelajari konsep OOP tingkat lanjut pada materi berikutnya.
