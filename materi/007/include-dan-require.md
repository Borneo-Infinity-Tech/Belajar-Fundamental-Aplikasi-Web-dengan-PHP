# Reusable Components dengan include dan require pada PHP

Dalam pengembangan aplikasi web menggunakan PHP, sering kali kita menulis kode yang **berulang**, seperti header, footer, menu navigasi, atau konfigurasi database. Jika kode tersebut ditulis berulang di setiap file, maka akan menyulitkan perawatan dan pengembangan aplikasi. Adapun cara mengatasi hal tersebut, PHP menyediakan fitur **Reusable Components** menggunakan `include` dan `require`. Dengan cara ini, kita dapat **menyimpan kode dalam satu file** dan **menggunakannya kembali** di banyak halaman.

## Pengertian `include` dan `require`

### `include`

`include` digunakan untuk **memasukkan isi file PHP lain** ke dalam file yang sedang dijalankan.

```php
include 'header.php';
```

Jika file yang di-`include` **tidak ditemukan**, PHP akan:

- Menampilkan **peringatan (warning)**
- **Script tetap berjalan**

### `required`

`require` juga digunakan untuk memasukkan file lain, namun bersifat **wajib**.

```php
require 'config.php';
```

Jika file yang di-`require` **tidak ditemukan**, PHP akan:

- Menampilkan **fatal error**
- **Script berhenti dijalankan**

## Perbedaan `include` dan `require`

<table><tbody><tr><td><strong>Aspek</strong></td><td><code>include</code></td><td><code>require</code></td></tr><tr><td>Jika file tidak ada</td><td>Warning</td><td>Fatal Error</td></tr><tr><td>Script tetap jalan</td><td>✅ Ya</td><td>❌ Tidak</td></tr><tr><td>Cocok untuk</td><td>Komponen tambahan</td><td>File penting</td></tr></tbody></table>

---

## Pengertian Reusable Components

**Reusable Components** adalah teknik memisahkan bagian kode tertentu ke dalam file terpisah agar dapat digunakan kembali di banyak halaman.

Contoh komponen yang sering dibuat reusable:

- Header
- Footer
- Sidebar
- Koneksi database
- Navigasi menu

### **Contoh Struktur Folder**

```
project/
│── index.php
│── about.php
│── header.php
│── footer.php
│── config.php
```

## Contoh Reusable Component: Header

File: `header.php`

```php
<!DOCTYPE html>
<html>
<head>
    <title>Website Saya</title>
</head>
<body>
    <h1>Selamat Datang di Website Saya</h1>
    <hr>
```

File: `footer.php`

```php
<hr>
<p>&copy; 2026 Website Saya</p>
</body>
</html>
```

File: `index.php`

```php
<?php
include 'header.php';
?>

<p>Ini adalah halaman utama.</p>

<?php
include 'footer.php';
?>
```

File: `about.php`

```php
<?php
include 'header.php';
?>

<p>Ini adalah halaman tentang kami.</p>

<?php
include 'footer.php';
?>
```

## Contoh `require` untuk File Penting

File: `connection.php`

```php
<?php
$host = "localhost";
$user = "root";
$password = "";
$database = "db_latihan";
?>
```

File: `index.php`

```php
<?php
require 'config.php';
?>
```

Jika `connection.php` tidak ada, aplikasi **tidak boleh berjalan**, sehingga `require` lebih aman digunakan.

## Best Practice Penggunaan

- Gunakan `**require**` untuk:
  - Konfigurasi database
  - File fungsi utama
- Gunakan `**include**` untuk:
  - Header
  - Footer
  - Sidebar
- Gunakan `include_once` / `require_once` untuk mencegah file dipanggil dua kali

```php
require_once 'connection.php';
```

Penggunaan **Reusable Components dengan** `**include**` **dan** `**require**` sangat penting dalam pengembangan aplikasi PHP. Teknik ini membuat kode:

- Lebih **rapi**
- Lebih **mudah dirawat**
- Lebih **efisien**
- Mudah dikembangkan di masa depan

Dengan memahami perbedaan dan fungsi `include` serta `require`, kita dapat menentukan kapan harus menggunakan masing-masing sesuai kebutuhan aplikasi. Reusable Components adalah langkah awal menuju penulisan kode PHP yang **profesional dan terstruktur**.
