# MODUL AJAR
## PEMROGRAMAN BERORIENTASI OBJEK (PBO)
### BAB 1 — Konsep Dasar PBO: Abstraction & Polymorphism

*Fase F — Kelas XI, Konsentrasi Pengembangan Perangkat Lunak dan Gim (PPLG)*
*Kurikulum Merdeka*

> **Catatan revisi:** Instalasi Laravel dan penerapan PBO pada arsitektur MVC dipindahkan ke modul semester 2. Pilar **Encapsulation**, **Inheritance**, dan pembahasan **Constructor** sudah dibahas pada modul terpisah, sehingga Bab 1 ini difokuskan pada pilar **Abstraction** dan **Polymorphism**, ditambah materi **Class Diagram sederhana** sebagai alat bantu merancang class sebelum menulis kode.

---

## A. INFORMASI UMUM

### 1. Identitas Modul

| Komponen | Keterangan |
|---|---|
| Mata Pelajaran | Pemrograman Berorientasi Objek (PBO) |
| Fase / Kelas | F / XI PPLG |
| Alokasi Waktu | 2 x pertemuan (@ 6 JP, 1 JP = 45 menit) |
| Elemen | Berpikir Komputasional & Pemrograman Berbasis Objek |
| Model Pembelajaran | Discovery Learning & Project Based Learning (PjBL) |
| Moda | Tatap muka / Blended Learning (Laboratorium Komputer) |

### 2. Capaian Pembelajaran (CP)

Pada akhir Bab 1, peserta didik mampu memahami konsep dasar pemrograman berorientasi objek (Class, Object, Property, Method), merancang class secara sederhana menggunakan Class Diagram, serta menerapkan pilar **Abstraction** dan **Polymorphism** dalam bahasa pemrograman PHP native, sebagai fondasi sebelum mempelajari pilar Encapsulation, Inheritance, dan penerapan PBO pada framework di semester berikutnya.

### 3. Tujuan Pembelajaran (TP)

1. Peserta didik dapat menjelaskan konsep dan perbedaan antara pemrograman prosedural dan pemrograman berorientasi objek dengan tepat.
2. Peserta didik dapat mengidentifikasi komponen utama PBO (Class, Object, Property, Method) dan menganalogikannya dengan contoh kehidupan sehari-hari.
3. Peserta didik dapat menggambarkan rancangan sebuah class secara sederhana dalam bentuk Class Diagram sebelum menuliskannya sebagai kode.
4. Peserta didik dapat menjelaskan dan memberi contoh pilar **Abstraction** dan **Polymorphism** dalam PBO.
5. Peserta didik dapat menuliskan kode PBO sederhana menggunakan PHP native (membuat class, object, property, dan method) sesuai rancangan yang telah dibuat.

### 4. Profil Pelajar Pancasila

- **Bernalar Kritis** — menganalisis perbedaan pendekatan prosedural dan PBO serta memilih solusi pemrograman yang tepat.
- **Mandiri** — merancang Class Diagram dan mempraktikkan kode PBO secara mandiri sesuai instruksi praktikum.
- **Kreatif** — merancang class dan object baru (tugas mandiri Laptop) dengan variasi property dan method sendiri.
- **Gotong Royong** — berdiskusi dalam kelompok untuk menemukan contoh Class dan Object dari aplikasi sehari-hari (LKPD 1) dan saling membantu saat praktik kode di laboratorium.

### 5. Sarana, Prasarana, dan Target Peserta Didik

| Aspek | Keterangan |
|---|---|
| Sarana | Laptop/PC, text editor/VS Code, PHP (XAMPP atau PHP CLI) untuk menjalankan kode, browser |
| Prasarana | Modul ajar, LKPD, proyektor, Laboratorium Komputer |
| Target Peserta Didik | Reguler (tidak ada kesulitan dalam mencerna materi ajar) |
| Jumlah Peserta Didik | Maksimal 36 peserta didik per rombel |

### 6. Pemahaman Bermakna

Peserta didik menyadari bahwa hampir seluruh aplikasi digital yang mereka gunakan sehari-hari — mulai dari aplikasi belanja online, transportasi online, hingga dompet digital — dibangun menggunakan konsep PBO. Sebelum menulis kode, seorang programmer perlu merancang terlebih dahulu class apa saja yang dibutuhkan; memahami PBO berarti memahami "cara berpikir" sekaligus "cara merancang" di balik aplikasi-aplikasi tersebut.

### 7. Pertanyaan Pemantik

