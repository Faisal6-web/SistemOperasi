# Laporan Praktikum Sistem Operasi Jobsheet 2

<h4>Nama : Faisal Rizky<h4>
<h4>NIM : 254107020224<h4>
<h4>Kelas : TI-1H<h4>

## 1.1 Deteksi Perangkat Keras di Linux ##

## Praktikum 2.1 Identifikasi CPU dan Memori
1. Tampilkan informasi CPU: (lscpu)
Gambar:

2. Tampilkan ringkasan memori: (free -h)
Gambar:

3. (Opsional) cek informasi hardware dari DMI/BIOS (butuh sudo): (sudo dmidecode -t system)
Gambar:
### Latihan 2.1 
Soal :
1. Catat: (1) jumlah CPU(s), core/thread, (2) total RAM, (3) total swap. 
2. Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.

Jawaban :
1. 
2. 


## Praktikum 2.2 — Identifikasi Perangkat PCI/USB dan Driver
1. Lihat daftar perangkat PCI: (lspci)
Gambar :
2. Lihat perangkat PCI beserta driver kernel yang digunakan: (lspci - nnk)
Gambar : 
3. Fokus pada NIC (Ethernet) untuk mencari modul driver: (lspci - nnk | grep - A3 -i ethernet)
Gambar :
4. Lihat perangkat USB : (lsusb)
Gambar :
5. Lihat topologi USB (tree): (lsusb -t)
Gambar : 
### Latihan 2.2
Soal :
1. Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.

Jawaban :
1. 


## Praktikum 2.3 — Identifikasi Storage dan Filesystem
1. Lihat daftar disk/partisi: (lsblk -f)
Gambar :
2. Tampilkan UUID dan tipe filesystem: (sudo blkid)
Gambar :
3. Lihat mount point untuk root filesystem: (findmnt /)
Gambar :

## 1.2 Modul Kernel dan Driver Perangkat ##


## Praktikum 2.4 — Melihat Modul Aktif dan Informasinya
1. Cek versi kernel: (uname -r)
Gambar :
2. Tampilkan daftar modul aktif: (lsmod | head)
Gambar : 
3.  Pilih salah satu modul (contoh aman: loop) dan lihat detailnya: (modinfo loop)
Gambar :
4. Muat modul (jika belum aktif), lalu verifikasi: (sudo modprobe loop) dan (lsmod | grep -i loop)
Gambar : 
5. (Opsional) lihat pesan kernel terbaru: (dmesg -T | tail -n 20)


## Praktikum 2.5 — Konfigurasi Auto-load dan Blacklist
1. Buat file auto-load: ( echo " loop " | sudo tee / etc / modules - load . d / loop . conf)
Gambar :
2. Simulasikan verifikasi (tanpa reboot) dengan memastikan modul sudah aktif: ( lsmod | grep -i loop)
Gambar :
3. (Opsional, konsep) blacklist modul: (# echo " blacklist loop " | sudo tee / etc/ modprobe .d/blacklist - loop . conf)
Gambar :


## 1.3 Sistem File dan /dev di Linux ##


## Praktikum 2.6 — Mengenali Block vs Character Device
1. Manajemen Perangkat Keras & Perintah Dasar Sistem Operasi : (ls -l / dev / sda)
Gambar :
2. Lihat detail device terminal: (ls -l / dev / tty)
Gambar :
3. Lihat disk dan partisi untuk mengaitkan dengan /dev : (lsblk)
Gambar :
### Latihan 2.3
Soal:
1. Dari output ls -l, jelaskan perbedaan penanda file untuk block device dancharacter device. (Hint: karakter pertama pada permission string)
Jawaban : 
1. 

## Praktikum 2.7 — Melihat Informasi udev
1. Cek atribut udev untuk disk: ( udevadm info -- query = all -- name =/ dev / sda | head -n 30)
Gambar : 
2. (Opsional) monitor event udev (jalankan, lalu colok/lepas USB pada mesin fisik) : (sudo udevadm monitor)
Gambar : 


## 1.4 Perintah Dasar Terminal Linux ##


## Praktikum 2.8 — Membuat Workspace Praktikum
1. Buat direktori praktikum dan masuk ke dalamnya: (mkdir -p ~/ praktikum - os / week02), (cd ~/ praktikum - os / week02) dan (pwd)
Gambar :
2. Buat beberapa file contoh: (touch notes . txt data . log config . txt) dan (ls - lah)
Gambar : 
3. Isi file log contoh (simulasi):
- echo " INFO : service started " >> data . log
- echo " WARN : disk usage high " >> data . log
- echo " ERROR : failed to connect " >> data . log
- cat data . log
Gambar :
4. Baca file dengan less: (less data . log)
Gambar :


## 1.5 Manipulasi Teks ##


## Praktikum 2.9 — Pencarian Pola dengan grep
1. Cari baris yang mengandung ERROR pada data.log: (grep " ERROR " data . log)
Gambar : 
2. Cari tanpa memperhatikan huruf besar/kecil: (grep -i " error " data . log)
Gambar : 
3. Tampilkan nomor baris: (grep -n " WARN " data . log)
Gambar :
4. Tampilkan baris yang tidak cocok (invert match): (grep -v " INFO " data . log)
Gambar :
### Latihan 2.4
1. Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif)

