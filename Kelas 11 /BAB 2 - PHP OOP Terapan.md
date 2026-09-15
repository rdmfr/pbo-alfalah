# BAB 2 (LANJUTAN): PHP OOP TERAPAN — JEMBATAN MENUJU FRAMEWORK
### Kelas XI RPL/PPLG — Fase F

---

## Pendahuluan

Setelah kalian menguasai **Inheritance, Polymorphism, Abstract Class, Interface,** dan **Static**, kalian sudah punya "kosa kata" OOP yang lengkap. Tapi kosa kata saja tidak cukup untuk membuat aplikasi yang benar-benar bisa dipakai.

Bab ini adalah **jembatan**. Setelah bab ini selesai, kalian akan siap belajar Laravel di kelas XII — karena kalian sudah memahami *apa yang sebenarnya dikerjakan Laravel di balik layar*.

Urutan materi:

| No | Materi | Analogi Sederhana |
|----|--------|--------------------|
| 1 | Error & Exception Handling | Sabuk pengaman mobil |
| 2 | Namespace & Autoloading | Alamat rumah & nama lengkap |
| 3 | Koneksi Database Modern (PDO OOP) | Penerjemah antara kamu dan database |
| 4 | Arsitektur MVC | Restoran (Dapur, Pelayan, Meja Makan) |
| 5 | Mini Project Terpadu | Ujian praktik gabungan semua bab |

---

## 2.1 Error & Exception Handling

### Kenapa Materi Ini Penting?

Bayangkan kalian membuka aplikasi marketplace, lalu tiba-tiba muncul tulisan aneh berwarna merah penuh kode dan nama file server. Pasti bikin panik dan tidak percaya pada aplikasi itu, kan?

Itulah yang terjadi kalau PHP mengalami **Fatal Error** tanpa ditangani. Aplikasi yang profesional **tidak boleh** menunjukkan error mentah ke pengguna. Sebaliknya, ia harus menangkap error itu diam-diam dan menampilkan pesan yang sopan, seperti "Maaf, terjadi kesalahan. Silakan coba lagi."

### Analogi: Sabuk Pengaman

Try-Catch itu seperti sabuk pengaman di mobil.

- **Try** = kamu mengemudi (menjalankan kode) seperti biasa.
- **Throw** = terjadi tabrakan (error muncul).
- **Catch** = sabuk pengaman menahan kamu supaya tidak terlempar (aplikasi tidak crash).
- **Finally** = petugas yang selalu datang mengecek kondisi, entah kamu selamat atau tidak (kode yang **selalu** dijalankan, apapun hasilnya).

### Struktur Dasar

```php
<?php
// try = "coba jalankan kode ini"
try {
    // Kode yang berpotensi menghasilkan error diletakkan di sini
    $harga = -50000;

    if ($harga < 0) {
        // throw = "lemparkan" sebuah error secara sengaja
        // new Exception() membungkus pesan error menjadi sebuah objek
        throw new Exception("Harga produk tidak boleh minus!");
    }

    echo "Produk berhasil disimpan dengan harga Rp" . $harga;

} catch (Exception $e) {
    // catch = "tangkap" error yang dilempar oleh blok try
    // $e adalah objek Exception, punya method getMessage()
    echo "Terjadi kesalahan: " . $e->getMessage();

} finally {
    // finally = kode ini SELALU dijalankan
    // baik try berhasil maupun terjadi error
    echo "\nProses validasi produk selesai diperiksa.";
}
```

**Output jika dijalankan:**
```
Terjadi kesalahan: Harga produk tidak boleh minus!
Proses validasi produk selesai diperiksa.
```

### Studi Kasus: Validasi Input Produk

```php
<?php
class Produk {
    private string $nama;
    private float $harga;

    public function __construct(string $nama, float $harga) {
        // Validasi dilakukan di dalam constructor
        if (empty($nama)) {
            throw new Exception("Nama produk tidak boleh kosong.");
        }
        if ($harga < 0) {
            throw new Exception("Harga produk tidak boleh minus.");
        }

        $this->nama = $nama;
        $this->harga = $harga;
    }

    public function tampilkanInfo(): string {
        return "Produk: {$this->nama}, Harga: Rp" . number_format($this->harga, 0, ',', '.');
    }
}

// Mencoba membuat beberapa produk, termasuk yang tidak valid
$daftarInput = [
    ["Keyboard Mekanik", 350000],
    ["Mouse Wireless", -75000],   // data ini sengaja salah
    ["", 100000],                 // data ini sengaja salah
];

foreach ($daftarInput as $input) {
    try {
        $produk = new Produk($input[0], $input[1]);
        echo $produk->tampilkanInfo() . "\n";
    } catch (Exception $e) {
        echo "[GAGAL] " . $e->getMessage() . "\n";
    }
}
```

