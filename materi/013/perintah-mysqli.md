# Perintah `mysqli` pada PHP

Dalam membangun aplikasi web, kita sering membutuhkan tempat untuk menyimpan data. Salah satu database yang paling sering digunakan adalah **MySQL**. Untuk berkomunikasi dengan MySQL, PHP menyediakan sebuah ekstensi bernama `**mysqli**` (MySQL Improved). `mysqli` memungkinkan kita:

- Terhubung ke database
- Mengirim perintah SQL
- Mengambil dan menampilkan data
- Menangani error saat bekerja dengan database

Materi berikut akan membahas perintah dasar `mysqli` yang paling penting, dijelaskan dengan bahasa sederhana agar mudah dipahami oleh pemula.

## Membuat Koneksi ke Database — `mysqli_connect()`

`mysqli_connect()` digunakan untuk **menghubungkan PHP dengan database MySQL**.

**Bentuk dasar**

```php
mysqli_connect(host, username, password, database);
```

**Penjelasan**

- **host** → alamat server database (jika di komputer sendiri)
- **username** → username MySQL
- **password** → password MySQL (kosong berarti tidak ada password)
- **database** → nama database yang ingin dipakai

## Mengirim Perintah SQL — `mysqli_query()`

Fungsi untuk **mengirim perintah SQL** ke database melalui koneksi yang sudah dibuat.

**Bentuk dasar**

```php
mysqli_query(koneksi, query);
```

- **koneksi →** Variabel koneksi hasil `mysqli_connect()`
- **query →** Perintah SQL, misalnya: `"SELECT * FROM users"`

## Mengubah Hasil Query Menjadi Array — `mysqli_fetch_assoc()`

Fungsi untuk **mengambil satu baris hasil query** dalam bentuk **array asosiatif** (nama kolom → nilai).

```php
mysqli_fetch_assoc(result);
```

**result →** Hasil dari `mysqli_query()` yang mengandung data SELECT

## Menghitung Jumlah Baris Hasil Query — `mysqli_num_rows()`

Menghitung jumlah baris data dari hasil SQL SELECT.

```php
mysqli_num_rows(result);
```

**result →** Hasil SELECT dari `mysqli_query()`

## `mysqli_real_escape_string()`

Membersihkan data dari karakter berbahaya untuk mencegah SQL injection.

```php
mysqli_real_escape_string(koneksi, string);
```

- **koneksi →** Variabel koneksi yang sebelumnya dibuat
- **string →** Data yang ingin dibersihkan

## Menutup Koneksi — `mysqli_close()`

Menutup koneksi database.

```php
mysqli_close(koneksi);
```

**koneksi →** Variabel koneksi yang sebelumnya dibuat

---

Dengan memahami **apa fungsi mysqli**, **apa saja parameter masing-masing**, dan **contoh penggunaannya**, kamu sudah menguasai dasar komunikasi PHP–MySQL.
