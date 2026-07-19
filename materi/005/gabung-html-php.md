# Menggabungkan PHP dengan HTML dan CSS

Saat membuat sebuah website, kita tidak hanya membutuhkan tampilan yang menarik, tetapi juga kemampuan untuk mengolah data. Di sinilah peran HTML, CSS, dan PHP saling melengkapi. Ketika ketiga teknologi tersebut digabungkan, kita dapat membuat halaman web yang tidak hanya menarik secara visual tetapi juga mampu menampilkan informasi sesuai kebutuhan pengguna.

Sebagai contoh, sebuah website sekolah dapat menampilkan nama siswa yang diambil dari database menggunakan PHP, sementara HTML menyusun tampilannya dan CSS membuat tampilannya lebih menarik.

## Hubungan HTML, CSS, dan PHP

Sebelum belajar menggabungkannya, pahami terlebih dahulu fungsi masing-masing.

<table><tbody><tr><td><strong>Teknologi</strong></td><td><strong>Fungsi</strong></td></tr><tr><td>HTML</td><td>Membuat struktur halaman</td></tr><tr><td>CSS</td><td>Mengatur tampilan halaman</td></tr><tr><td>PHP</td><td>Mengolah data dan membuat halaman menjadi dinamis</td></tr></tbody></table>

Ilustrasinya dapat dianalogikan seperti membangun rumah.

- HTML adalah kerangka rumah.
- CSS adalah cat dan dekorasi rumah.
- PHP adalah penghuni yang membuat rumah tersebut hidup.

Ketiganya bekerja bersama agar website menjadi lengkap.

## Cara Kerja PHP Bersama HTML

Berbeda dengan HTML yang langsung dibaca oleh browser, PHP akan diproses terlebih dahulu oleh web server.

Alurnya adalah sebagai berikut:

```
Browser
    │
    ▼
Web Server
    │
PHP diproses
    │
    ▼
Menghasilkan HTML
    │
    ▼
Browser menampilkan halaman
```

Artinya, browser **tidak pernah melihat kode PHP**, melainkan hanya hasil akhirnya berupa HTML.

## Menuliskan PHP di Dalam HTML

PHP ditulis menggunakan tag:

```php
<?php
    // kode PHP
?>
```

Tag tersebut dapat ditempatkan di mana saja di dalam dokumen HTML.

Contoh:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Belajar PHP</title>
  </head>
  <body>
    <h1>Belajar PHP</h1>

    <h2><?php echo "Selamat Datang"; ?></h2>

    <?php echo "Halo World!"; ?>
  </body>
</html>
```

### **Menampilkan Variabel PHP di HTML**

Misalkan kita memiliki variabel.

```php
<?php
$nama = "Andi";
?>

<h2>Halo, <?php echo $nama; ?></h2>
```

### **Sintaks Singkat PHP**

Selain menggunakan:

```php
<?php echo $nama; ?>
```

PHP juga memiliki sintaks singkat:

```php
<?= $nama ?>
```

Contoh:

```php
<?php
$kelas = "XI PPLG";
?>

<p>Kelas: <?= $kelas ?></p>
```

## Menggabungkan HTML dengan Percabangan atau Perulangan PHP

PHP dapat menentukan apakah suatu elemen HTML akan ditampilkan atau tidak.

Contoh:

```php
<?php
$login = true;
?>

<?php if($login){ ?>

<h2>Selamat datang!</h2>

<?php } ?>
```

PHP juga dapat membuat HTML secara otomatis menggunakan perulangan.

Contoh:

```php
<ul>

<?php
for($i=1; $i<=5; $i++){
?>

<li>Data ke-<?= $i ?></li>

<?php
}
?>

</ul>
```

## Kesalahan yang Sering Terjadi

<table><tbody><tr><td><strong>Kesalahan</strong></td><td><strong>Penyebab</strong></td><td><strong>Solusi</strong></td></tr><tr><td>PHP tidak berjalan</td><td>File disimpan sebagai <code>.html</code></td><td>Gunakan ekstensi <code>.php</code></td></tr><tr><td>Kode PHP muncul di browser</td><td>File dibuka langsung tanpa web server</td><td>Jalankan melalui Apache/Laragon</td></tr><tr><td>Halaman kosong</td><td>Ada kesalahan sintaks PHP</td><td>Periksa pesan error dan tanda titik koma (<code>;</code>)</td></tr></tbody></table>

Menguasai cara menggabungkan PHP dengan HTML dan CSS merupakan langkah penting bagi peserta didik yang ingin mengembangkan aplikasi web yang dinamis. Kemampuan ini memungkinkan sebuah halaman web tidak hanya memiliki tampilan yang menarik, tetapi juga mampu menampilkan informasi yang berubah sesuai kebutuhan pengguna. Dengan memahami bagaimana PHP menghasilkan konten, HTML menyusun struktur, dan CSS memperindah tampilannya, peserta didik telah memiliki dasar yang kuat dalam pengembangan aplikasi web.

---

# [Praktikum](latihan-praktikum.md)