**Output:**
```
Produk: Keyboard Mekanik, Harga: Rp350.000
[GAGAL] Harga produk tidak boleh minus.
[GAGAL] Nama produk tidak boleh kosong.
```

> **Catatan Guru:** Perhatikan bahwa program **tidak berhenti (crash)** meski ada 2 data salah. `foreach` tetap lanjut memproses produk berikutnya karena error ditangkap satu per satu di dalam `try-catch`.

### Latihan Mandiri
1. Buat class `Kasir` dengan method `bayar(float $totalBelanja, float $uangDibayar)`.
2. Lempar `Exception` jika `$uangDibayar` kurang dari `$totalBelanja`, dengan pesan "Uang tidak cukup!".
3. Tangkap error tersebut dan tampilkan pesan yang ramah kepada pengguna.

---

## 2.2 Namespace & Autoloading

### Kenapa Materi Ini Penting?

Bayangkan aplikasi kalian sudah punya 30 file Class: `Produk.php`, `Kategori.php`, `Kasir.php`, dan seterusnya. Setiap kali butuh salah satunya, kalian harus menulis:

```php
require_once 'Produk.php';
require_once 'Kategori.php';
require_once 'Kasir.php';
// ...dan 27 baris require lainnya
```

Selain melelahkan, ini juga rawan error: lupa satu `require`, urutan salah, atau bahkan dua class kebetulan punya nama yang sama (misalnya ada `Produk` versi kamu dan `Produk` dari library orang lain).

### Analogi: Alamat Rumah

Bayangkan ada dua orang bernama "Budi" di kelas yang sama. Untuk membedakan, kita perlu alamat lengkap: "Budi dari Jakarta" dan "Budi dari Surabaya".

**Namespace** bekerja persis seperti itu — ia memberi "alamat" pada setiap Class, sehingga `App\Models\Produk` jelas berbeda dari `App\Http\Produk`, walau nama classnya sama-sama `Produk`.

**Autoloading** pula seperti asisten pribadi yang otomatis mengambilkan buku yang kamu perlukan dari rak perpustakaan, tanpa kamu harus mengambilnya satu-satu sendiri.

### Contoh Namespace

**File: `Models/Produk.php`**
```php
<?php
// namespace = "alamat" folder/grup class ini
namespace App\Models;

class Produk {
    public function info(): string {
        return "Ini Produk dari Model";
    }
}
```

**File: `index.php`**
```php
<?php
// use = "panggil" class dari alamat tertentu
use App\Models\Produk;

require_once 'Models/Produk.php';

$produk = new Produk();
echo $produk->info(); // Ini Produk dari Model
```

### Autoloading dengan `spl_autoload_register()`

Daripada menulis banyak `require_once`, kita bisa membuat **satu fungsi** yang otomatis mencari file class begitu class itu dipanggil.

```php
<?php
// Fungsi ini didaftarkan untuk "mendengarkan" setiap kali
// ada class baru yang belum di-load
spl_autoload_register(function ($namaClass) {
    // Ubah namespace App\Models\Produk menjadi path App/Models/Produk.php
    $path = str_replace('\\', '/', $namaClass) . '.php';

    if (file_exists($path)) {
        require_once $path;
    }
});

// Tidak perlu require_once manual lagi!
use App\Models\Produk;

$produk = new Produk();
echo $produk->info();
```

Begitu `new Produk()` dipanggil, PHP otomatis menjalankan fungsi autoload, mencari file `App/Models/Produk.php`, dan memuatnya sendiri.

### Pengayaan: Composer

Di dunia kerja nyata, programmer jarang menulis `spl_autoload_register()` manual. Mereka memakai **Composer**, dependency manager PHP yang juga menyediakan autoloading otomatis lewat file `vendor/autoload.php`.

