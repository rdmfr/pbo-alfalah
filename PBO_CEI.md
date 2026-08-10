# PEMROGRAMAN BERORIENTASI OBJEK (PBO)
### Constructor, Encapsulation, dan Inheritance — Kelas XII RPL/PPLG (PHP Native)

> Materi ini melanjutkan materi **Class, Object, Property, Method, dan `$this`** yang sudah dipelajari di Kelas XI. Sebelum masuk ke Laravel, kalian perlu menguasai dulu 3 konsep OOP native PHP ini, karena Laravel (dan hampir semua framework modern) dibangun di atas konsep ini.

---

## 0. Sebelum Mulai: Bayangkan Dulu, Baru Ngoding

Banyak siswa langsung pusing lihat kode karena belum kebayang **analoginya di dunia nyata**. Jadi sebelum masuk kode, pahami dulu analogi berikut. Kalau analoginya sudah nempel di kepala, kodenya jadi jauh lebih gampang dipahami.

### 🔑 Konsep 1: Constructor — "Formulir Pendaftaran Otomatis"

Bayangkan kalian bikin **KTP baru**. Begitu formulirnya diserahkan ke petugas, otomatis nama, tanggal lahir, dan alamat langsung "diisikan" ke KTP kalian — tanpa kalian harus bilang "tolong isi nama saya" secara terpisah.

Nah, **constructor** (`__construct`) itu seperti petugas itu. Setiap kali ada objek baru dibuat pakai `new`, PHP otomatis "memanggil" constructor untuk langsung mengisi data-data awal objek tersebut. Kalian tidak perlu memanggilnya manual — dia jalan sendiri.

### 🔑 Konsep 2: Encapsulation — "Brankas dengan Loket Kaca"

Bayangkan sebuah **bank**. Uang nasabah disimpan di **brankas** yang tidak bisa dibuka sembarang orang (ini seperti `private`). Tapi nasabah tetap bisa tahu **saldo**-nya lewat **loket / mesin ATM** (ini seperti method getter).

Jadi, data (`private`/`protected`) itu "dikunci" supaya tidak bisa diubah/dibaca sembarangan dari luar class. Kalau mau baca datanya, harus lewat "loket resmi" yaitu method getter (`getMerk()`, `getNama()`, dsb).

> `protected` itu seperti brankas keluarga — orang luar tetap tidak bisa buka, tapi **anak/keturunan** dari class itu (child class) boleh mengaksesnya langsung.

### 🔑 Konsep 3: Inheritance — "Anak Mewarisi Sifat Orang Tua"

Bayangkan **anak yang mewarisi harta dan sifat dari orang tuanya**. Anak otomatis punya semua yang dimiliki orang tua (rumah, mobil, kebiasaan), tapi anak juga bisa **punya hal baru** yang tidak dimiliki orang tua (misalnya hobi baru), dan bisa juga **melakukan hal yang sama dengan cara berbeda** (misalnya orang tua masak pakai resep A, anaknya modifikasi jadi resep B tapi tetap berdasarkan resep asli).

Dalam PHP:
- `extends` = "anak dari"
- Method yang ditulis ulang di child class = **override**
- `parent::` = cara anak "memanggil dulu cara orang tuanya", baru ditambah bagian barunya sendiri

---

## 1. Contoh 1: Class `Kendaraan` & `Mobil` (Inheritance Sederhana)

`Kendaraan` menjadi **class induk (parent)** dengan property private dan constructor. `Mobil` adalah **class anak (child)** yang `extends Kendaraan`, menambah property baru, dan meng-override method `informasi()` dengan tetap memanggil versi milik induknya lewat `parent::`.

