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



## 