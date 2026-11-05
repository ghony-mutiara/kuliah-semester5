<h1>Kegiatan Praktikum 1 - Aplikasi Basis Data</h1>

1. Install XAMPP di URL https://www.apachefriends.org/index.html dan lakukan instalasi.
2. Buka XAMPP Control Panel, aktifkan service modul Apache dan MySQL dengan klik Start. Service dinyatakan aktif jika sudah berwarna hijau.
3. Buka Web Browser, lalu ketikkan http://localhost/phpmyadmin/ untuk mengakses phpMyadmin.

<h1>Kegiatan Praktikum 2 - SQL dengan XAMPP</h1>

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

**Praktik DDL (Data Definition Language)**
1. Membuat basis data.
```sql
CREATE DATABASE rumahsakit;
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
CREATE TABLE pasien (
  id_pasien int (3) PRIMARY KEY AUTO_INCREMENT,
  nama_pasien varchar(30),
  alamat_pasien varchar(100),
  jenis_kelamin varchar(1),
  penyakit varchar(100),
  no_hp varchar(15)
);
```
5. Membuat tabel administrator.
```sql
CREATE TABLE administrator (
  id_admin int (3) PRIMARY KEY AUTO_INCREMENT,
  nama_admin varchar(30),
  waktu_jaga varchar(100)
);
```
6. Membuat tabel dokter.
```sql
CREATE TABLE dokter (
  id_dokter int (3) PRIMARY KEY AUTO_INCREMENT,
  nama_dokter varchar(30),
  alamat_dokter varchar(100),
  tanggal_lahir date,
  no_hp varchar (15),
  spesialis varchar (15),
  waktu_kerja varchar (100)
);
```
7. Membuat tabel dokter_admin.
```sql
CREATE TABLE dokter_admin (
  id_data int (3) PRIMARY KEY AUTO_INCREMENT,
  id_dokter int (3),
  id_admin int(3)
);
```
8. Membuat tabel pasien_dokter.
```sql
CREATE TABLE pasien_dokter (
  id int (3) PRIMARY KEY AUTO_INCREMENT,
  id_dokter int (3),
  id_pasien int (3),
  waktu_periksa date,
  resep varchar (100)
);
```
9. Membuat tabel daftar.
```sql
CREATE TABLE daftar (
  id_daftar int (3) PRIMARY KEY AUTO_INCREMENT,
  id_pasien int (3),
  id_admin int (3)
);
```
10. Melihat tabel.
```sql
show tables;
```

**Praktik DML (Data Manipulation Language)**
1. Memasukkan data ke tabel.
```sql
INSERT INTO pasien (id_pasien, nama_pasien, alamat_pasien, jenis_kelamin) 
VALUES 
  (1, 'Joko Widodo', 'Jalan Pakis haji no 35 Jakarta', 1),
  (2, 'Budi Santoso', 'Jalan Pucuk Merah no 10 Palangkaraya', 1),
  (3, 'Siti Aminah', 'Jalan Sri Rejeki no 88 Bekasi', 2);
  (4, 'Prabowo Subianto', 'Jalan Lidah Buaya no 3 Jakarta', 1),
  (5, 'Megawati Soekarnoputri', 'Jalan Lidah Mertua no 79 Jakarta', 2);
```
2. Mengambil seluruh data pada tabel.
```sql
SELECT * FROM pasien;
```
3. Mengambil field spesifik.
```sql
SELECT nama_pasien, jenis_kelamin from pasien;
```
4. Mengambil data dengan syarat.
```sql
SELECT nama_pasien, jenis_kelamin from pasien where jenis_kelamin='1';
```
5. Mengambil data dari gabungan beberapa tabel.
```sql
SELECT p.nama_pasien, pd.waktu_periksa, pd.resep, d.nama_dokter 
FROM pasien p 
JOIN pasien_dokter pd ON p.id_pasien = pd.id_pasien 
JOIN dokter d ON pd.id_dokter = d.id_dokter;
```
6. Mengambil data dari gabungan tabel dengan syarat tambahan.
```sql
SELECT p.nama_pasien, pd.waktu_periksa, pd.resep, d.nama_dokter 
FROM pasien p 
JOIN pasien_dokter pd ON p.id_pasien = pd.id_pasien 
JOIN dokter d ON pd.id_dokter = d.id_dokter 
WHERE d.id_dokter='1';
```
7. Menghitung banyaknya baris data.
```sql
SELECT count(id_pasien) from pasien;
```
8. Mengambil data berdasarkan potongan string dari kiri.
```sql
SELECT * FROM pasien WHERE left(alamat_pasien,2)='Jl';
```
9. Mengambil data di antara dua rentang nilai.
```sql
SELECT * FROM pasien WHERE id_pasien BETWEEN 3 AND 5;
```
10. Mengambil data berdasarkan potongan karakter tertentu.
```sql
SELECT * FROM pasien WHERE alamat_pasien LIKE '%Jakarta%';
```
11. Mengurutkan data secara menurun.
```sql
SELECT * FROM pasien ORDER BY id_pasien DESC;
```
12. Mengelompokkan data berdasarkan field tertentu.
```sql
SELECT * FROM pasien GROUP BY jenis_kelamin;
```
13. Mengubah data spesifik.
```sql
UPDATE pasien SET nama_pasien='Mirna Maryati' WHERE id_pasien=5;
```
14. Menghapus data.
```sql

```













