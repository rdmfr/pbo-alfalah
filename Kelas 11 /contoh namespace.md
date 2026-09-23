# Memahami Namespace PHP

## Analogi Siswa dan Satpam

### Tujuan Pembelajaran

Setelah mempelajari materi ini, siswa diharapkan mampu:

1. Memahami konsep **Namespace** pada PHP.
2. Menjelaskan alasan penggunaan Namespace.
3. Membuat Namespace pada sebuah Class.
4. Memanggil Class menggunakan `use`.
5. Menggunakan **alias** dengan `use ... as ...`.
6. Memanggil Class menggunakan **Fully Qualified Name (FQN)**.

---

# 1. Apa Itu Namespace?

**Namespace** adalah fitur PHP yang digunakan untuk mengelompokkan Class, Interface, Function, dan Constant agar tidak terjadi konflik nama.

Bayangkan sebuah sekolah memiliki beberapa siswa yang memiliki nama sama.

Misalnya ada:

* Azka dari **MA Abu Amar**
* Azka dari **SMK As-Syifa**

Nama mereka sama-sama **Azka**, tetapi mereka berasal dari sekolah yang berbeda.

Dalam PHP, kita bisa menggunakan Namespace untuk membedakan keduanya.

### Analogi

| Dunia Nyata           | PHP                  |
| --------------------- | -------------------- |
| Nama sekolah          | Namespace            |
| Nama siswa            | Class                |
| Satpam                | File utama           |
| Memanggil siswa       | Membuat object       |
| Alamat lengkap siswa  | Fully Qualified Name |
| Nama panggilan khusus | Alias                |

Jadi:

```text
App\MA\Azka
App\SMK\Azka
```

Walaupun sama-sama memiliki Class bernama `Azka`, PHP dapat membedakannya karena Namespace-nya berbeda.

---

# 2. Struktur Folder

Kita akan membuat contoh project sederhana seperti berikut:

```text
sekolah_project/
│
├── src/
│   ├── MA/
│   │   └── Azka.php
│   │
│   └── SMK/
│       └── Azka.php
│
└── satpam.php
```

Keterangan:

* `sekolah_project/` → Root Folder atau folder utama project.
* `src/` → Tempat menyimpan Class.
* `MA/Azka.php` → Class `Azka` dari MA Abu Amar.
* `SMK/Azka.php` → Class `Azka` dari SMK As-Syifa.
* `satpam.php` → File utama yang memanggil kedua Class.

> Pada project PHP modern, pemanggilan file biasanya dibantu oleh **Composer Autoload**. Untuk mempermudah pembelajaran Namespace, contoh ini menggunakan `require_once`.

---

# 3. Membuat Class Azka dari MA

Buat file:

```text
src/MA/Azka.php
```

Isi file:

```php
<?php

namespace App\MA;

class Azka
{
    public function panggil()
    {
        return "Hadir Pak Satpam! Saya Azka dari MA Abu Amar.";
    }
}
```

Perhatikan bagian:

```php
namespace App\MA;
```

Kode tersebut memberikan identitas Namespace kepada Class `Azka`.

Secara sederhana:

```text
App\MA
   ↓
Nama Namespace

Azka
   ↓
Nama Class
```

Sehingga identitas lengkap Class tersebut adalah:

```text
App\MA\Azka
```

---

# 4. Membuat Class Azka dari SMK

Sekarang buat file:

```text
src/SMK/Azka.php
```

Isi:

```php
<?php

namespace App\SMK;

class Azka
{
    public function panggil()
    {
        return "Siap Pak Satpam! Saya Azka dari SMK As-Syifa.";
    }
}
```

Walaupun Class-nya juga bernama:

```php
class Azka
```

PHP tidak menganggapnya sebagai Class yang sama karena Namespace-nya berbeda.

Class pertama:

```text
App\MA\Azka
```

Class kedua:

```text
App\SMK\Azka
```

---

# 5. Memanggil Class dari File Utama

Sekarang kita buat:

```text
satpam.php
```

Pertama, kita harus memuat kedua file Class:

```php
<?php

require_once 'src/MA/Azka.php';
require_once 'src/SMK/Azka.php';
```

Setelah itu kita dapat menggunakan kedua Class tersebut.

---

# 6. Cara Pertama: Menggunakan Alias

Kita bisa memberikan nama panggilan khusus menggunakan:

```php
use ... as ...
```

Contoh:

```php
use App\MA\Azka as AzkaMA;
use App\SMK\Azka as AzkaSMK;
```

Sekarang:

