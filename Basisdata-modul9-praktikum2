<h1>Kegiatan Praktikum 2 - Intalasi Virtual Box dan Instalasi Sistem Operasi Linux Ubuntu</h1>

<h3>Pemasangan Aplikasi Virtual Box</h3>

1. Buka browser dan unduh aplikasi VirtualBox secara gratis melalui situs resmi https://www.virtualbox.org/.
2. Setelah diunduh, klik double click pada file instalasi.
3. Pada jendela Welcome to the Oracle VM VirtualBox Setup Wizard, klik Next.
4. Pada jendela Custom Setup, biarkan pengaturan secara default, lalu klik Next pada tahap opsi fitur maupun shortcut.
5. Akan muncul peringatan Warning: Network Interfaces yang akan memutuskan jaringan sementara saat instalasi. Klik Yes.
6. Klik Install pada jendela Ready to Install.
7. Jika muncul jendela konfirmasi Windows Security ("Would you like to install this device software?"), klik Install.
8. Setelah proses selesai, biarkan opsi "Start Oracle VM VirtualBox" dicentang, lalu klik Finish.

<h3>Pemasangan Sistem Operasi Linux Ubuntu</h3>

Sebelum memulai, unduh file ISO sistem operasi Ubuntu dari halaman https://ubuntu.com/download/desktop.

**Membuat Mesin Virtual Baru**

1. Buka aplikasi VirtualBox, lalu klik ikon Baru (New).
2. Isi Nama: ubuntu, pilih Tipe: Linux, dan Versi: Ubuntu (64-bit), lalu klik Lanjut.
3. Atur jumlah Ukuran memori (RAM) yang dialokasikan (misalnya: 2048 MB), lalu klik Lanjut.
4. Pada pengaturan Hard disk, pilih Buat hard disk virtual sekarang dan klik Buat.
5. Pilih Tipe berkas hard disk: VDI (VirtualBox Disk Image), klik Lanjut.
6. Pilih Penyimpanan pada hard disk fisik: Dialokasikan secara dinamik, klik Lanjut.
7. Tentukan lokasi penyimpanan file VDI dan atur batas ukurannya (misalnya 10.00 GB), lalu klik Buat.

**Pengaturan Penyimpanan File ISO dan Jaringan**

1. Pada antarmuka VirtualBox, pilih mesin virtual ubuntu yang baru dibuat, lalu klik Pengaturan.
2. Masuk ke menu Penyimpanan. Di bawah Pengendali IDE, klik tulisan Kosong. Pada bagian atribut di sebelah kanan, klik ikon disk (Drive Optik) lalu pilih Pilih sebuah berkas disk....
3. Cari dan pilih file ISO Ubuntu yang telah Anda unduh sebelumnya, lalu klik Open.
4. Selanjutnya masuk ke menu Jaringan. Pada Adaptor 1, ubah opsi "Terpasang pada" menjadi Adaptor Hanya-host (Host-Only Ethernet Adapter).
5. Klik opsi Tingkat Lanjut, kemudian klik ikon refresh (panah melingkar berwarna biru) pada kolom Alamat MAC untuk mencegah error (refresh mac address), kemudian klik OK.

**Proses Instalasi Ubuntu**

1. Klik tombol Mulai pada antarmuka utama VirtualBox.
2. Pada jendela Pilih disk awal mula, pastikan file ISO Ubuntu terpilih, lalu klik Mulai.
3. Tunggu proses pengecekan disk, lalu akan muncul jendela instalasi. Pilih Install Ubuntu.
4. Atur Keyboard layout ke English (US), klik Continue.
5. Pada Updates and other software, pilih Normal Installation dan centang opsi Install third-party software for graphics and Wi-Fi hardware..., lalu klik Continue.
6. Pada Installation type, pilih Something else untuk mengatur partisi secara manual, lalu klik Continue.
7. Klik New Partition Table... lalu klik Continue pada peringatan yang muncul.
8. Buat partisi Swap (cadangan memori): Klik ikon tambah (+), isi ukuran (misal 737 MB), pilih Logical, lalu pada Use as pilih swap area, klik OK.
9. Buat partisi Sistem (Ext4): Klik ruang kosong (free space), klik (+), isi ukuran (misal 10000 MB), pilih Logical, pada Use as pilih Ext4 journaling file system, dan pada Mount point ketik /, klik OK.
10. Klik Install Now, lalu klik Continue pada peringatan Write the changes to disks?.
11. Pada bagian Where are you?, pilih Jakarta Time, klik Continue.
12. Pada bagian Who are you?, isi Nama Anda, Nama komputer, Username, dan Password, lalu klik Continue.
13. Tunggu proses penyalinan file dan instalasi selesai. Jika sudah selesai, klik Restart Now.
14. Jika diminta untuk menekan ENTER (remove the installation medium), tekan ENTER pada keyboard Anda.
15. Saat Ubuntu menyala, pada jendela konfigurasi awal (Online Accounts, Livepatch, Help improve Ubuntu, Privacy), Anda dapat menekan Skip, Next, dan Done hingga selesai. Sistem operasi Ubuntu siap digunakan.

<h3>C. Pengecekan Koneksi Jaringan</h3>

Setelah instalasi selesai, Anda harus memastikan bahwa Komputer 1 (Windows 10) dapat saling berkomunikasi dengan Komputer 2 (Ubuntu).

**Cek IP Address Komputer 1 (Windows 10)**

1. Tekan tombol kombinasi Win + R pada keyboard, ketik cmd, dan tekan OK.
2. Di dalam Command Prompt, ketik ipconfig dan tekan Enter.
3. Catat alamat IP pada bagian Ethernet adapter VirtualBox Host-Only Network (misalnya 192.168.56.1).

**Cek IP Address Komputer 2 (Ubuntu)**

1. Di sistem operasi Ubuntu, klik ikon jaringan (network) di pojok kanan atas, pilih Wired Connected, lalu klik Wired Settings.
2. Klik ikon gerigi (pengaturan) pada menu Wired.
3. Catat IPv4 Address yang tertera (misalnya 192.168.56.104). Alamat ini menyesuaikan konfigurasi mesin virtual masing-masing.

**Pengujian Koneksi (Ping)**

1. Dari Komputer 2 (Ubuntu): Buka aplikasi Terminal (klik menu di pojok kiri bawah lalu cari "terminal"). Ketikkan ping 192.168.56.1 (alamat IP Windows 10). Jika sukses, pesan akan menampilkan balasan paket (bytes from...).
2. Dari Komputer 1 (Windows 10): Pada Command Prompt, ketik ping 192.168.56.104 (alamat IP Ubuntu). Jika sukses, hasilnya akan memunculkan teks Reply from 192.168.56.104.

Catatan: Jika hasil ping tidak menghasilkan Reply, pastikan Firewall pada komputer Windows dalam keadaan dinonaktifkan (non aktif).

 








