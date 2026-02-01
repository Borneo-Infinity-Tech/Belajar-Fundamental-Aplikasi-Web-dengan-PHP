# Pengenalan Autentikasi dan Otorisasi dalam PHP

Dalam pengembangan aplikasi web, keamanan adalah hal yang sangat penting. Aplikasi tidak hanya harus berfungsi dengan baik, tetapi juga harus memastikan bahwa **pengguna yang mengakses sistem adalah orang yang benar** dan **memiliki hak akses yang sesuai**.

Dua konsep utama yang sering digunakan untuk mengatur keamanan pengguna adalah **Autentikasi (Authentication)** dan **Otorisasi (Authorization)**. Dalam PHP, kedua konsep ini biasanya diterapkan menggunakan **session, database, dan pengelolaan hak akses pengguna**.

Materi ini akan membahas pengenalan autentikasi dan otorisasi, perbedaannya, serta bagaimana konsep tersebut diterapkan dalam aplikasi PHP.

## Pengertian Autentikasi

**Autentikasi** adalah proses **memverifikasi identitas pengguna**. Dengan kata lain, sistem akan memastikan bahwa pengguna benar-benar adalah orang yang dia klaim.

Contoh autentikasi:

- Login menggunakan **username dan password**
- Login menggunakan **email dan password**
- Login menggunakan **OTP atau token**

**Pertanyaan yang dijawab oleh autentikasi:**

> _“Siapa kamu?”_

### **Autentikasi dalam Aplikasi PHP**

Dalam aplikasi PHP, autentikasi biasanya dilakukan dengan langkah berikut:

1.  Pengguna mengisi **form login**
2.  Data dikirim ke server
3.  PHP mengecek data ke **database**
4.  Jika cocok → pengguna berhasil login
5.  Sistem menyimpan status login menggunakan **session**

Contoh konsep sederhana:

- Jika username dan password benar → buat session login
- Jika salah → tampilkan pesan error

### **Peran Session dalam Autentikasi**

Session digunakan untuk menyimpan informasi login pengguna selama mereka mengakses aplikasi.

Contoh informasi yang disimpan dalam session:

- ID pengguna
- Username
- Status login (sudah login / belum)

Tanpa session, pengguna harus login ulang setiap membuka halaman baru.

---

## Pengertian Otorisasi

**Otorisasi** adalah proses **menentukan hak akses pengguna** terhadap sistem setelah mereka berhasil login.

Otorisasi mengatur:

- Apa yang boleh dilakukan pengguna
- Halaman apa yang boleh diakses
- Fitur apa yang boleh digunakan

📌 **Pertanyaan yang dijawab oleh otorisasi:**

> _“Apa yang boleh kamu lakukan?”_

### **Contoh Otorisasi dalam Aplikasi**

Misalnya dalam sistem terdapat beberapa jenis pengguna:

- **Admin** → mengelola data, menambah pengguna, menghapus data
- **User** → hanya melihat dan mengubah data miliknya
- **Guest** → hanya melihat halaman tertentu

Walaupun semua pengguna sudah login, **tidak semua memiliki akses yang sama**.

## Perbedaan Autentikasi dan Otorisasi

<table><tbody><tr><td><strong>Autentikasi</strong></td><td><strong>Otorisasi</strong></td></tr><tr><td>Memastikan identitas pengguna</td><td>Mengatur hak akses pengguna</td></tr><tr><td>Terjadi saat login</td><td>Terjadi setelah login</td></tr><tr><td>Fokus pada “siapa pengguna”</td><td>Fokus pada “hak pengguna”</td></tr><tr><td>Contoh: login</td><td>Contoh: akses halaman admin</td></tr></tbody></table>

👉 **Autentikasi dulu, baru otorisasi**  
Otorisasi tidak bisa dilakukan jika pengguna belum terautentikasi.

## Penerapan Autentikasi dan Otorisasi dalam PHP

### **Alur Umum Sistem**

1.  Pengguna membuka halaman login
2.  Mengisi username dan password
3.  PHP memverifikasi ke database
4.  Jika valid → session dibuat
5.  Saat membuka halaman lain:
    - Cek apakah session login ada (autentikasi)
    - Cek peran pengguna (otorisasi)

### **Contoh Penerapan Otorisasi**

Dalam database biasanya ada kolom:

- `role` atau `level_user`

Contoh nilai:

- `admin`
- `user`

Saat membuka halaman:

- Jika role = admin → boleh masuk halaman admin
- Jika bukan → dialihkan atau ditolak

## Pentingnya Autentikasi dan Otorisasi

Tanpa autentikasi dan otorisasi:

- Data mudah diakses oleh orang tidak berwenang
- Risiko pencurian data meningkat
- Sistem mudah disalahgunakan

Dengan penerapan yang baik:

- Keamanan sistem meningkat
- Data lebih terlindungi
- Aplikasi terlihat profesional

---

Autentikasi dan otorisasi merupakan **fondasi keamanan dalam aplikasi PHP**.  
Autentikasi memastikan **siapa pengguna**, sedangkan otorisasi menentukan **apa yang boleh dilakukan pengguna**.

Dalam praktiknya, kedua konsep ini hampir selalu digunakan bersamaan untuk:

- Mengamankan halaman
- Membatasi akses fitur
- Mengelola hak pengguna

Dengan memahami konsep dasar ini, pengembang PHP dapat membangun aplikasi web yang **lebih aman, terstruktur, dan profesional**.