```text
App\MA\Azka
       ↓
   AzkaMA

App\SMK\Azka
       ↓
   AzkaSMK
```

Kode lengkapnya:

```php
<?php

require_once 'src/MA/Azka.php';
require_once 'src/SMK/Azka.php';

use App\MA\Azka as AzkaMA;
use App\SMK\Azka as AzkaSMK;

$siswa1 = new AzkaMA();
$siswa2 = new AzkaSMK();

echo "Panggilan 1: " . $siswa1->panggil() . "<br>";
echo "Panggilan 2: " . $siswa2->panggil() . "<br>";
```

Output:

```text
Panggilan 1: Hadir Pak Satpam! Saya Azka dari MA Abu Amar.
Panggilan 2: Siap Pak Satpam! Saya Azka dari SMK As-Syifa.
```

### Analogi

Satpam mengatakan:

> "Azka dari MA, saya panggil AzkaMA."

dan:

> "Azka dari SMK, saya panggil AzkaSMK."

Alias membuat pemanggilan Class menjadi lebih mudah dan jelas.

---

# 7. Cara Kedua: Menggunakan Nama Lengkap

Selain menggunakan alias, kita juga dapat langsung menuliskan Namespace lengkap ketika membuat object.

Contoh:

```php
$siswa1 = new \App\MA\Azka();
$siswa2 = new \App\SMK\Azka();
```

Perhatikan tanda:

```text
\
```

di awal:

```php
\App\MA\Azka
```

Tanda tersebut menunjukkan bahwa kita menggunakan **Fully Qualified Name (FQN)** dari Namespace tersebut.

Contoh lengkap:

```php
<?php

require_once 'src/MA/Azka.php';
require_once 'src/SMK/Azka.php';

$siswa1 = new \App\MA\Azka();
$siswa2 = new \App\SMK\Azka();

echo "Panggilan 1: " . $siswa1->panggil() . "<br>";
echo "Panggilan 2: " . $siswa2->panggil() . "<br>";
```

Output:

```text
Panggilan 1: Hadir Pak Satpam! Saya Azka dari MA Abu Amar.
Panggilan 2: Siap Pak Satpam! Saya Azka dari SMK As-Syifa.
```

---

# 8. Mengapa Namespace Dibutuhkan?

Tanpa Namespace, kita akan memiliki dua Class:

```php
class Azka
{
    // ...
}
```

dan:

```php
class Azka
{
    // ...
}
```

Jika kedua Class tersebut dimuat dalam satu program, PHP akan mengalami konflik karena terdapat dua Class dengan nama yang sama.

PHP dapat memberikan error seperti:

```text
Fatal error: Cannot declare class Azka,
because the name is already in use
```

Namespace menyelesaikan masalah tersebut dengan memberikan identitas tambahan.

Tanpa Namespace:

```text
Azka
Azka
```

Dengan Namespace:

```text
App\MA\Azka
App\SMK\Azka
```

Sekarang PHP dapat membedakannya.

---

# 9. Analogi Satpam dan Siswa

Bayangkan satpam sekolah sedang memanggil siswa.

Ada dua siswa:

```text
Azka — MA Abu Amar
Azka — SMK As-Syifa
```

Jika satpam hanya berteriak:

> "Azka!"

Maka bisa terjadi kebingungan.

Tetapi jika satpam mengatakan:

> "Azka dari MA Abu Amar!"

atau:

> "Azka dari SMK As-Syifa!"

maka identitas siswa menjadi jelas.

Konsep yang sama digunakan oleh Namespace.

### Tanpa Namespace

```text
Azka
Azka
```

PHP kesulitan membedakan.

### Dengan Namespace

```text
App\MA\Azka
App\SMK\Azka
```

PHP dapat membedakan kedua Class tersebut.

---

# 10. Perbedaan `use` dan `use ... as ...`

## Menggunakan `use`

Jika tidak ada konflik nama, kita cukup menggunakan:

```php
use App\MA\Azka;

$siswa = new Azka();
```

Artinya kita mengimpor Class:

```text
App\MA\Azka
```

sehingga cukup menulis:

```php
Azka
```

---

## Menggunakan `use ... as ...`

Jika terdapat dua Class dengan nama yang sama, kita dapat menggunakan alias:

```php
use App\MA\Azka as AzkaMA;
use App\SMK\Azka as AzkaSMK;
```

Kemudian:

```php
$siswa1 = new AzkaMA();
$siswa2 = new AzkaSMK();
```

Alias sangat berguna ketika terdapat nama Class yang sama dari Namespace yang berbeda.

