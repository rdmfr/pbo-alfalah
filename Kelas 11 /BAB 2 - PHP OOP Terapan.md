# BAB 2 (LANJUTAN): PHP OOP TERAPAN - JEMBATAN MENUJU FRAMEWORK

**Mata Pelajaran:** Pemrograman Berorientasi Objek (Informatika)
**Kurikulum:** Merdeka
**Kelas / Fase:** XI RPL/PPLG - Fase F
**Prasyarat:** Sudah paham Class, Object, Inheritance, Polymorphism, Abstract Class, Interface, dan Static (Bab 2 bagian awal)

---

## Tujuan Pembelajaran

Setelah menyelesaikan bab ini, kalian diharapkan mampu:

1. Menjelaskan alasan aplikasi butuh Try-Catch dan menerapkannya untuk mencegah program berhenti mendadak (crash).
2. Menjelaskan fungsi Namespace dalam mengorganisir banyak Class agar tidak bentrok nama.
3. Membuat koneksi database menggunakan PDO (PHP Data Objects) secara aman (anti SQL Injection).
4. Menjelaskan dan menerapkan pola arsitektur MVC (Model-View-Controller).
5. Menggabungkan seluruh konsep (Inheritance, Try-Catch, PDO, MVC) dalam satu Mini Project CRUD.

---

## Pendahuluan

Setelah kalian menguasai Inheritance, Polymorphism, Abstract Class, Interface, dan Static, kalian sudah punya "kosa kata" OOP yang lengkap. Tapi kosa kata saja tidak cukup untuk membuat aplikasi yang benar-benar bisa dipakai orang banyak.

Bab ini adalah jembatan. Setelah bab ini selesai, kalian akan siap belajar framework seperti Laravel di kelas XII, karena kalian sudah memahami apa yang sebenarnya dikerjakan Laravel di balik layar. Anggap saja: kalau Laravel itu mobil matic yang serba otomatis, bab ini mengajarkan kalian cara kerja mesin mobil manual-nya dulu. Supaya nanti waktu pakai yang otomatis, kalian tahu apa yang sedang terjadi, bukan cuma asal pakai.

### Peta Materi

| No | Materi | Analogi Sederhana | Bisa dites di onlinephp.io? |
|---|---|---|---|
| 1 | Error & Exception Handling | Sabuk pengaman mobil | Bisa |
| 2 | Namespace & Autoloading | Alamat rumah & nama lengkap | Bisa (disimulasikan) |
| 3 | Koneksi Database Modern (PDO OOP) | Penerjemah antara kamu dan database | Tidak, butuh XAMPP/Laragon |
| 4 | Arsitektur MVC | Restoran (Dapur, Pelayan, Meja Makan) | Tidak, butuh XAMPP/Laragon |
| 5 | Mini Project Terpadu | Ujian praktik gabungan semua bab | Tidak, butuh XAMPP/Laragon |

Catatan cara pakai modul: setiap sub-bab punya urutan tetap: Kenapa penting - Analogi - Kode - Penjelasan baris per baris - Kesalahan umum - Latihan Praktik - Cek Pemahaman. Ikuti urutan ini supaya tidak ada bagian yang terlewat.

---

## 1. Error & Exception Handling (Try-Catch)

### Kenapa Materi Ini Penting?

Bayangkan kalian membuka aplikasi marketplace, lalu tiba-tiba muncul tulisan aneh berwarna merah penuh kode dan nama file server (contoh: "Fatal error: Uncaught Exception in /var/www/index.php on line 42"). Pasti bikin panik, kan? Aplikasi yang profesional tidak boleh menunjukkan error mentah seperti itu ke pengguna. Aplikasi harus menangkap error itu diam-diam lalu menampilkan pesan yang sopan, misalnya "Maaf, terjadi kesalahan. Silakan coba lagi."

### Analogi: Sabuk Pengaman Mobil

| Istilah PHP | Analogi Mobil | Artinya |
|---|---|---|
| try | Kamu mengemudi seperti biasa | Blok kode yang dicoba dijalankan |
| throw | Terjadi tabrakan (error muncul) | Perintah untuk membuat sebuah error secara sengaja |
| catch | Sabuk pengaman menahanmu | Blok kode yang menangkap error supaya program tidak crash |
| finally | Lampu hazard tetap menyala, tabrakan atau tidak | Blok kode yang selalu dijalankan, apapun hasilnya (sukses atau gagal) |

Supaya tidak ambigu: throw bukan bagian yang kalian tulis di luar try. throw biasanya ada di dalam class atau fungsi yang kalian panggil (lihat method __construct di kode bawah). try-catch ada di tempat lain, yaitu di kode yang memanggil class/fungsi tersebut.

### Praktik Kode: Validasi Input Produk

Bisa dites di onlinephp.io. Buka onlinephp.io, hapus semua kode yang ada di layar, salin kode di bawah ini, lalu klik tombol "Execute" atau "Run".

