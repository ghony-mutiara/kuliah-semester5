<h1>Praktikum 1 - Aplikasi Basis Data</h1>

1. Install XAMPP di URL https://www.apachefriends.org/index.html dan lakukan instalasi.
2. Buka XAMPP Control Panel, aktifkan service modul Apache dan MySQL dengan klik Start. Service dinyatakan aktif jika sudah berwarna hijau.
3. Buka Web Browser, lalu ketikkan http://localhost/phpmyadmin/ untuk mengakses phpMyadmin.

<h1>Praktikum 2 - SQL dengan XAMPP</h1>

<h3>Menggunakan Command Prompt (CMD)</h3>

**Mengakses Basis Data**
1. Buka CMD dan arahkan directory aktif ke dalam folder XAMPP.
```bash
cd \xampp\mysql\bin
```
2. Masuk ke dalam MySQL.
```bash
Mysql -u root
```

**Praktik DDL (Data Definition Language**
1. Membuat basis data.
```sql
CREATE DATABASE rumahsakit;
```
```sql
CREATE DATABASE rumahduka;
```
2. Menghapus basis data.
```sql
DROP DATABASE rumahduka;
```
3. Mengaktifkan basis data.
```sql
use rumahsakit;
```
4. Membuat tabel pasien.
```sql
CREATE TABLE pasien (id_pasien int (3) PRIMARY KEY AUTO_INCREMENT, nama_pasien varchar(30), alamat_pasien varchar(100), jenis_kelamin varchar(1), penyakit varchar(100), no_hp varchar(15));
```
5. Membuat tabel administrator.
```sql
CREATE TABLE administrator (id_admin int (3) PRIMARY KEY AUTO_INCREMENT, nama_admin varchar(30), waktu_jaga varchar(100))
```
6. Membuat tabel dokter.
```sql
CREATE TABLE dokter (id_dokter int (3) PRIMARY KEY AUTO_INCREMENT, nama_dokter varchar(30), alamat_dokter varchar(100), tanggal_lahir date, no_hp varchar (15), spesialis varchar (15), waktu_kerja varchar (100))
```
7. Membuat tabel dokter_admin.
```sql
CREATE TABLE dokter_admin (id_data int (3) PRIMARY KEY AUTO_INCREMENT, id_dokter int (3), id_admin int(3))
```
8. Membuat tabel pasien_dokter.
```sql
CREATE TABLE pasien_dokter (id int (3) PRIMARY KEY AUTO_INCREMENT, id_dokter int (3), id_pasien int (3), waktu_periksa date, resep varchar (100))
```
9. Membuat tabel daftar.
```sql
CREATE TABLE daftar (id_daftar int (3) PRIMARY KEY AUTO_INCREMENT, id_pasien int (3), id_admin int (3))
```
10. Melihat tabel.
```sql
show tables;
```


