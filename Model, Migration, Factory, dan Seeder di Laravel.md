# Model, Migration, Factory, dan Seeder di Laravel

Di dalam Laravel, **Model**, **Migration**, **Factory**, dan **Seeder** adalah empat pilar utama untuk mengelola basis data (database). Bayangkan keempat komponen ini seperti proses membangun dan mengisi sebuah toko:

| Komponen | Analogi Sederhana | Peran Utama |
|---|---|---|
| **Migration** | Cetak biru / Desain Bangunan | Membuat struktur tabel (kolom, tipe data). |
| **Model** | Pengelola / Manajer Toko | Menjadi perantara antara logika kodingan dan data di tabel. |
| **Factory** | Mesin Pabrik Barang Contoh | Membuat pola/pabrik data palsu secara otomatis. |
| **Seeder** | Kurir / Staf Pengisi Barang | Memasukkan data awal atau data testing ke database. |

## 💡 Cara Pintas Membuat Keempatnya Sekaligus

Sebagaimana developer Laravel pada umumnya, kamu bisa membuat Model, Migration, Factory, dan Seeder sekaligus hanya dengan satu perintah Artisan:

```bash
php artisan make:model Product -mfs
```

Keterangan flag: `-m` (migration), `-f` (factory), `-s` (seeder).

---

## 📍 Ringkasan Lokasi Folder & Nama File

| Komponen | Lokasi Folder | Nama File (Contoh) |
|---|---|---|
| Migration | `database/migrations/` | `YYYY_MM_DD_HHMMSS_create_products_table.php` |
| Model | `app/Models/` | `Product.php` |
| Factory | `database/factories/` | `ProductFactory.php` |
| Seeder | `database/seeders/` | `ProductSeeder.php` & `DatabaseSeeder.php` |

---

## 1. Migration (Cetak Biru Tabel Database)

- **Folder:** `database/migrations/`
- **Nama file:** otomatis dibentuk dengan timestamp di depannya.
  Contoh: `2026_08_04_100000_create_products_table.php`
- **Cara membuat manual:**
  ```bash
  php artisan make:migration create_products_table
  ```

Migration adalah kontrol versi (*version control*) untuk database. Kamu tidak perlu membuka phpMyAdmin secara manual untuk membuat tabel. Di dalamnya terdapat fungsi `up()` yang akan dieksekusi saat kamu menjalankan `php artisan migrate`.

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    // Method up() dipanggil saat kita menjalankan: php artisan migrate
    public function up(): void
    {
        // Schema::create digunakan untuk membuat tabel baru di database dengan nama 'products'
        Schema::create('products', function (Blueprint $table) {

            // $table->id() membuat kolom 'id' sebagai Primary Key bertipe Auto Increment
            $table->id();

            // $table->string('name') membuat kolom 'name' bertipe VARCHAR (teks pendek)
            $table->string('name');

            // $table->integer('price') membuat kolom 'price' bertipe angka/bilangan bulat
            $table->integer('price');

            // $table->timestamps() otomatis membuat 2 kolom sekaligus:
            // 1. 'created_at' (mencatat waktu data dibuat)
            // 2. 'updated_at' (mencatat waktu data terakhir diubah)
            $table->timestamps();
        });
    }

    // Method down() dipanggil saat kita membatalkan migration (php artisan migrate:rollback)
    public function down(): void
    {
        // Menghapus tabel 'products' jika tabel tersebut ada
        Schema::dropIfExists('products');
    }
};
```

Jalankan perintah ini di terminal untuk menerapkan struktur ke database:

```bash
php artisan migrate
```

---

## 2. Model (Perantara Logika & Database)

- **Folder:** `app/Models/`
- **Nama file:** menggunakan huruf kapital di awal dan bentuk tunggal (*singular*).
  Contoh: `Product.php` (bukan `Products.php`)
- **Cara membuat manual:**
  ```bash
  php artisan make:model Product
  ```

Model menggunakan Eloquent ORM untuk berinteraksi dengan database. Secara default, model `Product` akan otomatis terhubung ke tabel `products` (bentuk jamak). Model adalah tempat kamu mendefinisikan aturan bagaimana kodingan PHP milikmu berinteraksi dengan tabel `products`.

```php
<?php

namespace App\Models;