- Pernahkah kalian membuka aplikasi Gojek, Shopee, atau dompet digital? Menurut kalian, bagaimana programmer mengatur ribuan data pengguna, driver, dan transaksi agar tetap rapi?
- Apa perbedaan antara "cetakan kue" dan "kue yang sudah jadi"? Menurut kalian, apa hubungannya dengan istilah Class dan Object dalam pemrograman?

---

## B. KEGIATAN PEMBELAJARAN

### Pertemuan 1 — Konsep Dasar PBO & Class Diagram (6 JP)

**Kegiatan Pendahuluan (15 menit)**
- Guru membuka kelas, menyapa, dan mengecek kehadiran peserta didik.
- Guru menyampaikan tujuan pembelajaran dan mengajukan pertanyaan pemantik.
- Apersepsi: guru menampilkan tampilan aplikasi Gojek/Shopee di layar proyektor sebagai pemantik diskusi.

**Kegiatan Inti (240 menit)**
- Peserta didik menyimak penjelasan guru mengenai konsep PBO, perbandingan Prosedural vs PBO, serta komponen utama PBO (materi bagian 1-2).
- Peserta didik berdiskusi kelompok kecil mencari 3 contoh Class dan Object dari aplikasi/benda di sekitar mereka (LKPD 1).
- Peserta didik menyimak penjelasan cara membaca dan menggambar Class Diagram sederhana (materi bagian 3).
- Peserta didik berlatih menggambar Class Diagram untuk sebuah studi kasus sederhana yang diberikan guru.

**Kegiatan Penutup (15 menit)**
- Peserta didik menyimpulkan materi bersama guru.
- Guru memberikan pertanyaan refleksi dan menutup pelajaran.

### Pertemuan 2 — Pilar Abstraction, Polymorphism & Praktik PHP Native (6 JP)

**Kegiatan Pendahuluan (15 menit)**
- Guru mengulas singkat Class Diagram yang dibuat pada pertemuan sebelumnya.
- Guru menyampaikan tujuan pembelajaran pertemuan ini.

**Kegiatan Inti (240 menit)**
- Peserta didik menyimak penjelasan pilar **Abstraction** dan **Polymorphism** beserta analogi kehidupan sehari-hari (materi bagian 4).
- Peserta didik mempraktikkan kode `dasar_pbo.php` secara mandiri di laboratorium komputer, mengacu pada Class Diagram yang telah dirancang (materi bagian 5).
- Peserta didik mengerjakan Tugas Mandiri (materi bagian 6) sebagai asesmen sumatif.

**Kegiatan Penutup (15 menit)**
- Peserta didik menyimpulkan materi bersama guru.
- Guru memberikan pertanyaan refleksi dan menutup pelajaran.

---

## C. MATERI PEMBELAJARAN

## BAB 1: Konsep Dasar Pemrograman Berorientasi Objek (PBO)

### 1. Identifikasi & Konsep Pemrograman Berorientasi Objek (PBO)

#### A. Apa itu PBO / OOP?

**Pemrograman Berorientasi Objek (Object-Oriented Programming / OOP)** adalah paradigma atau tata cara pembuatan program menggunakan konsep **Object**. Objek ini memiliki data (*property/attribute*) dan prosedur/fungsi (*method*).

> 🌍 **Analogi Kehidupan Sehari-hari**
> Bayangkan kalian sedang membuka aplikasi ojek online seperti Gojek atau Grab. Di dalam aplikasi tersebut ada banyak "objek" seperti Driver, Penumpang, dan Pesanan. Setiap Driver punya data (nama, plat nomor, rating) dan bisa melakukan aksi (menerima order, mengantar penumpang). Itulah cara berpikir PBO — semua hal di dunia nyata direpresentasikan sebagai objek yang punya data dan aksi.

#### B. Perbandingan: Prosedural vs PBO

- **Pemrograman Prosedural:** Berfokus pada langkah-langkah linier dari atas ke bawah. Ketika aplikasi membesar, kode menjadi sulit dikelola dan rentan berantakan (*spaghetti code*).
- **Pemrograman Berorientasi Objek (PBO):** Mengorganisasikan program ke dalam **Class** dan **Object** yang saling berinteraksi secara modular, sehingga kode lebih rapi, reusable, dan mudah dikembangkan.

> 🌍 **Analogi**
> Prosedural itu seperti resep masakan yang ditulis sebagai daftar langkah panjang dari awal sampai akhir dalam satu kertas. Kalau ingin membuat 10 masakan berbeda, kalian harus menulis 10 kertas resep terpisah, walaupun ada langkah yang sama (misalnya "potong bawang"). PBO itu seperti dapur profesional: setiap koki (object) punya tugas dan peralatan masing-masing (property & method), dan bisa dipanggil kapan saja tanpa menulis ulang instruksi dari nol.