```php
<?php
require 'vendor/autoload.php'; // satu baris ini menggantikan semua require manual

use App\Models\Produk;

$produk = new Produk();
```

> Inilah kenapa nanti di Laravel kalian tidak akan pernah menulis `require_once` untuk memanggil Class — semuanya sudah diurus Composer secara otomatis.

---

## 2.3 Koneksi Database Modern (PDO OOP)

### Kenapa Materi Ini Penting?

Selama ini data produk kalian hanya tersimpan sementara di `array` — begitu program berhenti, data hilang. Untuk aplikasi sungguhan, data harus tersimpan **permanen** di database.

Dulu programmer memakai `mysql_query()` (sudah tidak didukung PHP modern) atau `mysqli` versi prosedural. Sekarang standar industri adalah **PDO (PHP Data Objects)** — cara OOP untuk berbicara dengan database.

### Analogi: Penerjemah

PDO seperti seorang **penerjemah profesional**. Kamu (PHP) tidak perlu tahu bahasa asli si database (MySQL, PostgreSQL, SQLite, dll). Kamu cukup berbicara dengan PDO menggunakan cara yang sama, dan PDO yang menerjemahkannya ke database apa pun yang kamu pakai.

### Membuat Koneksi

```php
<?php
class Koneksi {
    private static ?PDO $koneksi = null;

    // static agar koneksi dibuat sekali saja untuk seluruh aplikasi
    public static function getKoneksi(): PDO {
        if (self::$koneksi === null) {
            try {
                $dsn = "mysql:host=localhost;dbname=toko_db;charset=utf8mb4";
                self::$koneksi = new PDO($dsn, "root", "");
                // Membuat PDO melempar Exception jika query gagal
                self::$koneksi->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
            } catch (PDOException $e) {
                throw new Exception("Koneksi database gagal: " . $e->getMessage());
            }
        }
        return self::$koneksi;
    }
}
```

### CRUD dengan PDO (Create, Read, Update, Delete)

```php
<?php
class ProdukModel {
    private PDO $db;

    public function __construct() {
        $this->db = Koneksi::getKoneksi();
    }

    // CREATE — menyimpan produk baru
    public function tambah(string $nama, float $harga): bool {
        // Tanda ? adalah "placeholder" — mencegah SQL Injection
        $stmt = $this->db->prepare("INSERT INTO produk (nama, harga) VALUES (?, ?)");
        return $stmt->execute([$nama, $harga]);
    }

    // READ — mengambil semua produk
    public function ambilSemua(): array {
        $stmt = $this->db->query("SELECT * FROM produk");
        return $stmt->fetchAll(PDO::FETCH_ASSOC);
    }

    // UPDATE — mengubah data produk
    public function update(int $id, float $hargaBaru): bool {
        $stmt = $this->db->prepare("UPDATE produk SET harga = ? WHERE id = ?");
        return $stmt->execute([$hargaBaru, $id]);
    }

    // DELETE — menghapus produk
    public function hapus(int $id): bool {
        $stmt = $this->db->prepare("DELETE FROM produk WHERE id = ?");
        return $stmt->execute([$id]);
    }
}

// Penggunaan
try {
    $model = new ProdukModel();
    $model->tambah("Headset Gaming", 250000);

    $semuaProduk = $model->ambilSemua();
    foreach ($semuaProduk as $p) {
        echo $p['nama'] . " - Rp" . number_format($p['harga'], 0, ',', '.') . "\n";
    }
} catch (Exception $e) {
    echo "Terjadi kesalahan: " . $e->getMessage();
}
```

> **Poin Penting:** Perhatikan penggunaan `?` (prepared statement) alih-alih menaruh variabel langsung ke dalam query SQL. Ini adalah kebiasaan **wajib** untuk mencegah serangan **SQL Injection** — topik keamanan dasar yang harus dipahami sejak sekarang.

### Latihan Mandiri
1. Buat tabel `kategori` dengan kolom `id` dan `nama_kategori`.
2. Buat class `KategoriModel` dengan method `tambah()`, `ambilSemua()`, dan `hapus()` mengikuti pola `ProdukModel` di atas.

---

## 2.4 Pengenalan Arsitektur MVC (Model-View-Controller)

