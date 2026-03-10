# Laporan Praktikum Sistem Operasi Jobsheet 4

<h4>Nama : Faisal Rizky <h4>
<h4>NIM : 254107020224<h4>
<h4>Kelas : TI-1H<h4>


## TUGAS PENDAHULUAN 
    Jawablah pertanyaan-pertanyaan dibawah ini :
1. Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir
Jawaban :
pwd (print working directory): untuk melihat di lokasi atau folder mana kita berada
cd (Change Directory): Digunakan untuk berpindah dari direktori saat ini ke direktori lain yang dituju.

mkdir (Make Directory): Digunakan untuk membuat direktori atau folder baru.

rmdir (Remove Directory): Menghapus direktori secara spesifik, dengan syarat direktori tersebut harus dalam keadaan kosong (tidak ada file di dalamnya).

2. Apa yang dimakdsud perintah-perintah manipulasi file : cp, mv dan rm (sertakan format yang digunakan)
Jawaban:
cp (Copy): Menyalin file atau direktori dari lokasi sumber ke lokasi tujuan.

mv (Move): Berfungsi ganda; bisa untuk memindahkan file/direktori ke tempat lain, dan juga digunakan untuk mengubah nama (rename) sebuah file/direktori.

rm (Remove): Menghapus file secara permanen. Jika menggunakan opsi -r, bisa juga digunakan untuk menghapus direktori beserta seluruh isinya.


3. Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect)
Jawaban:
Hard Link (Direct): Tautan yang terhubung langsung ke data fisik (inode) dari file aslinya di dalam hard disk. File asli dan hard link memiliki status yang sejajar. Jika file asli dihapus, datanya tetap utuh dan masih bisa dibuka melalui hard link tersebut.

Soft Link / Symbolic Link (Indirect): Bekerja persis seperti Shortcut di Windows. File ini hanya menyimpan teks berupa "alamat path" yang menunjuk ke lokasi file aslinya. Jika file aslinya dipindah atau dihapus, maka soft link ini akan rusak (broken link) karena alamat yang ditujunya sudah tidak ada.

4. Tuliskan maksud perintah-perintah : file, find, which, locate dan grep
Jawaban :
file: Memeriksa dan menampilkan jenis tipe data dari sebuah file berdasarkan isi kontennya, bukan berdasarkan ekstensinya (misalnya: file teks, file executable, atau arsip).

find: Mencari file atau direktori secara langsung (real-time) dengan menelusuri hierarki sistem file. Bisa mencari berdasarkan kriteria spesifik seperti nama, ukuran, tipe, atau tanggal modifikasi.

which: Menunjukkan lokasi spesifik dari sebuah program atau file executable yang akan dijalankan oleh sistem. Ini berguna untuk memastikan versi program mana yang sedang dipakai.

locate: Mencari lokasi file di seluruh sistem dengan sangat cepat, karena ia mencari melalui basis data (indeks) sistem yang sudah disiapkan sebelumnya, bukan mencari satu per satu ke dalam hard disk.

grep: Mencari baris teks atau kata tertentu di dalam isi sebuah file (atau output dari perintah lain) dan menampilkannya ke layar.

## Percobaan 1 : Direktory ##
1. Melihat direktori HOME
```
 pwd
 echo $HOME

 ```
<img![step1](Percobaan1-step1-js4.png)>

2. Melihat direktori aktual dan parent direktori
```
 pwd
 cd .
 pwd
 cd ..
 pwd
 cd

```
<img![step2](Percobaan1-step2-js4.png)>

3. Membuat satu direktori, lebih dari satu direktori atau sub direktori
```
 pwd
 mkdir A B C A/D A/E B/F A/D/A
 ls -l
 ls -l A
 ls -l A/D

 ```
<img![step3](Percobaan1-step3-js4.png)>

4. Menghapus satu atau lebih direktori hanya dapat dilakukan pada direktori kosong dan hanya dapat dihapus oleh pemiliknya kecuali bila diberikan ijin aksesnya
```
 rmdir B           (Terdapat pesan error, mengapa?)
 ls -l B
 rmdir B/F B
 ls -l B            (Terdapat pesan error, mengapa?)

 ```
 <img![step4](Percobaan1-step4-js4.png)>
- Terjadi error saat rmdir B karena direktori B tidak kosong sehingga tidak bisa dihapus
- Terjadi error saat ls -l B karena direktori B sudah dihapus sehingga tidak bisa di-list

 5. Navigasi direktori dengan instruksi cd untuk pindah dari satu direktori ke direktori lain.
 ```

pwd
ls -l
cd A
pwd
cd ..
pwd
cd /home/<user>/C
pwd
cd /<user>/C
pwd

```
<img![step5](Percobaan1-step5-js4.png)>

## Percobaan 2 : Manipulasi file
1. Perintah cp untuk mengkopi file atau seluruh direktori
```
cat > contoh

```
Membuat sebuah file
[Ctrl-d]
```
cp contoh contoh1
ls -l
cp contoh A
ls -l A
cp contoh contoh1 A/D
ls -l A/D

```
<img![step1](Percobaan2-step1-js4.png)>

2. Perintah mv untuk memindah file
```

mv contoh contoh2
ls -l
mv contoh1 contoh2 A/D
ls -l A/D
mv contoh contoh1 C
ls -l C

```
<img![step2](Percobaan2-step2-js4.png)>

3. Perintah rm untuk menghapus file
```

rm contoh2
ls -l
rm -i contoh
rm -rf A C
ls -l

```
<img![step3](Percobaan2-step3-js4.png)>

