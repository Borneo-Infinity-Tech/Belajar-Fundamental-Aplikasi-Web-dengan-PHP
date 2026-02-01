# Mencegah SQL Injection dengan Prepared Statement pada PHP

Dalam pengembangan aplikasi berbasis web, **keamanan data** adalah hal yang sangat penting. Salah satu serangan yang paling sering terjadi pada aplikasi web adalah **SQL Injection**. Serangan ini memungkinkan penyerang untuk memanipulasi query SQL sehingga dapat **mencuri data, mengubah data, bahkan menghapus seluruh database**.

PHP menyediakan solusi yang sangat efektif untuk mencegah SQL Injection, yaitu **Prepared Statement**.

## Apa itu SQL Injection?

**SQL Injection** adalah teknik serangan dengan cara menyisipkan perintah SQL berbahaya ke dalam input pengguna.

**Contoh Kasus Berbahaya**

Misalkan ada kode PHP seperti ini:

```php
$username = $_POST['username'];
$password = $_POST['password'];

$query = "SELECT * FROM users WHERE username='$username' AND password='$password'";
```

Jika pengguna mengisi input seperti:

```php
username: admin
password: ' OR '1'='1
```

Maka query yang dijalankan menjadi:

```php
SELECT * FROM users WHERE username='admin' AND password='' OR '1'='1'
```

Karena `'1'='1'` selalu benar, **penyerang bisa login tanpa password yang valid**.

## Mengapa SQL Injection Sangat Berbahaya?

SQL Injection dapat menyebabkan:

- 🔓 Login tanpa autentikasi
- 📂 Pencurian data pengguna
- 🗑️ Penghapusan tabel database
- 🛠️ Perubahan data penting
- 🚫 Kerusakan sistem secara keseluruhan

Oleh karena itu, **SQL Injection wajib dicegah**.

## Apa itu Prepared Statement?

**Prepared Statement** adalah metode menjalankan query SQL dengan cara:

- Query disiapkan terlebih dahulu
- Data pengguna dikirim terpisah
- Database tidak mengeksekusi input sebagai perintah SQL

Dengan metode ini, input berbahaya **tidak akan dijalankan sebagai SQL**.

## Contoh Login TANPA Prepared Statement (Tidak Aman)

```php
$username = $_POST['username'];
$password = $_POST['password'];

$sql = "SELECT * FROM users WHERE username='$username' AND password='$password'";
$result = mysqli_query($koneksi, $sql);
```

❌ **Kode ini sangat rentan SQL Injection.**

## Contoh Login DENGAN Prepared Statement (Aman)

```php
$username = $_POST['username'];
$password = $_POST['password'];

$sql = "SELECT * FROM users WHERE username = ? AND password = ?";
$stmt = mysqli_prepare($koneksi, $sql);
mysqli_stmt_bind_param($stmt, "ss", $username, $password);
mysqli_stmt_execute($stmt);
$result = mysqli_stmt_get_result($stmt);
```

## Penjelasan Kode Prepared Statement

### Query dengan Placeholder (?)

```php
$sql = "SELECT * FROM users WHERE username = ? AND password = ?";
```

**Penjelasan:**

- Tanda `?` disebut **placeholder**
- Placeholder akan diisi oleh data pengguna secara aman
- Input tidak akan dianggap sebagai SQL

### Menyiapkan Query

```php
$stmt = mysqli_prepare($koneksi, $sql);
```

**Penjelasan:**

- `mysqli_prepare()` menyiapkan query ke database
- Query belum dijalankan
- Struktur SQL dikunci sehingga aman

### Mengikat Parameter

```php
mysqli_stmt_bind_param($stmt, "ss", $username, $password);
```

**Penjelasan:**

- `"ss"` menunjukkan tipe data:
  - `s` → string (username)
  - `s` → string (password)
- Data dikirim terpisah dari query
- SQL Injection dapat dicegah

Jenis tipe data:

- `s` → string
- `i` → integer
- `d` → double

### Menjalankan Query

```php
mysqli_stmt_execute($stmt);
```

**Penjelasan:**

- Query dieksekusi setelah parameter aman
- Database tidak bisa dimanipulasi oleh input pengguna

### Mengambil Hasil Query

```php
$result = mysqli_stmt_get_result($stmt);
```

Digunakan untuk:

- Mengambil data hasil query
- Mengecek apakah login berhasil

## Keuntungan Menggunakan Prepared Statement

- ✅ Aman dari SQL Injection
- ✅ Lebih aman untuk input pengguna
- ✅ Query lebih rapi dan terstruktur
- ✅ Standar keamanan aplikasi web modern

SQL Injection adalah salah satu serangan paling berbahaya dalam aplikasi berbasis database. Dengan menggunakan **Prepared Statement pada MySQLi Prosedural**, kita dapat melindungi aplikasi dari serangan tersebut secara efektif.

Prepared Statement memastikan bahwa:

- Data pengguna tidak dianggap sebagai perintah SQL
- Query dijalankan dengan aman
- Aplikasi menjadi lebih profesional dan andal

Sebagai developer, membiasakan penggunaan Prepared Statement adalah langkah penting untuk membangun aplikasi yang **aman, stabil, dan terpercaya**.
