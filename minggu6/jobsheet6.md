# Laporan Praktikum Sistem Operasi Jobsheet 6

<h4>Nama : Faisal Rizky <h4>
<h4>NIM : 254107020224 <h4>
<h4>Kelas : TI-1H <h4>

## Praktikum 6.1 — Melihat Proses dan Thread
1. Tampilkan semua proses yang berjalan:
```
ps aux

```

2. Tampilkan proses beserta thread-nya, dapat dilihat pada kolom LWP (Light Weight Process ID):
```
ps aux -L

```

3. Lihat PID shell aktif dan detail prosesnya:
```
echo $$
ps -p $$ -f

```

4. Lihat hierarki proses secara visual:
```
pstree -p

```

### Latihan 6.1
Jalankan ps aux dan amati outputnya:

1. Berapakah total proses yang berjalan ? Proses apa yang memiliki PID terkecil ?
Jawaban :

2. Jalankan pstree -p dan temukan proses bash anda. Proses apa yang menjadi induk (PPID) dari bash tersebut ?
Jawaban :

3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang anda lihat ?
Jawaban : 


## Praktikum 6.2 — Mengamati Siklus Hidup Proses
1. Buat proses di background dan amati kondisinya:
```
sleep 60 &
ps aux | grep sleep

```

2. Amati perubahan exit code dari perintah yang berhasil dan gagal:
```
ls /tmp
echo "Sukses: $?"

ls /direktori-tidak-ada
echo "Gagal: $?"

```

### Latihan 6.2
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
Jawaban :

2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit code masing-masing. Pola apa yang anda temukan ?
Jawaban :


## Praktikum 6.3 — Mengatur Prioritas Proses
1. Jalankan proses dengan prioritas rendah:
```
nice -n 10 sleep 300 &

```

2. Verifikasi nilai nice pada kolom NI:
```
ps aux | grep sleep

```

3. Ubah nilai nice proses yang sudah berjalan:
```
renice -n 15 -p <PID>
ps -p <PID> -o pid , ni , cmd

```

4. Bersihkan proses percobaan:
```
kill %1

```

### Latihan 6.3
1. jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan ps
Jawaban : 

2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali
Jawaban :

3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi ? Mengapa Linux membatasi hal ini untuk user biasa ?
Jawaban :


## Praktikum 6.4 — Mengirim Sinyal ke Proses
1. Buat proses percobaan:
```
sleep 500 &
sleep 600 & 
sleep 700 &
ps aux | grep -v grep | grep sleep

```

2. Hentikan satu proses dengan SIGTERM dan verifikasi:
```
kill <PID-sleep-500>
ps aux | grep -v grep | grep sleep

```

3. jeda dan lanjutkan proses dengan SIGSTOP/SIGCONT:
```
kill -SIGSTOP <PID-sleeo-600>
ps aux | grep sleep  # amati kolom STAT : berubah menjadi T  

kill -SIGCONT <PID-sleep-600>
ps aux | grep sleep  # STAT kembali ke S

```

4. Hentikan semua proses sleep sekaligus:
```
pkill sleep

```

### Latihan 6.4
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul?
Jawaban :

2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
Jawaban :

3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?
Jawaban :


## Praktikum 6.5 — Manajemen Job Foreground dan Background
1. Jalankan tiga job di background:
```
sleep 200 &
sleep 300 &
sleep 400 &
jobs

```

2. Bawa job pertama ke foreground, jeda, lalu kembali ke background:
```
fg %1
# Tekan CTRL+Z untuk menjeda
bg %1
jobs

```

3. Hentikan semua job:
```
kill %1 %2 %3
jobs

```

### Latihan 6.5
1. Jalankan top di foreground. Apa yang terjadi di terminal?
Jawaban :

2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?
Jawaban :

3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan baik di background? Mengapa?
Jawaban :

4. Kembalikan ke foreground dengan fg, lalu keluar dengan q .
Jawaban :


## Praktikum 6.6 — Pemantauan Proses
1. 