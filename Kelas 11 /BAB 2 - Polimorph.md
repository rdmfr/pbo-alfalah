# 📘 Modul Ajar PHP OOP Lanjutan — Kelas XI RPL/PPLG
## Setelah Method Overriding: Polymorphism, Abstract Class, Interface & Static

> **Konteks studi kasus:** Sistem Data Produk Toko (lanjutan dari materi Inheritance & Method Overriding sebelumnya)
> **Kurikulum:** Merdeka — Informatika/Pemrograman Berorientasi Objek
> **Kelas:** XI RPL/PPLG
> **Prasyarat:** Siswa sudah paham Class, Object, Property, Method, `$this`, Constructor, Encapsulation, Inheritance, dan Method Overriding

---

## 🎯 Tujuan Pembelajaran

Setelah mempelajari modul ini, siswa mampu:
1. Menjelaskan konsep **Polymorphism** dan mengaitkannya dengan Method Overriding yang sudah dipelajari
2. Membuat dan menggunakan **Abstract Class** sebagai "blueprint wajib"
3. Membuat dan menggunakan **Interface** sebagai "kontrak" antar class
4. Membedakan kapan menggunakan Abstract Class vs Interface
5. Menggunakan **Static Property** dan **Static Method**
6. Menulis program PHP native yang bisa langsung dites di [onlinephp.io](https://onlinephp.io)

---

## 🔄 Recap Kilat: Sampai Mana Kita?

Sebelumnya kalian sudah belajar bahwa `class Produk` bisa "diturunkan" jadi `class ProdukElektronik` (Inheritance), dan `class ProdukElektronik` bisa "menimpa ulang" method dari induknya (Method Overriding). Contoh singkat biar ingat lagi:

```php
<?php
class Produk {
    public function infoDiskon() {
        return "Produk ini tidak ada diskon khusus.";
    }
}

class ProdukElektronik extends Produk {
    // Method Overriding: menimpa method infoDiskon() dari class induk
    public function infoDiskon() {
        return "Produk elektronik dapat diskon garansi tambahan 5%.";
    }
}

$p1 = new Produk();
$p2 = new ProdukElektronik();

echo $p1->infoDiskon() . "\n";
echo $p2->infoDiskon() . "\n";
```

Nah, sekarang pertanyaannya: **kalau kita punya 10 jenis produk, apakah kita harus menulis `if/else` panjang untuk manggil method yang beda-beda tiap produk?** Jawabannya: TIDAK PERLU. Di sinilah **Polymorphism** berperan.

---

## 1️⃣ Polymorphism — "Satu Perintah, Banyak Bentuk Jawaban"

### 🧠 Penjelasan Awam

**Polymorphism** artinya "banyak bentuk". Analoginya gini: bayangkan kalian punya *remote* universal, lalu kalian tekan tombol **"Nyala"**. Kalau remote itu diarahkan ke TV, yang nyala TV. Kalau diarahkan ke AC, yang nyala AC. Kalau diarahkan ke kipas angin, yang nyala kipas angin.

**Tombolnya sama** (`"Nyala"`), tapi **hasilnya beda-beda** tergantung objek apa yang menerima perintah itu.

Di PHP, ini artinya: kita bisa punya banyak class turunan (`ProdukElektronik`, `ProdukMakanan`, `ProdukPakaian`) yang semuanya punya method dengan **nama sama** (misalnya `infoDiskon()`), tapi kita bisa memanggilnya lewat satu alur kode yang seragam, dan PHP otomatis tahu harus menjalankan versi method milik class yang mana.

### 💻 Contoh Kode (Bisa Dites di onlinephp.io)

```php
<?php
class Produk {
    public $nama;

    public function __construct($nama) {
        $this->nama = $nama;
    }

    public function infoDiskon() {
        return "$this->nama: tidak ada diskon khusus.";
    }
}

class ProdukElektronik extends Produk {
    public function infoDiskon() {
        return "$this->nama: diskon garansi tambahan 5%.";
    }
}

class ProdukMakanan extends Produk {
    public function infoDiskon() {
        return "$this->nama: diskon 10% jika mendekati tanggal kedaluwarsa.";
    }
}

class ProdukPakaian extends Produk {
    public function infoDiskon() {
        return "$this->nama: diskon 20% untuk koleksi musim lalu.";
    }
}

// Kumpulkan semua produk dalam satu array (bertipe beda-beda)
$daftarProduk = [
    new ProdukElektronik("TV LED 32 inch"),
    new ProdukMakanan("Roti Tawar"),
    new ProdukPakaian("Jaket Denim"),
    new Produk("Barang Umum")
];

// INI KUNCI POLYMORPHISM:
// Kita panggil infoDiskon() dengan cara yang SAMA untuk semua produk,
// tapi hasilnya BEDA-BEDA sesuai jenis produknya masing-masing.
foreach ($daftarProduk as $produk) {
    echo $produk->infoDiskon() . "\n";
}
```

**Penjelasan baris per baris bagian penting:**
- `$daftarProduk = [...]` → kita taruh objek dari class yang berbeda-beda (`ProdukElektronik`, `ProdukMakanan`, dst) ke dalam **satu array yang sama**.
- `foreach ($daftarProduk as $produk)` → kita loop satu-satu, dan **kode di dalam loop ini tidak perlu tahu** objek yang sedang diproses itu jenis apa.
- `$produk->infoDiskon()` → baris ini **sama persis** untuk semua jenis produk, tapi PHP otomatis menjalankan method `infoDiskon()` milik class aslinya (elektronik, makanan, pakaian). Inilah yang disebut **polymorphism**.

> 💡 **Poin penting untuk siswa:** Polymorphism bukan fitur baru yang harus ditulis dengan syntax khusus. Polymorphism adalah **hasil otomatis** dari Inheritance + Method Overriding yang sudah kalian pelajari. Jadi kalau kalian sudah bisa overriding, kalian **sudah menerapkan polymorphism** tanpa sadar!

---

## 2️⃣ Abstract Class — "Blueprint yang Wajib Diikuti"

### 🧠 Penjelasan Awam

Bayangkan kalian jadi kepala arsitek dan bikin **cetak biru (blueprint)** rumah. Blueprint itu **tidak bisa dijadikan rumah asli** — dia cuma acuan. Tapi, blueprint itu **mewajibkan** setiap kontraktor yang memakainya untuk membuat "pintu depan" dan "atap" (walau modelnya bisa beda-beda tiap kontraktor).

**Abstract Class** persis seperti itu:
- Tidak bisa langsung dibuat objeknya (`new`) — dia cuma "cetakan"
- Bisa punya method biasa (sudah ada isinya) **dan** method abstract (wajib diisi/dioverride oleh class anak)
- Kalau class anak tidak mengisi method abstract-nya → PHP akan **error**

### 💻 Contoh Kode (Bisa Dites di onlinephp.io)

```php
<?php
// Abstract class = cetakan dasar, TIDAK bisa dibuat objeknya langsung
abstract class Produk {
    public $nama;
    public $harga;

    public function __construct($nama, $harga) {
        $this->nama = $nama;
        $this->harga = $harga;
    }

    // Method BIASA, sudah ada isinya, bisa langsung dipakai turunan
    public function tampilkanInfo() {
        return "Produk: $this->nama - Rp" . number_format($this->harga, 0, ',', '.');
    }

    // Method ABSTRACT: hanya "judul", TANPA isi ({}), WAJIB diisi oleh class anak
    abstract public function hitungPajak();
}

class ProdukElektronik extends Produk {
    // WAJIB ada, karena hitungPajak() abstract di class induk
    public function hitungPajak() {
        return $this->harga * 0.11; // PPN 11%
    }
}

class ProdukMakanan extends Produk {
    // WAJIB ada juga, tapi rumusnya boleh beda
    public function hitungPajak() {
        return 0; // Sembako tidak kena pajak
    }
}

// $produkInduk = new Produk("Contoh", 10000); // ❌ Ini akan ERROR jika di-uncomment!
// Pesan errornya: "Cannot instantiate abstract class Produk"

$tv = new ProdukElektronik("TV LED 32 inch", 2000000);
$roti = new ProdukMakanan("Roti Tawar", 15000);

echo $tv->tampilkanInfo() . " | Pajak: Rp" . number_format($tv->hitungPajak(), 0, ',', '.') . "\n";
echo $roti->tampilkanInfo() . " | Pajak: Rp" . number_format($roti->hitungPajak(), 0, ',', '.') . "\n";
```

**Penjelasan baris per baris bagian penting:**
- `abstract class Produk` → kata kunci `abstract` di depan `class` membuat class ini **tidak bisa langsung dibuat objeknya**.
- `abstract public function hitungPajak();` → perhatikan **tidak ada kurung kurawal `{ }`**, cuma diakhiri titik koma. Ini menandakan "method ini WAJIB diisi oleh class anak, saya cuma kasih judulnya saja".
- `class ProdukElektronik extends Produk` → karena mewarisi class abstract, class ini **wajib** menuliskan isi `hitungPajak()`, kalau tidak → PHP akan langsung error saat dijalankan.
- Baris yang di-comment `// $produkInduk = new Produk(...)` sengaja saya matikan supaya kode bisa jalan. Coba siswa **hapus tanda `//`** di onlinephp.io biar lihat sendiri pesan errornya!

> 💡 **Kapan pakai Abstract Class?** Kalau kalian punya beberapa class yang **jelas-jelas serumpun** (sama-sama "Produk") dan ingin **memaksa** semua anaknya wajib punya method tertentu, tapi tetap ingin berbagi kode/property yang sama (seperti `$nama`, `$harga`, `tampilkanInfo()`).

---

## 3️⃣ Interface — "Kontrak/Perjanjian Wajib"

### 🧠 Penjelasan Awam

Kalau Abstract Class itu seperti blueprint rumah (masih ada bagian yang sudah jadi), maka **Interface** itu murni **daftar perjanjian/kontrak** — isinya cuma daftar "apa saja yang WAJIB dimiliki", tanpa ada isi sama sekali.

Analoginya: bayangkan kalian melamar kerja jadi kasir di sebuah minimarket. Kontrak kerjanya bilang: *"Kamu wajib bisa: melayani pembayaran, dan mencetak struk."* Kontrak itu tidak peduli **caranya** bagaimana — mau bayar pakai QRIS, cash, atau kartu, yang penting fungsi "melayani pembayaran" itu **ada**.

Bedanya dengan Abstract Class:
- Interface **tidak bisa** punya property biasa dan **tidak bisa** punya method yang sudah ada isinya (semua method wajib kosong/tanpa isi)
- Satu class bisa "menandatangani" **banyak interface sekaligus** (pakai `implements`), tapi hanya bisa `extends` **satu** class saja

### 💻 Contoh Kode (Bisa Dites di onlinephp.io)

```php
<?php
// Interface = daftar kontrak, isinya cuma "judul-judul" method, TANPA isi
interface BisaDiskon {
    public function hitungDiskon();
}

interface BisaDikirim {
    public function estimasiOngkir();
}

class ProdukElektronik implements BisaDiskon, BisaDikirim {
    public $nama;
    public $harga;

    public function __construct($nama, $harga) {
        $this->nama = $nama;
        $this->harga = $harga;
    }

    // WAJIB ada karena implements BisaDiskon
    public function hitungDiskon() {
        return $this->harga * 0.05; // diskon 5%
    }

    // WAJIB ada karena implements BisaDikirim
    public function estimasiOngkir() {
        return "2-3 hari (barang elektronik perlu packing khusus)";
    }
}

class ProdukDigital implements BisaDiskon {
    // Produk digital TIDAK implements BisaDikirim,
    // karena e-book/aplikasi tidak perlu dikirim fisik!
    public $nama;
    public $harga;

    public function __construct($nama, $harga) {
        $this->nama = $nama;
        $this->harga = $harga;
    }

    public function hitungDiskon() {
        return $this->harga * 0.15; // diskon 15%, karena tidak ada biaya gudang
    }
}

$tv = new ProdukElektronik("TV LED 32 inch", 2000000);
$ebook = new ProdukDigital("E-book Belajar PHP", 50000);

echo "Diskon TV: Rp" . number_format($tv->hitungDiskon(), 0, ',', '.') . "\n";
echo "Ongkir TV: " . $tv->estimasiOngkir() . "\n";
echo "Diskon E-book: Rp" . number_format($ebook->hitungDiskon(), 0, ',', '.') . "\n";
```

**Penjelasan baris per baris bagian penting:**
- `interface BisaDiskon { public function hitungDiskon(); }` → cuma daftar "judul" method, tanpa `{ }` isi sama sekali.
- `class ProdukElektronik implements BisaDiskon, BisaDikirim` → kata kunci **`implements`** (bukan `extends`) dipakai untuk "menandatangani kontrak". Bisa lebih dari satu interface, dipisah koma.
- Perhatikan `ProdukDigital` **hanya** `implements BisaDiskon` (tanpa `BisaDikirim`) — karena produk digital memang tidak butuh ongkir. Ini menunjukkan fleksibilitas interface: class boleh pilih kontrak mana saja yang relevan untuknya.

### 📊 Perbandingan Abstract Class vs Interface

| Aspek | Abstract Class | Interface |
|---|---|---|
| Kata kunci | `abstract class` + `extends` | `interface` + `implements` |
| Bisa punya method dengan isi? | ✅ Bisa | ❌ Tidak bisa (semua kosong) |
| Bisa punya property biasa? | ✅ Bisa | ❌ Tidak bisa |
| Jumlah yang bisa "diwarisi" sekaligus | Hanya 1 (single inheritance) | Boleh banyak sekaligus |
| Dipakai untuk | Class yang serumpun & ingin berbagi kode | Class beda-beda yang wajib punya kemampuan tertentu |

---

## 4️⃣ Static Property & Static Method — "Milik Bersama, Bukan Milik Perorangan"

### 🧠 Penjelasan Awam

Sejauh ini, tiap kali kita bikin objek baru (`new Produk(...)`), setiap objek punya **datanya sendiri-sendiri**. Tapi kadang kita butuh data yang **dipakai bareng-bareng** oleh semua objek — contohnya: **jumlah total produk yang sudah dibuat**.

Analoginya: bayangkan sebuah kelas sekolah. Setiap siswa (objek) punya nama dan nilai masing-masing (property biasa). Tapi **"jumlah total siswa di kelas ini"** adalah data milik **kelasnya**, bukan milik satu siswa. Itulah **static property**.

### 💻 Contoh Kode (Bisa Dites di onlinephp.io)

```php
<?php
class Produk {
    public $nama;

    // STATIC PROPERTY: dimiliki bersama oleh CLASS, bukan oleh satu objek
    public static $totalProduk = 0;

    public function __construct($nama) {
        $this->nama = $nama;
        // Setiap kali ada objek baru dibuat, tambah hitungan bersama ini
        self::$totalProduk++;
    }

    // STATIC METHOD: bisa dipanggil TANPA harus bikin objek dulu
    public static function tampilkanTotal() {
        return "Total produk yang sudah dibuat: " . self::$totalProduk;
    }
}

$p1 = new Produk("TV LED");
$p2 = new Produk("Kulkas");
$p3 = new Produk("Roti Tawar");

// Panggil static method langsung lewat nama Class, PAKAI :: bukan ->
echo Produk::tampilkanTotal() . "\n";

// Bisa juga diakses lewat objek, tapi tetap datanya SAMA untuk semua objek
echo "Cek lewat objek p1: " . $p1::tampilkanTotal() . "\n";
```

**Penjelasan baris per baris bagian penting:**
- `public static $totalProduk = 0;` → kata kunci `static` bikin property ini **bukan milik satu objek**, tapi milik **class itu sendiri**, dan nilainya **dibagi bersama** semua objek.
- `self::$totalProduk++;` → di dalam class, kita akses static property pakai `self::` (bukan `$this->`), karena `$this` itu untuk data milik objek, sedangkan `self::` untuk data milik class.
- `public static function tampilkanTotal()` → static method bisa dipanggil **tanpa** perlu `new` dulu.
- `Produk::tampilkanTotal()` → perhatikan tanda **`::`** (disebut *scope resolution operator*), bukan `->` seperti biasanya. Ini karena kita memanggil langsung dari nama Class, bukan dari objek.

> 💡 **Kapan pakai static?** Ketika data atau fungsi itu **tidak butuh** data pribadi dari objek tertentu, dan **masuk akal untuk dipakai bersama** — misalnya: penghitung jumlah objek, konfigurasi tetap (pajak nasional), atau fungsi bantu/utility seperti `formatRupiah()`.

---

## 🧪 Latihan Siswa

**Soal 1 (Polymorphism):**
Buat 3 class turunan dari `Produk` (misalnya `ProdukBuku`, `ProdukMainan`, `ProdukKosmetik`), masing-masing punya method `infoDiskon()` sendiri. Buat array berisi ketiga objek itu, lalu tampilkan semua diskonnya pakai satu `foreach` saja.

**Soal 2 (Abstract Class):**
Buat `abstract class Kendaraan` dengan method abstract `hitungBiayaSewa()`. Buat 2 class anak: `Motor` dan `Mobil`, masing-masing dengan rumus sewa berbeda. Coba juga uncomment baris `new Kendaraan()` untuk membuktikan errornya.

**Soal 3 (Interface):**
Buat interface `BisaDicetak` dengan method `cetakLabel()`. Terapkan pada class `ProdukFisik`, tapi jangan diterapkan pada class `ProdukDigital` (karena produk digital tidak butuh label cetak).

**Soal 4 (Static):**
Tambahkan static property `$totalPendapatan` pada class `Produk`. Setiap kali produk "terjual" (buat method `jual($jumlah)`), tambahkan hasil penjualan ke `$totalPendapatan`. Tampilkan total pendapatan di akhir program.

---

## ✅ Ringkasan

| Konsep | Intinya |
|---|---|
| **Polymorphism** | Satu cara pemanggilan method, hasil berbeda tergantung objeknya — otomatis terjadi dari inheritance + overriding |
| **Abstract Class** | Cetakan yang tidak bisa langsung dipakai, tapi mewajibkan sebagian method diisi oleh anaknya |
| **Interface** | Kontrak murni (tanpa isi kode) yang wajib dipenuhi, bisa "ditandatangani" lebih dari satu sekaligus |
| **Static** | Property/method milik bersama seluruh class, dipanggil pakai `::`, bukan milik satu objek saja |

> 📌 **Catatan untuk guru:** Semua contoh kode di atas sudah diuji berjalan tanpa error dan bisa langsung disalin ke [https://onlinephp.io](https://onlinephp.io) untuk didemokan di depan kelas atau dibagikan sebagai link latihan mandiri siswa.
