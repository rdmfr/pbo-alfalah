# 📘 PANDUAN TAMBAHAN — Analogi & Contoh Pengerjaan
## Tugas PBO (PHP Native) — Kelas XI RPL/PPLG

> Panduan ini **bukan jawaban tugas**. Contoh kode di sini memakai nama class dan property yang berbeda dari soal (`Laptop`, `Produk`, dll), jadi kalian tetap wajib mengerjakan dengan nama dan logika kalian sendiri sesuai instruksi "dilarang menyalin persis".
> Semua contoh murni **PHP Native** — bisa langsung dites di [onlinephp.io](https://onlinephp.io).

---

## 🧠 Analogi Dasar Sebelum Mulai

| Istilah PBO | Analogi Sehari-hari |
|---|---|
| **Class** | Cetakan kue (belum jadi kue, hanya bentuknya) |
| **Object** | Kue yang sudah jadi dari cetakan tadi (bisa dibuat banyak, rasanya bisa beda-beda) |
| **Property** | Bahan/ciri kue: rasa, ukuran, topping |
| **Method** | Hal yang bisa dilakukan kue itu: "dipotong()", "disajikan()" |
| **Constructor** | Proses "menuang adonan ke cetakan" — dijalankan otomatis saat kue (object) dibuat |
| **Abstract Class** | Resep umum "Cara Membuat Kue" yang wajib ada langkah "panggang()", tapi tiap jenis kue (bolu, brownies) punya cara panggang sendiri. Resep umum ini **tidak bisa langsung dipakai masak**, harus jadi resep turunan dulu |
| **Interface** | Sertifikat/kontrak, misalnya "Sertifikat Halal". Banyak jenis makanan berbeda bisa punya sertifikat yang sama, tapi cara masing-masing memenuhi syaratnya beda-beda |
| **Polymorphism** | Tombol "Play" di remote — untuk TV artinya nyalakan siaran, untuk speaker artinya putar musik. **Perintahnya sama, hasilnya beda** tergantung objeknya |
| **Static Property/Method** | Meja kasir toko kue — bukan milik satu kue tertentu, tapi milik **tokonya**. Semua kue yang laku dicatat di kasir yang sama |

---

## 🅰️ BAGIAN A — Dasar PBO

### Analogi
Bayangkan kalian bikin aplikasi katalog laptop. `Laptop` itu cetakannya, tiap laptop yang kalian beli/jual (ASUS, Lenovo) adalah objek hasil cetakan itu.

### Contoh Pengerjaan (A1 + A2 + A3)

```php
<?php
// Contoh ini pakai nama HandphoneSaya, kalian WAJIB pakai nama lain (misal: Laptop, Sepatu, dll)

class HandphoneSaya {
    // Property (ciri-ciri objek)
    public $merk;
    public $ram;
    public $harga;

    // Constructor: dijalankan otomatis saat object dibuat
    public function __construct($merk, $ram, $harga) {
        $this->merk  = $merk;
        $this->ram   = $ram;
        $this->harga = $harga;
    }

    // Method: menampilkan spesifikasi
    public function tampilkanSpesifikasi() {
        return "Merk: {$this->merk}, RAM: {$this->ram} GB, Harga: Rp" . number_format($this->harga);
    }

    // Method dengan parameter (setara soal A3 / hitungTotalHarga)
    public function hitungHargaSetelahDiskon($persenDiskon) {
        $potongan = $this->harga * ($persenDiskon / 100);
        $hargaAkhir = $this->harga - $potongan;
        return "Harga setelah diskon {$persenDiskon}%: Rp" . number_format($hargaAkhir);
    }
}

// Membuat 2 object berbeda
$hp1 = new HandphoneSaya("Samsung", 8, 3500000);
$hp2 = new HandphoneSaya("Xiaomi", 6, 2200000);

echo $hp1->tampilkanSpesifikasi() . "<br>";
echo $hp1->hitungHargaSetelahDiskon(10) . "<br><br>";

echo $hp2->tampilkanSpesifikasi() . "<br>";
echo $hp2->hitungHargaSetelahDiskon(15) . "<br>";
```

**Yang harus kalian ubah untuk soal A:**
- Nama class jadi `Laptop`
- Property jadi `$merk`, `$ram`, `$prosesor` (sesuai soal)
- Buat 2 object laptop (misal ASUS & Lenovo), bukan handphone
- Tambahkan `hitungTotalHarga($diskon)` sesuai nama yang diminta soal A3

💡 **Kesalahan umum:** lupa `$this->` saat mengakses property di dalam method — hasilnya `Undefined variable`.

---

## 🅱️ BAGIAN B — Polymorphism, Abstract, Interface, Static

### Analogi B1 (Polymorphism)
Tiga jenis produk toko (buku, mainan, kosmetik) semuanya "anak" dari `Produk`. Semua "bisa didiskon", tapi caranya beda-beda — seperti tombol "Play" yang beda hasil tergantung alatnya.

### Contoh Pengerjaan B1

```php
<?php
class ItemToko {
    public $nama;
    public $harga;
    public function __construct($nama, $harga) {
        $this->nama = $nama;
        $this->harga = $harga;
    }
    public function infoDiskon() {
        return "Item umum, belum ada aturan diskon.";
    }
}

class ItemElektronik extends ItemToko {
    public function infoDiskon() {
        return "{$this->nama}: diskon 5% karena elektronik.";
    }
}

class ItemPakaian extends ItemToko {
    public function infoDiskon() {
        return "{$this->nama}: diskon 20% (obral musim panas).";
    }
}

class ItemMakanan extends ItemToko {
    public function infoDiskon() {
        return "{$this->nama}: diskon 50% karena mendekati kedaluwarsa.";
    }
}

// Array berisi objek berbeda-beda jenis
$daftarItem = [
    new ItemElektronik("Kabel USB", 25000),
    new ItemPakaian("Kaos Polos", 60000),
    new ItemMakanan("Roti Tawar", 15000),
];

// SATU foreach saja, tidak perlu if/else cek jenis produk
foreach ($daftarItem as $item) {
    echo $item->infoDiskon() . "<br>";
}
```
📌 Ini yang disebut polymorphism: `foreach` memanggil `infoDiskon()` yang **sama namanya**, tapi PHP otomatis tahu harus menjalankan versi milik `ItemElektronik`, `ItemPakaian`, atau `ItemMakanan` — tanpa kalian tulis `if ($item instanceof ...)`.

### Analogi B2 (Abstract Class)
`Kendaraan` seperti resep "Cara Menghitung Ongkos Sewa" yang **wajib** diisi tiap jenis kendaraan, tapi resep induknya sendiri tidak bisa "dimasak" langsung (tidak bisa `new Kendaraan()`).

### Contoh Pengerjaan B2

```php
<?php
abstract class AlatTransportasi {
    public $namaUnit;
    public function __construct($namaUnit) {
        $this->namaUnit = $namaUnit;
    }
    // Method abstract: WAJIB diisi oleh class anak, tidak boleh punya isi di sini
    abstract public function hitungBiayaSewa($jam);
}

class Sepeda extends AlatTransportasi {
    public function hitungBiayaSewa($jam) {
        return $jam * 5000; // tarif sepeda per jam
    }
}

class MobilPribadi extends AlatTransportasi {
    public function hitungBiayaSewa($jam) {
        return $jam * 75000; // tarif mobil per jam
    }
}

$sepeda = new Sepeda("Sepeda Gunung");
echo $sepeda->namaUnit . " - Biaya 3 jam: Rp" . $sepeda->hitungBiayaSewa(3) . "<br>";

$mobil = new MobilPribadi("Avanza");
echo $mobil->namaUnit . " - Biaya 3 jam: Rp" . $mobil->hitungBiayaSewa(3) . "<br>";

// Uncomment baris di bawah untuk membuktikan error:
// $tes = new AlatTransportasi("Contoh");
// Error yang muncul: "Fatal error: Uncaught Error: Cannot instantiate abstract class AlatTransportasi"
// Artinya: abstract class hanya boleh jadi "cetakan dasar", tidak boleh dibuat objeknya langsung.
```

### Analogi B3 (Interface)
`BisaDicetak` seperti sertifikat "Boleh Dicetak Label". Barang fisik (baju, buku) butuh sertifikat itu; barang digital (e-book, lisensi software) tidak butuh karena tidak ada wujud fisiknya.

### Contoh Pengerjaan B3

```php
<?php
interface BisaDikirim {
    public function kirimBarang();
}

interface BisaDicetak {
    public function cetakLabel();
}

// BarangFisik menerapkan 2 interface sekaligus (dipisah koma)
class BarangFisik implements BisaDikirim, BisaDicetak {
    public $nama;
    public function __construct($nama) { $this->nama = $nama; }

    public function kirimBarang() {
        return "{$this->nama} dikirim via kurir.";
    }
    public function cetakLabel() {
        return "Label pengiriman untuk {$this->nama} berhasil dicetak.";
    }
}

// BarangDigital TIDAK implements BisaDicetak, karena tidak perlu label fisik
class BarangDigital implements BisaDikirim {
    public $nama;
    public function __construct($nama) { $this->nama = $nama; }

    public function kirimBarang() {
        return "{$this->nama} dikirim otomatis via email/link download.";
    }
}

$fisik = new BarangFisik("Buku Tulis");
echo $fisik->kirimBarang() . "<br>";
echo $fisik->cetakLabel() . "<br>";

$digital = new BarangDigital("E-book PBO");
echo $digital->kirimBarang() . "<br>";
// $digital->cetakLabel(); // ini akan ERROR karena BarangDigital tidak implements BisaDicetak
```

### Analogi B4 (Static)
`$totalPendapatan` seperti **mesin kasir toko** — satu mesin dipakai bersama untuk semua transaksi, bukan dompet pribadi tiap kue. Berapa pun kue yang terjual, semua uangnya masuk ke kasir yang sama.

### Contoh Pengerjaan B4

```php
<?php
class Barang {
    public $nama;
    public $harga;
    // static property: dimiliki BERSAMA oleh semua object Barang, bukan milik satu object saja
    public static $totalPendapatan = 0;

    public function __construct($nama, $harga) {
        $this->nama = $nama;
        $this->harga = $harga;
    }

    public function jual($jumlah) {
        $subtotal = $this->harga * $jumlah;
        self::$totalPendapatan += $subtotal; // pakai self:: bukan $this-> untuk static
        echo "{$this->nama} terjual {$jumlah} pcs, subtotal Rp" . number_format($subtotal) . "<br>";
    }

    // static method: bisa dipanggil tanpa membuat object dulu -> Barang::tampilkanTotalPendapatan()
    public static function tampilkanTotalPendapatan() {
        echo "TOTAL PENDAPATAN TOKO: Rp" . number_format(self::$totalPendapatan) . "<br>";
    }
}

$barang1 = new Barang("Pensil", 2000);
$barang2 = new Barang("Penghapus", 1500);

$barang1->jual(10); // subtotal masuk ke kasir bersama
$barang2->jual(5);  // subtotal ini JUGA masuk ke kasir yang sama

Barang::tampilkanTotalPendapatan(); // dipanggil pakai nama Class, bukan $barang1 atau $barang2
```
⚠️ **Kesalahan umum:** menulis `$this->totalPendapatan` — ini salah karena static property bukan milik satu object, harus pakai `self::$totalPendapatan` (di dalam class) atau `NamaClass::$totalPendapatan` (dari luar class).

---

## 🅲 BAGIAN C — Contoh Cara Menjawab Refleksi

> Ini **contoh gaya jawaban**, isi dengan kalimat kalian sendiri, jangan disalin persis.

**1. Perbedaan Abstract Class vs Interface**
Contoh gaya jawaban: "Menurut saya, abstract class itu seperti resep dasar yang sudah punya sebagian langkah jadi (property, method biasa), tapi ada bagian yang wajib diisi sendiri oleh resep turunannya. Interface lebih seperti daftar 'janji' method yang harus ada, tanpa isi sama sekali, dan satu class bisa punya banyak 'janji' sekaligus lewat `implements`."

**2. Kenapa static cocok untuk "total objek" tapi tidak cocok untuk "nama satu produk"**
Contoh gaya jawaban: "Static itu miliknya bareng-bareng semua object, jadi cocok untuk hitungan seperti total objek atau total pendapatan yang memang harus terus bertambah dan dibagikan ke semua. Tapi kalau untuk nama satu produk, itu harus beda-beda tiap object, jadi kalau dibuat static malah semua object akan 'berebut' nilai yang sama dan jadi tertimpa terus."

**3. Contoh aplikasi lain yang menerapkan Polymorphism**
Contoh gaya jawaban: "Aplikasi dompet digital seperti DANA — tombol 'Bayar' yang sama bisa dipakai untuk bayar listrik, bayar pulsa, atau transfer, tapi proses di baliknya beda-beda tergantung jenis objek transaksinya. Ini mirip konsep polymorphism karena satu perintah (method) menghasilkan perilaku berbeda tergantung objeknya."

---

## ✅ Checklist Sebelum Mengumpulkan

- [ ] Semua nama class/property **beda** dari contoh di panduan ini maupun modul
- [ ] Semua kode sudah dites di onlinephp.io tanpa error
- [ ] Ada komentar penjelas di bagian penting (constructor, abstract, static, dll)
- [ ] Screenshot output untuk A1–A3 dan B1–B4 sudah lengkap
- [ ] Jawaban Bagian C ditulis dengan kalimat sendiri, bukan salinan
- [ ] Nama file sesuai format: `Nama_Kelas_TugasPBO.php`
