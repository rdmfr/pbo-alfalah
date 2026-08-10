# Menampilkan Data ke View & Membuat Data Manual di Seeder
### Lanjutan Materi Laravel — Kelas XII RPL/PPLG

> Materi ini melanjutkan materi **Model, Migration, Factory, dan Seeder** yang sudah dipelajari sebelumnya. Sekarang setelah tabel `products` sudah punya data (hasil `php artisan db:seed`), langkah selanjutnya adalah **menampilkan data itu ke layar (browser)**, dan belajar mengisi data **secara manual** di Seeder (tanpa Factory) — misalnya untuk data admin/kategori yang nilainya harus tetap, bukan acak.

---

## 0. Analogi Dulu Sebelum Ngoding

Bayangkan sebuah **restoran**:

| Komponen | Analogi | Peran |
|---|---|---|
| **Model** (`Product`) | Dapur & bahan mentah | Tempat data "mentah" disimpan dan diolah |
| **Controller** | Koki | Mengambil data dari dapur (Model), lalu menyiapkannya untuk disajikan |
| **Route** | Nomor meja / pintu masuk | Menentukan alamat URL mana yang memanggil koki yang mana |
| **View (Blade)** | Piring saji di meja pelanggan | Tempat data ditampilkan rapi ke pelanggan (user) |

Jadi alurnya: **Pelanggan datang lewat pintu (Route) → Koki (Controller) ambil bahan dari dapur (Model) → disajikan di piring (View)**.

Untuk **Seeder manual**, bayangkan kamu tidak selalu butuh "mesin pabrik" (Factory) yang membuat barang acak. Kadang kamu butuh menaruh **barang spesifik** sendiri dengan tangan — misalnya kategori tetap seperti "Makanan", "Minuman", "Snack" yang tidak boleh acak namanya.

---

## 1. Menampilkan Data Product ke View

### Langkah-Langkah

1. **Buat Controller** untuk mengambil data dari Model.
2. **Daftarkan Route** yang mengarah ke Controller tersebut.
3. **Buat file View (Blade)** untuk menampilkan data.
4. **Uji coba** di browser.

### 1.1 Membuat Controller

Buat Controller lewat Artisan:

```
php artisan make:controller ProductController
```

**Lokasi folder:** `app/Http/Controllers/`
**Nama file:** `ProductController.php`

```php
<?php

namespace App\Http\Controllers;

use App\Models\Product; // Mengimpor Model Product agar bisa diakses di sini

class ProductController extends Controller
{
    // Method index() akan dipanggil saat halaman daftar produk dibuka
    public function index()
    {
        // Product::all() mengambil SEMUA baris data dari tabel 'products'
        // Hasilnya berbentuk Collection (mirip array, tapi lebih canggih)
        $products = Product::all();

        // view('products.index', ...) artinya:
        // "Tampilkan file resources/views/products/index.blade.php"
        // Data $products dikirim ke view dengan nama variabel 'products'
        return view('products.index', [
            'products' => $products
        ]);
    }
}
```

> 💡 **Kenapa `Product::all()` bisa langsung dipakai?** Karena `Product` sudah `extends Model` (dari materi sebelumnya), sehingga otomatis mewarisi kemampuan Eloquent ORM untuk mengambil data — kamu tidak perlu menulis query SQL manual.

### 1.2 Mendaftarkan Route

**Lokasi file:** `routes/web.php`

```php
<?php

use App\Http\Controllers\ProductController;
use Illuminate\Support\Facades\Route;

// Ketika user membuka alamat: http://nama-project.test/products
// Laravel akan memanggil method index() di dalam ProductController
Route::get('/products', [ProductController::class, 'index']);
```

### 1.3 Membuat View (Blade Template)

**Lokasi folder:** `resources/views/products/`
**Nama file:** `index.blade.php`

```blade
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Daftar Produk</title>
</head>
<body>

    <h1>Daftar Produk</h1>

    <table border="1" cellpadding="8">
        <tr>
            <th>Nama Produk</th>
            <th>Harga</th>
        </tr>

        {{-- @foreach mengulang setiap data di dalam $products satu per satu --}}
        @foreach ($products as $product)
            <tr>
                {{-- {{ }} adalah cara Blade menampilkan nilai variabel ke HTML --}}
                <td>{{ $product->name }}</td>
                <td>Rp{{ number_format($product->price, 0, ',', '.') }}</td>
            </tr>
        @endforeach
    </table>

</body>
</html>
```

### 🧪 Coba Sendiri (Praktik 1)

1. Pastikan tabel `products` sudah terisi data (jalankan `php artisan db:seed` kalau belum).
2. Buat Controller, Route, dan View persis seperti di atas.
3. Jalankan server lokal: `php artisan serve`
4. Buka browser ke `http://127.0.0.1:8000/products`
5. **Cek keberhasilan:** kalau tabel HTML muncul berisi 50 baris data produk (nama + harga terformat rupiah), berarti alur Controller → Model → View sudah berhasil.
6. **Tantangan kecil:** ubah `Product::all()` menjadi `Product::orderBy('price', 'desc')->get();` lalu refresh halaman. Kalau urutan harga berubah dari termahal ke termurah, berarti kamu sudah paham cara mengurutkan data dari Model.
7. **Kalau halaman blank/error:** cek pesan error di browser — biasanya karena nama file view salah folder, atau lupa `use App\Models\Product;` di Controller.

