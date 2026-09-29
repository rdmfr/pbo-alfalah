# LATIHAN SOAL ASESMEN SUMATIF TENGAH SEMESTER (ASTS)

**SMK Al-Falah Nagreg – Bandung**

| | |
|---|---|
| **Mata Pelajaran** | Pemrograman Berbasis Objek (PBO) |
| **Kelas / Paket Keahlian** | XI (Sebelas) / RPL |
| **Waktu (simulasi)** | 60 Menit |
| **Jenis** | Latihan mandiri (bukan soal ujian sebenarnya) |

**Materi yang dilatih:** Konsep dasar PBO (Class, Object, Property, Method), Class Diagram, Abstraction, Polymorphism, Constructor, Encapsulation (visibility), dan Inheritance dalam PHP Native.

---

## I. SOAL PILIHAN GANDA

**Petunjuk:** Pilihlah salah satu jawaban yang paling tepat!

**1.** Pada pengembangan aplikasi berskala besar, perbedaan mendasar antara pemrograman prosedural dan Pemrograman Berorientasi Objek (PBO) adalah...

- A. PBO tidak boleh menggunakan fungsi, sedangkan prosedural wajib menggunakan fungsi.
- B. Pemrograman prosedural selalu menggunakan konsep *inheritance* untuk menghemat kode.
- C. Pemrograman prosedural berfokus pada urutan instruksi/fungsi, sedangkan PBO memecah program menjadi objek yang memiliki data dan perilaku sehingga lebih modular dan mudah dipakai ulang.
- D. PBO hanya bisa dijalankan pada aplikasi desktop, sedangkan prosedural hanya untuk web.
- E. Pemrograman prosedural lebih cocok untuk sistem besar karena semua data bersifat global.

**2.** Dalam membuat aplikasi toko online, seorang programmer membuat rancangan/format kosong untuk data produk (berisi variabel nama, harga, dan stok) tanpa nilai yang nyata. Rancangan dasar atau *blueprint* tersebut disebut...

- A. Class
- B. Object
- C. Method
- D. Property
- E. Database

**3.** Pasangan Class dan Object yang paling tepat dalam kehidupan sehari-hari adalah...

- A. Class: Sepeda motor Vario milik saya | Object: Kendaraan
- B. Class: Berlari | Object: Atlet
- C. Class: Warna biru | Object: Cat dinding
- D. Class: Sepatu | Object: Sepatu Nike Air Max milik saya
- E. Class: Laptop Lenovo | Object: Perangkat keras

**4.** Sebelum menulis kode, programmer sering membuat *Class Diagram*. Fungsi utama *Class Diagram* adalah...

- A. Menggantikan fungsi database dalam menyimpan data secara permanen.
- B. Sebagai alat bantu merancang struktur class (nama, atribut, dan operasi) sebelum diimplementasikan ke dalam kode.
- C. Menjalankan program PHP tanpa memerlukan web server.
- D. Memperbaiki kode program yang error secara otomatis.
- E. Mengubah kode PHP menjadi HTML biasa.

**5.** Perhatikan *Class Diagram* sederhana berikut:

| Guru |
|---|
| - nip |
| - nama |
| + tampilkanProfil() |

Bagian yang menunjukkan **nama class** pada diagram di atas adalah...

- A. nip dan nama
- B. tampilkanProfil()
- C. Tanda plus (+)
- D. Tanda minus (-)
- E. Guru

**6.** Dalam sistem aplikasi streaming, sebuah objek Film memerlukan atribut untuk menyimpan judul dan durasi, serta aksi untuk memutar film. *Property* dan *Method* yang paling tepat untuk Class Film adalah...

- A. Property: putarFilm(), hentikanFilm() | Method: judul
- B. Property: putarFilm() | Method: durasi
- C. Property: judul, durasi | Method: putarFilm()
- D. Property: judul | Method: durasi
- E. Property: hentikanFilm(), durasi | Method: judul

**7.** Konsep PBO yang menyembunyikan detail implementasi yang rumit dan hanya menampilkan fitur penting kepada pengguna (seperti tombol-tombol pada remote TV tanpa perlu tahu rangkaian elektroniknya) disebut...