```php
<?php
// ==========================================
// 1. CLASS INDUK (Parent Class) - Kendaraan
// ==========================================
// Class ini akan menjadi "class dasar" yang nanti diturunkan (inheritance)
class Kendaraan {

    // ---- PROPERTY (dibuat PRIVATE agar tidak bisa diubah sembarangan dari luar) ----
    private $merk;
    private $tahunProduksi;
    protected $kecepatanMaksimal; // protected: bisa diakses oleh class turunan

    // ---- CONSTRUCTOR ----
    // Method khusus yang otomatis dijalankan setiap kali objek dibuat dengan 'new'
    // Berguna untuk langsung mengisi property saat objek pertama kali dibuat
    public function __construct($merk, $tahunProduksi, $kecepatanMaksimal) {
        $this->merk = $merk;
        $this->tahunProduksi = $tahunProduksi;
        $this->kecepatanMaksimal = $kecepatanMaksimal;
    }

    // ---- GETTER ----
    // Property private tidak bisa dibaca langsung dari luar class,
    // maka kita sediakan method khusus untuk "membaca" nilainya
    public function getMerk() {
        return $this->merk;
    }

    // ---- METHOD ----
    public function informasi() {
        return "Kendaraan merk " . $this->merk . " tahun " . $this->tahunProduksi
                . ", kecepatan maksimal " . $this->kecepatanMaksimal . " km/jam";
    }
}

// ==========================================
// 2. CLASS ANAK (Child Class) - Mobil
// ==========================================
// 'extends' artinya Mobil MEWARISI seluruh property & method milik Kendaraan
class Mobil extends Kendaraan {

    // Property tambahan yang HANYA dimiliki Mobil (tidak ada di Kendaraan)
    private $jumlahPintu;

    public function __construct($merk, $tahunProduksi, $kecepatanMaksimal, $jumlahPintu) {
        // 'parent::' memanggil constructor milik class induk (Kendaraan)
        // agar property merk, tahunProduksi, kecepatanMaksimal ikut terisi
        parent::__construct($merk, $tahunProduksi, $kecepatanMaksimal);
        $this->jumlahPintu = $jumlahPintu;
    }

    // Method 'informasi()' di-OVERRIDE (ditulis ulang) agar hasilnya lebih lengkap
    public function informasi() {
        // 'parent::informasi()' memanggil versi asli milik class induk dahulu
        $infoDasar = parent::informasi();
        return $infoDasar . ", jumlah pintu: " . $this->jumlahPintu;
    }
}

// ==========================================
// 3. MEMBUAT OBJECT & MEMANGGIL METHOD
// ==========================================
$mobilSatu = new Mobil("Toyota Avanza", 2023, 160, 5);
$mobilDua  = new Mobil("Honda Jazz", 2022, 180, 3);

echo $mobilSatu->informasi();
echo "<br>";
echo $mobilDua->informasi();
?>
```

**Output:**
```
Kendaraan merk Toyota Avanza tahun 2023, kecepatan maksimal 160 km/jam, jumlah pintu: 5
Kendaraan merk Honda Jazz tahun 2022, kecepatan maksimal 180 km/jam, jumlah pintu: 3
```

### Penjelasan Bagian per Bagian

- **Constructor:** `__construct()` dijalankan otomatis begitu `new Mobil(...)` dipanggil — tidak perlu dipanggil manual. Ingat analogi "petugas KTP" tadi — begitu formulir masuk, data langsung terisi.
- **Encapsulation:** `$merk` dan `$tahunProduksi` bertipe `private` (hanya bisa diakses dari dalam class `Kendaraan` sendiri), sedangkan `$kecepatanMaksimal` bertipe `protected` (bisa diakses class turunannya, yaitu `Mobil`) — ini seperti brankas keluarga tadi.
- **Inheritance:** `class Mobil extends Kendaraan` berarti `Mobil` otomatis punya semua property & method `Kendaraan`, tanpa perlu menulis ulang — seperti anak yang otomatis mewarisi harta orang tua.
- **`parent::`:** `parent::__construct()` dan `parent::informasi()` dipakai supaya `Mobil` tidak perlu menulis ulang logika yang sudah ada di `Kendaraan` — cukup menambahkan bagian barunya saja.

### 🧪 Coba Sendiri (Praktik 1)

