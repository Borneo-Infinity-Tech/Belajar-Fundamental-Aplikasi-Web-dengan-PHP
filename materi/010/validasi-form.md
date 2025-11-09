# Validasi Form, Menangani Error, dan Pesan Validasi pada PHP

Dalam pembuatan aplikasi web, form digunakan untuk menerima data dari pengguna — seperti nama, email, atau password. Namun, tidak semua pengguna akan mengisi form dengan benar. Misalnya:

- Ada yang lupa mengisi kolom wajib.
- Ada yang memasukkan email dengan format salah.
- Ada yang mengetik angka di kolom nama.

Untuk mencegah hal tersebut, **validasi form** diperlukan agar data yang masuk ke sistem sudah sesuai dengan aturan yang ditentukan. Dengan validasi, aplikasi menjadi lebih aman dan data yang disimpan lebih terjamin kebenarannya.

## Apa Itu Validasi Form

**Validasi form** adalah proses untuk memeriksa apakah data yang diinput oleh pengguna sudah sesuai dengan ketentuan sebelum disimpan atau diproses lebih lanjut.

Contoh:

- Kolom nama tidak boleh kosong.
- Email harus memiliki format yang benar (misalnya: user@example.com).
- Password minimal 8 karakter.

Validasi bisa dilakukan di dua tempat:

1.  **Client-side** → menggunakan JavaScript (langsung di browser).
2.  **Server-side** → menggunakan PHP (saat data dikirim ke server).

> Validasi di PHP wajib dilakukan meskipun sudah ada validasi di JavaScript, karena data yang dikirim bisa dimanipulasi.

## Fungsi-Fungsi PHP untuk Validasi

Berikut penjelasan fungsi-fungsi PHP yang sering digunakan untuk melakukan validasi form:

### `empty()`

Fungsi ini digunakan untuk memeriksa apakah sebuah variabel kosong atau tidak. Biasanya digunakan untuk mengecek apakah kolom form diisi atau tidak.

```php
if (empty($nama)) {
    echo "Nama tidak boleh kosong!";
}
```

### `strlen()`

Digunakan untuk menghitung panjang string (jumlah karakter). Berguna untuk memeriksa panjang password, username, atau teks tertentu.

```php
if (strlen($password) < 8) {
    echo "Password minimal 8 karakter!";
}
```

### `filter_var()`

Fungsi ini digunakan untuk memeriksa format data, misalnya email, URL, atau angka.  
Contoh validasi email:

```php
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
    echo "Format email tidak valid!";
}
```

### `preg_match()`

Digunakan untuk mencocokkan pola teks menggunakan **regular expression (regex)**. Bisa digunakan untuk memastikan input hanya berisi angka atau huruf tertentu.

```php
if (!preg_match("/^[0-9]+$/", $telepon)) {
    echo "Nomor telepon hanya boleh berisi angka!";
}
```

### `trim()`

Fungsi ini menghapus spasi di awal dan akhir input pengguna. Berguna agar input tetap bersih.

```php
$nama = trim($_POST['nama']);
```

### `htmlspecialchars()`

Fungsi ini mengubah karakter khusus seperti `<`, `>`, dan `&` menjadi teks biasa.  
Berguna untuk **mencegah serangan XSS** (Cross Site Scripting).

```php
$nama = htmlspecialchars($_POST['nama']);
```

## Contoh Form HTML

Berikut contoh form sederhana yang akan divalidasi menggunakan PHP:

```html
<form method="POST" action="">
  Nama: <input type="text" name="nama" /><br /><br />
  Email: <input type="text" name="email" /><br /><br />
  Password: <input type="password" name="password" /><br /><br />
  No. Telepon: <input type="text" name="telepon" /><br /><br />
  <input type="submit" name="submit" value="Kirim" />
</form>
```

## Contoh Penerapan Validasi di PHP

Berikut contoh penerapan semua fungsi validasi di PHP:

```php
<?php

if ($_SERVER["REQUEST_METHOD"] === "POST") {
    $nama = trim($_POST['nama']);
    $email = trim($_POST['email']);
    $password = trim($_POST['password']);
    $telepon = trim($_POST['telepon']);
    $error = [];

    // Validasi nama
    if (empty($nama)) {
        $error[] = "Nama wajib diisi.";
    }

    // Validasi email
    if (empty($email)) {
        $error[] = "Email wajib diisi.";
    } elseif (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $error[] = "Format email tidak valid.";
    }

    // Validasi password
    if (strlen($password) < 8) {
        $error[] = "Password minimal 8 karakter.";
    }

    // Validasi nomor telepon
    if (!preg_match("/^[0-9]+$/", $telepon)) {
        $error[] = "Nomor telepon hanya boleh berisi angka.";
    }

    // Tampilkan hasil
    if (count($error) > 0) {
        foreach ($error as $err) {
            echo "<p style='color:red;'>$err</p>";
        }
    } else {
        echo "<p style='color:green;'>Data berhasil dikirim dan valid!</p>";
    }
}
?>
```

## Menampilkan pesan Error

Pesan error harus jelas agar pengguna tahu kesalahannya.

Contoh:

```
Nama wajib diisi.
Format email tidak valid.
Password minimal 8 karakter.
```

## Tips Validasi yang Baik

- Gunakan warna dan pesan yang ramah pengguna.
- Jangan hanya validasi di sisi klien (JavaScript), lakukan juga di **server (PHP)**.
- Gunakan fungsi bawaan PHP agar validasi aman dan efisien.
- Bersihkan semua input sebelum disimpan ke database.

---

Validasi form merupakan bagian penting dalam pengembangan web.  
Dengan memahami fungsi-fungsi seperti `empty()`, `filter_var()`, `preg_match()`, dan `htmlspecialchars()`, kita bisa membuat aplikasi yang **aman, bersih, dan nyaman digunakan**. Selalu lakukan validasi di sisi server agar data yang diterima **terjamin kebenarannya dan terhindar dari serangan berbahaya**. Validasi yang baik bukan hanya menjaga keamanan, tapi juga membantu pengguna mengisi data dengan benar.