- A. Abstraction
- B. Inheritance
- C. Polymorphism
- D. Instansiasi
- E. Overloading

**8.** Perhatikan ilustrasi berikut: *"Saat menggunakan mesin cuci, Anda cukup memilih program dan menekan tombol start tanpa harus memahami cara kerja motor penggerak dan sensor air di dalamnya."* Ilustrasi tersebut merupakan penerapan konsep...

- A. Inheritance
- B. Polymorphism
- C. Instansiasi
- D. Abstraction
- E. Constructor

**9.** Dalam sebuah game, terdapat method `serang()` pada class Ksatria, Penyihir, dan Pemanah. Nama method-nya sama, tetapi efek serangannya berbeda-beda pada setiap class. Konsep pilar PBO ini dinamakan...

- A. Abstraction
- B. Polymorphism
- C. Inheritance
- D. Encapsulation
- E. Instansiasi

**10.** Kemampuan objek-objek dari class yang berbeda untuk merespons pemanggilan method bernama sama dengan cara yang berbeda-beda disebut...

- A. Encapsulation
- B. Abstraction
- C. Constructor
- D. Visibility
- E. Polymorphism

**11.** Manakah di bawah ini yang merupakan contoh nyata penerapan konsep *Polymorphism*?

- A. Menyembunyikan nomor kartu kredit menggunakan modifier `private`.
- B. Membuat rancangan aplikasi menggunakan *Class Diagram*.
- C. Class Bentuk memiliki method `hitungLuas()`, lalu class Lingkaran dan Segitiga mengimplementasikannya dengan rumus yang berbeda.
- D. Membuat objek baru menggunakan keyword `new`.
- E. Mengakses property di dalam class menggunakan `$this->`.

**12.** Pada aplikasi ojek online, class Tarif menerapkan *Abstraction* dan class Promo menerapkan *Polymorphism*. Perbedaan utama antara *Abstraction* dan *Polymorphism* adalah...

- A. Abstraction menyembunyikan detail kompleks dengan hanya menampilkan fungsi penting (misalnya lewat class abstrak/interface), sedangkan Polymorphism memakai nama method yang sama dengan bentuk aksi yang beragam.
- B. Abstraction wajib memakai database, sedangkan Polymorphism tidak.
- C. Abstraction hanya bisa dipakai di PHP, sedangkan Polymorphism hanya di Java.
- D. Abstraction mengatur hak akses `private`, sedangkan Polymorphism mengatur hak akses `public`.
- E. Tidak ada perbedaan karena keduanya memiliki fungsi yang sama persis.

**13.** Perhatikan potongan kode PHP berikut:

```php
class PersegiPanjang {
    public $panjang = 8;
    public $lebar = 5;

    public function hitungKeliling() {
        return 2 * ($this->panjang + $this->lebar);
    }
}

$pp = new PersegiPanjang();
echo $pp->hitungKeliling();
```

Output yang dihasilkan saat kode di atas dijalankan adalah...

A. 40
B. 26
C. 13
D. Error
E. 65

**14.** Perhatikan potongan kode PHP berikut yang mengalami error:

```php
class Produk {
    public $harga = 5000;

    public function info() {
        return "Harga: " . harga;
    }
}
```

Penyebab utama error pada kode di atas adalah...

- A. Keyword `public` salah penulisan.
- B. Nama class diawali huruf kapital.
- C. Class Produk belum memiliki constructor.
- D. Property `harga` dipanggil di dalam method tanpa `$this->` sehingga tidak dikenali.
- E. Method `info()` tidak boleh mengembalikan string.

**15.** Dalam PHP, fungsi utama dari method khusus `__construct()` adalah...

- A. Menghapus objek dari memori secara otomatis.
- B. Mengubah hak akses `private` menjadi `public`.
- C. Menginisialisasi/mengisi nilai awal property secara otomatis saat objek pertama kali dibuat.
- D. Menggandakan objek menjadi dua bagian.
- E. Menghubungkan script PHP langsung ke database.

**16.** Kapan method constructor (`__construct()`) dieksekusi secara otomatis oleh PHP?