#### C. Penggunaan PBO

PBO digunakan secara luas dalam bahasa seperti PHP, Java, C#, Python, dan C++. Contoh nyata aplikasi berbasis PBO yang sering digunakan siswa: aplikasi e-commerce (Shopee, Tokopedia), aplikasi perbankan digital, aplikasi presensi sekolah, dan sistem informasi akademik. Pada semester berikutnya, kalian akan mempelajari bagaimana konsep PBO ini diterapkan secara penuh pada sebuah *framework* PHP untuk membangun aplikasi yang lebih besar dan terstruktur.

---

### 2. Komponen Utama PBO

| Komponen | Penjelasan | Contoh Dunia Nyata |
| --- | --- | --- |
| **Class** | Draf, rancangan, atau *blueprint* yang mendeskripsikan struktur dan perilaku objek. | Formulir pendaftaran siswa baru (formatnya sama untuk semua siswa) |
| **Object** | Wujud nyata (*instansiasi*) yang dibuat dari sebuah Class. | Formulir yang sudah diisi data siswa bernama Ahmad |
| **Property / Attribute** | Variabel di dalam class yang menyimpan data/karakteristik objek. | Nama, NIS, Kelas, Alamat siswa |
| **Method / Function** | Fungsi di dalam class yang mendeskripsikan aksi/perilaku objek. | `daftarUlang()`, `lihatNilai()`, `absen()` |

> 🌍 **Analogi Tambahan: Aplikasi Sekolah**
> Class `Siswa` adalah "format data siswa" yang berlaku untuk seluruh siswa di sekolah. Ketika kalian mendaftar dan data kalian dimasukkan ke sistem, sistem membuat satu Object baru dari Class `Siswa`, yaitu "kalian sendiri" dengan nama, NIS, dan kelas masing-masing. Setiap siswa (object) berbeda datanya, tetapi strukturnya (property & method) tetap sama karena berasal dari Class yang sama.

---

### 3. Merancang Class dengan Class Diagram Sederhana

Sebelum menulis kode, seorang programmer biasanya merancang dahulu class yang dibutuhkan agar tidak salah struktur di tengah jalan. Salah satu alat bantu yang umum dipakai adalah **Class Diagram**, yaitu notasi visual sederhana berbentuk kotak yang terbagi menjadi tiga bagian:

1. **Nama Class** — di bagian paling atas.
2. **Property** — daftar data yang dimiliki class, di bagian tengah.
3. **Method** — daftar aksi/perilaku yang dimiliki class, di bagian bawah.

**Contoh Class Diagram untuk Class `Mobil`:**

```
┌───────────────────────────┐
│           Mobil            │
├───────────────────────────┤
│ merk                       │
│ warna                      │
│ kecepatan                  │
├───────────────────────────┤
│ tambahKecepatan(tambahan)  │
│ mengeram()                 │
└───────────────────────────┘
```

> 🌍 **Analogi**
> Class Diagram itu seperti sketsa arsitek sebelum membangun rumah. Arsitek tidak langsung menumpuk bata, tetapi menggambar dulu denahnya — ruang apa saja yang ada dan apa fungsinya. Begitu juga programmer: sebelum menulis `class Mobil { ... }`, akan lebih mudah kalau sudah punya sketsa property dan method apa saja yang dibutuhkan.

> 💡 **Catatan:** Pada bab ini, Class Diagram digunakan secara sederhana hanya untuk latihan merancang property dan method. Notasi lanjutan seperti tanda visibilitas (`+`/`-`) dan relasi antar-class (Inheritance) akan dipelajari lebih lanjut pada modul terpisah.

---

### 4. Pilar PBO yang Dipelajari pada Bab Ini: Abstraction & Polymorphism

> 💡 Empat pilar utama PBO adalah Abstraction, Encapsulation, Inheritance, dan Polymorphism. Pada bab ini kita membahas **Abstraction** dan **Polymorphism** terlebih dahulu. **Encapsulation** dan **Inheritance** dibahas secara khusus pada modul terpisah.

#### a. Abstraction (Abstraksi)

- **Pengertian:** Proses menentukan data dan method yang dimiliki oleh suatu class dengan melihat objek dalam bentuk yang lebih umum/sederhana.
- **Fungsi:** Menyederhanakan sistem kompleks menjadi kumpulan subsistem yang mudah dipahami.
- **Contoh:** Class `Hewan` membawahi subsistem spesifik seperti `Sapi`, `Kambing`, dan `Kucing`.