```php
<?php
class Produk {
    private string $nama;
    private float $harga;

    public function __construct(string $nama, float $harga) {
        // Validasi dilakukan di dalam constructor, sebelum data disimpan ke properti.
        // Kalau data tidak masuk akal, kita "throw" (lempar) sebuah Exception
        // supaya objek yang salah ini tidak pernah selesai dibuat.
        if (empty($nama)) {
            throw new Exception("Nama produk tidak boleh kosong.");
        }
        if ($harga < 0) {
            throw new Exception("Harga produk tidak boleh minus.");
        }

        // Baris ini hanya akan dijalankan jika kedua validasi di atas lolos,
        // karena "throw" langsung menghentikan eksekusi constructor.
        $this->nama = $nama;
        $this->harga = $harga;
    }

    public function tampilkanInfo(): string {
        // number_format() dipakai supaya angka harga tampil rapi, misalnya
        // 350000 menjadi "350.000" (pakai titik sebagai pemisah ribuan).
        return "Produk: {$this->nama}, Harga: Rp" . number_format($this->harga, 0, ',', '.');
    }
}

// Mencoba membuat beberapa produk, termasuk yang sengaja dibuat salah,
// supaya kita bisa melihat try-catch bekerja pada data yang bermasalah.
$daftarInput = [
    ["Keyboard Mekanik", 350000],
    ["Mouse Wireless", -75000],   // data ini sengaja salah (harga minus)
    ["", 100000],                 // data ini sengaja salah (nama kosong)
];

// Kita proses pakai try-catch agar program tidak mati di tengah jalan
// ketika salah satu data ternyata tidak valid.
foreach ($daftarInput as $input) {
    try {
        $produk = new Produk($input[0], $input[1]);
        echo "BERHASIL: " . $produk->tampilkanInfo() . "\n";
    } catch (Exception $e) {
        echo "GAGAL: " . $e->getMessage() . "\n";
    } finally {
        echo "   (data ini selesai diproses)\n";
    }
}
```

### Penjelasan Baris per Baris

- `throw new Exception("...")` membuat "amplop error" baru berisi pesan, lalu langsung dikirim ke atas, yaitu ke kode yang memanggil `new Produk(...)`. Begitu baris ini dijalankan, semua kode setelahnya di dalam constructor langsung diabaikan.
- `foreach ($daftarInput as $input)` kita punya tiga data uji coba. Loop ini mencoba membuat objek Produk untuk setiap data, satu per satu, secara berurutan.
- `try { ... }` bagian yang "dicoba". Kalau di dalamnya ada `throw`, PHP langsung lompat ke `catch`, tanpa menjalankan sisa kode di dalam `try`. Contohnya, baris `echo "BERHASIL: ..."` tidak akan pernah tercetak untuk data yang gagal.
- `catch (Exception $e)` menangkap error apapun yang dilempar. Variabel `$e` menyimpan objek Exception, dan `$e->getMessage()` mengambil isi pesan yang tadi kita tulis di `throw`.
- `finally { ... }` baris ini selalu tercetak, baik data itu berhasil maupun gagal. Cocok dipakai misalnya untuk menutup koneksi file/database supaya tidak "nyangkut" terbuka, apapun hasil prosesnya.

### Kesalahan Umum yang Sering Terjadi

1. Menaruh `try` di dalam `__construct`, bukan di luar. Yang benar: `throw` di dalam class, `try-catch` di kode yang memanggil class-nya.
2. Lupa `Exception`, cuma menulis `throw "pesan error"`. Di PHP, `throw` wajib melempar objek (misalnya `new Exception(...)`), bukan teks biasa.
3. Berpikir `finally` hanya jalan kalau sukses. Padahal `finally` jalan selalu, mau sukses ataupun masuk ke `catch`.

### Latihan Praktik

Kerjakan langsung di onlinephp.io, berdasarkan kode Produk di atas.

1. Tambahkan class `Produk` versi kalian sendiri dengan aturan validasi baru: harga maksimal adalah 10.000.000. Kalau melebihi itu, lempar Exception dengan pesan "Harga produk melebihi batas maksimal."
2. Buat array `$daftarInput` baru berisi lima data, dengan tiga data valid dan dua data sengaja salah (salah satunya melanggar aturan baru di soal nomor 1).
3. Tambahkan penghitung sederhana menggunakan dua variabel, misalnya `$jumlahBerhasil` dan `$jumlahGagal`, yang bertambah nilainya di dalam blok `try` dan `catch` masing-masing. Cetak kedua variabel itu setelah loop `foreach` selesai.
4. Tantangan tambahan: ubah `catch (Exception $e)` menjadi dua blok catch berurutan, satu untuk `TypeError` dan satu untuk `Exception`, lalu coba jelaskan pada diri sendiri kapan `TypeError` bisa muncul pada kode ini.

