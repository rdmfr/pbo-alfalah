# PENJELASAN OOP DENGAN BAHASA AWAM + ANALOGI
## Pendamping Tugas Praktik PBO Kelas XI — Data Produk Toko

> Dokumen ini dibuat supaya kalian **paham konsepnya dulu**, baru nulis kodenya. Kalau langsung ngoding tanpa paham analoginya, biasanya cuma jadi "copy-paste" doang.

---

## 🧠 Cara Baca Dokumen Ini

Setiap konsep dijelaskan dengan urutan:

1. **Analogi dulu** (cerita sehari-hari)
2. **Terjemahan ke istilah OOP**
3. **Kaitannya ke tugas kalian** (kasus Produk Toko)
4. **Kode singkat** biar kebayang

---

## 1. Class & Object — "Cetakan Kue vs Kue-nya"

### Analogi
Bayangkan kalian punya **cetakan kue bentuk bintang**. Cetakan itu cuma satu, tapi dari cetakan itu kalian bisa bikin **banyak kue** — kue rasa coklat, kue rasa vanilla, dll. Semua kue itu bentuknya sama (bintang), tapi rasanya bisa beda-beda.

- **Cetakan kue** = `class`
- **Kue yang jadi** = `object`

Cetakan itu sendiri **tidak bisa dimakan**. Yang bisa dimakan adalah kue hasil cetakannya. Sama seperti `class Produk` — dia cuma "blueprint", belum jadi data sungguhan sampai kalian bikin `new Produk(...)`.

### Kaitan ke Tugas
```php
class Produk { ... }        // ini cetakannya

$makanan1 = new Produk(...); // ini "kue" hasil cetakan pertama
$makanan2 = new Produk(...); // ini "kue" hasil cetakan kedua
```
Setiap kali kalian pakai `new`, kalian lagi "mencetak kue baru" dari cetakan yang sama.

---

## 2. Property & Method — "Ciri-Ciri vs Kemampuan"

### Analogi
Kalau kue tadi kita anggap sebagai **object**, maka:
- **Property** = ciri-ciri kue itu (rasa, warna, ukuran)
- **Method** = apa yang bisa dilakukan kue itu (dipotong, dihias, dikemas)

Dalam kehidupan nyata: kalau objeknya adalah **manusia**, propertinya adalah `nama`, `umur`, `tinggi`. Methodnya adalah `makan()`, `tidur()`, `belajar()`.

### Kaitan ke Tugas
```php
class Produk
{
    private $nama;   // property = ciri-ciri produk
    private $harga;  // property

    public function infoProduk()   // method = kemampuan produk untuk "cerita tentang dirinya"
    {
        return "Nama: " . $this->nama;
    }
}
```

---

## 3. `$this` — "Kata Ganti 'Aku'"

### Analogi
Bayangkan ada banyak murid di kelas, dan gurunya bilang: *"Tolong tulis nama **kamu** di buku **kamu** masing-masing."*

Setiap murid akan menulis namanya sendiri, bukan nama temannya. Kata **"kamu"** di situ merujuk ke **diri masing-masing murid**, tergantung siapa yang sedang diajak bicara.

`$this` itu seperti kata **"aku"** di dalam class. Waktu kode di dalam class dijalankan oleh sebuah object tertentu, `$this` akan merujuk ke **object itu sendiri** — bukan object lain.

### Kaitan ke Tugas
```php
class Produk
{
    private $nama;

    public function __construct($nama)
    {
        $this->nama = $nama; // artinya: "nama milik AKU (object ini) = nilai yang dikasih"
    }
}

$makanan1 = new Produk("Indomie");
$makanan2 = new Produk("Roti");
```
Waktu `$makanan1` dibuat, `$this` di dalam constructor artinya `$makanan1`. Waktu `$makanan2` dibuat, `$this` artinya `$makanan2`. **Bukan tertukar.**

---

## 4. Constructor — "Petugas Penyambutan Waktu Object Lahir"

### Analogi
Bayangkan setiap kali ada bayi lahir di rumah sakit, ada **prosedur otomatis** yang langsung jalan: dicatat berat badan, dikasih gelang nama, dicatat jam lahir. Prosedur itu **otomatis jalan sendiri**, tanpa harus disuruh manual satu-satu.

