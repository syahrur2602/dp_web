# Wireframe & User Flow — SIMPUS-Mini

Dokumen ini berisi rancangan awal tampilan (wireframe) dan alur penggunaan (user flow) untuk fitur yang akan dikembangkan pada aplikasi SIMPUS-Mini.

---

## 1. Login Petugas

### Wireframe

```text
+------------------------------------------------+
|                 SIMPUS-Mini                    |
|          Sistem Informasi Perpustakaan         |
|                                                |
|              LOGIN PETUGAS                     |
|                                                |
|  Username                                      |
|  +------------------------------------------+  |
|  |                                          |  |
|  +------------------------------------------+  |
|                                                |
|  Password                                      |
|  +------------------------------------------+  |
|  |                                          |  |
|  +------------------------------------------+  |
|                                                |
|             +----------------+                 |
|             |      MASUK     |                 |
|             +----------------+                 |
|                                                |
+------------------------------------------------+
```

### User Flow

```text
Buka halaman Login
        ↓
Masukkan username
        ↓
Masukkan password
        ↓
Klik "Masuk"
        ↓
Sistem melakukan validasi
        ↓
   ┌────┴────┐
   ↓         ↓
 Valid    Tidak Valid
   ↓         ↓
Dashboard   Tampilkan
Petugas     pesan error
             ↓
        Kembali ke Login
```

---

## 2. Dashboard Petugas

### Wireframe

```text
+----------------------------------------------------------------+
| SIMPUS-Mini                    Petugas ▼        [ Logout ]      |
+----------------------------------------------------------------+
|                                                                |
| Dashboard Petugas                                              |
|                                                                |
| +------------+ +------------+ +------------+ +---------------+ |
| | TOTAL BUKU | |  ANGGOTA   | | DIPINJAM   | |   TERLAMBAT   | |
| |     120    | |     45     | |     18     | |       5       | |
| +------------+ +------------+ +------------+ +---------------+ |
|                                                                |
| Peminjaman Terbaru                                             |
| +------------------------------------------------------------+ |
| | Anggota | Buku                  | Tanggal    | Status       | |
| +------------------------------------------------------------+ |
| | Andi    | Pemrograman Web      | 10/09/2026 | Dipinjam     | |
| | Budi    | Basis Data           | 09/09/2026 | Dipinjam     | |
| +------------------------------------------------------------+ |
|                                                                |
| [ Buku ] [ Anggota ] [ Peminjaman ] [ Pengembalian ] [ Riwayat ]|
+----------------------------------------------------------------+
```

### User Flow

```text
Login berhasil
      ↓
Dashboard Petugas
      ↓
Pilih menu yang diperlukan
      ↓
 ┌────┼──────────┬──────────────┬──────────┐
 ↓    ↓          ↓              ↓          ↓
Buku Anggota Peminjaman   Pengembalian Riwayat
```

---

## 3. Peminjaman Buku

### Wireframe

```text
+------------------------------------------------+
|              PEMINJAMAN BUKU                   |
+------------------------------------------------+
|                                                |
| Anggota                                        |
| +--------------------------------------------+ |
| | Pilih anggota                         ▼    | |
| +--------------------------------------------+ |
|                                                |
| Buku                                            |
| +--------------------------------------------+ |
| | Pilih buku                            ▼    | |
| +--------------------------------------------+ |
|                                                |
| Tanggal Peminjaman                             |
| +--------------------------------------------+ |
| | 10/09/2026                                 | |
| +--------------------------------------------+ |
|                                                |
| Tanggal Pengembalian                            |
| +--------------------------------------------+ |
| | 17/09/2026                                 | |
| +--------------------------------------------+ |
|                                                |
|           [ SIMPAN PEMINJAMAN ]                |
+------------------------------------------------+
```

### User Flow

```text
Dashboard
    ↓
Pilih "Peminjaman"
    ↓
Pilih anggota
    ↓
Pilih buku
    ↓
Sistem mengecek stok buku
    ↓
   ┌───────────────┐
   ↓               ↓
Tersedia        Tidak tersedia
   ↓               ↓
Isi tanggal      Tampilkan
   ↓             pesan error
Simpan
   ↓
Sistem menyimpan transaksi
   ↓
Stok buku berkurang
   ↓
Peminjaman berhasil
```

### Edge Case

* Anggota belum dipilih.
* Buku belum dipilih.
* Stok buku habis.
* Data peminjaman gagal disimpan.

---

## 4. Pengembalian Buku

### Wireframe

