# Laporan Praktikum Sistem Operasi Jobsheet 10

<h4>Nama : Faisal Rizky <h4>
<h4>NIM : 254107020224 <h4>
<h4>Kelas : TI-1H <h4>

## Praktikum 10.1  Melihat Penggunaan Memori
1. Jalankan free -h untuk melihat ringkasan RAM dan swap
```
free -h
```
Hasil :


2. Lihat detail memori dari kernel melalui /proc/meminfo
```
cat / proc / meminfo | head -n 20
```
Hasil :

Analisis:
1. Hitung persentase memori tersedia: available / total × 100%. Jika hasilnya di bawah 10%, sistem mulai kekurangan memori
2. Pada baris Swap, apakah kolom used bernilai 0? Jika lebih dari 0, kernel sudah pernah memindahkan data ke disk karena RAM tidak cukup
3. Perhatikan field Cached dan Buffers di /proc/meminfo. Nilai ini sesuai dengan kolom buff/cache pada free -h

### Studi Kasus 10.1 Server Lambat karena Memori
1. Periksa kondisi memori secara keseluruhan
```
free -h
```
Hasil :

2. Pantau proses secara real-time
``` 
top
```
Hasil :

Analisis:
1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori
2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang menggunakan swap, yang berarti performa menurun
3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut menjadi kandidat utama penyebab lambatnya server

## Praktikum 10.2 Mengamati Aktivitas Paging
1.  Jalankan vmstat dengan interval 1 detik, 5 sampel
```
vmstat 1 5
```
Hasil :

Analisis:
1. Amati nilai si dan so pada kelima baris. Pada sistem normal dengan RAM cukup, kedua nilai ini selalu 0
2. Jika nilai si atau so sesekali muncul lebih dari 0, artinya pernah ada aktivitas swap. Ini masih wajar jika tidak terus-menerus
3. Jika si dan so terus-menerus lebih dari 0, sistem dalam kondisi memory pressure serius — performa turun drastis karena akses disk jauh lebih lambat dari RAM
4. Perhatikan juga kolom free (RAM kosong) dan buff (buffer) untuk memahami kondisi keseluruhan RAM saat itu


## Praktikum 10.3 Membuat dan Mengonfigurasi Swap File
1. Buat file berukuran 512 MB sebagai calon swap
```
sudo fallocate -l 512 M / swapfile - week10
```
Hasil :


2. Atur permission file menjadi 600 — hanya root yang boleh membaca dan menulis
```
sudo chmod 600 / swapfile - week10
```
Hasil :


3. Format file sebagai area swap, lalu aktifkan
```
sudo mkswap / swapfile - week10
sudo swapon / swapfile - week10
```
Hasil :


4. Verifikasi swap aktif. Anda akan melihat entri /swapfile-week10 dengan ukuran 512M, dan nilai total pada baris Swap di free -h bertambah 512M
```
swapon -- show
free -h
```
Hasil :


5. Periksa nilai swappiness, ubah sementara, dan verifikasi perubahan
```
cat / proc / sys / vm / swappiness
sudo sysctl vm . swappiness =10
cat / proc / sys / vm / swappiness
```
Hasil :

Analisis:
1. Berapa nilai swappiness default? Apa artinya bagi perilaku kernel dalam menggunakan swap?
2. Setelah diubah ke 10, konfirmasi nilai berubah pada output cat kedua. Apa dampak nilai 10 terhadap penggunaan swap dibanding nilai 60?
3. Apakah entri /swapfile-week10 muncul di swapon –show? Jika tidak, pastikan Langkah 2 (chmod 600) sudah dijalankan sebelum Langkah 3


## Praktikum 10.4 Monitoring Memory
1. Ambil snapshot proses diurutkan dari penggunaan memori terbesar
```
ps aux -- sort = -% mem | head
```
Hasil :


2. Pantau secara real-time dengan top
```
top
```
Hasil :