---

# 11. Contoh Lengkap

Berikut seluruh project:

```text
sekolah_project/
│
├── src/
│   ├── MA/
│   │   └── Azka.php
│   │
│   └── SMK/
│       └── Azka.php
│
└── satpam.php
```

### `src/MA/Azka.php`

```php
<?php

namespace App\MA;

class Azka
{
    public function panggil()
    {
        return "Hadir Pak Satpam! Saya Azka dari MA Abu Amar.";
    }
}
```

### `src/SMK/Azka.php`

```php
<?php

namespace App\SMK;

class Azka
{
    public function panggil()
    {
        return "Siap Pak Satpam! Saya Azka dari SMK As-Syifa.";
    }
}
```

### `satpam.php`

```php
<?php

require_once 'src/MA/Azka.php';
require_once 'src/SMK/Azka.php';

use App\MA\Azka as AzkaMA;
use App\SMK\Azka as AzkaSMK;

$siswa1 = new AzkaMA();
$siswa2 = new AzkaSMK();

echo "Panggilan 1: " . $siswa1->panggil() . "<br>";
echo "Panggilan 2: " . $siswa2->panggil() . "<br>";

echo "<hr>";

$siswa3 = new \App\MA\Azka();
$siswa4 = new \App\SMK\Azka();

echo "Panggilan 3: " . $siswa3->panggil() . "<br>";
echo "Panggilan 4: " . $siswa4->panggil() . "<br>";
```

---

# 12. Namespace pada Framework

Konsep Namespace tidak hanya digunakan pada PHP murni.

Framework seperti **Laravel** juga sangat banyak menggunakan Namespace.

Contohnya:

```php
namespace App\Models;

class User
{
    // ...
}
```

Kemudian Class tersebut dapat digunakan di file lain:

```php
use App\Models\User;

$user = new User();
```

Dalam Laravel, struktur folder dan Namespace biasanya saling berhubungan.

Contoh:

```text
app/
└── Models/
    └── User.php
```

dengan:

```php
namespace App\Models;

class User
{
}
```

Sehingga identitas lengkap Class tersebut adalah:

```text
App\Models\User
```

---

# 13. Intisari

Namespace dapat dianggap sebagai **alamat atau identitas tambahan sebuah Class**.

Jika terdapat dua Class dengan nama yang sama, Namespace dapat membedakan keduanya.

Contoh:

```text
App\MA\Azka
App\SMK\Azka
```

Keduanya sama-sama bernama `Azka`, tetapi memiliki Namespace berbeda.

Untuk memanggilnya kita dapat menggunakan:

### `use`

```php
use App\MA\Azka;
```

### Alias

```php
use App\MA\Azka as AzkaMA;
```

### Fully Qualified Name

```php
new \App\MA\Azka();
```

**Kesimpulan sederhana:**

> Namespace adalah cara PHP memberikan "alamat" kepada Class agar Class dengan nama yang sama dapat hidup dalam kelompok yang berbeda tanpa saling bertabrakan.

---

# Latihan

## Latihan 1

Buat dua Class dengan nama:

```text
Guru
```

dengan Namespace:

```text
App\MA
App\SMK
```

Masing-masing Class memiliki method:

```php
public function mengajar()
```

yang mengembalikan pesan berbeda.

Kemudian panggil kedua Class tersebut dari:

```text
satpam.php
```

menggunakan alias.

---

## Latihan 2

Buat struktur:

```text
sekolah_project/
│
├── src/
│   ├── MA/
│   │   └── Guru.php
│   │
│   └── SMK/
│       └── Guru.php
│
└── satpam.php
```

Gunakan:

```php
use App\MA\Guru as GuruMA;
use App\SMK\Guru as GuruSMK;
```

Kemudian buat object:

```php
$guru1 = new GuruMA();
$guru2 = new GuruSMK();
```

---

## Pertanyaan Pemahaman

1. Apa fungsi Namespace pada PHP?

2. Mengapa dua Class dengan nama `Azka` dapat digunakan jika Namespace-nya berbeda?

3. Apa fungsi keyword `use`?

4. Apa fungsi `as` pada:

   ```php
   use App\MA\Azka as AzkaMA;
   ```

5. Apa yang dimaksud dengan Fully Qualified Name?

6. Apa perbedaan:

   ```php
   new AzkaMA();
   ```

   dengan:

   ```php
   new \App\MA\Azka();
   ```

7. Mengapa Framework seperti Laravel banyak menggunakan Namespace?