```text
+------------------------------------------------+
|             PENGEMBALIAN BUKU                  |
+------------------------------------------------+
|                                                |
| Cari Peminjaman                                |
| +--------------------------------+ [ CARI ]   |
| | Nama / ID Anggota              |             |
| +--------------------------------+             |
|                                                |
| Data Peminjaman                                |
| +--------------------------------------------+ |
| | Anggota       : Andi                       | |
| | Buku          : Pemrograman Web             | |
| | Tanggal Pinjam: 03/09/2026                 | |
| | Jatuh Tempo   : 10/09/2026                 | |
| | Status        : Dipinjam                   | |
| +--------------------------------------------+ |
|                                                |
|              [ PROSES PENGEMBALIAN ]           |
+------------------------------------------------+
```

### User Flow

```text
Dashboard
    ↓
Pilih "Pengembalian"
    ↓
Cari data peminjaman
    ↓
Pilih transaksi
    ↓
Sistem mengecek tanggal pengembalian
    ↓
   ┌───────────────┐
   ↓               ↓
Tepat waktu     Terlambat
   ↓               ↓
Tidak ada       Hitung denda
denda               ↓
   └───────┬───────┘
           ↓
Proses pengembalian
           ↓
Status menjadi "Dikembalikan"
           ↓
Stok buku bertambah
           ↓
Pengembalian berhasil
```

### Edge Case

* Data peminjaman tidak ditemukan.
* Buku sudah dikembalikan.
* Pengembalian terlambat.
* Gagal memperbarui data.

---

## 5. Riwayat Peminjaman

### Wireframe

```text
+----------------------------------------------------------------+
|                    RIWAYAT PEMINJAMAN                          |
+----------------------------------------------------------------+
|                                                                |
| Cari Data                                                      |
| +--------------------------------------+ [ CARI ]              |
| | Nama anggota / judul buku            |                       |
| +--------------------------------------+                       |
|                                                                |
| Status: [ Semua ▼ ]                                            |
|                                                                |
| +------------------------------------------------------------+ |
| | Anggota | Buku             | Pinjam     | Kembali | Status | |
| +------------------------------------------------------------+ |
| | Andi    | Pemrograman Web  | 03/09/2026 |10/09/26 | Selesai| |
| | Budi    | Basis Data       | 04/09/2026 |    -     | Dipinjam| |
| | Citra   | Java Dasar       | 05/09/2026 |09/09/26 | Selesai| |
| +------------------------------------------------------------+ |
|                                                                |
| [ < Sebelumnya ]                              [ Berikutnya > ] |
+----------------------------------------------------------------+
```

### User Flow

```text
Dashboard
    ↓
Pilih "Riwayat"
    ↓
Sistem menampilkan data peminjaman
    ↓
Petugas dapat mencari data
    ↓
Petugas dapat memilih filter status
    ↓
Sistem menampilkan hasil
    ↓
Petugas melihat riwayat transaksi
```

### Edge Case

* Belum ada riwayat transaksi.
* Data pencarian tidak ditemukan.
* Filter tidak menghasilkan data.

---

## 6. User Flow Keseluruhan

```text
                         +-------------+
                         |    LOGIN    |
                         +------+------+
                                |
                                ↓
                    +-----------------------+
                    | DASHBOARD PETUGAS     |
                    +----------+------------+
                               |
        +----------+-----------+-----------+----------+
        |          |           |           |          |
        ↓          ↓           ↓           ↓          ↓
      Buku      Anggota   Peminjaman  Pengembalian  Riwayat
        |          |           |           |          |
        |          |           ↓           ↓          |
        |          |      Transaksi   Transaksi       |
        |          |           |           |          |
        +----------+-----------+-----------+----------+
                               |
                               ↓
                        Data Perpustakaan
```

---

## 7. Hak Akses Pengguna

### Tamu

```text
Tamu
 ↓
Beranda
 ↓
Daftar Buku
```

Tamu hanya dapat melihat informasi umum dan daftar buku.

### Petugas

```text
Petugas
 ↓
Login
 ↓
Dashboard
 ├── Buku
 ├── Anggota
 ├── Peminjaman
 ├── Pengembalian
 └── Riwayat
```

Petugas memiliki akses untuk mengelola data dan transaksi perpustakaan.

---

## 8. Kesimpulan

Wireframe digunakan sebagai rancangan awal tampilan sebelum proses implementasi dilakukan. User flow digunakan untuk menggambarkan urutan aktivitas pengguna ketika menjalankan fitur tertentu.

Rancangan ini menjadi acuan untuk tahap pengembangan aplikasi SIMPUS-Mini pada tahap berikutnya.