### Cek Pemahaman

1. Apa yang terjadi jika baris di dalam `try` menghasilkan error tapi kalian lupa menulis blok `catch`?
2. Kalau `$harga` yang dimasukkan adalah 0 (nol), apakah program akan menganggapnya error? Kenapa?
3. Tuliskan satu skenario nyata (bukan dari contoh di atas) di mana `finally` berguna.

---

## 2. Namespace & Autoloading

### Kenapa Materi Ini Penting?

Bayangkan aplikasi kalian sudah punya 30 file Class. Setiap kali butuh salah satunya, kalian harus menulis `require_once '...';` berulang-ulang secara manual. Selain melelahkan, cara ini rawan error dan rawan bentrok nama class, misalnya kalian sudah punya `class Produk` untuk data, lalu tanpa sengaja membuat `class Produk` lagi untuk keperluan lain. PHP akan bingung dan menghasilkan error fatal.

### Analogi: Alamat Rumah

Bayangkan ada dua orang bernama Budi di Indonesia. Supaya surat tidak tertukar, kita tidak cukup menulis "Budi" saja di amplop, kita tulis alamat lengkap: "Budi, Jl. Mawar No. 5, Jakarta" dan "Budi, Jl. Melati No. 3, Surabaya".

| Istilah PHP | Analogi | Artinya |
|---|---|---|
| namespace App\Models | Alamat "Jl. Mawar No. 5, Jakarta" | "Folder virtual" tempat class ini tinggal |
| class Produk | Nama "Budi" | Nama class, boleh sama dengan class lain asalkan alamatnya (namespace) beda |
| use App\Models\Produk as ProdukModel; | Menulis "Budi dari Jakarta, kita panggil dia Pak Budi" | Memanggil class dari alamat lengkapnya, lalu memberinya nama panggilan singkat (alias) |
| Autoloading | Kurir profesional yang otomatis tahu jalan ke setiap alamat | Sistem otomatis yang mencari dan memuat file class begitu class itu dipanggil, kalian tidak perlu menulis require manual lagi |

Supaya tidak ambigu: `use ... as ...` itu hanya nama panggilan di dalam satu file, bukan mengganti nama class yang sebenarnya. `App\Models\Produk` tetap punya nama asli Produk, kita cuma memberi julukan ProdukModel supaya tidak tertukar dengan `App\Controllers\Produk` di file yang sama.

### Praktik Kode: Simulasi Namespace

Bisa dites di onlinephp.io. Karena onlinephp.io hanya punya satu file, kita akan mensimulasikan "beda folder" menggunakan blok kurung kurawal `{ }`. Di project sungguhan nanti, setiap namespace ada di file terpisah, bukan dalam satu file seperti ini. Salin dan Execute kode di bawah.

```php
<?php
// SIMULASI FOLDER 1: Folder Models.
// Semua class di dalam blok ini "beralamat" di App\Models.
namespace App\Models {
    class Produk {
        public function info() {
            return "Ini data Produk dari bagian Model (Database).";
        }
    }
}

// SIMULASI FOLDER 2: Folder Controllers.
// Class Produk di sini BOLEH punya nama sama dengan yang di atas,
// karena alamat (namespace) keduanya berbeda.
namespace App\Controllers {
    class Produk {
        public function info() {
            return "Ini alur Produk dari bagian Controller (Logika).";
        }
    }
}

// FOLDER UTAMA (mewakili file index.php).
// Blok namespace kosong ini mewakili kode yang "tidak beralamat khusus",
// seperti file index.php di root project.
namespace {
    // Kita panggil kedua class yang namanya sama-sama "Produk".
    // Tapi karena namespace-nya beda, PHP tidak bingung, dan kita
    // memberi julukan singkat lewat "as" supaya mudah dipanggil.
    use App\Models\Produk as ProdukModel;
    use App\Controllers\Produk as ProdukController;

    $produkDariModel = new ProdukModel();
    $produkDariController = new ProdukController();

    echo $produkDariModel->info() . "\n";
    echo $produkDariController->info() . "\n";
}
```

### Penjelasan Baris per Baris