### Kenapa Materi Ini Penting?

Ini adalah **gerbang paling krusial** di kelas XI. Tanpa MVC, semua kode — HTML, query database, dan logika — akan tercampur dalam satu file besar yang berantakan dan sulit diperbaiki. Begitu kalian memahami MVC secara native (tanpa framework), belajar Laravel di kelas XII akan terasa jauh lebih mudah karena Laravel pun dibangun di atas konsep yang sama persis.

### Analogi: Restoran

Bayangkan sebuah restoran yang berjalan dengan baik:

| Bagian Restoran | Komponen MVC | Tugasnya |
|---|---|---|
| **Dapur** (koki mengolah bahan mentah) | **Model** | Mengurus data — mengambil, menyimpan, mengubah data dari database |
| **Meja Makan** (piring cantik yang dilihat pelanggan) | **View** | Tampilan — HTML murni yang dilihat pengguna, tanpa logika rumit |
| **Pelayan** (penghubung dapur dan meja) | **Controller** | Menerima permintaan pelanggan, meminta dapur (Model) menyiapkan data, lalu membawanya ke meja (View) |

Pelanggan (pengguna) **tidak pernah masuk ke dapur**. Mereka hanya berbicara dengan pelayan, dan menerima makanan di meja. Begitu pula pengguna aplikasi — mereka tidak pernah menyentuh query database secara langsung; semua lewat Controller.

### Struktur Folder Sederhana

```
project/
├── Models/
│   └── ProdukModel.php
├── Views/
│   └── produk_list.php
├── Controllers/
│   └── ProdukController.php
└── index.php
```

### Model — Urusan Database

```php
<?php
// Models/ProdukModel.php
namespace App\Models;
use PDO;

class ProdukModel {
    private PDO $db;

    public function __construct(PDO $koneksi) {
        $this->db = $koneksi;
    }

    public function ambilSemua(): array {
        $stmt = $this->db->query("SELECT * FROM produk");
        return $stmt->fetchAll(PDO::FETCH_ASSOC);
    }
}
```

### View — Tampilan Murni

```php
<!-- Views/produk_list.php -->
<!-- Perhatikan: file ini HANYA berisi HTML dan variabel, TIDAK ADA query database -->
<!DOCTYPE html>
<html>
<head><title>Daftar Produk</title></head>
<body>
    <h1>Daftar Produk</h1>
    <ul>
        <?php foreach ($daftarProduk as $produk): ?>
            <li><?= htmlspecialchars($produk['nama']) ?> - Rp<?= number_format($produk['harga'], 0, ',', '.') ?></li>
        <?php endforeach; ?>
    </ul>
</body>
</html>
```

### Controller — Penghubung Logika

```php
<?php
// Controllers/ProdukController.php
namespace App\Controllers;
use App\Models\ProdukModel;

class ProdukController {
    private ProdukModel $model;

    public function __construct(ProdukModel $model) {
        $this->model = $model;
    }

    // index() = tugas pelayan: minta data ke dapur, bawa ke meja
    public function index(): void {
        $daftarProduk = $this->model->ambilSemua(); // minta data ke Model
        require '../Views/produk_list.php';          // kirim data ke View
    }
}
```

### index.php — Titik Masuk Aplikasi

```php
<?php
// index.php
require '../vendor/autoload.php'; // autoloading, lihat materi 2.2

use App\Models\ProdukModel;
use App\Controllers\ProdukController;

$koneksi = Koneksi::getKoneksi();           // dari materi 2.3
$model = new ProdukModel($koneksi);
$controller = new ProdukController($model);

$controller->index(); // menjalankan alur: Controller -> Model -> View
```

### Alur Kerja MVC

```
Pengguna buka index.php
        │
        ▼
   Controller menerima permintaan
        │
        ▼
   Controller memanggil Model
        │
        ▼
   Model mengambil data dari Database (PDO)
        │
        ▼
   Model mengembalikan data ke Controller
        │
        ▼
   Controller mengirim data ke View
        │
        ▼
   View menampilkan HTML ke Pengguna
```

> **Catatan Guru:** Tekankan pada siswa bahwa struktur folder di atas adalah versi **native/manual**. Saat belajar Laravel, folder ini sudah otomatis tersedia sebagai `app/Models`, `resources/views`, dan `app/Http/Controllers` — dengan konsep yang persis sama.

