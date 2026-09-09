# 📝 LEMBAR TUGAS SISWA
## Pemrograman Berorientasi Objek (PBO) — PHP Native
### Kelas XI RPL/PPLG — Kurikulum Merdeka

> **Cakupan materi:** Dasar PBO (Class, Object, 4 Pilar), Polymorphism, Abstract Class, Interface, Static Property/Method
> **Sifat tugas:** Individu
> **Alat bantu:** Text editor / VS Code, [onlinephp.io](https://onlinephp.io)
> **Pengumpulan:** File kode (.php) + tangkapan layar (screenshot) hasil output

---

## 🧭 Petunjuk Umum

1. Kerjakan setiap soal sesuai kelompok materinya (Bagian A, B, atau C).
2. Semua kode PHP native **wajib** dites dan terbukti jalan tanpa error (boleh pakai onlinephp.io).
3. Beri **komentar** pada bagian kode yang penting, seperti dicontohkan di modul.
4. Kumpulkan dalam satu folder berisi: file `.php` dan screenshot output.
5. Dilarang menyalin persis contoh kode dari modul — gunakan nama class/property yang berbeda dari contoh.

---

## 🅰️ BAGIAN A — Dasar PBO (Tugas Mandiri Sumatif)

Kerjakan secara individu, lalu kumpulkan file kode dan tangkapan layar hasil output.

**Soal A1**
Buatlah sebuah class baru bernama `Laptop` dengan ketentuan:
- Property: `$merk`, `$ram`, dan `$prosesor`.
- Method: `tampilkanSpesifikasi()` yang mengembalikan deskripsi laptop tersebut.

**Soal A2**
Buat **2 Object laptop yang berbeda** (misalnya ASUS dan Lenovo), lalu tampilkan hasilnya (bisa dijalankan di onlinephp.io dan tunjukkan hasil outputnya).

**Soal A3 (Tantangan tambahan)**
Tambahkan method `hitungTotalHarga($diskon)` yang menghitung harga laptop setelah diskon, untuk melatih pemahaman kalian tentang method dengan parameter.

### Rubrik Penilaian Bagian A

| Aspek Penilaian | Skor 4 (Sangat Baik) | Skor 3 (Baik) | Skor 2 (Cukup) | Skor 1 (Perlu Bimbingan) |
|---|---|---|---|---|
| Struktur Class & Property | Class dan seluruh property benar & sesuai ketentuan | Class benar, 1 property kurang tepat | Class benar, lebih dari 1 property kurang tepat | Class tidak terbentuk dengan benar |
| Method & Logika | Method berjalan sempurna dan menghasilkan output sesuai | Method berjalan, output kurang lengkap | Method ada namun terdapat error kecil | Method tidak berhasil dijalankan |
| Object (Instansiasi) | 2 object dibuat dengan data berbeda & benar | 2 object dibuat, sedikit kesalahan data | Hanya 1 object berhasil dibuat | Belum berhasil membuat object |
| Kerapian & Penamaan Kode | Penamaan variabel/method jelas, indentasi rapi | Cukup rapi, ada sedikit inkonsistensi | Kurang rapi namun tetap terbaca | Tidak rapi dan sulit dibaca |

---

## 🅱️ BAGIAN B — Polymorphism, Abstract Class, Interface & Static

**Soal B1 (Polymorphism)**
Buat 3 class turunan dari `Produk` (misalnya `ProdukBuku`, `ProdukMainan`, `ProdukKosmetik`), masing-masing punya method `infoDiskon()` sendiri dengan aturan diskon yang berbeda-beda. Buat array berisi ketiga objek itu, lalu tampilkan semua diskonnya menggunakan **satu** `foreach` saja.

**Soal B2 (Abstract Class)**
Buat `abstract class Kendaraan` dengan method abstract `hitungBiayaSewa()`. Buat 2 class anak: `Motor` dan `Mobil`, masing-masing dengan rumus sewa yang berbeda. Coba juga uncomment/tuliskan baris `new Kendaraan()` untuk membuktikan pesan error yang muncul, lalu jelaskan errornya di komentar kode kalian.

**Soal B3 (Interface)**
Buat interface `BisaDicetak` dengan method `cetakLabel()`. Terapkan interface tersebut pada class `ProdukFisik`, tapi **jangan** diterapkan pada class `ProdukDigital` (karena produk digital tidak butuh label cetak). Tambahkan minimal satu interface lain jika ingin menunjukkan bahwa satu class bisa `implements` lebih dari satu interface.

**Soal B4 (Static)**
Tambahkan static property `$totalPendapatan` pada class `Produk`. Setiap kali produk "terjual" (buat method `jual($jumlah)`), tambahkan hasil penjualan ke `$totalPendapatan`. Tampilkan total pendapatan di akhir program menggunakan static method, misalnya `Produk::tampilkanTotalPendapatan()`.

### Rubrik Penilaian Bagian B

| Aspek Penilaian | Skor 4 (Sangat Baik) | Skor 3 (Baik) | Skor 2 (Cukup) | Skor 1 (Perlu Bimbingan) |
|---|---|---|---|---|
| Polymorphism (B1) | 3 class turunan + foreach tunggal berjalan sempurna | Berjalan, 1 class kurang sesuai konsep | Berjalan namun masih pakai if/else manual | Tidak menunjukkan polymorphism |
| Abstract Class (B2) | Abstract class, method abstract, dan bukti error lengkap & benar | Salah satu bagian kurang tepat | Class anak tidak lengkap mengisi method abstract | Konsep abstract tidak diterapkan |
| Interface (B3) | Interface benar, implements tepat sasaran (fisik vs digital) | Interface benar, penerapan kurang tepat di satu class | Interface dibuat tapi tidak sesuai konteks | Interface tidak berfungsi/error |
| Static (B4) | Static property & method benar, total pendapatan akurat | Berjalan, sedikit kesalahan perhitungan | Static digunakan tapi salah konsep (tercampur `$this`) | Static tidak berhasil diterapkan |

---

## 🅲 BAGIAN C — Refleksi Singkat

Jawab singkat (2-3 kalimat per poin), lampirkan bersama file kode kalian:

1. Apa perbedaan utama antara **Abstract Class** dan **Interface** menurut pemahaman kalian sendiri (bukan salinan dari modul)?
2. Menurut kalian, mengapa **static property** cocok dipakai untuk menghitung "total objek yang sudah dibuat", tetapi tidak cocok dipakai untuk menyimpan nama satu produk tertentu?
3. Sebutkan satu aplikasi (selain Gojek/Shopee) yang menurut kalian menerapkan konsep **Polymorphism**, dan jelaskan contohnya.

---

## 📌 Catatan Pengumpulan

- Format nama file: `Nama_Kelas_TugasPBO.php` (atau `.zip` jika lebih dari satu file).
- Sertakan screenshot output untuk **setiap** soal (A1–A3 dan B1–B4).
