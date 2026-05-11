# Laporan Praktikum Sistem Operasi Jobsheet 11

<h4>Nama : Faisal Rizky <h4>
<h4>NIM : 254107020224 <h4>
<h4>Kelas : TI-1H <h4>

## Praktikum 11.1 — Permissions
1. Buat direktori kerja dan dua file uji
```
mkdir ~/ lab - permissions && cd ~/ lab - permissions
echo " data rahasia " > secret . txt
echo '#!/ bin/ bash ' > myscript . sh
echo 'echo Hello ' >> myscript . sh
ls - la
```
Hasil :


2. Jadikan secret.txt privat hanya untuk owner
```
chmod 600 secret . txt
ls -l secret . txt
```
Hasil :

3. Jadikan myscript.sh dapat dijalankan
```
chmod 755 myscript . sh
ls -l myscript . sh
./ myscript . sh
```
Hasil :


4. Buat direktori bersama dan amati efek SGID sederhana
```
mkdir shared - dir
chmod g + s shared - dir
ls - ld shared - dir
```
Hasil :

5. Uji efek umask pada file baru
```
umask
umask 027
touch testfile -027
ls -l testfile -027
```
Hasil :


Analisis
1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?

Tantangan
Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem, kemudian jelaskan perubahan output ls -l sebelum dan sesudahnya.



## Praktikum 11.2 — ACL
1. Siapkan file dan lihat permission standar tanpa ACL tambahan
```
mkdir ~/ lab - acl && cd ~/ lab - acl
echo " Data penting " > confidential . txt
chmod 640 confidential . txt
ls -l confidential . txt
getfacl confidential . txt
```
Hasil :


2. Beri akses baca ke satu user tertentu tanpa mengubah owner atau group
```
setfacl -m u : userA : r confidential . txt
ls -l confidential . txt
getfacl confidential . txt
```
Hasil :


3. Buat direktori bersama yang mewariskan ACL ke file baru
```
mkdir shared
setfacl -d -m u : userA : rwx shared
setfacl -d -m u : userB :r - x shared
getfacl shared
touch shared / inherited . txt
getfacl shared / inherited . txt
```
Hasil :


Analisis
1. Mengapa getfacl confidential.txt awalnya tidak menampilkan user tertentu?
2. Setelah setfacl -m u:userA:r confidential.txt, apa perbedaan output ls -l dan getfacl?
3. Mengapa file inherited.txt mewarisi ACL dari direktori shared?

Tantangan
Tambahkan satu ACL lagi agar group readonly-group hanya dapat membaca confidential.txt. Setelah itu, hapus ACL untuk userA dan verifikasi hasil akhirnya dengan getfacl.



## Praktikum 11.3A — Membuat dan Mengelola User
```
# buat dua user
sudo useradd -m -s / bin / bash userA
sudo useradd -m -s / bin / bash userB
sudo passwd userA
sudo passwd userB
# verifikasi
id userA
getent passwd userA
# modifikasi shell userA
sudo usermod -s / bin / zsh userA
getent passwd userA
# lock dan unlock userB
sudo usermod -L userB
sudo passwd -S userB
sudo usermod -U userB
sudo passwd -S userB
```
Hasil :


Pertanyaan 
1. Apa perbedaan output id userA sebelum dan sesudah menambah group?
2. Bagaimana status passwd -S userB berubah saat akun di-lock?


## Praktikum 11.3B — Group Management
```
# buat dua group
sudo groupadd labgroup
sudo groupadd readonly - group
# tambahkan userA ke kedua group
sudo usermod - aG labgroup , readonly - group userA
# tambahkan userB hanya ke readonly - group
sudo usermod - aG readonly - group userB
# verifikasi
id userA
id userB
getent group labgroup
getent group readonly - group
```
Hasil :


Pertanyaan:
1. Apa yang ditampilkan id userA vs groups userA?
2. Mengapa -a pada usermod -aG penting?


## Praktikum 11.3C — Password Aging Policy
```
# set aging policy untuk userA
sudo chage -M 60 -W 7 -m 1 userA
sudo chage -l userA
# paksa userA ganti password saat login pertama
sudo chage -d 0 userA
# kunci password userB
sudo passwd -l userB
sudo passwd -S userB
# unlock kembali
sudo passwd -u userB
sudo passwd -S userB
```
Hasil :


Pertanyaan:
1. Apa arti nilai yang ditampilkan chage -l userA?
2. Bagaimana cara membuktikan userB terkunci dari output passwd -S?
3. Kapan sebaiknya menggunakan chage -d 0 vs passwd -e?
Tantangan
Buat user bernama intern yang:
• memiliki shell /bin/bash;
• menjadi anggota labgroup;
• dipaksa ganti password pada login pertama;
• password expired setelah 45 hari dengan warning 7 hari sebelumnya.



## Praktikum 11.4 — Konfigurasi sudo
1. Buat file konfigurasi sudo khusus untuk userA
```
sudo visudo -f / etc / sudoers . d / lab - userA
```
Hasil :


2. Verifikasi aturan yang aktif dan uji hasilnya
```
sudo -l -U userA
sudo grep " userA " / var / log / auth . log | tail -10
```
Hasil :


Analisis
1. Mengapa aturan disimpan di /etc/sudoers.d//, bukan langsung di /etc/sudoers?
2. Mana perintah yang bisa dijalankan tanpa password, dan mana yang masih perlu autentikasi?
3. Informasi apa saja yang dicatat di log sudo?
Tantangan
Tambahkan satu aturan baru agar userA boleh menjalankan /bin/systemctl restart ssh tetapi tidak boleh menjalankan reboot


## Praktikum 11.5 — Disk Quota
1. Buat image filesystem kecil dan mount dengan opsi quota
```
sudo dd if =/ dev / zero of =/ tmp / quota - test . img bs =1 M count =100
sudo mkfs . ext4 / tmp / quota - test . img
sudo mkdir -p / mnt / quota - test
sudo mount -o loop , usrquota , grpquota / tmp / quota - test . img / mnt /
quota - test
```
Hasil :


2. Buat database quota dan aktifkan enforcement
```
sudo quotacheck - cug / mnt / quota - test
sudo quotaon -v / mnt / quota - test
sudo repquota / mnt / quota - test
```
Hasil :


3. Tetapkan quota untuk user uji dan amati hasilnya
```
sudo edquota -u userA
# contoh : soft block 5120 , hard block 10240
sudo repquota / mnt / quota - test
```
Hasil :


4. Bersihkan lingkungan uji setelah selesai
```
sudo quotaoff / mnt / quota - test
sudo umount / mnt / quota - test
sudo rm / tmp / quota - test . img
```
Hasil :


Analisis
1. Apa perbedaan soft limit dan hard limit saat quota mulai terlampaui?
2. Mengapa praktikum ini memakai loopback filesystem, bukan langsung /home/?
3. Dari output repquota, informasi apa yang menunjukkan quota sudah aktif?
Tantangan
Coba atur quota baru untuk userA dengan batas inode yang sangat kecil, kemudian jelaskan kapan pembatasan
inode lebih penting daripada pembatasan block