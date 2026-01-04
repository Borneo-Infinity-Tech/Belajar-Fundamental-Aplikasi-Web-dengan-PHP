# Upload File dengan PHP

Dalam pengembangan aplikasi web, fitur **upload file** sangat sering digunakan, misalnya untuk:

- Upload foto profil
- Upload dokumen (PDF, Word, Excel)
- Upload gambar produk
- Upload tugas atau laporan

PHP menyediakan mekanisme bawaan untuk menangani upload file melalui **form HTML** dan **variabel superglobal** `$_FILES`. Pada materi ini, kita akan mempelajari konsep upload file dari dasar hingga praktik, termasuk validasi dan keamanan dasar agar upload file berjalan dengan aman.

## Konsep Dasar Upload File di PHP

Proses upload file di PHP melibatkan:

1.  **Form HTML** dengan metode `POST`
2.  Atribut `enctype="multipart/form-data"`
3.  File dikirim dan disimpan sementara di server
4.  PHP memindahkan file ke folder tujuan

Ketika file diupload, PHP otomatis menyimpannya sementara dan informasinya dapat diakses melalui `**$_FILES**`.

## Membuat Form Upload File (HTML)

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
  <label>Pilih File:</label>
  <input type="file" name="fileUpload" />
  <br /><br />
  <button type="submit" name="upload">Upload</button>
</form>
```

**Penjelasan Kode:**

- `method="post"` → Upload file **wajib** menggunakan metode POST.
- `enctype="multipart/form-data"` → Digunakan agar file dapat dikirim ke server.
- `input type="file"` → Field khusus untuk memilih file.
- `name="fileUpload"` → Nama ini digunakan untuk mengakses file di PHP (`$_FILES['fileUpload']`).

## Struktur Variabel `$_FILES`

Saat file diupload, PHP menyediakan data berikut:

```php
$_FILES['fileUpload'] = [
    'name'      => 'contoh.jpg',
    'type'      => 'image/jpeg',
    'tmp_name'  => '/tmp/php123.tmp',
    'error'     => 0,
    'size'      => 245678
];
```

**Penjelasan**

- `name` → Nama asli file
- `type` → Tipe MIME file
- `tmp_name` → Lokasi sementara file
- `error` → Status error upload
- `size` → Ukuran file (byte)

## Proses Upload File dengan PHP

Buat file `upload.php`:

```php
<?php
if ($_SERVER["REQUEST_METHOD"] === "POST") {

    $file = $_FILES['fileUpload'];

    $namaFile = $file['name'];
    $tmpFile  = $file['tmp_name'];
    $ukuran   = $file['size'];
    $error    = $file['error'];

    $folderTujuan = "uploads/";

    if ($error === 0) {
        move_uploaded_file($tmpFile, $folderTujuan . $namaFile);
        echo "File berhasil diupload";
    } else {
        echo "Terjadi kesalahan saat upload";
    }
}
?>
```

**Penjelasan**

- `move_uploaded_file()` → Memindahkan file dari folder sementara ke folder tujuan.

## Validasi Ekstensi File

Validasi ekstensi penting untuk keamanan.

```php
$ekstensiDiizinkan = ['jpg', 'png', 'pdf'];
$ekstensiFile = strtolower(pathinfo($namaFile, PATHINFO_EXTENSION));

if (in_array($ekstensiFile, $ekstensiDiizinkan)) {
    move_uploaded_file($tmpFile, $folderTujuan . $namaFile);
    echo "Upload berhasil";
} else {
    echo "Ekstensi file tidak diizinkan";
}
```

### **Penjelasan**:

- `pathinfo()` → mengambil ekstensi file
- `strtolower()` → menghindari perbedaan huruf besar/kecil
- `in_array()` → mengecek apakah ekstensi diperbolehkan

## Validasi Ukuran File

```php
$maxSize = 2 * 1024 * 1024; // 2MB

if ($ukuran <= $maxSize) {
    move_uploaded_file($tmpFile, $folderTujuan . $namaFile);
    echo "Upload berhasil";
} else {
    echo "Ukuran file terlalu besar";
}
```

### **Penjelasan**:

- 1MB = 1024 × 1024 byte
- Validasi ukuran mencegah server overload

## Mengganti Nama File (Disarankan)

Untuk menghindari nama file yang sama:

```php
$namaBaru = uniqid() . "." . $ekstensiFile;
move_uploaded_file($tmpFile, $folderTujuan . $namaBaru);
```

### **Penjelasan**:

- `uniqid()` → menghasilkan nama unik
- Mencegah file tertimpa file lain

## Contoh Upload File Lengkap (Aman)

```php
<?php
if (isset($_POST['upload'])) {

    $file = $_FILES['fileUpload'];
    $namaFile = $file['name'];
    $tmpFile = $file['tmp_name'];
    $ukuran = $file['size'];
    $error = $file['error'];

    $ekstensiDiizinkan = ['jpg', 'png', 'pdf'];
    $maxSize = 2 * 1024 * 1024;
    $folderTujuan = "uploads/";

    $ekstensiFile = strtolower(pathinfo($namaFile, PATHINFO_EXTENSION));

    if ($error === 0) {
        if (in_array($ekstensiFile, $ekstensiDiizinkan)) {
            if ($ukuran <= $maxSize) {
                $namaBaru = uniqid() . "." . $ekstensiFile;
                move_uploaded_file($tmpFile, $folderTujuan . $namaBaru);
                echo "File berhasil diupload";
            } else {
                echo "Ukuran file terlalu besar";
            }
        } else {
            echo "Tipe file tidak diizinkan";
        }
    } else {
        echo "Terjadi kesalahan upload";
    }
}
?>
```

Upload file dengan PHP merupakan fitur penting dalam aplikasi web. Dengan memahami:

- Struktur `$_FILES`
- Fungsi `move_uploaded_file()`
- Validasi ekstensi dan ukuran
- Pengamanan nama file

kita dapat membuat sistem upload file yang **aman, efisien, dan profesional**. Selalu lakukan validasi agar server terhindar dari file berbahaya dan kesalahan sistem.
