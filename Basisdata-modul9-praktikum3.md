<h1>Kegiatan Praktikum 3 – Basis Data Terdistribusi</h1>

<h3>Pemasangan XAMPP di Komputer 2 (Linux Ubuntu)</h3>

1. Buka browser (seperti Mozilla Firefox) langsung di dalam sistem operasi Ubuntu. Kunjungi situs https://www.apachefriends.org dan unduh installer XAMPP for Linux. File ini akan otomatis tersimpan di folder Downloads pada Ubuntu.
2. Buka aplikasi Terminal di Ubuntu, kemudian masuk ke direktori unduhan dengan mengetikkan perintah
```bash
cd Downloads
````
3. Lalu tekan ENTER.
4. Eksekusi installer dengan mengetikkan
```bash
sudo ./xampp-linux-x64-7.4.10-0-installer.run
```
5. Lalu tekan ENTER.
6. Masukkan password akun Ubuntu Anda saat diminta untuk memberikan izin instalasi.
7. Ikuti proses Setup Wizard dengan menekan Next >. Pastikan komponen XAMPP Core Files dan XAMPP Developer Files terpilih. XAMPP akan diinstal ke direktori /opt/lampp. Selesaikan instalasi hingga muncul tombol Finish.
8. Buka XAMPP Control Panel, masuk ke tab Manage Servers, lalu klik Start untuk menjalankan Apache Web Server dan MySQL Database.
9. Uji keberhasilan instalasi dengan mengakses http://localhost/phpmyadmin melalui browser Ubuntu.