`__construct()` itu seperti "prosedur penyambutan" yang otomatis jalan **setiap kali object baru lahir** (dibuat pakai `new`). Isinya biasanya: "kasih nilai awal ke property-property si object".

### Kaitan ke Tugas
```php
class Produk
{
    private $nama;
    private $harga;

    public function __construct($nama, $harga)
    {
        $this->nama = $nama;   // "gelang nama" dipasang otomatis
        $this->harga = $harga; // "data berat badan" dicatat otomatis
    }
}

$makanan1 = new Produk("Indomie", 3500);
// begitu baris ini jalan, __construct() otomatis dipanggil PHP sendiri
```
Kalian **tidak perlu manggil** `__construct()` secara manual. Dia jalan sendiri begitu ada `new`.

---

## 5. Encapsulation — "Kotak Terkunci dengan Loket Resmi"

### Analogi
Bayangkan **brankas uang di bank**. Kalian tidak bisa asal buka brankas dan ambil uang sendiri. Kalian harus lewat **teller (petugas resmi)** di loket. Teller yang punya akses langsung ke brankas, sedangkan nasabah cuma bisa minta lewat loket.

- **Brankas (data asli)** = property `private`
- **Teller (loket resmi)** = method `public` seperti `getNama()`, `getHarga()`

Kenapa harus begitu? Supaya data **tidak bisa diubah atau diambil sembarangan** dari luar. Kalau semua data dibuat `public`, siapa saja bisa "colongan masuk" dan mengubah data seenaknya — ini bahaya, terutama untuk data penting seperti harga produk.

### Kaitan ke Tugas
```php
class Produk
{
    private $nama; // "brankas" - tidak bisa diakses langsung dari luar

    public function getNama() // "loket resmi" - cara sah untuk ambil data
    {
        return $this->nama;
    }
}

$p = new Produk("Indomie", 3500);

echo $p->nama;       // ❌ ERROR! Ini sama seperti coba masuk ke brankas langsung
echo $p->getNama();  // ✅ BENAR! Ini lewat "loket resmi"
```

> 💡 Inilah kenapa di tugas kalian diminta coba `echo $makanan1->nama;` dan lihat errornya — itu bukti brankasnya beneran terkunci, bukan cuma tulisan `private` doang tanpa efek.

---

## 6. Inheritance — "Warisan dari Orang Tua ke Anak"

### Analogi
Bayangkan seorang **anak mewarisi sifat dan barang dari orang tuanya** — misalnya warna mata, atau bahkan warisan rumah. Anak **otomatis punya** apa yang dimiliki orang tua, **tanpa harus bikin dari nol**. Tapi anak juga bisa punya sifat tambahan yang orang tuanya tidak punya (misalnya anak jago main gitar padahal orang tuanya tidak).

- **Orang tua** = Parent Class (`Produk`)
- **Anak** = Child Class (`ProdukMakanan`, `ProdukElektronik`)
- **Sifat yang diwarisi** = property & method dari Parent
- **Sifat tambahan anak** = property/method baru yang cuma dimiliki Child

### Kaitan ke Tugas
```php
class Produk
{
    public function infoProduk()
    {
        return "Ini produk umum";
    }
}

class ProdukMakanan extends Produk // "anak" yang mewarisi dari Produk
{
    private $tanggalKadaluarsa; // sifat tambahan yang cuma dimiliki anak ini
}

$makanan = new ProdukMakanan(...);
echo $makanan->infoProduk(); // bisa dipakai walau tidak ditulis ulang di ProdukMakanan
```
`ProdukMakanan` **otomatis mewarisi** method `infoProduk()` dari `Produk`, sama seperti anak yang otomatis mewarisi rumah orang tuanya tanpa perlu membangun rumah baru dari nol.

### Kenapa Perlu `parent::__construct()`?
Analoginya: waktu anak "mendaftar identitas resmi" (akta lahir), dia tetap butuh data dasar dari orang tua (nama keluarga, misalnya) **plus** data tambahan miliknya sendiri (nama panggilan). `parent::__construct()` artinya *"jalankan dulu prosedur pendaftaran milik orang tua, baru tambahkan data khusus milik anak."*

```php
class ProdukMakanan extends Produk
{
    private $tanggalKadaluarsa;

    public function __construct($nama, $harga, $tanggalKadaluarsa)
    {
        parent::__construct($nama, $harga);      // urus dulu data dari "orang tua"
        $this->tanggalKadaluarsa = $tanggalKadaluarsa; // baru urus data tambahan si "anak"
    }
}
```