- `namespace App\Models { ... }` semua class di dalam blok ini "beralamat" di `App\Models`. Tanda `\` di sini seperti tanda `/` pada alamat folder komputer (`App/Models`).
- `use App\Models\Produk as ProdukModel;` artinya, ambil class Produk yang beralamat di App\Models, lalu di file ini panggil dia ProdukModel.
- `new ProdukModel();` karena sudah diberi alias di atas, di sini kita cukup pakai nama pendeknya, bukan nama lengkap `App\Models\Produk`.
- Dua baris `echo` terakhir memanggil method `info()` dari masing-masing objek. Meskipun keduanya sama-sama bernama asli "Produk", hasil cetaknya berbeda karena isi method di tiap namespace berbeda.

Catatan guru: di dunia nyata (dan di Laravel nanti), kita menggunakan fitur Composer dengan aturan bernama PSR-4, di mana struktur namespace (`App\Models\...`) harus cocok persis dengan struktur folder fisik (`app/Models/...`). Setelah itu, Autoloading akan mencari file secara otomatis begitu class-nya dipanggil, sehingga kalian tidak perlu menulis require sama sekali.

### Kesalahan Umum yang Sering Terjadi

1. Menganggap namespace mengubah isi/fungsi class. Padahal namespace hanya soal "alamat", bukan soal perilaku class.
2. Lupa `use`, lalu memanggil `new Produk()` langsung di dalam blok `namespace { }` paling bawah. PHP akan bingung, karena ada dua class Produk. Solusinya wajib pakai `use ... as ...` atau menuliskan nama lengkap seperti `new \App\Models\Produk()`.

### Latihan Praktik

Kerjakan langsung di onlinephp.io, berdasarkan kode simulasi namespace di atas.

1. Tambahkan namespace ketiga bernama `App\Repositories` dengan class `Produk` yang isinya berbeda lagi, misalnya method `info()` mengembalikan teks "Ini Produk dari bagian Repository (penyimpanan sementara)."
2. Di blok `namespace { }` paling bawah, tambahkan `use` dan alias baru untuk class dari `App\Repositories`, lalu buat objeknya dan cetak hasil `info()`-nya, sehingga total ada tiga objek Produk dari tiga alamat berbeda.
3. Coba hapus salah satu baris `use ... as ...` lalu ganti pemanggilannya dengan nama lengkap, misalnya `new \App\Controllers\Produk()`. Amati bahwa hasilnya tetap sama, untuk membuktikan bahwa alias hanyalah "jalan pintas" penulisan.
4. Tantangan tambahan: buat class baru bernama `Kategori` di namespace `App\Models` dan `App\Controllers` sekaligus, lalu panggil keduanya dengan alias berbeda dalam satu file, seperti pada contoh Produk.

### Cek Pemahaman

1. Kalau dua class punya nama sama tapi namespace-nya sama juga, apa yang terjadi?
2. Apa bedanya `use` di PHP namespace dengan `use App\Models\Produk;` tanpa `as`?

---

## 3. Koneksi Database Modern (PDO OOP)

### Kenapa Materi Ini Penting?

Selama ini data kita hilang setiap kali aplikasi ditutup, karena hanya disimpan di variabel/array biasa. PDO (PHP Data Objects) adalah cara standar industri (berbasis OOP) untuk berbicara dengan database MySQL. PDO ibarat penerjemah profesional yang menjaga sistem kita dari serangan peretas seperti SQL Injection, yaitu teknik jahat di mana peretas "menyisipkan" perintah SQL berbahaya lewat form input biasa (misalnya kolom login).

Butuh XAMPP/Laragon. Kode di bawah ini tidak bisa dijalankan di onlinephp.io karena membutuhkan server database MySQL sungguhan. Kalian harus mencobanya di XAMPP/Laragon masing-masing, dengan database `toko_db` dan tabel `produk` (kolom `nama`, `harga`) sudah dibuat lebih dulu lewat phpMyAdmin.

### Analogi: Penerjemah dan Loket Anti-Sogok

Bayangkan database adalah kantor pemerintahan yang bahasanya berbeda dari bahasa PHP. PDO adalah penerjemah yang menjembatani percakapan kita dengan kantor itu. Untuk pertanyaan seperti "tolong simpan data ini", PDO tidak membiarkan data mentah dari pengguna langsung "dibisikkan" ke database, semua data harus lewat loket khusus (`?` sebagai placeholder) supaya tidak ada yang bisa menyelundupkan perintah jahat.

| Kode | Analogi | Artinya |
|---|---|---|
| private static ?PDO $koneksi = null; | Nomor antrean yang boleh kosong atau boleh sudah terisi | ?PDO artinya "boleh berisi objek PDO, atau boleh null (kosong)" |
| self::$koneksi === null | Petugas mengecek "apakah loket sudah dibuka?" | Mengecek apakah koneksi sudah pernah dibuat sebelumnya |
| ? di dalam query SQL | Loket resmi untuk menitipkan data | Placeholder, tempat aman untuk menaruh data dari pengguna, bukan ditulis langsung di teks SQL |
| $stmt->execute([$nama, $harga]) | Menitipkan data lewat loket sesuai urutan nomor | Data dikirim sesuai urutan ? yang ada di query |

Supaya tidak ambigu: `self::` dipakai untuk mengakses properti/method yang sifatnya static (milik class, bukan milik objek tertentu). Ini berbeda dari `$this->`, yang kalian pelajari sebelumnya untuk mengakses properti milik objek itu sendiri. Karena `$koneksi` di sini static, kita wajib pakai `self::`, bukan `$this->`.

### Praktik Kode

```php
<?php
class Koneksi {
    // "static" artinya properti ini dimiliki bersama oleh seluruh aplikasi,
    // bukan dibuat ulang setiap kali ada objek baru. Ini disebut pola
    // "Singleton": koneksi database cukup dibuat SEKALI saja, lalu dipakai
    // berulang-ulang tanpa membuka koneksi baru setiap saat.
    private static ?PDO $koneksi = null;