> 🌍 **Analogi**
> Saat kalian mengendarai motor, kalian cukup tahu cara "tarik gas" dan "tekan rem" untuk berjalan atau berhenti. Kalian tidak perlu tahu detail rumit di dalam mesin (pembakaran bahan bakar, kerja piston, dsb). Itulah abstraksi — pengguna hanya melihat fitur penting (method) tanpa perlu tahu cara kerja rinci di baliknya. Begitu juga aplikasi dompet digital: pengguna cukup tekan tombol "Bayar", tanpa perlu tahu proses enkripsi dan verifikasi bank di belakang layar.

#### b. Polymorphism (Polimorfisme)

- **Pengertian:** Memungkinkan penggunaan nama interface/method yang sama pada objek berbeda, namun dengan cara kerja yang disesuaikan.
- **Contoh:** Class `Mobil` dan Class `Motor` sama-sama memiliki method `melaju()`, namun mekanisme mesin internalnya berbeda.

> 🌍 **Analogi**
> Coba perhatikan berbagai aplikasi pembayaran digital seperti GoPay, OVO, dan DANA. Ketiganya memiliki method yang sama yaitu `bayar()`, tetapi proses di baliknya berbeda-beda (beda server, beda cara verifikasi). Contoh lain: Class `Kucing` dan Class `Bebek` sama-sama punya method `bersuara()`, tapi hasilnya berbeda — kucing mengeong, bebek berkwek. Satu "nama perintah" yang sama, hasil kerja yang berbeda sesuai objeknya — itulah polimorfisme.

---

### 5. Implementasi Kode PBO pada PHP Native

Buat file baru bernama `dasar_pbo.php` di text editor kalian, lalu ketik kode berikut. Kode ini adalah hasil "terjemahan" dari Class Diagram `Mobil` yang sudah kita rancang pada materi bagian 3.

```php
<?php

// 1. MEMBUAT CLASS (Blueprint / Cetakan)
class Mobil {
    // Property (Attribute / Data)
    public $merk;
    public $warna;
    public $kecepatan = 0;

    // Method (Aksi / Perilaku)
    public function tambahKecepatan($tambahan) {
        // Keyword '$this' merujuk pada objek yang sedang aktif
        $this->kecepatan += $tambahan;
        return "Mobil " . $this->merk . " berwarna " . $this->warna . " sedang melaju " . $this->kecepatan . " km/jam!";
    }

    public function mengeram() {
        return "Mobil " . $this->merk . " sedang mengeram.";
    }
}

// 2. MEMBUAT OBJECT (Instansiasi dengan keyword 'new')
$mobilSatu = new Mobil();
$mobilSatu->merk = "Toyota Supra";
$mobilSatu->warna = "Merah";

$mobilDua = new Mobil();
$mobilDua->merk = "Honda Civic";
$mobilDua->warna = "Hitam";

// 3. MEMANGGIL METHOD MENGGUNAKAN OPERATOR '->'
echo $mobilSatu->tambahKecepatan(80);
// Output: Mobil Toyota Supra berwarna Merah sedang melaju 80 km/jam!

echo "<br>";

echo $mobilDua->mengeram();
// Output: Mobil Honda Civic sedang mengeram.

?>
```

#### Simbol Penting dalam PHP PBO

| Simbol | Fungsi |
|---|---|
| `new` | Perintah untuk membuat Object baru dari sebuah Class. |
| `->` | Operator untuk mengakses Property atau Method milik objek. |
| `$this` | Variabel khusus yang merujuk pada objek yang sedang dieksekusi di dalam Class. |

---

## D. ASESMEN

### 1. Asesmen Formatif (Diagnostik Awal & Proses)

Dilakukan melalui tanya jawab lisan saat apersepsi dan pengamatan keaktifan diskusi kelompok (LKPD 1) mengenai contoh Class/Object di sekitar peserta didik, serta hasil latihan menggambar Class Diagram.

**Contoh Soal Latihan Lisan/Kuis Singkat**

1. Sebutkan 3 contoh Class dan Object dari aplikasi yang kalian gunakan sehari-hari!
2. Mengapa saat mengendarai motor kita cukup tahu "tarik gas" dan "tekan rem" tanpa perlu tahu cara kerja mesin di dalamnya? Pilar PBO apa yang berkaitan dengan hal ini?
3. GoPay, OVO, dan DANA sama-sama memiliki method `bayar()`, tetapi cara kerja di baliknya berbeda. Pilar PBO apa yang ditunjukkan oleh contoh ini?
4. Jelaskan perbedaan antara Class `Kendaraan` dengan Object "motor Ahmad bernomor plat B 1234 XYZ".