Analisis:
1. Proses apa yang berada di urutan pertama? Catat nilai %MEM dan RSS-nya.
2. Konversikan RSS dari KB ke MB (bagi 1024). Misalnya, RSS=524288 berarti proses menggunakan 512 MB RAM. Apakah wajar untuk jenis program tersebut?
3. Mengapa VSZ selalu lebih besar dari RSS pada proses yang sama?
4. Apakah urutan proses di ps konsisten dengan tampilan top saat diurutkan berdasarkan %MEM?


## Praktikum 10.5 Script Monitor Memori
1. Masuk ke direktori kerja dan buat file script:
```
cd ~/ praktikum - os / week10 - memory
nano monitor - memori . sh
```
Hasil :


2. Ketik script berikut:
```
#!/ bin / bash
set - euo pipefail
THRESHOLD =20
echo "=== Monitor Memori ==="
date
echo
free -h
echo
AVAIL = $ ( free | awk '/ Mem / { printf "% d " , $7 / $2 *100} ')
if [ " $AVAIL " - lt " $THRESHOLD " ]; then
echo " PERINGATAN : Memori tersedia hanya $ { AVAIL }%!"
else
echo " Status : Memori tersedia $ { AVAIL }% ( normal ) "
fi
echo
echo " - - - 5 Proses Memori Tertinggi - - -"
ps aux -- sort = -% mem | head -n 6 | tail -n 5
```
Hasil :

3. izinkan dan jalankan
```
chmod + x monitor - memori . sh
bash monitor - memori . sh
```
Hasil :

Analisis
1. Variabel THRESHOLD=20 menetapkan batas persentase. Perintah free | awk ’/Mem/ {printf "%d", $7/$2*100}’ mengambil kolom ke-7 (available) dibagi kolom ke-2 (total) dari baris Mem, lalu dikalikan 100 untuk menghasilkan persentase bilangan bulat
2. Kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] bernilai benar jika persentase memori tersedia di bawah 20
3. Ubah THRESHOLD menjadi 90 dan jalankan ulang. Apa yang berubah pada output? Mengapa demikian?

### Studi Kasus 10.2 Gagal Akses File
1. Buat direktori dan file konfigurasi contoh
```
mkdir -p ~/ praktikum - os / week10 - memory / syscall - case
cd ~/ praktikum - os / week10 - memory / syscall - case
echo " PORT =8080" > app . conf
ls -l app . conf
cat app . conf
```
Hasil :

2. Simulasikan permission bermasalah
```
chmod 000 app . conf
cat app . conf
```
Hasil :


3. Kembalikan permission dan verifikasi
```
chmod 644 app . conf
cat app . conf
```
Hasil :


Analisis:
1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System call apa yang gagal?
2. Apa perbedaan pesan error Permission denied vs No such file or directory? Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya
3. Permission 644 berarti apa untuk owner, group, dan others?


## Praktikum 10.6 Mengamati System Call dengan strace
1. Lihat 30 baris pertama system call dari perintah ls
```
strace ls 2 >&1 | head -n 30
```
Hasil :


2. Lihat ringkasan statistik dan bandingkan dua direktori berbeda
```
strace -c ls
strace -c ls / etc 2 >&1 | tail -5
```
Hasil :


Analisis:
1. Dari output Langkah 1, identifikasi minimal 4 system call berbeda. Jelaskan fungsi singkat masing-masing berdasarkan argumen yang terlihat
2. Dari ringkasan strace -c, system call mana yang paling sering dipanggil? Mengapa?
3. Apakah ada system call dengan errors lebih dari 0? Apakah itu berarti program bermasalah, ataukah bagian normal dari logika program?
4. Apakah jumlah system call berbeda antara ls dan ls /etc? Faktor apa yang menyebabkan perbedaan tersebut?


## TUGAS PRAKTIKUM 
Kerjakan seluruh tugas pada direktori berikut :
```
mkdir -p ~/ praktikum - os / week10 - memory
cd ~/ praktikum - os / week10 - memory
```

### Tugas 10.1 Audit Penggunaan Memori Sistem
Buat script memory-audit.sh yang menghasilkan laporan kondisi memori sistem secara otomatis
```
nano ~/ praktikum - os / week10 - memory / memory - audit . sh
```