    public static function getKoneksi(): PDO {
        // Jika koneksi belum pernah dibuat (masih null), buat baru.
        // Jika sudah ada isinya, langsung pakai yang lama tanpa membuat ulang.
        if (self::$koneksi === null) {
            try {
                // $dsn (Data Source Name) adalah "alamat lengkap" database:
                // jenisnya (mysql), lokasi server (host), dan nama database (dbname).
                $dsn = "mysql:host=localhost;dbname=toko_db;charset=utf8mb4";
                self::$koneksi = new PDO($dsn, "root", "");

                // Baris ini memberitahu PDO: kalau ada error database,
                // jangan diam-diam saja, lempar Exception supaya bisa
                // ditangkap oleh try-catch di kode yang memanggilnya.
                self::$koneksi->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
            } catch (PDOException $e) {
                throw new Exception("Koneksi database gagal: " . $e->getMessage());
            }
        }
        return self::$koneksi;
    }
}

class ProdukModel {
    private PDO $db;

    public function __construct() {
        // Setiap kali ProdukModel dibuat, ia meminta koneksi yang sama
        // dari Koneksi::getKoneksi(), bukan membuat koneksi baru sendiri.
        $this->db = Koneksi::getKoneksi();
    }

    // CREATE - menyimpan produk baru dengan cara yang aman
    public function tambah(string $nama, float $harga): bool {
        // Tanda ? adalah "placeholder", mencegah serangan SQL Injection,
        // karena data pengguna tidak pernah ditulis langsung ke teks SQL.
        $stmt = $this->db->prepare("INSERT INTO produk (nama, harga) VALUES (?, ?)");

        // Data dikirim lewat array, urutannya harus sama dengan urutan
        // tanda ? di query: ? pertama diisi $nama, ? kedua diisi $harga.
        return $stmt->execute([$nama, $harga]);
    }
}
```

### Penjelasan Baris per Baris

- `$dsn` (Data Source Name) alamat lengkap database: jenisnya (`mysql`), lokasi server (`host=localhost`), dan nama database (`dbname=toko_db`).
- `PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION` memberitahu PDO, kalau ada error database, jangan diam-diam saja, lempar `Exception` supaya bisa ditangkap `try-catch`.
- `->prepare("... VALUES (?, ?)")` menyiapkan "kerangka" perintah SQL dengan dua loket kosong (`?`), tanpa langsung mengeksekusinya.
- `->execute([$nama, $harga])` mengisi loket-loket tadi sesuai urutan array, `?` pertama diisi `$nama`, `?` kedua diisi `$harga`, lalu perintah SQL benar-benar dijalankan.
- `Koneksi::getKoneksi()` dipanggil dengan tanda `::` bukan `->`, karena method ini `static`, artinya dipanggil langsung dari nama class, tanpa perlu membuat objek `Koneksi` terlebih dahulu.

### Kesalahan Umum yang Sering Terjadi

1. Menyambung data pengguna langsung ke teks SQL, misalnya `"... VALUES ('$nama', '$harga')"`. Ini membuka pintu SQL Injection dan harus dihindari, selalu pakai `?` dan `execute()`.
2. Urutan array di `execute()` tidak sesuai urutan `?` di query. Kalau query-nya `(nama, harga)` tapi array-nya `[$harga, $nama]`, data akan tertukar tempat.
3. Lupa membuat database/tabel di phpMyAdmin dulu sebelum menjalankan kode, PDO akan melempar Exception "koneksi gagal" kalau `toko_db` belum ada.

### Latihan Praktik

Kerjakan di XAMPP/Laragon, menggunakan database dan tabel yang sudah dibuat di phpMyAdmin.

1. Tambahkan method baru `ambilSemua()` di dalam `ProdukModel` yang menggunakan `$this->db->query("SELECT * FROM produk")` lalu mengembalikan hasilnya dengan `->fetchAll(PDO::FETCH_ASSOC)`. Tampilkan hasilnya menggunakan `print_r()`.
2. Tambahkan method `hapus(int $id)` yang memakai `prepare("DELETE FROM produk WHERE id = ?")` lalu `execute([$id])`. Bungkus pemanggilan method ini dengan try-catch di file terpisah, supaya kalau `$id` tidak ditemukan, program tetap tidak crash.
3. Buat file uji coba kecil (`test_koneksi.php`) yang hanya berisi pemanggilan `Koneksi::getKoneksi()` dua kali, lalu bandingkan dengan `var_dump()` apakah kedua hasil pemanggilan itu benar-benar objek PDO yang sama (petunjuk: gunakan `$koneksi1 === $koneksi2`).
4. Tantangan tambahan: tambahkan method `update(int $id, string $nama, float $harga)` menggunakan `prepare("UPDATE produk SET nama = ?, harga = ? WHERE id = ?")`, lalu perhatikan baik-baik urutan `?` dan urutan array di `execute()`.

### Cek Pemahaman

1. Kenapa `$koneksi` dibuat static, bukan properti biasa?
2. Apa fungsi tanda `?` di dalam query SQL pada kode di atas?

---

## 4. Pengenalan Arsitektur MVC (Model-View-Controller)

### Kenapa Materi Ini Penting?

Ini adalah gerbang paling krusial di kelas XI. Tanpa MVC, semua kode (HTML dan PHP Database) akan tercampur jadi satu file besar yang berantakan dan susah diperbaiki. Laravel, dan hampir semua framework PHP modern, dibangun di atas pola ini.

### Analogi: Restoran

| Bagian MVC | Analogi Restoran | Tugasnya |
|---|---|---|
| Model | Dapur | Mengurus data, ambil dari database lewat PDO, olah, lalu siapkan |
| View | Meja makan (tampilan untuk pelanggan) | HTML murni untuk menampilkan data ke pengguna, tidak boleh ada query database di sini |
| Controller | Pelayan | Menerima permintaan (request) dari pengguna, minta data ke dapur (Model), lalu antarkan ke meja makan (View) |

Alur permintaan (mohon dihafal urutannya, ini sering keliru):

```
Pengguna (buka browser)
      |
      v
