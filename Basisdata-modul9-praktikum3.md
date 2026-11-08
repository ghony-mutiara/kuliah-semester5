<h1>Kegiatan Praktikum 3 – Basis Data Terdistribusi</h1>

<h3>Pemasangan XAMPP di Komputer 2 (Linux Ubuntu)</h3>

1. Buka web browser di Ubuntu. Kunjungi situs https://www.apachefriends.org dan unduh installer XAMPP for Linux. File ini akan otomatis tersimpan di folder Downloads pada Ubuntu.
2. Buka aplikasi Terminal di Ubuntu, kemudian masuk ke direktori unduhan dengan mengetikkan perintah:
```bash
cd Downloads
````
3. Eksekusi installer dengan mengetikkan perintah:
```bash
sudo ./xampp-linux-x64-7.4.10-0-installer.run
```
4. Jika terdapat error "Permission Denied", masukkan perintah:
```bash
chmod +x xampp-linux-x64-8.2.4-0-installer.run
``` 
6. Masukkan password akun Ubuntu saat diminta untuk memberikan izin instalasi.
7. Ikuti proses Setup Wizard dengan menekan Next >. Pastikan komponen XAMPP Core Files dan XAMPP Developer Files terpilih. XAMPP akan diinstal ke direktori /opt/lampp. Selesaikan instalasi hingga muncul tombol Finish.
8. Buka XAMPP Control Panel, masuk ke tab Manage Servers, lalu klik Start untuk menjalankan Apache Web Server dan MySQL Database.
9. Uji keberhasilan instalasi dengan mengakses http://localhost/phpmyadmin melalui browser Ubuntu.

<h3>Konfigurasi Replikasi Basis Data</h3>

**Konfigurasi Komputer 1 (Master - Windows 10)**

1. Aktifkan Apache dan MySQL pada XAMPP Control Panel Windows 10. Buka http://localhost/phpmyadmin dan masuk ke menu Replication.
2. Pada bagian Master replication, klik configure it. Pilih basis data rumahsakit untuk direplikasi.
3. Terdapat 4 baris kode konfigurasi yang muncul. Salin kode tersebut, buka XAMPP Control Panel, klik Config -> my.ini, lalu paste 4 baris kode tersebut (server-id, log_bin, log_error, dan binlog_do_db) ke dalam file my.ini dan simpan.
4. Lakukan Restart pada service MySQL di XAMPP Control Panel.
5. Kembali ke phpMyAdmin, klik tombol Go pada halaman konfigurasi master tadi. Catat data pada Show master status (khususnya nilai File dan Position).
6. Buka menu User accounts dan klik Add user account untuk membuat akun replikasi.
7. Isi Username, Hostname (isi dengan IP Address Komputer 2/Ubuntu), dan Password.
8. Centang opsi Replication client dan Replication slave, lalu klik Go.
9. Pilih basis data rumahsakit, klik tab Export, tekan Go, dan simpan file rumahsakit_export.sql.
10. Unggah file rumahsakit_export.sql ke Google Drive atau kirimkan file tersebut ke email sendiri melalui browser di Windows 10, agar nanti bisa di pakai oleh komputer 2.

**Konfigurasi Komputer 2 (Slave - Linux Ubuntu)**

1. Buka web browser di Ubuntu, masuk ke akun email atau Google Drive, lalu unduh file rumahsakit_export.sql dan simpan ke folder Documents.
2. Buka Terminal, jalankan XAMPP dengan perintah:
```bash
cd /opt/lampp lalu sudo ./manager-linux-x64.run
```
3. Jalankan service MySQL dan Apache.
4. Buka phpMyAdmin di browser Ubuntu, buat basis data baru bernama rumahsakit. Klik menu Import, cari file rumahsakit_export.sql yang disimpan, lalu klik Go.
5. Klik menu Replication di phpMyAdmin, lalu pada Slave replication klik configure it.
6. Isi User name dan Password sesuai dengan akun replikasi yang dibuat di Windows, isi Host dengan IP Address Windows 10, dan Port 3306. Jangan klik Go terlebih dahulu. Salin kode server-id yang ditampilkan di layar.
7. Pada XAMPP Control Panel di Ubuntu, klik Configure -> Open Conf File -> Yes untuk membuka my.cnf. Hilangkan tanda # pada server-id, masukkan angka server-id yang disalin, dan tambahkan baris
```sql
replicate-do-db=rumahsakit
```
8. Jika file tidak bisa disimpan karena read-only, ubah hak aksesnya melalui terminal menggunakan perintah:
```bash
cd /opt/lampp/etc
```
```bash
sudo chmod a+rwx my.cnf
```
9. Simpan file my.cnf dan Restart service Apache dan MySQL di XAMPP. Kembali ke browser phpMyAdmin, lalu klik Go.
10. Jika muncul peringatan "Connection server disable...", ubah hak akses file konfigurasi melalui terminal dengan perintah:
```bash
cd /opt/lampp/phpmyadmin/libraries
```
```bash
sudo chmod a+rwx config.default.php
```
11. Buka file tersebut dan ubah nilai $cfg['AllowArbitraryServer'] = false menjadi true, lalu simpan dan restart service XAMPP kembali.
12. Untuk mengaktifkan Slave via Terminal, buka Terminal Ubuntu, masuk ke direktori MySQL dengan perintah:
```bash
cd /opt/lampp/bin
```
```bash
sudo ./mysql -u root
```
13. Untuk melihat status slave ketikkan perintah:
```sql
show status slave;
```
14. Jika error (slave tidak aktif), lanjutkan ke langkah konfigurasi. Jika error tetapi slave dalam keadaan aktif, hentikan dulu dengan perintah:
```sql
stop slave;
```
15. Ketikkan perintah berikut (sesuaikan Log File dan Log Pos berdasarkan Master Status yang dicatat dari Windows 10):
```sql
CHANGE MASTER TO
MASTER_HOST='192.168.56.1',
MASTER_USER='prodisi',
MASTER_PASSWORD='prodisi',
MASTER_LOG_FILE='mysql-bin.000014',
MASTER_LOG_POS=2926;
```
17. Untuk memulai slave ketikkan perintah:
```sql
start slave;
```
18. Cek kembali status di phpMyAdmin menu Replication. Jika nilai Slave_IO_Running dan Slave_SQL_Running menunjukkan Yes, maka konfigurasi telah berhasil.

<h3>Pengujian Replikasi Basis Data</h3>

1. Buka tabel obat pada komputer 1 (Windows 10 - Master).
2. Lakukan insert data, contoh: menambahkan obat "Demam" dengan kode A005, harga 1500, dan stok 100.
```sql
INSERT INTO obat (kode_obat, nama_obat, harga, stok) 
VALUES ('A005', 'Demam', 1500, 100);
```
3. Cek tabel obat pada komputer 2 (Ubuntu - Slave).
```sql
SELECT * FROM obat;
```

Jika data tersebut secara otomatis bertambah dan identik dengan data di komputer 1, maka proses replikasi basis data satu arah (master to slave) telah sukses dijalankan.