```
#!/ bin / bash
set - euo pipefail
LAPORAN =" memory - report . txt "
{
echo "=== LAPORAN MEMORI SISTEM ==="
date
echo
echo " - - - Ringkasan free -h - - -"
free -h
echo
echo " - - - / proc / meminfo - - -"
cat / proc / meminfo | head -n 20
} > " $LAPORAN "
echo " Laporan disimpan ke : $LAPORAN "
cat " $LAPORAN "
```

```
chmod + x ~/ praktikum - os / week10 - memory / memory - audit . sh
cd ~/ praktikum - os / week10 - memory
bash memory - audit . sh
```
Hasil :

Analisis
1. Hitung persentase memori tersedia (available / total × 100%). Apakah sistem dalam kondisi normal?
2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut pandang ketersediaan untuk aplikasi?
3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree?


### Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
Simpan daftar 10 proses pengguna memori terbesar ke file
```
ps aux -- sort = -% mem | head -n 10 > top - memory - process . txt
cat top - memory - process . txt
```

Analisis
1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka gunakan bersama?


### Tugas 10.3 Membuat dan Memverifikasi Swap File
Buat swap file khusus tugas sebesar 256 MB dan verifikasi
```
sudo fallocate -l 256 M / swapfile - tugas - week10
sudo chmod 600 / swapfile - tugas - week10
sudo mkswap / swapfile - tugas - week10
sudo swapon / swapfile - tugas - week10
```

```
{
echo "=== VERIFIKASI SWAP ==="
swapon -- show
echo
free -h
} > swap - check . txt
cat swap - check . txt
```

Analisis
1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?


### Tugas 10.4 Analisis System Call dengan strace
Analisis system call yang dipanggil perintah ls
```
strace -c ls 2 > strace - summary . txt
strace ls / etc 2 > strace - ls - etc . txt
cat strace - summary . txt
```

Analisis
1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya
2. System call mana yang paling sering dipanggil? Mengapa?
3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?


### Tugas 10.5 Studi Kasus Diagnosa Server Lambat
```
nano ~/ praktikum - os / week10 - memory / diagnosa - server . sh
```
#!/ bin/ bash
set - euo pipefail

LAPORAN =" diagnosa -server - lambat .txt"
WARN_MEM = false
WARN_SWAP =0
cek_memori () {
echo " --- Kondisi Memori ---"
free -h
echo
AVAIL_PCT = $ ( free | awk '/Mem/ { printf "%d" , $7/$2 *100}
')
if [ " $AVAIL_PCT " - lt 20 ]; then
echo " PERINGATAN : Memori tersedia hanya ${
AVAIL_PCT }%"
WARN_MEM = true
fi
}
cek_swap () {
echo " --- Penggunaan Swap ---"
swapon -- show 2 >/ dev / null || echo " Tidak ada swap
aktif "
echo
WARN_SWAP = $ ( free | awk '/ Swap / { print $3}')
if [ " $WARN_SWAP " - gt 0 ]; then
echo " INFO : Swap digunakan (${ WARN_SWAP } kB)"
fi
}
cek_proses () {
echo " --- 10 Proses Memori Tertinggi ---"
ps aux -- sort = -% mem | head -n 11
echo
}
cek_paging () {
echo " --- Aktivitas Paging (5 sampel ) ---"
vmstat 1 5
echo
}
ringkasan () {
    echo "=== RINGKASAN ==="
if [ " $WARN_MEM " = true ]; then
echo "- Memori : KRITIS - perlu tindakan segera "
else
echo "- Memori : normal "
fi
if [ " $WARN_SWAP " - gt 0 ]; then
echo "- Swap : aktif - pantau aktivitas paging "
else
echo "- Swap : tidak digunakan "
fi
}
{
echo "=== LAPORAN DIAGNOSA SERVER ==="
date
echo
cek_memori
cek_swap
cek_proses
cek_paging
ringkasan
} | tee " $LAPORAN "
echo
echo " Laporan disimpan ke: $LAPORAN "
```

```
chmod + x ~/ praktikum - os / week10 - memory / diagnosa - server . sh
cd ~/ praktikum - os / week10 - memory
bash diagnosa - server . sh
```
Hasil :


Analisis
1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses, cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script
3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?