1. index.php  (pintu masuk, menyalakan Controller)
      |
      v
2. Controller (Pelayan)  --->  3. Model (Dapur, ambil data)
      |                              |
      <-------- data dikirim balik --
      |
      v
4. View (Meja Makan, tampilkan data ke pengguna)
```

Supaya tidak ambigu: pengguna tidak pernah langsung berbicara ke Model atau View. Semua permintaan wajib lewat Controller dulu, persis seperti pelanggan restoran yang tidak boleh masuk ke dapur sendiri, harus lewat pelayan.

Butuh XAMPP/Laragon. Materi ini membutuhkan struktur folder sungguhan. Buat folder `project_mvc` di dalam `htdocs`, lalu buat struktur berikut:

```
project_mvc/
├── index.php
├── Models/
│   └── ProdukModel.php
└── Views/
    └── produk_list.php
```

**Langkah 1: Buat Dapur (Model)**

```php
<?php
// File: Models/ProdukModel.php
namespace App\Models;

class ProdukModel {
    // Anggap saja ini array yang nantinya diambil lewat PDO dari database.
    // Untuk latihan awal MVC, kita sengaja pakai data statis dulu supaya
    // fokus belajar alur MVC-nya, bukan koneksi database-nya.
    public function ambilSemua() {
        return [
            ['nama' => 'Buku Pemrograman', 'harga' => 85000],
            ['nama' => 'Mouse Wireless', 'harga' => 120000]
        ];
    }
}
```

**Langkah 2: Buat Meja Makan (View)**

```php
<!-- File: Views/produk_list.php -->
<!-- File ini murni HTML, tugasnya cuma menampilkan, bukan memikirkan query. -->
<!DOCTYPE html>
<html>
<body>
    <h1>Daftar Produk</h1>
    <ul>
        <?php foreach ($daftarProduk as $produk): ?>
            <li><?= $produk['nama'] ?> - Rp<?= number_format($produk['harga'], 0, ',', '.') ?></li>
        <?php endforeach; ?>
    </ul>
</body>
</html>
```

Dapur sudah siap, meja sudah ditata. Sekarang mari kita panggil pelayannya.

**Langkah 3: Buat Pelayan (Controller) dan Pintu Masuk (index.php)**

```php
<?php
// File: index.php (letakkan di luar folder Models/ dan Views/)
// Di dunia nyata pakai autoload Composer, untuk latihan kita require manual.
require_once 'Models/ProdukModel.php';

// CONTROLLER - Si Pelayan
class ProdukController {
    public function index() {
        $model = new \App\Models\ProdukModel();      // 1. Minta makanan ke dapur
        $daftarProduk = $model->ambilSemua();         // 2. Data diterima dari Model
        require 'Views/produk_list.php';              // 3. Antar ke meja makan.
                                                        //    Variabel $daftarProduk otomatis
                                                        //    "terlihat" oleh file View karena
                                                        //    dipanggil dengan require di sini.
    }
}