- A. Saat file PHP pertama kali dibuka di browser.
- B. Saat method biasa dipanggil menggunakan tanda panah (`->`).
- C. Ketika program mengalami error.
- D. Saat script PHP selesai dijalankan.
- E. Saat keyword `new` dipanggil untuk membuat objek dari class.

**17.** Perhatikan potongan kode PHP berikut:

```php
class Laptop {
    public $tipe;

    public function __construct($t) {
        $this->tipe = $t;
    }
}

$lp = new Laptop("Acer");
```

Nilai property `$tipe` pada objek `$lp` setelah instansiasi di atas adalah...

- A. NULL
- B. "Acer"
- C. "Laptop"
- D. "Error"
- E. $t

**18.** Dalam konsep *Encapsulation* terdapat tiga hak akses (*visibility*). Perbedaan utama antara `public`, `protected`, dan `private` adalah...

- A. `public` dapat diakses dari mana saja, `protected` hanya dari class asal dan class turunannya, `private` hanya dari dalam class itu sendiri.
- B. `public` hanya untuk database, `private` hanya untuk tampilan HTML.
- C. `protected` tidak dapat diwariskan ke child class.
- D. `private` membuat property dapat diakses bebas dari luar class.
- E. Ketiganya memiliki hak akses yang sama persis.

**19.** Sebuah sistem login memiliki property `$passwordAdmin` di dalam class Admin. Agar property tersebut tidak dapat dibaca atau diubah sembarangan dari luar class, hak akses (*visibility*) yang paling tepat adalah...

- A. Public
- B. Protected
- C. Static
- D. Private
- E. Global

**20.** Perhatikan potongan kode berikut:

```php
class Dompet {
    private $isi = 50000;
}

$d = new Dompet();
echo $d->isi;
```

Saat dijalankan, PHP akan menampilkan pesan error. Penyebab utama error tersebut adalah...

- A. Keyword `new` salah penulisan.
- B. Perintah `echo` tidak boleh digunakan untuk mencetak angka.
- C. Property `$isi` bersifat `private` sehingga tidak boleh diakses langsung dari luar class.
- D. Class Dompet harus memiliki constructor.
- E. Nilai `$isi` terlalu besar.

---

## II. SOAL URAIAN

**1.** Konsep dasar PBO (Class, Object, Property, Method) sangat erat dengan kehidupan sehari-hari. Buatlah satu analogi rancangan PBO versi Anda sendiri (**jangan** gunakan contoh Mobil, KTP, Karyawan, Ponsel, Buku, atau Kamera). Sebutkan apa yang menjadi Class, Object, 2 contoh Property, dan 2 contoh Method-nya!

**2.** Jelaskan dengan bahasamu sendiri, apa tujuan utama penggunaan Constructor (`__construct`) dalam PBO! Apa perbedaannya dengan method biasa?

**3.** Mengapa dalam konsep *Encapsulation* data penting (seperti PIN atau nilai rapor) diatur dengan visibility `private` dan bukan `public`? Bagaimana cara membaca dan mengubah data `private` tersebut secara aman?

**4.** Jelaskan apa yang dimaksud dengan *Inheritance* (pewarisan) dalam PBO, sebutkan satu keuntungan utamanya, dan berikan satu contoh hubungan *Parent Class* dan *Child Class*!

**5.** Tuliskan sintaks PHP sederhana untuk mengimplementasikan skenario berikut:

- a. Buat class induk bernama `Hewan` yang memiliki satu property `protected` bernama `$nama`.
- b. Buat class `Hewan` tersebut memiliki constructor untuk mengisi nilai `$nama`.
- c. Buat class anak bernama `Kucing` yang merupakan turunan (`extends`) dari `Hewan`.
- d. Di dalam class `Kucing`, buat method `getNamaHewan()` yang mengembalikan string `"Nama Hewan: "` digabung dengan nilai property `$nama`.
- e. Buat 1 objek dari class `Kucing` (misalnya dengan nama `"Mochi"`), lalu panggil method `getNamaHewan()` dan `echo` hasilnya!

**— SELAMAT BERLATIH —**