1. Salin kode di atas ke file bernama `kendaraan.php`.
2. Jalankan pakai XAMPP (letakkan di folder `htdocs`, lalu buka `http://localhost/kendaraan.php`) **atau** coba online di [onlinephpfunctions.com](https://onlinephpfunctions.com).
3. **Cek keberhasilan:** pastikan output persis sama seperti bagian "Output" di atas. Kalau ada error, baca pesan errornya — biasanya salah ketik nama property/method atau lupa titik koma.
4. **Tantangan kecil:** tambahkan objek `Mobil` ketiga dengan data buatanmu sendiri, lalu `echo` hasil `informasi()`-nya. Jika muncul dengan benar (termasuk jumlah pintu), berarti kamu sudah paham cara kerja constructor + inheritance.
5. **Uji encapsulation:** coba tulis `echo $mobilSatu->merk;` langsung di luar class (setelah baris `new Mobil(...)`). Ini **seharusnya error** ("Cannot access private property"), karena `$merk` bersifat `private`. Kalau errornya muncul seperti itu, berarti encapsulation-nya berhasil bekerja!

---

## 2. Contoh 2: Class `Karyawan` & `Manager` (Encapsulation + Method Override)

Contoh kedua menunjukkan bahwa method yang di-override boleh punya **logika perhitungan** yang berbeda dari method aslinya, bukan sekadar menambah teks seperti contoh sebelumnya.

```php
<?php
// ==========================================
// 1. CLASS INDUK (Parent Class) - Karyawan
// ==========================================
class Karyawan {

    private $nama;
    private $gajiPokok;

    public function __construct($nama, $gajiPokok) {
        $this->nama = $nama;
        $this->gajiPokok = $gajiPokok;
    }

    public function getNama() {
        return $this->nama;
    }

    // Aturan gaji versi Karyawan biasa: gaji = gaji pokok saja
    public function hitungGaji() {
        return $this->gajiPokok;
    }

    public function infoGaji() {
        return "Gaji " . $this->nama . ": Rp" . number_format($this->hitungGaji(), 0, ',', '.');
    }
}

// ==========================================
// 2. CLASS ANAK (Child Class) - Manager
// ==========================================
// Manager adalah "jenis khusus" dari Karyawan, tapi aturan gajinya berbeda
class Manager extends Karyawan {

    private $tunjanganJabatan;

    public function __construct($nama, $gajiPokok, $tunjanganJabatan) {
        parent::__construct($nama, $gajiPokok);
        $this->tunjanganJabatan = $tunjanganJabatan;
    }

    // OVERRIDE: aturan hitung gaji Manager BERBEDA dari Karyawan biasa
    public function hitungGaji() {
        // Ambil dulu hasil hitungan gaji versi Karyawan (gaji pokok)
        $gajiKaryawan = parent::hitungGaji();
        // Lalu tambahkan tunjangan jabatan khusus milik Manager
        return $gajiKaryawan + $this->tunjanganJabatan;
    }
}

// ==========================================
// 3. MEMBUAT OBJECT & MEMANGGIL METHOD
// ==========================================
$karyawanSatu = new Karyawan("Budi", 4500000);
$managerSatu  = new Manager("Sari", 6000000, 2500000);

echo $karyawanSatu->infoGaji();
echo "<br>";
echo $managerSatu->infoGaji();
?>
```

**Output:**
```
Gaji Budi: Rp4.500.000
Gaji Sari: Rp8.500.000
```

### Penjelasan Bagian per Bagian

- **Aturan gaji berbeda:** Karyawan biasa (`hitungGaji()` versi induk) hanya menerima gaji pokok, sedangkan Manager (`hitungGaji()` versi override) menerima gaji pokok ditambah tunjangan jabatan. Ibarat resep masakan tadi — Manager "meniru" resep dasar Karyawan, lalu menambah bumbu ekstra.
- **Reuse logika induk:** Manager tetap memanggil `parent::hitungGaji()` untuk mengambil gaji pokok, lalu menambahkan tunjangan di atasnya — bukan menulis ulang dari nol. Ini prinsip penting di OOP: **jangan menulis ulang kode yang sudah ada**, cukup manfaatkan dan tambahkan.
- **Encapsulation tetap berlaku ke child:** Property `$nama` dan `$gajiPokok` bersifat `private` di `Karyawan`, sehingga `Manager` (class anak) tetap **wajib** melewati constructor induknya (`parent::__construct()`) untuk mengisinya — tidak bisa mengakses langsung, meski dia "anak".

### 🧪 Coba Sendiri (Praktik 2)

1. Salin kode di atas ke file `karyawan.php`, lalu jalankan seperti Praktik 1.
2. **Cek keberhasilan:** pastikan hasil `Rp4.500.000` dan `Rp8.500.000` muncul persis (perhatikan format titik ribuan — itu dari `number_format`).
3. **Tantangan kecil:** buat class baru `Direktur extends Manager` yang menambahkan `$tunjanganMobil`, lalu override lagi `hitungGaji()` supaya hasilnya = gaji Manager + tunjangan mobil. Ini melatih **inheritance berlapis** (multi-level).
4. **Uji logikanya sendiri:** sebelum menjalankan kode, coba hitung manual dulu di kertas berapa gaji Direktur versimu. Kalau hasil `echo`-nya sama dengan hitungan manualmu, berarti logikanya sudah benar.

---

## 3. Langkah-Langkah Belajar Materi Ini

Ikuti urutan berikut supaya materi lebih mudah dicerna, jangan loncat-loncat:

1. **Pahami dulu analoginya** (Bagian 0) sebelum baca kode — jangan langsung buka editor.
2. **Baca Contoh 1** baris per baris sambil bandingkan dengan analogi "petugas KTP" dan "anak mewarisi sifat orang tua".
3. **Praktikkan Contoh 1** di komputer (jangan cuma dibaca!) — ketik ulang manual, jangan copy-paste, supaya tangan juga hafal strukturnya.
4. **Coba tantangan encapsulation** di Praktik 1 langkah 5 — rasakan sendiri kenapa `private` itu penting (biar ngerti gunanya, bukan cuma hafal aturan).
5. **Baca Contoh 2**, fokus pada perbedaan: di Contoh 1 override cuma nambah teks, di Contoh 2 override mengubah **logika perhitungan**.
6. **Praktikkan Contoh 2**, lalu kerjakan tantangan `Direktur extends Manager` untuk melatih pemahaman inheritance berlapis.
7. **Kerjakan Tugas Siswa** di bagian bawah — isi dulu tabel rancangan, baru menulis kode (jangan langsung ngoding tanpa rancangan, nanti bingung sendiri).
8. **Uji coba tugasmu** dengan checklist di bagian "Cara Mengecek Tugas Berhasil atau Tidak" di bawah.

---

## 4. Tugas Siswa

Pilih satu pasangan objek dunia nyata yang punya hubungan **"kategori umum → jenis khusus"** (bebas, boleh dari hobi/minat masing-masing), lalu rancang Parent Class dan Child Class-nya terlebih dahulu di tabel di bawah ini **sebelum** menuliskan kode.

Contoh pasangan: Hewan → Burung, Karyawan → Manager, Akun → AkunPremium, Produk → ProdukDiskon.

### Tabel Rancangan Class

| Bagian | Yang harus ditentukan | Contoh (jangan dipakai, buat versi sendiri) |
|---|---|---|
| Nama Parent Class | Nama kategori umum dari objek yang dipilih | Kendaraan |
| Property Parent 1 | private/protected, nama data | `$merk` |
| Property Parent 2 | private/protected, nama data | `$tahunProduksi` |
| Constructor Parent | Parameter apa saja yang diterima `__construct()` | `__construct($merk, $tahunProduksi)` |
| Method Getter | Method untuk membaca 1 property private | `getMerk()` |
| Method Utama (akan di-override) | Nama aksi/hitungan + logikanya | `informasi()` |
| Nama Child Class | extends Parent Class di atas | `Mobil extends Kendaraan` |
| Property Tambahan Child | Property baru yang HANYA ada di Child | `$jumlahPintu` |
| Constructor Child | Wajib panggil `parent::__construct()` | `__construct(..., $jumlahPintu)` |
| Method yang Di-override | Wajib panggil `parent::namaMethod()` di dalamnya | `informasi()` |
| Jumlah Object | Berapa objek Child dan nama variabelnya | `$mobilSatu, $mobilDua` |

### Ketentuan Kode

- Buat 1 Parent Class dan 1 Child Class (menggunakan `extends`) sesuai hasil rancangan di tabel.
- Parent Class minimal punya 2 property private/protected, 1 constructor, 1 method getter, dan 1 method utama.
- Child Class wajib menambah minimal 1 property baru yang tidak ada di Parent Class.
- Constructor Child Class **WAJIB** memanggil `parent::__construct()` untuk mengisi property milik Parent.
- Child Class **WAJIB** meng-override minimal 1 method dari Parent, dan di dalam method tersebut **WAJIB** memanggil `parent::namaMethod()` (seperti pada kedua contoh di atas).
- Buat minimal 2 object dari Child Class, dengan nilai property yang berbeda.
- Panggil method dari masing-masing object menggunakan `->`, lalu tampilkan hasilnya dengan `echo`.
- Tambahkan komentar (`//`) di setiap bagian kode untuk menjelaskan apa yang sedang dilakukan.

### ✅ Cara Mengecek Tugas Berhasil atau Tidak

Sebelum dikumpulkan, cek satu per satu:

- [ ] Kode dijalankan **tanpa error merah** di browser/terminal.
- [ ] Ada 2 property `private`/`protected` di Parent Class.
- [ ] `Child extends Parent` sudah benar (bukan sebaliknya).
- [ ] Constructor Child memanggil `parent::__construct(...)`.
- [ ] Minimal 1 method di-override, dan di dalamnya ada `parent::namaMethod()`.
- [ ] Ada minimal 2 objek Child dengan data berbeda, dan hasil `echo`-nya **berbeda sesuai datanya masing-masing** (kalau hasilnya sama semua, kemungkinan ada variabel yang salah/tertukar).
- [ ] Coba akses property `private` langsung dari luar class (`echo $objek->propertyPrivate;`) — kalau muncul error, berarti encapsulation-mu benar.
- [ ] Tabel rancangan sudah diisi lengkap dan **sesuai** dengan kode yang ditulis (nama class, property, method harus sama persis).

### Format Pengumpulan

- File `.php` (boleh dites di Sublime/VSCode + XAMPP, atau editor online seperti [onlinephpfunctions.com](https://onlinephpfunctions.com)).
- Sertakan juga tabel rancangan class yang sudah diisi.