// 4. Pelanggan datang, Controller mulai bekerja.
$app = new ProdukController();
$app->index();
```

### Penjelasan Baris per Baris

- `require_once 'Models/ProdukModel.php';` memuat file Model satu kali saja, supaya class-nya bisa dipakai di `index.php`. Kalau tanpa baris ini, PHP tidak tahu class `ProdukModel` itu apa.
- `new \App\Models\ProdukModel();` perhatikan `\` di depan `App`. Ini artinya "mulai dari alamat paling atas", karena `index.php` sendiri tidak berada di dalam sebuah namespace.
- Kenapa `$daftarProduk` bisa "muncul" di file View padahal tidak dikirim lewat parameter fungsi? Karena `require 'Views/produk_list.php';` dipanggil di dalam method `index()`, semua variabel yang sudah ada di method itu (termasuk `$daftarProduk`) otomatis bisa diakses oleh file yang di-require. Ini salah satu bagian yang sering membingungkan siswa, sifat khusus dari `require`/`include` di PHP.
- Baris `$app = new ProdukController(); $app->index();` adalah titik awal seluruh alur, ibarat "pelanggan baru saja datang dan pelayan mulai bertugas".

### Kesalahan Umum yang Sering Terjadi

1. Menaruh query database langsung di file View. Ini melanggar prinsip MVC, View hanya boleh menampilkan, bukan mengambil data sendiri.
2. Lupa `require_once` Model sebelum dipakai di Controller, sehingga muncul error `Class "App\Models\ProdukModel" not found`.
3. Salah urutan alur, mencoba memanggil View duluan sebelum Model selesai mengambil data.

### Latihan Praktik

Kerjakan di XAMPP/Laragon, melanjutkan struktur folder `project_mvc` di atas.

1. Tambahkan produk ketiga dan keempat langsung di dalam array method `ambilSemua()`, lalu jalankan ulang `index.php` di browser untuk memastikan View otomatis menampilkan seluruh data baru tanpa mengubah kode View sama sekali.
2. Buat file View baru `Views/produk_kosong.php` yang menampilkan pesan "Belum ada produk" apabila `$daftarProduk` adalah array kosong. Ubah method `index()` di Controller supaya bisa memilih View mana yang dipanggil, tergantung apakah data kosong atau tidak.
3. Tambahkan method baru `cariBerdasarkanNama(string $kataKunci)` di `ProdukModel` yang memfilter array menggunakan `array_filter()`, lalu buat Controller dan View tambahan untuk menampilkan hasil pencarian.
4. Tantangan tambahan: ganti isi `ambilSemua()` supaya datanya diambil dari `ProdukModel` versi Bab sebelumnya yang memakai PDO (gabungkan dengan materi sub-bab 3), sehingga Model benar-benar mengambil data dari MySQL, bukan array statis lagi.

### Cek Pemahaman

1. Kalau ada bug di tampilan (misalnya harga tidak muncul), bagian mana (Model/View/Controller) yang pertama kali harus dicek?
2. Kenapa View tidak boleh berisi kode PDO/query database?

---

## 5. Mini Project Terpadu (Asesmen Akhir Bab)

### Tugas Praktik: Aplikasi "Manajemen Data Produk MVC"

Siswa/i membangun aplikasi CRUD (Create, Read, Update, Delete) sederhana yang menggabungkan seluruh materi bab ini dan bab sebelumnya.

Struktur folder yang disarankan:

```
mini_project/
├── index.php
├── Models/
│   ├── Koneksi.php
│   ├── Barang.php          <- class induk (Inheritance)
│   └── ProdukDiskon.php    <- class turunan (Inheritance + Polymorphism)
└── Views/
    ├── produk_list.php
    ├── produk_tambah.php
    └── produk_edit.php
```

Contoh kerangka awal untuk kebutuhan Inheritance & Polymorphism (silakan kembangkan sendiri, ini hanya titik awal):

```php
<?php
// File: Models/Barang.php
// Class induk (parent) yang menyimpan sifat dasar sebuah barang.
class Barang {
    protected string $nama;
    protected float $harga;

    public function __construct(string $nama, float $harga) {
        $this->nama = $nama;
        $this->harga = $harga;
    }

    // Method ini akan di-override (ditimpa) oleh class turunan,
    // sehingga hasilnya bisa berbeda tergantung jenis objeknya (Polymorphism).
    public function getHargaFinal(): float {
        return $this->harga;
    }
}
```

```php
<?php
// File: Models/ProdukDiskon.php
// Class turunan (child) dari Barang, mewarisi $nama dan $harga.
class ProdukDiskon extends Barang {
    private float $persenDiskon;

    public function __construct(string $nama, float $harga, float $persenDiskon) {
        // parent::__construct() memanggil constructor milik Barang terlebih
        // dahulu, supaya $nama dan $harga tetap terisi seperti biasa,
        // sebelum kita menambahkan properti baru khusus ProdukDiskon.
        parent::__construct($nama, $harga);
        $this->persenDiskon = $persenDiskon;
    }

