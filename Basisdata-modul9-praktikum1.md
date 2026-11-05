<h1>Kegiatan Praktikum 1 - Praktikum Transaksi</h1>

<h3>Persiapan Basis Data & XAMPP</h3>

1. Buka XAMPP Control Panel, aktifkan service modul Apache dan MySQL dengan klik Start. Service dinyatakan aktif jika sudah berwarna hijau.
2. Buka web browser dan akses URL http://localhost/phpmyadmin/.
3. Pilih basis data rumah sakit yang telah disiapkan sebelumnya pada praktikum Modul 6.
4. Periksa tipe tabel (Storage Engine) pada basis data tersebut dan pastikan tipenya adalah InnoDB. Transaksi dalam basis data MySQL hanya dapat berjalan jika menggunakan storage engine InnoDB (atau BDB).

<h3>Praktikum Commit</h3>

**Membuat Transaksi Tanpa Commit (transaksi1)**
Langkah pertama adalah membuat transaksi untuk memasukkan data pasien baru tanpa perintah commit. Data yang akan dimasukkan adalah id_pasien = 6, nama_pasien = Tito, alamat_pasien = Jl.Pakis Haji no 23, dan jenis_kelamin = 1.

1. Pilih basis data rumahsakit, kemudian masuk ke menu Routines.
2. Klik Add routine.
3. Pada kotak dialog yang muncul, isi Routine name dengan transaksi1 dan pastikan Type adalah PROCEDURE.
4. Pada kolom Definition, masukkan kode SQL berikut:

5. Klik Go untuk menyimpan.
6. Buka menu SQL dan jalankan routine tersebut dengan memasukkan perintah CALL transaksi1;.
7. Layar akan menampilkan hasil query di mana data pasien dengan id 6 (Tito) muncul.
8. Buka tabel pasien untuk memverifikasi. Pada tabel tersebut, Anda akan melihat bahwa data dengan id_pasien 6 tidak ada.
Kesimpulannya, perintah apapun yang disimpan pada sebuah transaksi tidak akan masuk ke dalam tabel basis data jika belum diakhiri dengan commit.

**Membuat Transaksi Dengan Commit (transaksi2)**
Untuk memastikan data tersimpan secara permanen ke dalam tabel, perintah transaksi harus dimodifikasi dengan menambahkan COMMIT.

1. Buat store procedure baru (melalui Add routine) dan beri nama transaksi2.
2. Masukkan modifikasi kode SQL berikut pada kolom Definition:

3. Klik Go untuk menyimpannya.
4. Buka menu SQL dan eksekusi perintah CALL transaksi2;.
5. Buka kembali tabel pasien. Kini Anda dapat melihat bahwa data id_pasien 6 telah berhasil masuk ke dalam tabel pasien. 
Kesimpulan dari commit adalah jika perintah SQL belum sampai pada commit, maka perintah tersebut tidak akan merubah isi data tabel.



