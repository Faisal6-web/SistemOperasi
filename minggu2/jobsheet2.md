# Laporan Praktikum Sistem Operasi Jobsheet 2

<h4>Nama : Faisal Rizky<h4>
<h4>NIM : 254107020224<h4>
<h4>Kelas : TI-1H<h4>

## 1.1 Deteksi Perangkat Keras di Linux ##

## Praktikum 2.1 Identifikasi CPU dan Memori
1. Tampilkan informasi CPU
Gambar: <img ![alt text](image-1.png) >

2. Tampilkan ringkasan memori
Gambar: <img ![alt text](image-2.png)>

3. (Opsional) cek informasi hardware dari DMI/BIOS (butuh sudo): 
Gambar: <img ![alt text](image.png)>
### Latihan 2.1 
Soal :
1. Catat: (1) jumlah CPU(s), core/thread, (2) total RAM, (3) total swap. 
2. Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.

Jawaban :
1. CPU : 6, core/thread : 1 RAM: 2GB
2. RAM: perangkat keras yang digunakan untuk menyimpan data sementara.
Swap: bentuk lain dari RAM yang menggunakan sebagian storage dari hdd atau ssd untuk dijadikan sebagai RAM. Swap digunakan ketika RAM sudah habis digunakan.


## Praktikum 2.2 — Identifikasi Perangkat PCI/USB dan Driver
1. Lihat daftar perangkat PCI
Gambar : <img ![alt text](image-3.png)>
2. Lihat perangkat PCI beserta driver kernel yang digunakan:
Gambar : <img ![alt text](image-4.png)>
3. Fokus pada NIC (Ethernet) untuk mencari modul driver
Gambar : <img ![alt text](image-5.png)>
4. Lihat perangkat USB 
Gambar : <img ![alt text](image-6.png)>
5. Lihat topologi USB (tree)
Gambar : <img ![alt text](image-7.png)>
### Latihan 2.2
Soal :
1. Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.

Jawaban :
1. VGA compatible controller : VMware SVGA II Adapter
Device ID : 15ad:0405
nama driver : vmwgfx
Perangkat ini adalah kartu grafis virtual yang berfungsi menjembatani komunikasi antara sistem operasi tamu (Ubuntu) dengan kartu grafis fisik di komputer asli (Host) agar Ubuntu bisa merender antarmuka visual (GUI).



## Praktikum 2.3 — Identifikasi Storage dan Filesystem
1. Lihat daftar disk/partisi
Gambar : <img ![alt text](image-8.png)>
2. Tampilkan UUID dan tipe filesystem
Gambar : <img ![alt text](image-9.png)>
3. Lihat mount point untuk root filesystem
Gambar : <img ![alt text](image-10.png)>

## 1.2 Modul Kernel dan Driver Perangkat ##


## Praktikum 2.4 — Melihat Modul Aktif dan Informasinya
1. Cek versi kernel
Gambar : <img ![alt text](image-11.png)>
2. Tampilkan daftar modul aktif
Gambar : <img ![alt text](image-12.png)>
3.  Pilih salah satu modul (contoh aman: loop) dan lihat detailnya
Gambar : <img ![alt text](image-13.png)>
4. Muat modul (jika belum aktif), lalu verifikasi
Gambar : <img ![alt text](image-14.png)>
5. (Opsional) lihat pesan kernel terbaru
Gambar : <img ![alt text](image-15.png)>


## Praktikum 2.5 — Konfigurasi Auto-load dan Blacklist
1. Buat file auto-load
Gambar : <img ![alt text](image-16.png)>
2. Simulasikan verifikasi (tanpa reboot) dengan memastikan modul sudah aktif
Gambar : <img ![alt text](image-17.png)>
3. (Opsional, konsep) blacklist modul
Gambar : <img ![alt text](image-18.png)>


## 1.3 Sistem File dan /dev di Linux ##


## Praktikum 2.6 — Mengenali Block vs Character Device
1. Manajemen Perangkat Keras & Perintah Dasar Sistem Operasi 
Gambar : <img ![alt text](image-19.png)>
2. Lihat detail device terminal
Gambar : <img ![alt text](image-20.png)>
3. Lihat disk dan partisi untuk mengaitkan dengan /dev 
Gambar : <img ![alt text](image-21.png)>
### Latihan 2.3
Soal:
1. Dari output ls -l, jelaskan perbedaan penanda file untuk block device dancharacter device. (Hint: karakter pertama pada permission string)
Jawaban : 
1. Karakter pertama pada permission string menunjukkan tipe filenya. B untuk Block device, sedangkan C untuk Character device

## Praktikum 2.7 — Melihat Informasi udev
1. Cek atribut udev untuk disk
Gambar : <img ![alt text](image-22.png)>
2. (Opsional) monitor event udev (jalankan, lalu colok/lepas USB pada mesin fisik) 
Gambar : <img ![alt text](image-23.png)>


## 1.4 Perintah Dasar Terminal Linux ##


## Praktikum 2.8 — Membuat Workspace Praktikum
1. Buat direktori praktikum dan masuk ke dalamnya
Gambar : <img ![alt text](image-24.png)>
2. Buat beberapa file contoh
Gambar : <img ![alt text](image-25.png)>
3. Isi file log contoh (simulasi)
Gambar : <img ![alt text](image-26.png)>
4. Baca file dengan less
Gambar : <img ![alt text](image-27.png)>


## 1.5 Manipulasi Teks ##


