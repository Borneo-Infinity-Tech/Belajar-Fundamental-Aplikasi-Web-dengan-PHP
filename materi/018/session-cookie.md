# Mengenal Session dan Cookie pada PHP

Dalam pengembangan website menggunakan PHP, sering kali kita membutuhkan cara untuk **menyimpan data pengguna sementara**, seperti data login, nama pengguna, atau preferensi tertentu. Masalahnya, **HTTP bersifat stateless**, artinya setiap kali pengguna membuka halaman baru, server tidak otomatis mengingat data sebelumnya. Untuk mengatasi hal tersebut, PHP menyediakan dua mekanisme penting, yaitu **Session** dan **Cookie**.

## Pengertian Session

**Session** adalah mekanisme untuk menyimpan data pengguna **di sisi server** selama pengguna masih aktif mengakses website.

Ciri utama Session:

- Data disimpan di **server**
- Data akan hilang jika browser ditutup atau session berakhir
- Umumnya digunakan untuk **login pengguna**

Contoh penggunaan Session

- Menyimpan status login
- Menyimpan username sementara
- Menyimpan data keranjang belanja

## Cara Menggunakan Session di PHP

### **Memulai Session**

Sebelum menggunakan session, kita **wajib memanggil fungsi** `session_start()`.

```php
<?php
session_start();
?>
```

**Penjelasan kode:**

- `session_start()` berfungsi untuk memulai session
- Harus ditulis **sebelum output HTML** (sebelum `<html>`)

### **Menyimpan Data ke Session**

```php
<?php
session_start();
$_SESSION['username'] = "Indira";
$_SESSION['status'] = "login";
?>
```

**Penjelasan kode:**

- `$_SESSION` adalah variabel global untuk menyimpan data session
- `'username'` dan `'status'` adalah nama data session
- `"Indira"` dan `"login"` adalah nilai yang disimpan

### **Mengambil Data Session**

```php
<?php
session_start();
echo $_SESSION['username'];
?>
```

**Penjelasan kode:**

- Data session dipanggil menggunakan `$_SESSION['nama_session']`
- Akan menampilkan **Indira**

### **Menghapus Session**

Menghapus satu data session

```php
unset($_SESSION['username']);
```

Menghapus semua session

```php
session_destroy();
```

**Penjelasan kode:**

- `unset()` menghapus satu data session
- `session_destroy()` menghapus seluruh data session

## Pengertian Cookie

**Cookie** adalah mekanisme untuk menyimpan data pengguna **di sisi browser (client)**.

Ciri utama Cookie:

- Data disimpan di **browser pengguna**
- Memiliki **waktu kadaluarsa**
- Kurang aman dibanding Session
- Cocok untuk data ringan seperti preferensi pengguna

Contoh penggunaan Cookie

- Menyimpan tema website
- Mengingat bahasa pilihan
- Mengingat username (remember me)

## Cara Menggunakan Cookie di PHP

### **Membuat Cookie**

```php
<?php
setcookie("username", "Indira", time() + 3600);
?>
```

**Penjelasan kode:**

- `"username"` → nama cookie
- `"Indira"` → nilai cookie
- `time() + 3600` → cookie berlaku selama 1 jam (3600 detik)

⚠️ `setcookie()` harus dipanggil **sebelum output HTML**

### **Mengambil Data Cookie**

```php
<?php
echo $_COOKIE['username'];
?>
```

**Penjelasan kode:**

- `$_COOKIE` digunakan untuk mengambil data cookie
- Akan menampilkan **Andi**

### **Menghapus Cookie**

```php
<?php
setcookie("username", "", time() - 3600);
?>
```

**Penjelasan kode:**

- Waktu diatur ke masa lalu agar cookie otomatis terhapus

## Perbedaan Session dan Cookie

<table><tbody><tr><td><strong>Perbandingan</strong></td><td><strong>Session</strong></td><td><strong>Cookie</strong></td></tr><tr><td>Lokasi data</td><td>Server</td><td>Browser</td></tr><tr><td>Keamanan</td><td>Lebih aman</td><td>Kurang aman</td></tr><tr><td>Waktu simpan</td><td>Sementara</td><td>Bisa lama</td></tr><tr><td>Kapasitas</td><td>Lebih besar</td><td>Terbatas</td></tr><tr><td>Cocok untuk</td><td>Login, data sensitif</td><td>Preferensi pengguna</td></tr></tbody></table>

## Kapan Menggunakan Session dan Cookie?

Gunakan **Session** jika:

- Menyimpan data penting
- Membuat sistem login
- Menyimpan data sementara

Gunakan **Cookie** jika:

- Menyimpan data ringan
- Mengingat preferensi pengguna
- Data tidak terlalu sensitif

Session dan Cookie merupakan konsep dasar yang **sangat penting** dalam pemrograman PHP, terutama untuk membangun website yang interaktif dan dinamis.  
Dengan memahami perbedaan serta cara penggunaannya, kita dapat menentukan **kapan harus menggunakan Session dan kapan harus menggunakan Cookie** dengan tepat.

Sebagai pengembang PHP, disarankan:

- Gunakan **Session untuk keamanan**
- Gunakan **Cookie untuk kenyamanan pengguna**