// Mengimpor trait HasFactory agar Model ini bisa menggunakan Factory nantinya
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Product extends Model
{
    // Mengaktifkan fitur Factory untuk model Product ini
    use HasFactory;

    // $fillable berfungsi sebagai pengaman (whitelist).
    // Hanya kolom yang dicantumkan di dalam array ini yang BOLEH diisi secara massal (mass assignment).
    // Ini mencegah peretas/user jahat menyisipkan data ke kolom yang sensitif.
    protected $fillable = [
        'name',  // Mengizinkan kolom 'name' diisi
        'price', // Mengizinkan kolom 'price' diisi
    ];
}
```

---

## 3. Factory (Pabrik Pembuat Data Palsu)

- **Folder:** `database/factories/`
- **Nama file:** nama Model diikuti kata `Factory`.
  Contoh: `ProductFactory.php`
- **Cara membuat manual:**
  ```bash
  php artisan make:factory ProductFactory
  ```

Factory digunakan untuk mendefinisikan seperti apa bentuk data buatan/palsu (*dummy data*) yang ingin dibuat menggunakan bantuan library **Faker**.

```php
<?php

namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;

class ProductFactory extends Factory
{
    // Method definition() berisi resep/aturan pembuatan data acak
    public function definition(): array
    {
        return [
            // $this->faker->words(2, true) akan menghasilkan 2 kata acak berbentuk string
            // Contoh hasil: "Kopi Hitam" atau "Sepatu Lari"
            'name' => $this->faker->words(2, true),

            // $this->faker->numberBetween(10000, 500000) menghasilkan angka acak di rentang tersebut
            // Contoh hasil: 25000 atau 150000
            'price' => $this->faker->numberBetween(10000, 500000),
        ];
    }
}
```

---

## 4. Seeder (Pengisi Data ke Database)

- **Folder:** `database/seeders/`
- **Nama file:** nama Model diikuti kata `Seeder` (serta file bawaan `DatabaseSeeder.php`).
  Contoh: `ProductSeeder.php`
- **Cara membuat manual:**
  ```bash
  php artisan make:seeder ProductSeeder
  ```

Seeder bertugas menjalankan perintah untuk memasukkan data ke database, baik data tetap (seperti data admin) maupun data tes yang diambil dari Factory. Di sini kita menentukan berapa banyak data yang ingin dibuat berdasarkan resep dari Factory.

**File A: `ProductSeeder.php`**

```php
<?php

namespace Database\Seeders;

use App\Models\Product; // Mengimpor Model Product
use Illuminate\Database\Seeder;

class ProductSeeder extends Seeder
{
    // Method run() berisi perintah pengisian data yang akan dieksekusi
    public function run(): void
    {
        // Perintah ini memerintahkan Model Product untuk menggunakan Factory-nya
        // dan membuat (create) sebanyak 50 baris data palsu sekaligus ke dalam database.
        Product::factory(50)->create();
    }
}
```

**File B: `DatabaseSeeder.php` (Seeder Utama)**

File ini adalah saklar utama. Saat kamu mengetik `php artisan db:seed`, Laravel akan menjalankan file ini terlebih dahulu.

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    public function run(): void
    {
        // Memanggil Seeder lain agar ikut dijalankan
        // Kamu bisa mendaftarkan banyak Seeder di dalam array ini
        $this->call([
            ProductSeeder::class, // Menjalankan ProductSeeder
        ]);
    }
}
```

Eksekusi seeder dengan terminal:

```bash
php artisan db:seed
```

---

## 🚀 Ringkasan Cara Pakai untuk Pemula

Ingat urutan mengeksekusi perintah di terminal ini saat kamu mencoba dari awal:

1. **Buat file sekaligus:**
   ```bash
   php artisan make:model Product -mfs
   ```
2. Ketik kodingan di migration, model, factory, dan seeder seperti penjelasan di atas.
3. **Jalankan struktur tabel ke database:**
   ```bash
   php artisan migrate
   ```
4. **Isi database dengan data palsu:**
   ```bash
   php artisan db:seed
   ```

## 🔄 Alur Kerja Lengkap (Cheat Sheet)

Jika kamu ingin mengulang/reset seluruh database dari awal dan langsung mengisinya dengan data dummy:

```bash
php artisan migrate:fresh --seed
```

Perintah di atas akan menghapus semua tabel, membuat ulang tabel dari migration, dan menjalankan seeder secara otomatis.

---

## Topik Berikutnya yang Bisa Dipelajari

- Cara menampilkan data Product dari database ke layar/view
- Cara membuat data manual (tanpa Factory) di Seeder