    // Override method milik induk, inilah contoh Polymorphism: objek
    // Barang biasa dan objek ProdukDiskon sama-sama punya method
    // getHargaFinal(), tapi cara menghitungnya berbeda.
    public function getHargaFinal(): float {
        $potongan = $this->harga * ($this->persenDiskon / 100);
        return $this->harga - $potongan;
    }
}
```

### Penjelasan Baris per Baris

- `class ProdukDiskon extends Barang` menandakan `ProdukDiskon` mewarisi semua properti dan method milik `Barang`, termasuk `$nama`, `$harga`, dan `getHargaFinal()`, sebelum method itu ditimpa ulang di bawahnya.
- `parent::__construct($nama, $harga);` memastikan proses inisialisasi milik class induk tetap dijalankan, supaya kita tidak perlu menulis ulang `$this->nama = $nama;` dan `$this->harga = $harga;` di `ProdukDiskon`.
- Method `getHargaFinal()` di `ProdukDiskon` sengaja dituliskan ulang dengan isi berbeda dari milik `Barang`. Ketika kode lain memanggil `$barang->getHargaFinal()`, PHP otomatis menjalankan versi yang sesuai dengan jenis objek aslinya, inilah inti dari Polymorphism.

### Latihan Praktik Bertahap

Kerjakan satu per satu di XAMPP/Laragon, sebagai latihan sebelum menyelesaikan Mini Project penuh.

1. Lengkapi `Models/Koneksi.php` menggunakan pola Singleton seperti pada sub-bab 3, lalu uji koneksinya dengan file kecil terpisah sebelum dipakai di Model lain.
2. Buat class `BarangModel` yang memakai `Koneksi::getKoneksi()` untuk melakukan operasi Create dan Read ke tabel `produk`, memakai prepared statement seperti pada sub-bab 3.
3. Buat Controller `BarangController` dengan method `index()`, `tambah()`, `simpan()`, `edit()`, `update()`, dan `hapus()`. Setiap method yang berhubungan dengan database wajib dibungkus try-catch, supaya kalau ada input tidak valid (misalnya harga minus), aplikasi menampilkan pesan yang sopan alih-alih error mentah.
4. Setelah CRUD dasar berjalan, tambahkan class `ProdukDiskon` seperti contoh di atas, lalu tampilkan hasil `getHargaFinal()` di `Views/produk_list.php` untuk membuktikan bahwa harga barang biasa dan produk diskon dihitung dengan cara yang berbeda meski dipanggil dengan method yang sama.

### Checklist Penilaian (dipakai guru & siswa untuk cek kelengkapan)

| No | Kriteria | Sudah? |
|---|---|---|
| 1 | Folder terpisah Model / View / Controller (struktur MVC) | |
| 2 | Koneksi PDO memakai prepared statement (?), bukan query digabung manual | |
| 3 | Fitur Simpan (Create) berjalan dan tersimpan ke MySQL | |
| 4 | Fitur Ubah (Update) dan Hapus (Delete) berjalan | |
| 5 | Input harga minus ditangkap try-catch dan menampilkan pesan yang sopan | |
| 6 | Ada class Barang dan turunannya class ProdukDiskon (Inheritance) | |
| 7 | Method getHargaFinal() di ProdukDiskon benar-benar meng-override method induk (Polymorphism) | |

Selamat. Jika kalian berhasil menyelesaikan Mini Project ini, kalian sudah memiliki pondasi programming level industri. Sampai jumpa di materi Framework Laravel.

---

## Glosarium Istilah

| Istilah | Penjelasan Singkat |
|---|---|
| Exception | "Amplop" yang membawa informasi tentang error, bisa dilempar (throw) dan ditangkap (catch) |
| Namespace | "Alamat" virtual sebuah class supaya tidak bentrok dengan class bernama sama |
| Autoloading | Sistem otomatis yang memuat file class tanpa perlu require manual |
| PDO | PHP Data Objects, cara OOP standar untuk terhubung ke berbagai jenis database |
| Prepared Statement | Query SQL dengan "loket" (?) supaya data pengguna aman dari SQL Injection |
| SQL Injection | Serangan siber yang menyisipkan perintah SQL jahat lewat form input |
| MVC | Pola arsitektur yang memisahkan data (Model), tampilan (View), dan logika alur (Controller) |
| Singleton | Pola desain di mana sebuah objek (misalnya koneksi database) hanya dibuat satu kali lalu dipakai berulang |

## Rangkuman Bab

- Try-Catch menjaga aplikasi tetap berjalan meski ada input yang salah.
- Namespace mencegah bentrok nama class saat aplikasi membesar.
- PDO adalah cara aman dan standar untuk bicara dengan database.
- MVC memisahkan tanggung jawab kode: Model (data), View (tampilan), Controller (alur).
- Kelima materi ini adalah fondasi yang dipakai hampir semua framework PHP modern, termasuk Laravel.

---

*Modul disusun untuk SMK Al-Falah, Mata Pelajaran Pemrograman Berorientasi Objek, Kelas XI RPL/PPLG.*
