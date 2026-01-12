# Studi Kasus Membuat Halaman Web Dinamis

Dalam pengembangan web, **halaman dinamis** memungkinkan konten berubah sesuai interaksi pengguna tanpa harus membuat banyak file terpisah. Salah satu cara sederhana untuk membuat halaman dinamis adalah dengan:

- Membagi layout menjadi beberapa bagian (header, sidebar, konten, footer)
- Menggunakan **PHP** untuk memuat konten
- Memanfaatkan **method GET** pada URL untuk menentukan halaman yang ditampilkan

Pada studi kasus ini, kita akan membuat sebuah **website sederhana** dengan navigasi menu yang berubah berdasarkan parameter URL.

Buat folder **project-web-dinamis** di **laragon/www**

Didalam folder tersebut buat struktur folder dan file seperti di bawah.

```
project-web-dinamis/
│
├── index.php
├── layouts/
│   ├── topbar.php
│   ├── sidebar.php
│   └── footer.php
│
├── pages/
│   ├── dashboard.php
│   ├── users.php
│   └── settings.php
```

Buka file **index.php** dan tambahkan kode berikut.

```php
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dashboard Template</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100">
      <!-- Wrapper -->
      <div class="flex min-h-screen">

        <!-- Sidebar -->

        <!-- End Sidebar -->

        <!-- Main -->
        <div class="flex-1 flex flex-col">

            <!-- Topbar -->

            <!-- End Topbar -->

            <!-- Content -->
            <main class="flex-1 p-6">

            </main>
            <!-- End Content -->

            <!-- Footer -->

            <!-- End Footer -->

        </div>
        <!-- End Main -->

      </div>
      <!-- End Wrapper -->

</body>
</html>
```

Buka file **sidebar.php** tambahkan kode berikut.

```php
<aside class="w-64 bg-slate-800 text-white flex flex-col">
    <div class="px-6 py-4 text-xl font-bold border-b border-slate-700">
        My Dashboard
    </div>
    <nav class="flex-1 px-4 py-6 space-y-2">
        <a href="#" class="block px-4 py-2 rounded hover:bg-slate-700">Dashboard</a>
        <a href="#" class="block px-4 py-2 rounded hover:bg-slate-700">User</a>
        <a href="#" class="block px-4 py-2 rounded hover:bg-slate-700">Setting</a>
    </nav>
</aside>
```

Pada **index.php** tambahkan kode diantara komentar sidebar.

```php
<?php include "layouts/sidebar.php"; ?>
```

Buka file **topbar.php** tambahkan kode berikut.

```php
<header class="bg-white shadow px-6 py-4 flex justify-between items-center">
    <h1 class="text-xl font-semibold text-gray-700">Dashboard</h1>
    <span class="text-gray-600">Halo, Admin</span>
</header>
```

Pada **index.php** tambahkan kode diantara komentar topbar.

```php
<?php include "layouts/topbar.php"; ?>
```

Buka file **footer.php** tambahkan kode berikut.

```php
<footer class="bg-white text-center py-4 text-sm text-gray-500 border-t">
    © 2026 My Dashboard. All rights reserved.
</footer>
```

Pada **index.php** tambahkan kode diantara komentar footer.

```php
<?php include "layouts/footer.php"; ?>
```

Pada kasus di atas kita sudah membagi komponen menjadi file terpisah, keuntungannya kita cukup menuliskan satu kali, namun bisa dipakai dibeberapa halaman.

Selanjutnya buka file **dashboard.php** dan tambahkan kode berikut.

```php
<div class="bg-white rounded-lg shadow p-6 max-w-3xl">
    <h2 class="text-lg font-semibold mb-2">Halaman Dashboard</h2>
    <p class="text-gray-600">
        Ini adalah satu card saja sebagai konten utama.
        Kamu bisa isi form, tabel, atau informasi lain di sini.
    </p>
</div>
```

Selanjutnya buka file **users.php** dan tambahkan kode berikut.

```php
<div class="bg-white rounded-lg shadow p-6 max-w-3xl">
    <h2 class="text-lg font-semibold mb-2">Halaman User</h2>
    <p class="text-gray-600">
        Ini adalah satu card saja sebagai konten utama.
        Kamu bisa isi form, tabel, atau informasi lain di sini.
    </p>
</div>
```

