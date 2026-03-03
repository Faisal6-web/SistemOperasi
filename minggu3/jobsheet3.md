# Laporan Praktikum Sistem Operasi Jobsheet 3

<h4>Nama : Faisal Rizky <h4>
<h4>NIM :  254107020224<h4>
<h4>Kelas : TI-1H<h4>

##  1.11 Latihan ##

### Latihan 3.1 
Buatlah script yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log
Script yang dibuat: 
nano cari_log.sh
#!/bin/bash

echo "=== Cari 10 file terbesar di /var/log/ ==="

sudo find /var/log/ -type f -exec du -h {} + 2> error.log | sort -rh | head -n 10 | tee large-logs.txt

echo "=== Proses Selesai ==="
echo "Hasil pencarian disimpan di 'large-logs.txt'."
echo "Jika ada error dialihkan ke 'error.log'."

chmod +x cari_log.sh
./cari_log.sh
cat large-logs.txt
cat error.log
Hasil:
<img![Step1-Latihan_3.1](Step1-Js3-Latihan-3.1.png)>
<img![Step2-latihan-3.2](Step2-Js3-Latihan-3.1.png)>


### Latihan 3.2 
Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt
Hint: Gunakan cut, sort, dan operator redirect.
Pipeline yang dibuat :
cut -d: -f1 /etc/passwd | sort > sorted-users.txt
cat sorted-users.txt
Hasil :
<img![Latihan-3.2](Js3-Latihan-3.2.png)>


### Latihan 3.3
Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
2. Menyimpan log dengan timestamp
3. Berjalan selama 1 menit (12 iterasi)
4. Output ditampilkan di terminal DAN disimpan ke file
Script yang dijalankan :
nano monitor.sh

#!/bin/bash
LOGFILE="/home/faisal/praktikum-os/week03/monitor.log"

for i in $(seq 1 12); do
    echo "=== $(date) ===" | tee -a "$LOGFILE"
    top -bn1 | grep "Cpu(s)" | tee -a "$LOGFILE"
    free -h | tee -a "$LOGFILE"
    sleep 5
done

chmod +x monitor.sh
./monitor.sh
Hasil :
<img![Latihan-3.3](Hasil-Js3-Latihan-3.3.png)>



### Latihan 3.4
Buat perintah yang:
1. Mencari semua file .conf di sistem
2. Membuang pesan "Permission denied"
3. Menghitung jumlah file yang ditemukan
4. Menyimpan daftar path lengkap ke file
Script :
find / -type f -name "*.conf" 2>/dev/null | tee daftar_conf.txt | wc -l
head -n 10 daftar_conf.txt
Hasil :
<img![Latihan-3.4](Hasil-Js3-Latihan 3.4-1.png>)>


### Latihan 3.5
Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
2. Menampilkan progress dengan tee
3. Mencatat stdout ke backup-success.log
4. Mencatat stderr ke backup-error.log
5. Menambahkan timestamp di setiap log entry
Script: 
nano backup.sh

#!/bin/bash

TIMESTAMP="$(date '+%Y-%m-%d %H:%M:%S')"

echo "[$TIMESTAMP] Backup dimulai" | tee -a backup-success.log

tar -czvf backup.tar.gz $HOME 2>> backup-error.log | tee -a backup-success.log

echo "[$TIMESTAMP] Backup selesai" | tee -a backup-success.log

chmod +x backup.sh
./backup.sh
Hasil :
<img![Latihan-3.5](Hasil-Js3-Latihan 3.5-1.png>)>