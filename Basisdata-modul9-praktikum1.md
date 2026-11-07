<h1>Kegiatan Praktikum 1 - Praktikum Transaksi</h1>

<h3>Persiapan Basis Data & XAMPP</h3>

1. Buka XAMPP Control Panel, aktifkan service modul Apache dan MySQL dengan klik Start. Service dinyatakan aktif jika sudah berwarna hijau.
2. Buka web browser dan akses URL http://localhost/phpmyadmin/.
3. Pilih basis data rumah sakit yang telah disiapkan sebelumnya pada praktikum Modul 6.
4. Periksa tipe tabel (Storage Engine) pada basis data tersebut dan pastikan tipenya adalah InnoDB. Transaksi dalam basis data MySQL hanya dapat berjalan jika menggunakan storage engine InnoDB atau BDB.

<h3>Praktikum Commit</h3>

**Membuat Transaksi Tanpa Commit (transaksi1)**

Langkah pertama adalah membuat transaksi untuk memasukkan data pasien baru tanpa perintah commit. Data yang akan dimasukkan adalah id_pasien = 6, nama_pasien = Tito, alamat_pasien = Jl.Pakis Haji no 23, dan jenis_kelamin = 1.

1. Pilih basis data rumahsakit, kemudian masuk ke menu Routines.
2. Klik Add routine.
3. Pada kotak dialog yang muncul, isi Routine name dengan transaksi1 dan pastikan Type adalah PROCEDURE.
4. Pada kolom Definition, masukkan kode SQL berikut:
```sql
BEGIN
START TRANSACTION;
INSERT INTO `pasien` (`id_pasien`, `nama_pasien`, `alamat_pasien`, `jenis_kelamin`)
VALUES (6, 'Tito', 'Jl.Pakis Haji no 23', '1');
SELECT * FROM pasien;
END
```
5. Klik Go untuk menyimpan.
6. Buka menu SQL dan jalankan routine tersebut dengan memasukkan perintah:
```sql
CALL transaksi1;
```
7. Layar akan menampilkan hasil query di mana data pasien dengan id 6 (Tito) muncul.
8. Buka tabel pasien untuk memverifikasi. Pada tabel tersebut, akan terlihat bahwa data dengan id_pasien 6 tidak ada.

Kesimpulannya, perintah apapun yang disimpan pada sebuah transaksi tidak akan masuk ke dalam tabel basis data jika belum diakhiri dengan commit.

**Membuat Transaksi Dengan Commit (transaksi2)**

Untuk memastikan data tersimpan secara permanen ke dalam tabel, perintah transaksi harus dimodifikasi dengan menambahkan COMMIT.

1. Buat store procedure baru (melalui Add routine) dan beri nama transaksi2.
2. Masukkan modifikasi kode SQL berikut pada kolom Definition:
```sql
BEGIN
START TRANSACTION;
INSERT INTO `pasien` (`id_pasien`, `nama_pasien`, `alamat_pasien`, `jenis_kelamin`)
VALUES (6, 'Tito', 'Jl.Pakis Haji no 23', '1');
SELECT * FROM pasien;
COMMIT;
END
```
3. Klik Go untuk menyimpannya.
4. Buka menu SQL dan eksekusi perintah CALL transaksi2;.
5. Buka kembali tabel pasien. Kini dapat terlihat bahwa data id_pasien 6 telah berhasil masuk ke dalam tabel pasien. 

Kesimpulan dari commit adalah jika perintah SQL belum sampai pada commit, maka perintah tersebut tidak akan merubah isi data tabel.

<h3>Praktikum 2 Rollback</h3>

Pernyataan rollback digunakan untuk menggugurkan perintah yang sedang berjalan. Perintah ini berguna untuk mengantisipasi hal yang tidak diinginkan pada sistem, namun hanya akan berpengaruh jika perintah yang sedang berjalan belum di-commit.

**Menggugurkan Perintah Update (transaksi3)**

Sebagai contoh, kita akan menjalankan perintah update data untuk mengubah nama pasien "Popi" menjadi "Danar" dengan id_pasien = 3.

1. Buat routine baru dengan nama transaksi3.
2. Masukkan kode SQL berikut pada Definition:
```sql
BEGIN
START TRANSACTION;
UPDATE pasien SET nama_pasien='Danar' WHERE id_pasien='3';
ROLLBACK;
COMMIT;
SELECT * FROM pasien;
END
```
3. Simpan dengan klik Go.
4. Jalankan perintah CALL transaksi3; pada menu SQL.

Pada layar hasil, akan terlihat tidak ada perubahan data yang terjadi, karena perintah perubahan telah digugurkan oleh ROLLBACK sebelum COMMIT dilakukan.