---

## 2.5 Mini Project Terpadu (Assessment Akhir Bab)

### Tugas Praktik: Aplikasi "Manajemen Data Produk / Kasir Sederhana"

Siswa membangun aplikasi CRUD produk sederhana yang menggabungkan **seluruh materi Bab 2**, baik dari materi inti maupun materi lanjutan ini.

### Syarat Wajib

| No | Syarat | Materi Terkait |
|----|--------|-----------------|
| 1 | Minimal 2 Class dengan relasi **Inheritance** (contoh: `Barang` → `Produk`, `ProdukDiskon`) | Bab 2 Inti |
| 2 | Struktur folder **MVC** (Model, View, Controller) | 2.4 |
| 3 | Koneksi ke database MySQL menggunakan **PDO** | 2.3 |
| 4 | Semua input divalidasi dengan **Try-Catch** (harga tidak boleh minus, nama tidak boleh kosong) | 2.1 |
| 5 | Class diatur menggunakan **Namespace**, dipanggil lewat **Autoloading** | 2.2 |
| 6 | Fitur CRUD lengkap: tambah, lihat, ubah, hapus data produk | 2.3 & 2.4 |

### Rubrik Penilaian

| Aspek | Bobot | Kriteria Nilai Maksimal |
|---|---|---|
| Struktur MVC | 25% | Model, View, Controller terpisah rapi, tidak ada query di dalam View |
| Penerapan OOP (Inheritance) | 20% | Ada relasi turunan class yang logis dan digunakan secara nyata |
| Koneksi Database (PDO) | 20% | CRUD berjalan penuh, memakai prepared statement (`?`) |
| Error Handling | 20% | Semua input tervalidasi, tidak ada Fatal Error yang tampil ke pengguna |
| Namespace & Autoloading | 15% | Tidak ada `require_once` manual berulang, namespace tertata benar |

### Contoh Kerangka Awal (Starter)

```php
<?php
// Models/Barang.php
namespace App\Models;

// Class induk - berisi sifat umum semua barang
class Barang {
    protected string $nama;
    protected float $harga;

    public function __construct(string $nama, float $harga) {
        if (empty($nama)) {
            throw new \Exception("Nama barang tidak boleh kosong.");
        }
        if ($harga < 0) {
            throw new \Exception("Harga barang tidak boleh minus.");
        }
        $this->nama = $nama;
        $this->harga = $harga;
    }

    public function getInfo(): string {
        return "{$this->nama} - Rp" . number_format($this->harga, 0, ',', '.');
    }
}
```

```php
<?php
// Models/ProdukDiskon.php
namespace App\Models;

// Class turunan - mewarisi Barang, menambah sifat khusus diskon
class ProdukDiskon extends Barang {
    private float $persenDiskon;

    public function __construct(string $nama, float $harga, float $persenDiskon) {
        parent::__construct($nama, $harga); // memanggil validasi dari induk
        $this->persenDiskon = $persenDiskon;
    }

    // Override method induk - menambahkan info diskon
    public function getInfo(): string {
        $hargaSetelahDiskon = $this->harga - ($this->harga * $this->persenDiskon / 100);
        return parent::getInfo() . " (Diskon {$this->persenDiskon}% -> Rp" .
               number_format($hargaSetelahDiskon, 0, ',', '.') . ")";
    }
}
```

Siswa melanjutkan kerangka ini dengan membuat `ProdukModel` (PDO), `ProdukController`, dan `View` sesuai pola pada materi 2.3 dan 2.4.

---

## Ringkasan Bab 2 Lanjutan

```
Try-Catch          -> Aplikasi tidak boleh "meledak" di depan pengguna
Namespace/Autoload -> Class yang rapi dan mudah dipanggil tanpa require manual
PDO OOP             -> Data tersimpan permanen & aman dari SQL Injection
MVC                 -> Kode terpisah rapi: Data (Model), Tampilan (View), Logika (Controller)
Mini Project        -> Semua konsep di atas digabung jadi satu aplikasi nyata
```

Setelah menguntaskan bab ini, siswa telah membangun aplikasi PHP native yang terstruktur selayaknya aplikasi profesional — bekal utama sebelum masuk ke Laravel di kelas XII.
