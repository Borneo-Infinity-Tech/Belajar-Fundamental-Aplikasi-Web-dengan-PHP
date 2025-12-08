# Query Dasar: SELECT, INSERT, UPDATE, DELETE

Dalam pengembangan aplikasi berbasis web, terutama yang menggunakan PHP, sangat umum untuk berinteraksi dengan database MySQL. MySQLi (MySQL Improved) adalah ekstensi PHP yang memungkinkan kita menjalankan perintah-perintah SQL seperti mengambil data, menambah data baru, memperbarui data, dan menghapus data. Empat perintah SQL dasar yang paling sering digunakan adalah:

1.  **SELECT** → mengambil data
2.  **INSERT** → menambah data
3.  **UPDATE** → memperbarui data
4.  **DELETE** → menghapus data

Memahami keempat perintah ini sangat penting karena merupakan fondasi dari operasi CRUD (Create, Read, Update, Delete).

## SELECT (Mengambil Data)

Perintah SELECT digunakan untuk mengambil atau menampilkan data dari database.

### **Contoh Query Dasar**

```php
SELECT * FROM users;
```

Artinya: Ambil semua data dari tabel `users`.

### **Contoh Penggunaan dengan MySQLi**

```php
<?php
include 'koneksi.php'; // file koneksi

$sql = "SELECT * FROM users";
$result = mysqli_query($conn, $sql);

while ($row = mysqli_fetch_assoc($result)) {
    echo "ID: " . $row['id'] . "<br>";
    echo "Nama: " . $row['nama'] . "<br><br>";
}
?>
```

**Penjelasan**

- `mysqli_query` → menjalankan perintah SQL.
- `mysqli_fetch_assoc` → mengambil setiap data dalam bentuk array asosiatif.

## INSERT (Menambah Data)

Perintah INSERT digunakan untuk memasukkan data baru ke dalam tabel.

### **Contoh Query Dasar**

```php
INSERT INTO users (nama, email) VALUES ('Budi', 'budi@gmail.com');
```

### **Contoh Penggunaan dengan MySQLi**

```php
<?php
include 'koneksi.php';

$nama = "Budi";
$email = "budi@gmail.com";

$sql = "INSERT INTO users (nama, email) VALUES ('$nama', '$email')";
if (mysqli_query($conn, $sql)) {
    echo "Data berhasil ditambahkan!";
} else {
    echo "Error: " . mysqli_error($conn);
}
?>
```

### **Penjelasan**

- Data dimasukkan menggunakan VALUES.
- Jangan lupa pastikan nama kolom sesuai dengan struktur tabel.

## UPDATE (Memperbarui Data)

Perintah UPDATE digunakan untuk mengubah data tertentu di dalam tabel.

### **Contoh Query Dasar**

```php
UPDATE users SET nama = 'Andi' WHERE id = 1;
```

### **Contoh Penggunaan dengan MySQLi**

```php
<?php
include 'koneksi.php';

$id = 1;
$nama_baru = "Andi";

$sql = "UPDATE users SET nama='$nama_baru' WHERE id=$id";
if (mysqli_query($conn, $sql)) {
    echo "Data berhasil diperbarui!";
} else {
    echo "Error: " . mysqli_error($conn);
}
?>
```

### **Penjelasan**

- Sangat penting menggunakan **WHERE**, agar data yang diperbarui sesuai target.
- Jika tidak menggunakan WHERE, semua data bisa ikut ter-update.

## DELETE (Menghapus Data)

Perintah DELETE digunakan untuk menghapus data dari tabel.

### **Contoh Query Dasar**

```php
DELETE FROM users WHERE id = 2;
```

### **Contoh Penggunaan dengan MySQLi**

```php
<?php
include 'koneksi.php';

$id = 2;

$sql = "DELETE FROM users WHERE id=$id";
if (mysqli_query($conn, $sql)) {
    echo "Data berhasil dihapus!";
} else {
    echo "Error: " . mysqli_error($conn);
}
?>
```

### **Penjelasan**

Sama seperti UPDATE, DELETE **harus menggunakan WHERE** agar tidak menghapus semua data.

## Tips Penting

- Gunakan `mysqli_real_escape_string` atau prepared statement untuk keamanan (mencegah SQL Injection).
- Selalu cek apakah query berhasil dieksekusi.
- Tampilkan pesan error saat terjadi kegagalan agar mudah melakukan debugging.

Empat operasi dasar SQL (SELECT, INSERT, UPDATE, DELETE) merupakan dasar utama dalam membangun aplikasi yang berhubungan dengan database. Dengan memahami cara menggunakan perintah tersebut melalui MySQLi, Anda sudah memiliki pondasi kuat untuk membuat aplikasi CRUD sederhana hingga aplikasi yang lebih kompleks.