### 2. Asesmen Sumatif — Tugas Mandiri

Kerjakan tugas berikut secara individu, lalu kumpulkan gambar Class Diagram, file kode, dan tangkapan layar (screenshot) hasil output di browser.

1. Rancang terlebih dahulu **Class Diagram sederhana** untuk sebuah class baru bernama `Laptop` dengan ketentuan:
   - Property: `$merk`, `$ram`, dan `$prosesor`.
   - Method: `tampilkanSpesifikasi()` yang mengembalikan deskripsi laptop tersebut.
2. Terjemahkan Class Diagram tersebut menjadi kode PHP native (`class Laptop { ... }`).
3. Buat **2 Object laptop yang berbeda** (contoh: ASUS dan Lenovo), lalu tampilkan hasilnya di browser!
4. *(Tantangan tambahan)* Tambahkan method `hitungTotalHarga($diskon)` yang menghitung harga laptop setelah diskon, untuk melatih pemahaman kalian tentang method dengan parameter.

**Rubrik Penilaian Tugas Mandiri**

| Aspek Penilaian | Skor 4 (Sangat Baik) | Skor 3 (Baik) | Skor 2 (Cukup) | Skor 1 (Perlu Bimbingan) |
|---|---|---|---|---|
| Class Diagram | Diagram lengkap dan sesuai dengan kode yang dibuat | Diagram ada, sedikit tidak sesuai dengan kode | Diagram dibuat namun kurang lengkap | Diagram tidak dibuat |
| Struktur Class & Property | Class dan seluruh property benar & sesuai ketentuan | Class benar, 1 property kurang tepat | Class benar, lebih dari 1 property kurang tepat | Class tidak terbentuk dengan benar |
| Method & Logika | Method berjalan sempurna dan menghasilkan output sesuai | Method berjalan, output kurang lengkap | Method ada namun terdapat error kecil | Method tidak berhasil dijalankan |
| Object (Instansiasi) | 2 object dibuat dengan data berbeda & benar | 2 object dibuat, sedikit kesalahan data | Hanya 1 object berhasil dibuat | Belum berhasil membuat object |
| Kerapian & Penamaan Kode | Penamaan variabel/method jelas, indentasi rapi | Cukup rapi, ada sedikit inkonsistensi | Kurang rapi namun tetap terbaca | Tidak rapi dan sulit dibaca |

### 3. Refleksi Peserta Didik

- Bagian materi PBO mana yang menurut kalian paling mudah dipahami? Mengapa?
- Apakah membuat Class Diagram terlebih dahulu membantu kalian saat menulis kode? Mengapa?
- Setelah mempelajari bab ini, coba sebutkan satu aplikasi baru (selain yang dicontohkan) beserta kemungkinan Class dan Object di dalamnya!

### 4. Refleksi Guru

- Apakah peserta didik cukup terbantu dengan latihan Class Diagram sebelum menulis kode, atau justru terasa sebagai langkah tambahan yang membingungkan?
- Apakah analogi kehidupan sehari-hari membantu peserta didik memahami pilar Abstraction dan Polymorphism?
- Perlukah alokasi waktu tambahan untuk sesi praktik kode PHP native pada pertemuan berikutnya?

---

## E. GLOSARIUM

| Istilah | Arti |
|---|---|
| Class | Blueprint/rancangan yang mendefinisikan struktur dan perilaku objek. |
| Object | Instansiasi/wujud nyata dari sebuah class. |
| Property | Variabel yang menyimpan data/karakteristik suatu objek. |
| Method | Fungsi di dalam class yang mendeskripsikan perilaku/aksi objek. |
| Instansiasi | Proses membuat object baru dari sebuah class menggunakan keyword `new`. |
| Class Diagram | Notasi visual sederhana untuk merancang nama class, property, dan method sebelum menulis kode. |
| Abstraction | Penyederhanaan sistem kompleks dengan hanya menampilkan hal-hal penting/relevan. |
| Polymorphism | Kemampuan method dengan nama sama bekerja berbeda pada objek berbeda. |

---

## F. DAFTAR PUSTAKA

- PHP Manual — Object-Oriented Programming. https://www.php.net/manual/en/language.oop5.php
- UML Diagrams — Class Diagram Overview. https://www.uml-diagrams.org/class-diagrams-overview.html
- Modul Pembelajaran Informatika/RPL Kurikulum Merdeka, Kemendikbudristek.