---

## 7. Method Overriding — "Anak Punya Gaya Bicara Sendiri"

### Analogi
Orang tua punya cara memperkenalkan diri: *"Saya adalah anggota keluarga ini."* Tapi si anak, meskipun mewarisi cara itu, bisa bilang dengan versi **lebih spesifik**: *"Saya adalah anggota keluarga ini, dan saya suka main gitar."*

Anak **tidak menghapus** cara bicara orang tua, tapi **menulis ulang versi miliknya sendiri** yang lebih detail — dan kalau perlu, anak masih bisa **mengutip** cara bicara orang tua di dalam versinya sendiri.

- **Menulis ulang cara bicara** = Method Overriding
- **Mengutip cara bicara orang tua di dalam versi sendiri** = `parent::infoProduk()`

### Kaitan ke Tugas
```php
class Produk
{
    public function infoProduk()
    {
        return "Nama: $this->nama, Harga: $this->harga";
    }
}

class ProdukMakanan extends Produk
{
    private $tanggalKadaluarsa;

    public function infoProduk() // override — versi baru milik anak
    {
        $infoDasar = parent::infoProduk(); // "mengutip" info dari orang tua dulu
        return $infoDasar . ", Kadaluarsa: $this->tanggalKadaluarsa"; // baru ditambah info khusus
    }
}
```

Kalau `ProdukMakanan` **tidak** menulis ulang `infoProduk()`, dia akan pakai versi milik `Produk` apa adanya (itu namanya inheritance biasa). Tapi karena `ProdukMakanan` **butuh nunjukin info tambahan** (tanggal kadaluarsa), dia perlu override method-nya.

---

## 🔗 Menghubungkan Semua Konsep dalam Satu Cerita

Bayangkan kalian sedang membuat **formulir pendaftaran produk toko**:

1. Ada **formulir kosong** (`class Produk`) yang jadi template.
2. Setiap kali ada produk baru masuk toko, kalian **isi formulir baru** (`new Produk(...)`) — ini bikin object.
3. Waktu formulir diisi, ada **prosedur otomatis** (`__construct()`) yang langsung mencatat nama dan harga.
4. Data nama dan harga itu **disimpan di laci terkunci** (`private`), orang lain harus lewat **loket resmi** (`getNama()`, `getHarga()`) untuk melihatnya — ini encapsulation.
5. Untuk produk makanan dan elektronik, kalian **buat formulir turunan** (`extends`) yang otomatis punya semua kolom formulir dasar, **plus** kolom tambahan sesuai jenisnya — ini inheritance.
6. Karena formulir turunan itu perlu menampilkan info tambahan, kalian **tulis ulang cara menampilkan info** (`infoProduk()` di-override), tapi tetap **mengutip** info dasar dari formulir induk (`parent::infoProduk()`).

Kalau kalian bisa menceritakan ulang alur di atas pakai kata-kata sendiri (tanpa lihat kode), berarti kalian sudah **paham konsepnya**, bukan cuma hafal syntax-nya.

---

## ✅ Checklist Pemahaman Diri (Sebelum Ngoding)

Coba jawab dulu tanpa buka kode:

- [ ] Bisa jelaskan bedanya `class` dan `object` pakai analogi sendiri?
- [ ] Ngerti kenapa `$this` bisa merujuk ke object yang berbeda-beda?
- [ ] Ngerti kenapa constructor jalan otomatis tanpa dipanggil manual?
- [ ] Bisa jelaskan kenapa `private` itu penting, bukan cuma aturan formal?
- [ ] Ngerti kenapa `ProdukMakanan` butuh `parent::__construct()`?
- [ ] Ngerti bedanya "mewarisi method" vs "override method"?

Kalau semua sudah dicentang, kalian siap lanjut ke pengerjaan tugas di bawah ini. Selamat mengerjakan! 🚀

---
---

# 📝 TUGAS PRAKTIK PBO KELAS XI
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

> 💡 Kalau masih bingung dengan istilah-istilah di atas, baca lagi bagian **Penjelasan dengan Bahasa Awam + Analogi** di awal dokumen ini sebelum mulai ngoding.

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