## Percobaan 3: Symbolic Link ##
1. Membuat shortcut (file link)
``` 

echo "Hallo apa kabar" > halo.txt
ls -l
ln halo.txt z
ls -l
cat z
mkdir mydir
ln z mydir/halo.juga
cat mydir/halo.juga
ls -s z bye.txt
ls -l bye.txt
cat bye.txt

```
<img![step1](Percobaan3-step1-js4.png)>

## Percobaan 4: Melihat Isi File ##
```

ls -l
file halo.txt
file bye.txt

```
<img![step1](Percobaan4-step1-js4.png)>

## Percobaan 5: Mencari File ##
1. perintah find
```

find /home -name "*.txt" -print > myerror.txt
cat myerror.txt
find . -name "*.txt" -exec wc -l '{}' ';'

```
<img![step1](Percobaan5-step1-js4.png)>

2. Perintah which
```
which is

```
<img![step2](Percobaan5-step2-js4.png)>

3. Perintah locate
```
locate "*.txt"

```
<img![step3](Percobaan5-step3-js4.png)>

## Percobaan 6: Mencari text pada file ##
```
grep Hallo *.txt

```
<img![step1](Percobaan6-step1-js4.png)>

### Latihan
1. Cobalah urutan perintah berikut :
```
cd
pwd
ls -al
cd .
pwd
cd ..
pwd
ls -al
cd ..
pwd
ls -al
cd /etc
ls -al | more
cat passwd
cd -
pwd

```
<img![1.1](Latihan-step1.1-js4.png)>
<img![1.2](Latihan-step1.2-js4.png)>
<img![1.3](Latihan-step1.3-js4.png)>
<img![1.4](Latihan-step1.4-js4.png)>

2. Lanjutkan penelusuran pohon pada sistem file menggunakan cd, ls,, pwd dan cat.
Telusuri direktory /bin, /usr/bin, /sbin, /tmp dan /boot
/bin
<img![bin](Latihan-step2-bin-js4.png)>
/usr/bin
<img![usr,bin](Latihan-step2-usr,bin-js4.png)>
 /sbin
 <img![sbin](Latihan-step2-sbin-js4.png)>
/tmp
<img![tmp](Latihan-step2-tmp-js4.png)>
/boot
<img![boot](Latihan-step2-boot-js4.png)>

3. Telusuri direktory /dev. Identifikasi perangkat yang tersedia. Identifikasi tty (terminal) Anda (ketik who am i); siapa pemilih tty Anda (gunakan ls -l).
<img![step3](Latihan-step3-js4.png)>


4. Telusuri derectory /proc. Tampilkan isi file interrupts, devices, cpuinfo, meminfo dan uptime menggunakan perintah cat. Dapatkah Anda melihat mengapa directory /proc disebut pseudo-filesystem yang memungkinkan akses ke struktur data kernel?
Jawaban:
Karena file-file di dalam /proc sebenarnya tidak ada secara fisik di hardisk Anda. File-file itu otomatis dibuat oleh Kernel (inti sistem operasi Linux) secara langsung (real-time). Saat menjalankan cat cpuinfo misalnya, Anda sedang membaca langsung status CPU dari memori sistem.
- interrupts
<img![interrupts](Latihan-step4-interrupts-js4.png)>
- devices
<img![devices](Latihan-step4-devices-js4.png)>
- cpuinfo
<img![cpuinfo](Latihan-step4-cpuinfo-js4.png)>
- meminfo
<img![meminfo](Latihan-step4-meminfo-js4.png)>
- uptime
<img![uptime](Latihan-step4-uptime-js4.png)>



5. Ubahlah direktory home ke user lain secara langsung menggunakan cd ~username.
<img![step5](Latihan-step5-js4.png)>


6. Ubah kembali ke direktory home Anda.
<img![step6](Latihan-step6-js4.png)>


7. Buat subdirektory work dan play.
<img![step7](Latihan-step7-js4.png)>


8. Hapus subdirektory work
<img![step8](Latihan-step8-js4.png)>


9. Copy file /etc/passwd ke direktory home Anda
10. Pindahkan ke subdirectory play.
gambar step 9 &10 :
<img![step9&10](Latihan-step9&10-js4.png)>


11. Ubahlah ke subdirectory play dan buat symbolic link dengan nama terminal yang menunjuk ke perangkat tty. Apa yang terjadi jika melakukan hard link ke perangkat tty ?
Jawaban:
Sistem akan menolak (error). Linux tidak mengizinkan pembuatan hard link yang mengarah ke file perangkat keras (device file seperti terminal/tty) atau ke sebuah direktori demi alasan keamanan dan untuk menjaga agar sistem file tidak rusak/berputar tanpa ujung.
<img![step11](Latihan-step11-js4.png)>


12. Buatlah file bernama hello.txt yang berisi kata "hello word". Dapatkah Anda gunakan "cp" menggunakan "terminal" sebagai file asal untuk menghasilkan efek yang sama ?
Jawaban :
Bisa, tetapi prosesnya berbeda. Jika Anda menggunakan perintah cp terminal hello.txt, perintah tidak akan langsung selesai dan kembali ke prompt. Terminal akan "menunggu"untuk mengetik kata "hello word" secara manual di keyboard, lalu Anda harus menekan kombinasi tombol Ctrl + D (End of File) untuk menyelesaikannya dan menyimpannya. Menggunakan echo jauh lebih otomatis dan instan.
<img![step12](Latihan-step12-js4.png)>


13. Copy hello.txt ke terminal. Apa yang terjadi ?
<img![step13](Latihan-step13-js4.png)>


14. Masih direktory home, copy keseluruhan direktory play ke direktory bernama work menggunakan symbolic link.
<img![step14](Latihan-step14-js4.png)>


15. Hapus direktory work dan isinya dengan satu perintah
<img![step15](Latihan-step15-js4.png)>