## Praktikum 2.9 — Pencarian Pola dengan grep
1. Cari baris yang mengandung ERROR pada data.log
Gambar : <img ![alt text](image-28.png)>
2. Cari tanpa memperhatikan huruf besar/kecil
Gambar : <img ![alt text](image-29.png)>
3. Tampilkan nomor baris: (grep -n " WARN " data . log)
Gambar : <img ![alt text](image-30.png)>
4. Tampilkan baris yang tidak cocok (invert match)
Gambar : <img ![alt text](image-31.png)>
### Latihan 2.4
1. Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif)
Jawaban : <img ![alt text](image-32.png)>

## Praktikum 2.10 — Substitusi dengan sed (Aman di File Latihan)
1. Siapkan file konfigurasi latihan
Gambar : <img ![alt text](image-33.png)>
2. Ganti dev menjadi prod (tanpa mengubah file asli)
Gambar : <img ![alt text](image-34.png)>
3. Terapkan perubahan langsung ke file (-i)
Gambar : <img ![alt text](image-35.png)>
4. Ganti semua kemunculan kata (g untuk global), contoh ubah myserver menjadi node
Gambar : <img ![alt text](image-36.png)>

## Praktikum 2.11 — Ekstraksi Kolom dengan awk
1. Lihat output df -h
Gambar : <img ![alt text](image-37.png)>
2. Ambil kolom filesystem dan persentase pemakaian
Gambar : <img ![alt text](image-38.png)>
3. Filter hanya yang pemakaian disk di atas 80%
Gambar : <img ![alt text](image-39.png)>


## 1.6 Manajemen Proses ##


## Praktikum 2.12 — Melihat Proses dengan ps
1. Tampilkan semua proses (format BSD)
Gambar : <img ![alt text](image-40.png)>
2. Cari proses tertentu (misal sshd)
Gambar : <img ![alt text](image-41.png)>


## Praktikum 2.13 — Monitoring Real-time dengan top
1. Jalankan top
Gambar : <img ![alt text](image-42.png)>
2. Amati nilai load average, pemakaian CPU, dan proses teratas. Tekan q untuk keluar.
Gambar : <img ![alt text](image-43.png)>


## Praktikum 2.14 — Menghentikan Proses dengan kill
1. Jalankan proses dummy di background
Gambar : <img ![alt text](image-44.png)>
2. Cari PID proses sleep
Gambar : <img ![alt text](image-45.png)>
3. Hentikan dengan SIGTERM: ( kill < PID_ANDA >)
Gambar : <img ![alt text](image-46.png)>
4. Verifikasi proses berhenti
Gambar : <img ![alt text](image-47.png)>
5. (Opsional) Jika proses sulit untuk dihentikan dan Anda membutukan untuk menghentikan proses tersebut, gunakan SIGKILL
Gambar : <img ![alt text](image-48.png)>


## 1.7 Pemantauan Sistem ##



## Praktikum 2.15 — Cek Disk, Load, dan Service
1. Cek penggunaan disk
Gambar : <img ![alt text](image-49.png)>
2. Cari direktori yang besar (contoh pada /var)
Gambar : <img ![alt text](image-50.png)>
3. Cek load dan uptime
Gambar : <img ![alt text](image-51.png)>
4. Cek service yang gagal
Gambar : <img ![alt text](image-52.png)>
5. Ambil log error terbaru (jika ada indikasi masalah)
Gambar : <img ![alt text](image-53.png)>


## Praktikum 2.16 — Monitoring Port dan Koneksi (Network Basics)
1. Lihat interface dan IP
Gambar : <img ![alt text](image-54.png)>
2. Lihat routing table
Gambar : <img ![alt text](image-55.png)>
3. Lihat port yang sedang listening
Gambar : <img ![alt text](image-56.png)>
### Latihan 2.5
Soal :
1. Pilih satu port yang listening dari output ss -tulpn(misal port 22), lalu tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut secara singkat.
Jawaban :
1. saya memilih sshd (Secure Shell Daemon), yang berfungsi untuk masuk ke terminal ubuntu dari perangkat lain, selaa terhubug dalam jarigan yang sama atau melalui internet dan sshd memastikan semua data yang dikirim dienkripsi



### LATIHAN ###
1. Latihan 2.A
Jalankan lspci -nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat, ID vendor:device, dan kernel driver in use.
Gambar : <img ![alt text](image-57.png)>
perangkat : VGA compatible controller (VGA SVGA II Adapter)
ID Vendor : 15ad:0405
kernel driver in use : vmwgfx
2. Latihan 2.B
Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan lsblk -f dan tuliskan tipe filesystem serta UUID-nya
Jawaban :device root filesystem berda di sda3 dengan nama ubuntu--vg-ubuntu--lv. dengan UUID (93bf59f7-7f0e-4001-9824-069284b47073)
Gambar : <img ![alt text](image-58.png)>
3. Latihan 2.C
Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO, WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR.
Gambar : <img ![alt text](image-59.png)>
4. Latihan 2.D
Gunakan sed untuk mengganti semua kata server menjadi node pada file latihan. Tunjukkan sebelum dan sesudah.
Gambar : <img ![alt text](image-60.png)>
5. Latihan 2.E
Gunakan df -h lalu awk untuk menampilkan filesystem yang penggunaan disk di atas 70%.
Gambar : <img ![alt text](image-61.png)>
6. Latihan 2.F
Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan SIGTERM. Jelaskan beda SIGTERM vs SIGKILL.
Gambar : <img ![alt text](image-62.png)>
SIGTERM: cara berhenti dengan kata lain "sopan", karena program akan menerima sinyal lebih dahulu sebelum membersihkan, menyimpan data, menutup koneksi database, dll
SIGKILL : sedangkan sigkill bersifat secara paksa atau mutlak, program akan langsung berhenti, tanpa bisa menolak
7. Latihan 2.G
Gunakan systemctl –failed. Jika tidak ada yang gagal, pilih satu service aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.
Gambar : <img ![alt text](image-63.png)>
<img ![alt text](image-64.png)>