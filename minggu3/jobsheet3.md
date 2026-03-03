# Laporan Praktikum Sistem Operasi Jobsheet 3

<h4>Nama : Faisal Rizky <h4>
<h4>NIM :  254107020224<h4>
<h4>Kelas : TI-1H<h4>

##  1.11 Latihan ##

### Latihan 3.1 
Buatlah script yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
<img>
2. Menyimpan hasilnya ke file large-logs.txt
<img>
3. Menampilkan output juga di terminal menggunakan tee
<img>
4. Menangani error dengan redirect ke error.log
<img>


### Latihan 3.2 
Buat pipeline yang:
1. Membaca /etc/passwd
<img>
2. Mengekstrak username (kolom pertama)
<img>
3. Mengurutkan alfabetis
<img>
4. Menyimpan ke file sorted-users.txt
<img>
Hint: Gunakan cut, sort, dan operator redirect.



### Latihan 3.3
Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
<img>
2. Menyimpan log dengan timestamp
<img>
3. Berjalan selama 1 menit (12 iterasi)
<img>
4. Output ditampilkan di terminal DAN disimpan ke file
<img>



### Latihan 3.4
Buat perintah yang:
1. Mencari semua file .conf di sistem
<img>
2. Membuang pesan "Permission denied"
<img>
3. Menghitung jumlah file yang ditemukan
<img>
4. Menyimpan daftar path lengkap ke file
<img>


### Latihan 3.5
Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
<img>
2. Menampilkan progress dengan tee
<img>
3. Mencatat stdout ke backup-success.log
<img>
4. Mencatat stderr ke backup-error.log
<img>
5. Menambahkan timestamp di setiap log entry
<img>