Selanjutnya buka file **settings.php** dan tambahkan kode berikut.

```php
<div class="bg-white rounded-lg shadow p-6 max-w-3xl">
    <h2 class="text-lg font-semibold mb-2">Halaman Settings</h2>
    <p class="text-gray-600">
        Ini adalah satu card saja sebagai konten utama.
        Kamu bisa isi form, tabel, atau informasi lain di sini.
    </p>
</div>
```

Buka kembali file **sidebar.php** dan ubah isi **href** seperti kode di bawah ini.

```php
<a href="index.php?page=dashboard" class="block px-4 py-2 rounded hover:bg-slate-700">Dashboard</a>
<a href="index.php?page=users" class="block px-4 py-2 rounded hover:bg-slate-700">User</a>
<a href="index.php?page=settings" class="block px-4 py-2 rounded hover:bg-slate-700">Setting</a>
```

`index.php?page=dashboard` merupakan parameter yang akan tampil pada URL.

Buka file **index.php** tulis kode di bawahi ini pada bagian awal baris file.

```php
<?php
$pages = [
    'dashboard' => 'layouts/dashboard.php',
    'users' => 'layouts/users.php',
    'settings' => 'layouts/settings.php'
];

$page = $_GET['page'] ?? 'home';
$page_file = $pages[$page] ?? $pages['home'];
?>
```

Tambahkan kode berikut di antara tag pembuka dan penutup `<main>` pada file **index.php**.

```php
<?php include $page_file; ?>
```

Sehingga kode keseluruhan pada **index.php** sebagai berikut.

```php
<?php
$pages = [
    'dashboard' => 'pages/dashboard.php',
    'users' => 'pages/users.php',
    'settings' => 'pages/settings.php'
];

$page = $_GET['page'] ?? 'dashboard';
$page_file = $pages[$page] ?? $pages['dashboard'];
?>

<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dashboard Template</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100">
    <!-- Wrapper -->
      <div class="flex min-h-screen">

          <!-- Sidebar -->
          <?php include "layouts/sidebar.php"; ?>
          <!-- End Sidebar -->


          <!-- Main -->
          <div class="flex-1 flex flex-col">

              <!-- Topbar -->
              <?php include "layouts/topbar.php"; ?>
              <!-- End Topbar -->

              <!-- Content -->
              <main class="flex-1 p-6">
                  <?php include $page_file; ?>
              </main>
              <!-- End Content -->

              <!-- Footer -->
              <?php include "layouts/footer.php"; ?>
              <!-- End Footer -->

          </div>
          <!-- End Main -->

      </div>
      <!-- End Wrapper -->
</body>
</html>
```

Lalu buka pada browser, maka kalian sudah berhasil membuat halaman web dinamis menggunakan PHP.

## Penjelasan Kode

Kode di bawah ini adalah **daftar mapping halaman**, yang menghubungkan **nama halaman di URL** dengan **file PHP yang boleh ditampilkan**.

```php
$pages = [
    'dashboard' => 'pages/dashboard.php',
    'users' => 'pages/users.php',
    'settings' => 'pages/settings.php'
];
```

Pada kode Kode ini digunakan **mengambil parameter** `page` **dari URL**, dan **jika tidak ada maka otomatis bernilai** `home`.

```php
$page = $_GET['page'] ?? 'home';
```

Kode ini **menentukan file halaman yang akan ditampilkan**:

- jika `$page` ada di array `$pages` → pakai file tersebut,
- jika tidak → pakai halaman default (`home`).

```php
$page_file = $pages[$page] ?? $pages['home'];
```

Kode ini **memasukkan (menampilkan) isi file PHP yang ditentukan oleh** `$page_file` **ke halaman saat ini**.

```php
<?php include $page_file; ?>
```

Melalui studi kasus ini, dapat disimpulkan bahwa pembuatan halaman web dinamis menggunakan PHP dapat dilakukan dengan sederhana melalui pembagian layout dan penggunaan method GET. Pendekatan ini membuat struktur kode lebih rapi, mudah dikembangkan, serta efisien dalam pengelolaan halaman. Dengan dukungan Tailwind CSS, tampilan web dapat dibuat menarik tanpa proses yang rumit.
