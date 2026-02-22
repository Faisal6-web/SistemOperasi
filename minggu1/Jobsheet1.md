# Laporan Praktikum Sistem Operasi Jobsheet 1

<h4>Nama : Faisal Rizky<h4>
<h4>NIM : 254107020224<h4>
<h4>Kelas : TI-1H<h4>

## Latihan 

### 10.1 Latihan Konseptual 
### Pertanyaan 
1. Jelaskan 5 fungsi utama sistem operasi dengan contoh konkret dari minimal 2OS berbeda (Windows, macOS, atau Linux)
2. Kapan sebaiknya menggunakan Windows vs Linux vs macOS? Analisis berdasarkan use case: gaming, development, server, creative work, dan enterprise.

### Jawaban 
1. fungsi utama sistem operasi :
 - Sebagai pengelola utama sumber daya perangkat keras (CPU, memori, I/O) dan perangkat lunak
 - Process scheduling — Menentukan proses mana yang mendapat CPU time
 - Process creation dan termination — Membuat dan mengakhiri proses
 - Process synchronization — Mengkoordinasikan multiple processes
 - Inter-process communication (IPC) — Memfasilitasi komunikasi antar
proses
*contoh implementasi* :
- Windows: Task Manager menampilkan proses yang berjalan dan penggunaan
sumber daya
- Linux: Perintah ps, top, dan htop untuk memantau proses

2. Gaming & enterprise : Windows (kompatibilitas terbaik)
   Development : macOS atau Linux (tools berbasis Unix)
   server: Linux (stabilitas, keamanan, tanpa biaya lisensi)
   creative work : macOS (standar industri untuk video/audio editing)
  

### 10.2 Latihan Praktikal
### Pertanyaan
1. Download Ubuntu Server ISO dari website resmi
2. Create VM baru di VirtualBox (RAM: 2GB, Disk: 25GB)
3. Install dengan automatic partitioning (guided)
4. Buat user account dengan password yang kuat
5. Reboot dan login ke sistem
6. Dokumentasikan proses instalasi dengan screenshot key steps
7. Update package list: sudo apt update
8. Upgrade packages: sudo apt upgrade
9. Install neofetch: sudo apt install neofetch
10. Jalankan neofetch dan screenshot hasilnya
11. Check disk usage dengan df -h
12. Check memory dengan free -h
13. Dokumentasikan output dari setiap command
14. Tampilkan informasi OS: cat /etc/os-release
15. Tampilkan versi kernel: uname -r
16. List partisi: lsblk
17. Check network connectivity: ping -c 4 google.com
18. Install dan jalankan htop untuk melihat resource usage
19. Buat laporan singkat tentang konfigurasi sistem Anda


### Jawaban 
1. <img ![alt text](<Screenshot 2026-02-22 141848.png>)>
2. <img![alt text](<Screenshot 2026-02-22 142706.png>)>
3. <img ![alt text](<Screenshot 2026-02-22 143202.png>)>
4. <img ![alt text](<Screenshot 2026-02-22 143301.png>)>

### 10.3 Latihan Refleksi
### Pertanyaan
1. Sistem operasi apa yang Anda gunakan sehari-hari? (Windows, macOS,Linux, atau lainnya)
2. Berapa lama Anda menggunakan sistem operasi tersebut?
3. Apa yang Anda sukai dari sistem operasi tersebut?
4. Apa tantangan atau masalah yang pernah Anda hadapi?
5. Apakah Anda pernah menggunakan sistem operasi lain? Bandingkan pengalaman Anda.
6.  Setelah mempelajari bab ini, apakah ada sistem operasi lain yang ingin Anda coba? Mengapa?

### Jawaban
1. saya sehari-hari menggunakan sistem operasi windows
2. sudah 5 tahun saya menggunakan windows
3. karena user friendly atau familier, karna banyak digunakan dan mudah menggunakannya
4. sistem untuk update yang kadang mengganggu serta memakan banyak kapasitas RAM dan ruang penyimpanan
5. belum pernah
6. linux, karena open-source serta gratis dan ringan