**Menggugurkan Perintah Insert dan Melanjutkan Update (transaksi4)**

Pada kasus ini, kita akan memasukkan data baru pada tabel pasien, namun dilanjutkan dengan perintah rollback. Setelah perintah rollback, transaksi dilanjutkan dengan perintah update nama pasien menjadi "Septin" pada id_pasien 3, yang kemudian diakhiri dengan commit.

1. Buat routine baru bernama transaksi4.
2. Masukkan kode SQL modifikasi berikut pada Definition:
```sql
BEGIN
START TRANSACTION;
INSERT INTO `pasien` (`id_pasien`, `nama_pasien`, `alamat_pasien`, `jenis_kelamin`)
VALUES (7, 'Hanif', 'Jl.Babakan loa no 22', '1');
ROLLBACK;
UPDATE pasien SET nama_pasien='Septin' WHERE id_pasien='3';
COMMIT;
SELECT * FROM pasien;
END
```
3. Simpan dengan klik Go.
4. Panggil routine ini dengan mengetikkan CALL transaksi4; pada menu SQL.

Dari hasil tabel yang ditampilkan, terlihat bahwa tidak terjadi penambahan data baru pasien bernama Hanif karena telah di-rollback. Namun, pada perintah update terjadi perubahan data, yaitu nama pada id_pasien 3 berubah menjadi Septin.

<h3>Praktikum Check Point</h3>

Check point merupakan tempat titik di mana proses terakhir disimpan. Suatu perintah rollback membatalkan atau mengembalikan suatu perintah ke kondisi di mana transaksi belum terjadi. Namun, supaya sebuah transaksi berjalan dengan optimal, kondisi rollback tidak harus dikembalikan ke kondisi awal, akan tetapi bisa dikembalikan ke posisi tempat check point terakhir.

Sebagai contoh, akan dipraktikkan skenario di mana terdapat 3 buah data yang akan dimasukkan ke dalam basis data.

1. Buat sebuah routine baru (melalui Add routine) di halaman phpMyAdmin.
2. Isi Routine name dengan transaksi5 dan pastikan tipenya adalah PROCEDURE.
3. Pada bagian Definition, masukkan kode SQL berikut ini:
```sql
BEGIN
START TRANSACTION;
INSERT INTO `pasien` (`id_pasien`, `nama_pasien`, `alamat_pasien`, `jenis_kelamin`) 
VALUES (7, 'Hanif', 'Jl.Babakan loa no 22', '1');

SAVEPOINT POINT1;

INSERT INTO `pasien` (`id_pasien`, `nama_pasien`, `alamat_pasien`, `jenis_kelamin`) 
VALUES (8, 'Tina', 'Jl.Sangkuriang no 45', '2');

ROLLBACK TO SAVEPOINT POINT1;

INSERT INTO `pasien` (`id_pasien`, `nama_pasien`, `alamat_pasien`, `jenis_kelamin`) 
VALUES (9, 'Lutfhi', 'Jl. Dipenogoro 24', '1');

COMMIT;
SELECT * FROM pasien;
END
```
4. Berdasarkan kode di atas, setelah melakukan INSERT yang pertama, dilakukan proses penandaan menggunakan savepoint dengan nama point1.
5. Kemudian dilakukan INSERT data Tina, namun perintah tersebut di-rollback kembali ke titik savepoint point1.
6. Selanjutnya dilakukan kembali perintah INSERT yang data Lutfhi.
7. Klik tombol Go untuk menyimpan routine transaksi tersebut.
8. Untuk menjalankan transaksi ini, buka menu SQL dan lakukan pemanggilan dengan cara mengetikkan perintah CALL transaksi5;.

Hasil dari eksekusi transaksi 5 ini memperlihatkan bahwa data yang berhasil masuk ke dalam basis data hanya 2 data, yaitu id_pasien 7 (Hanif) dan id_pasien 9 (Lutfhi). Sedangkan data untuk id_pasien 8 (Tina) tidak masuk ke dalam basis data karena telah di-rollback kembali ke titik simpan point1 sebelum diakhiri dengan COMMIT.

<h3>Praktikum Check Trigger</h3>

Trigger merupakan sebuah perintah atau event yang dapat memicu perubahan sebuah basis data. Event yang dapat digunakan yaitu insert, update, dan delete. Event-event tersebut digabungkan dengan kata kunci pemicu, yaitu BEFORE (dilakukan sebelum perintah dilaksanakan) dan AFTER (dilakukan setelah perintah dilaksanakan).

Berikut adalah kombinasi perintah dalam trigger:

