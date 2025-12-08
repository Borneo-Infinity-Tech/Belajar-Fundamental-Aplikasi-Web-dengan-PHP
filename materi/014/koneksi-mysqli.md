# Menghubungkan PHP dengan MySQL menggunakan `mysqli`

Pada tahap sebelumnya, kalian sudah mempelajari berbagai perintah penting dalam `mysqli`. Namun, semua perintah tersebut tidak dapat digunakan jika PHP belum terhubung dengan database MySQL. Karena itu, materi kali ini akan fokus pada pemahaman dan implementasi koneksi database menggunakan fungsi inti yang bernama mysqli_connect. Memahami koneksi dengan benar sangat penting sebelum masuk ke penggunaan mysqli yang lebih kompleks.

## `mysqli_connect`

`mysqli_connect` adalah fungsi PHP yang digunakan untuk:

✔ Membuka koneksi ke server MySQL  
✔ Mengonfigurasi login ke database  
✔ Menentukan database mana yang akan digunakan  
✔ Menghasilkan _connection object_ yang dipakai oleh semua fungsi mysqli lainnya

Tanpa objek koneksi ini, seluruh fungsi `mysqli` tidak akan dapat dijalankan.

## Struktur Dasar Koneksi PHP ke MySQL

```php
mysqli_connect(host, username, password, database);
```

`mysqli_connect` mempunyai 4 parameter yaitu `host` sebagai alamat server, `username` nama pengguna untuk login ke MySQL, `password` yaitu password untuk login ke MySQL, dan `database` yaitu nama database yang digunakan.

**Contoh Kode Koneksi Dasar**

```php
<?php
$server   = "localhost";
$user     = "root";
$password = "";
$database = "db_sekolah";

// Mencoba membuat koneksi
$conn = mysqli_connect($server, $user, $password, $database);

// Mengecek apakah koneksi berhasil
if (!$conn) {
    die("Koneksi gagal: " . mysqli_connect_error());
}

echo "Koneksi ke database berhasil!";
?>
```

## Penjelasan Bagian-Bagian Kode

**a. Variabel server dan login**

```php
$server   = "localhost";
$user     = "root";
$password = "";
$database = "db_sekolah";
```

- **localhost** → server database (umumnya tidak berubah saat mengembangkan di komputer sendiri).
- **root** → username default MySQL.
- **password** → biasanya kosong untuk instalasi lokal.
- **db_sekolah** → nama database yang ingin digunakan.

**b. Membuat koneksi**

```php
$conn = mysqli_connect($server, $user, $password, $database);
```

Jika koneksi berhasil, `$conn` akan menyimpan objek koneksi yang digunakan di seluruh file PHP lain.

**c. Mengecek status koneksi**

```php
if (!$conn) {
    die("Koneksi gagal: " . mysqli_connect_error());
}
```

`mysqli_connect_error()` digunakan untuk menampilkan pesan kesalahan jika koneksi gagal.

## Mengapa Koneksi Biasanya Dipisah ke File Terpisah?

Dalam pengembangan web profesional, koneksi database **tidak ditulis berulang-ulang** pada setiap file. Sebaliknya, dibuat satu file khusus — biasanya bernama `**koneksi.php**` — lalu dipanggil dari file program lainnya.

### **Manfaat memisahkan file koneksi:**

- Mempermudah perawatan (cukup mengubah 1 file jika server berubah)
- Menghindari duplikasi kode
- Membuat struktur proyek lebih rapi dan rapih
- Meningkatkan keamanan (bisa disembunyikan dari akses langsung)

**Contoh file** `**koneksi.php**`**:**

```php
<?php
$server   = "localhost";
$user     = "root";
$password = "";
$database = "db_sekolah";

$conn = mysqli_connect($server, $user, $password, $database);

if (!$conn) {
    die("Koneksi gagal: " . mysqli_connect_error());
}
?>
```

**Cara menggunakan file koneksi:**

```php
<?php
include "koneksi.php";

echo "Koneksi siap digunakan!";
?>
```

---

Memahami koneksi database menggunakan `mysqli_connect` merupakan fondasi utama sebelum menggunakan berbagai fungsi `mysqli` lainnya. Karena kalian telah mempelajari perintah-perintah mysqli sebelumnya, kini penting untuk memastikan koneksi yang kalian buat sudah benar, terstruktur, dan mudah dipelihara.
