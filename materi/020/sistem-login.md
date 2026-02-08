# Alur Sistem Login (Flow Autentikasi)

Dalam sebuah aplikasi berbasis web, **sistem login** merupakan komponen yang sangat penting. Sistem login berfungsi untuk **memverifikasi identitas pengguna** sebelum mereka dapat mengakses fitur tertentu. Proses ini disebut juga **autentikasi**.

Pada materi ini, kita akan membahas **alur sistem login (flow autentikasi) menggunakan PHP**, mulai dari pengguna memasukkan data login hingga sistem memberikan akses atau menolak login. Penjelasan akan dibuat sederhana agar mudah dipahami, terutama bagi pemula.

## Pengertian Autentikasi

**Autentikasi** adalah proses untuk memastikan bahwa pengguna yang mencoba masuk ke sistem benar-benar adalah orang yang berhak. Biasanya dilakukan dengan:

- **Username / Email**
- **Password**

Jika data yang dimasukkan sesuai dengan data yang tersimpan di database, maka pengguna dinyatakan **berhasil login**.

## Komponen Utama Sistem Login PHP

Sebelum masuk ke alur, ada beberapa komponen penting dalam sistem login:

1.  **Form Login**: Tempat pengguna memasukkan username/email dan password.
2.  **File Proses Login (PHP)**: File yang memproses data dari form login.
3.  **Database**: Menyimpan data akun pengguna (username/email dan password yang sudah di-hash).
4.  **Session**: Digunakan untuk menyimpan status login pengguna.

## Alur Sistem Login (Flow Autentikasi)

### **Pengguna Mengakses Halaman Login**

Pengguna membuka halaman login (`login.php`) melalui browser.

Di halaman ini terdapat:

- Input username/email
- Input password
- Tombol login

### **Pengguna Mengisi Form Login**

Pengguna memasukkan:

- Username atau email
- Password

Kemudian menekan tombol **Login**.

Data ini dikirim ke server menggunakan metode:

- `POST` (lebih aman daripada GET)

### **Data Diterima oleh PHP**

File PHP (misalnya `proses_login.php`) menerima data dari form:

- Username/email dari `$_POST`
- Password dari `$_POST`

Pada tahap ini, **data belum dianggap valid**.

### **Validasi Input**

Sistem melakukan pengecekan awal, seperti:

- Apakah username/email kosong?
- Apakah password kosong?

Jika ada data kosong:

- Login gagal
- Sistem menampilkan pesan error

Tujuan validasi ini adalah **mencegah kesalahan dan input tidak valid**.

### **Mengambil Data Pengguna dari Database**

Jika input valid, sistem akan:

- Mencari data pengguna di database berdasarkan username/email
- Mengambil password yang tersimpan (biasanya dalam bentuk hash)

Jika username/email **tidak ditemukan**:

- Login gagal
- Sistem menampilkan pesan “Akun tidak ditemukan”

### **Verifikasi Password**

Jika akun ditemukan:

- Password yang dimasukkan pengguna dibandingkan dengan password di database
- Biasanya menggunakan `password_verify()`

Kemungkinan hasil:

- **Cocok** → lanjut ke proses login
- **Tidak cocok** → login gagal

### **Membuat Session Login**

Jika password benar:

- Sistem membuat **session**
- Session menandakan bahwa pengguna sudah login

Contoh data session:

- ID user
- Username
- Role (admin/user)

Session ini digunakan agar pengguna **tidak perlu login ulang** setiap membuka halaman.

### **Redirect ke Halaman Utama**

Setelah session dibuat:

- Pengguna diarahkan ke halaman dashboard atau halaman utama
- Halaman ini hanya bisa diakses jika session login aktif

Jika pengguna mencoba mengakses halaman ini tanpa login:

- Sistem akan mengarahkan kembali ke halaman login

### **Logout (Akhir Autentikasi)**

Saat pengguna logout:

- Session dihapus
- Status login berakhir
- Pengguna kembali ke halaman login

## Ilustrasi Alur Login (Sederhana)

1.  User membuka halaman login
2.  User memasukkan username & password
3.  PHP menerima data
4.  Sistem validasi input
5.  Cek akun di database
6.  Verifikasi password
7.  Buat session
8.  User masuk ke dashboard

## Keamanan Dasar yang Perlu Diperhatikan

Beberapa hal penting dalam sistem login PHP:

- Password **harus di-hash**, bukan disimpan teks biasa
- Gunakan `POST` untuk form login
- Gunakan session untuk mengelola login
- Jangan menampilkan pesan error yang terlalu detail

Sistem login merupakan bagian krusial dalam pengembangan aplikasi web berbasis PHP. Dengan memahami **alur autentikasi**, kita dapat membangun sistem yang **aman, terstruktur, dan mudah dikembangkan**.

Mulai dari proses input data, validasi, pengecekan database, hingga pembuatan session, semua tahapan saling berkaitan dan harus dirancang dengan baik. Dengan pemahaman yang benar, sistem login tidak hanya berfungsi dengan baik, tetapi juga mampu melindungi data dan privasi pengguna.