---

## 2. Membuat Data Manual di Seeder (Tanpa Factory)

Factory cocok untuk data **acak dalam jumlah banyak** (misal 50 produk testing). Tapi kadang kamu butuh data **tetap/pasti**, seperti akun admin, kategori baku, atau beberapa produk contoh yang namanya sudah kamu tentukan sendiri — bukan hasil acakan Faker.

### Contoh: Seeder Manual untuk Kategori

Misalnya kita ingin menambahkan kolom `category` yang isinya harus tetap: "Makanan", "Minuman", "Snack" — bukan kata acak.

**Lokasi file:** `database/seeders/ProductSeeder.php`

```php
<?php

namespace Database\Seeders;

use App\Models\Product; // Mengimpor Model Product
use Illuminate\Database\Seeder;

class ProductSeeder extends Seeder
{
    public function run(): void
    {
        // ==========================================
        // BAGIAN 1: DATA MANUAL (Tanpa Factory)
        // ==========================================
        // Cocok untuk data yang nilainya HARUS pasti/tetap, bukan acak.
        // Product::create() akan langsung memasukkan 1 baris data ke database.

        Product::create([
            'name'  => 'Nasi Goreng Spesial',
            'price' => 25000,
        ]);

        Product::create([
            'name'  => 'Es Teh Manis',
            'price' => 5000,
        ]);

        Product::create([
            'name'  => 'Kentang Goreng',
            'price' => 15000,
        ]);

        // ==========================================
        // BAGIAN 2: DATA ACAK (Pakai Factory)
        // ==========================================
        // Cocok untuk data testing dalam jumlah banyak yang isinya bebas/acak.
        Product::factory(20)->create();
    }
}
```

> ⚠️ **Perhatikan:** kamu boleh menggabungkan data manual dan data Factory di dalam **satu Seeder yang sama**, seperti contoh di atas — data pasti (misalnya 3 menu andalan) ditulis manual, sisanya (20 data testing) tetap dibuat otomatis lewat Factory.

### Jalankan Ulang Seeder

Karena `id` di tabel `products` bertipe auto-increment dan kemungkinan sudah terisi dari percobaan sebelumnya, sebaiknya reset dulu database sebelum mengisi ulang:

```
php artisan migrate:fresh --seed
```

Perintah ini akan menghapus semua tabel, membuat ulang strukturnya dari Migration, lalu langsung menjalankan Seeder (baik data manual maupun data Factory).

### 🧪 Coba Sendiri (Praktik 2)

1. Tambahkan 3 data manual seperti contoh di atas ke dalam `ProductSeeder.php` milikmu.
2. Jalankan `php artisan migrate:fresh --seed`.
3. Buka lagi `http://127.0.0.1:8000/products` di browser.
4. **Cek keberhasilan:** pastikan 3 nama produk manual yang kamu tulis (misalnya "Nasi Goreng Spesial") muncul persis sesuai yang kamu ketik — **tidak boleh berubah/acak** — sedangkan sisa data lainnya tetap acak hasil Factory.
5. **Tantangan kecil:** tambahkan 2 data manual lagi dengan nama & harga buatanmu sendiri, lalu buktikan keduanya muncul di halaman `/products` setelah `migrate:fresh --seed` dijalankan ulang.

---

## 3. Ringkasan Alur Kerja Lengkap (Cheat Sheet)

```
1. php artisan make:controller ProductController   → buat "koki"
2. Daftarkan Route di routes/web.php                → buat "pintu masuk"
3. Buat file Blade di resources/views/products/     → buat "piring saji"
4. Isi ProductSeeder.php dengan data manual + Factory
5. php artisan migrate:fresh --seed                 → reset & isi ulang database
6. php artisan serve → buka /products di browser     → cek hasil tampilan
```

---

## ✅ Checklist Sebelum Mengumpulkan Tugas

- [ ] Controller berhasil mengambil data dengan `Product::all()` (atau variasi query lain).
- [ ] Route mengarah ke method yang benar di Controller.
- [ ] View menampilkan data dalam bentuk tabel HTML menggunakan `@foreach`.
- [ ] Seeder berisi **kombinasi** data manual (`Product::create()`) dan data Factory (`Product::factory(n)->create()`).
- [ ] Setelah `php artisan migrate:fresh --seed`, data manual muncul persis sesuai yang ditulis di kode (tidak acak).
- [ ] Halaman `/products` bisa dibuka tanpa error dan menampilkan harga dalam format rupiah yang rapi.

---

## Topik Berikutnya yang Bisa Dipelajari

- Menampilkan **detail 1 produk** (Route dengan parameter `{id}`, misalnya `/products/1`)
- Membuat **form tambah produk** dari browser (Create) menggunakan `<form>` dan Controller `store()`
- **Update** dan **Delete** data produk langsung dari tampilan web (melengkapi konsep CRUD)