- BEFORE INSERT: Trigger berjalan sebelum perintah insert dilaksanakan.
- AFTER INSERT: Trigger berjalan setelah perintah insert dilaksanakan.
- BEFORE UPDATE: Trigger berjalan sebelum perintah update dilaksanakan.
- AFTER UPDATE: Trigger berjalan setelah perintah update dilaksanakan.
- BEFORE DELETE: Trigger berjalan sebelum perintah delete dilaksanakan.
- AFTER DELETE: Trigger berjalan setelah perintah delete dilaksanakan.

**Persiapan Basis Data dan Tabel**

Untuk menjalankan trigger, Anda harus menyiapkan tabel-tabel pada basis data rumahsakit dan menambahkan 2 tabel baru.

1. Tabel obat:
```sql
CREATE TABLE obat (
  id_obat INT(6) AUTO_INCREMENT PRIMARY KEY,
  kode_obat VARCHAR(5),
  nama_obat VARCHAR(30),
  harga integer(10),
  stok integer(5)
);
```
2. Tabel transaksi_obat:
```sql
CREATE TABLE transaksi_obat (
  id_transaksi int(3) AUTO_INCREMENT PRIMARY KEY,
  id_pasien INT(3),
  id_obat INT(6),
  jumlah int(10),
  total_harga int(10)
);
```

Masukkan kode SQL di atas pada menu SQL untuk membuat kedua tabel tersebut. Selanjutnya, relasikan tabel-tabel tersebut dengan mengklik menu Designer, lalu pilih Show/Hide table list, dan centang seluruh tabel agar siap direlasikan.

Sebelum masuk ke trigger, isi tabel obat dengan minimal 3 data. Sebagai contoh:

- id_obat 1: Amikacin (stok 10).
- id_obat 2: Amoxillin (stok 20).
- id_obat 3: Betadine (stok 5).

```sql
INSERT INTO obat (id_obat, kode_obat, nama_obat, harga, stok)
VALUES 
  (1, 'K0001', 'Amikacin', 50000, 10),
  (2, 'K0002', 'Amoxillin', 15000, 20),
  (3, 'K0003', 'Betadine', 10000, 5);
```

**Membuat Trigger**

Kasus yang dipraktikkan adalah seorang pasien membeli obat Amoxillin sebanyak 5 buah. Ketika atribut jumlah pada tabel transaksi_obat diisi, stok pada tabel obat harus berkurang secara otomatis.

Berikut adalah kode SQL dan penjelasan untuk membuat trigger tersebut:
```sql
DELIMITER $$
CREATE TRIGGER tg_jual AFTER INSERT
ON transaksi_obat
FOR EACH ROW
BEGIN
  UPDATE obat 
  SET stok = stok - new.jumlah
  WHERE id_obat = new.id_obat;
END $$
DELIMITER ;
```

Penjelasan kode:

- DELIMITER $$: Batas awal sebuah event trigger.
- CREATE TRIGGER tg_jual AFTER INSERT: Membuat trigger bernama tg_jual yang akan dijalankan setelah data dimasukkan.
- ON transaksi_obat: Event trigger bekerja jika ada perubahan pada tabel transaksi_obat.
- FOR EACH ROW: Berlaku untuk setiap baris pada tabel transaksi_obat.
- BEGIN: Mulai eksekusi perintah SQL.
- UPDATE obat ...: Melakukan update pada atribut stok di tabel obat, yaitu mengurangi stok saat ini dengan data baru yang diinput ke transaksi_obat, dengan kondisi id_obat yang baru diinputkan sama dengan id_obat pada tabel obat.
- END $$: Akhir eksekusi perintah SQL.
- DELIMITER ;: Batas akhir sebuah event trigger.

Pada phpMyAdmin, Anda dapat memasukkan kode ini langsung melalui menu SQL atau melalui menu Triggers dengan mengklik Add trigger dan mengisikan detail namanya, tabel, waktu, event, dan definisi SQL-nya, lalu klik Go.

**Pengujian Trigger**

1. Perhatikan kondisi awal tabel obat, di mana stok Amoxillin berjumlah 20.
2. Masukkan data ke tabel transaksi_obat melalui phpMyAdmin tab Insert atau menu SQL dengan perintah:
```sql
INSERT INTO transaksi_obat (id_transaksi, id_pasien, id_obat, jumlah, total_harga)
VALUES
  (NULL, '1', '2', '5', '0');
```
3. Setelah data berhasil dimasukkan, periksa kembali tabel obat.
4. Kondisi stok Amoxillin secara otomatis berkurang sebanyak 5 menjadi 15 berdasarkan jumlah data yang dimasukkan pada tabel transaksi_obat.

Kesimpulan dari trigger adalah sebagai pemicu jika ada perubahan pada baris sebuah tabel, baik insert, update, ataupun delete, di dalam basis data.
 