## Praktikum 2.10 — Substitusi dengan sed (Aman di File Latihan)
1. Siapkan file konfigurasi latihan: 
- cat > config . txt << ’EOF ’
- PORT =8080
- MODE = dev
- SERVICE_NAME = myserver
- EOF
- cat config . txt
Gambar : 
2. Ganti dev menjadi prod (tanpa mengubah file asli): (sed ’s/ MODE =dev/ MODE = prod /’ config . txt)
Gambar :
3. Terapkan perubahan langsung ke file (-i): (sed -i ’s/ MODE =dev/ MODE = prod /’ config . txt) (cat config . txt)
Gambar : 
4. Ganti semua kemunculan kata (g untuk global), contoh ubah myserver menjadi node: 
- (sed -i ’s/ myserver / node /g’ config . txt)
- (cat config . txt)
Gambar : 

## Praktikum 2.11 — Ekstraksi Kolom dengan awk
1. Lihat output df -h: (df -h)
Gambar : 
2. Ambil kolom filesystem dan persentase pemakaian: (df -h | awk ’NR ==1 { print $1 , $5 , $6} NR >1 { print $1 , $5 , $6}’)
Gambar :
3. Filter hanya yang pemakaian disk di atas 80%: (df -h | awk ’NR ==1 || ($5 +0) > 80 { print $1 , $5 , $6}’)
Gambar : 


## 1.6 Manajemen Proses ##


## Praktikum 2.12 — Melihat Proses dengan ps
1. Tampilkan semua proses (format BSD): (ps aux | head)
Gambar : 
2. Cari proses tertentu (misal sshd): (ps aux | grep -i sshd)
Gambar : 


## Praktikum 2.13 — Monitoring Real-time dengan top
1. Jalankan top: (top)
Gambar :
2. Amati nilai load average, pemakaian CPU, dan proses teratas. Tekan q untuk keluar.
Gambar :


## Praktikum 2.14 — Menghentikan Proses dengan kill
1. Jalankan proses dummy di background: (sleep 300 &)
Gambar :
2. Cari PID proses sleep: (ps aux | grep -E " sleep 300 " | grep -v grep)
Gambar :
3. Hentikan dengan SIGTERM: ( kill < PID_ANDA >)
Gambar : 
4. Verifikasi proses berhenti: (ps aux | grep -E " sleep 300 " | grep -v grep)
Gambar :
5. (Opsional) Jika proses sulit untuk dihentikan dan Anda membutukan untuk menghentikan proses tersebut, gunakan SIGKILL: (kill -9 < PID_ANDA >)
Gambar :


## 1.7 Pemantauan Sistem ##



## Praktikum 2.15 — Cek Disk, Load, dan Service
1. Cek penggunaan disk: (df -h)
Gambar :
2. Cari direktori yang besar (contoh pada /var): (sudo du - sh / var /* 2 >/ dev / null | sort -h | tail -n 10)
Gambar :
3. Cek load dan uptime: (uptime)
Gambar :
4. Cek service yang gagal: (systemctl -- failed)
Gambar :
5. Ambil log error terbaru (jika ada indikasi masalah): (journalctl - xe | tail -n 50)
Gambar :


## Praktikum 2.16 — Monitoring Port dan Koneksi (Network Basics)
1. Lihat interface dan IP: (ip a)
Gambar :
2. Lihat routing table: (ip r)
Gambar :
3. Lihat port yang sedang listening: (sudo ss - tulpn)
Gambar :
### Latihan 2.5
Soal :
1. Pilih satu port yang listening dari output ss -tulpn(misal port 22), lalu tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut secara singkat.
Jawaban :
1. 



### LATIHAN ###
1. Latihan 2.A
Jalankan lspci -nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat, ID vendor:device, dan kernel driver in use.
Gambar :
2. Latihan 2.B
Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan lsblk -f dan tuliskan tipe filesystem serta UUID-nya
Gambar :
3. Latihan 2.C
Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO, WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR.
Gambar :
4. Latihan 2.D
Gunakan sed untuk mengganti semua kata server menjadi node pada file latihan. Tunjukkan sebelum dan sesudah.
Gambar :
5. Latihan 2.E
Gunakan df -h lalu awk untuk menampilkan filesystem yang penggunaan disk di atas 70%.
Gambar :
6. Latihan 2.F
Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan SIGTERM. Jelaskan beda SIGTERM vs SIGKILL.
Gambar :
7. Latihan 2.G
Gunakan systemctl –failed. Jika tidak ada yang gagal, pilih satu service aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.
Gambar :
