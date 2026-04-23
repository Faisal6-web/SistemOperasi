# Laporan Praktikum Sistem Operasi Jobsheet 9

<h4>Nama : Faisal Rizky <h4>
<h4>NIM : 254107020224 <h4>
<h4>Kelas : TI-1H <h4>

## Praktikum 9.1 Script Pertama: Laporan Sistem
1. Buat workspace praktikum:
```
mkdir -p ~/praktikum-os/week09/{scripts,logs,data}
cd ~/praktikum-os/week09/scripts
```
Hasil :



2. Buat script dengan nano:
```
nano laporan-sistem.sh
```
Hasil :



3. Ketik isi berikut, simpan(Ctrl+O lalu Enter), lalu keluar(Ctrl+X)\
```
#!/bin/bash
# Script: laporan-sistem.sh

echo "======================================"
echo "            LAPORAN SISTEM            "
echo "======================================"
echo "Tanggal   : $(date '+%A, %d %B %Y')"
echo "Jam       : $(date '+%H:%M:%S')"
echo "Hostname  : $(hostname)"
echo "User      : $(whoami)"
echo "CPU core  : $(nproc)"
echo "RAM bebas : $(free -h | awk '/^Mem/ {print $4}')"
echo "Disk /    : $(df -h / | awk 'NR==2 {print $5}') terpakai"
echo "========================================================="
```
Hasil :


4. Beri izin dan jalankan:
```
chmod +x laporan-sistem.sh
./laporan-sistem.sh
```
Hasil :


### Latihan 9.1
Soal:

1. Modifikasi laporan-sistem.sh agar menyimpan output ke file laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk: gunakan tee yang sudah dipelajari di bab sebelumnya

Jawaban :



## Praktikum 9.2 Script Info Sistem dengan Argumen
1. Buat script:
```
nano ~/praktikum-os/week09/scripts/info-sistem.sh
```
Hasil :


2. Ketik isi berikut:
```
#!/bin/bash
# pengguna: ./info-sistem.sh [nama-admin] [batas-disk-persen]

ADMIN=${1:-"Tidak dikenal"}
BATAS=${2:-80}
TANGGAL=$(date '+%F %T')
DISK_PERSEN=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

echo "Admin     : $ADMIN"
echo "Tanggal   : $TANGGAL"
echo "Disk      : ${DISK_PERSEN}% terpakai"
echo "Batas     : ${BATAS}%"

if [ "$DISK_PERSEN" -gt "$BATAS" ]; then
    echo "STATUS    : PERINGATAN - disk melebihi batas!"
else
    SISA=$((BATAS - DISK_PERSEN))
    echo "STATUS    : Normal (sisa toleransi ${SISA}%)"
fi
```
Hasil :



3. Simpan, beri izin, uji dengan berbagai kombinasi argumen:
```
chmod +x ~/praktikum-os/week09/scripts/info-sistem.sh
./info-sistem.sh
./info-sistem.sh "Dian" 50
./info-sistem.sh "Dian" 10
```
Hasil :



### Latihan 9.2
Soal :

1. Buat script kalkulator.sh yang menerima tiga argumen: <angka1> <operator> <angka2> dengan operator +, -, *, atau /. Contoh: ./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih operasi, dan validasi jika argumen tidak lengkap.

Jawaban :



## Praktikum 9.3 Script Grading dan Menu Interaktif
1. Buat script grading (menggunakan if dan for):
```
nano ~/praktikum-os/week09/scripts/grading-batch.sh
```
Hasil :


2. Ketik isi berikut:
```
#!/bin/bash
# Script: grading-batch.sh
# Proses daftar nilai mahasiswa

MAHASISWA=("Andi: =92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")

echo "=== HASIL GRADING ==="
for ENTRI in "${MAHASISWA[@]}"; do
    NAMA=$(echo "$ENTRI" | cut -d: -f1)
    NILAI=$(echo "$ENTRI" | cut -d: -f2)

    if [ "$NILAI" -ge 85 ]; then
        GRADE="A"
    elif [ "$NILAI" -ge 75 ]; then
        GRADE="B"
    elif [ "$NILAI" -ge 65 ]; then
        GRADE="C"
    elif [ "$NILAI" -ge 55 ]; then
        GRADE="D"
    else
        GRADE="E"
    fi

    printf "%-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"
done
echo "============================================"
```
Hasil :


3. Simpan, beri izin dan jalankan:
```
chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh
./grading-batch.sh
```
Hasil :


4. Buat script menu interaktif (while+case):
```
nano ~/praktikum-os/week09/scripts/menu-sistem.sh
```
Hasil :


5. Ketik isi berikut:
```
#!/bin/bash
# Menu interaktif pemantauan sistem

while true; do
    echo ""
    echo "===  MENU MONITOR ==="
    echo "1) Info disk"
    echo "2) Info memori"
    echo "3) Proses teratas"
    echo "4) Keluar"
    echo -n "Pilih [1-4]: "
    read PILIHAN
  case $PILIHAN in
    1) df -h ;;
    2) free -h ;;
    3) ps aux --sort=-%cpu \ head -6 ;;
    4) echo "Sampai jumpa!"; exit 0 ;;
    *) echo "Pilihan tidak valid." ;;
  esac
done
```
Hasil :


6. Beri izin dan jalankan, coba setiap opsi:
```
chmod +x ~/praktikum-os/week09/scripts/menu-sistem.sh
./menu-sistem.sh
```
Hasil :



### Latihan 9.3
Soal :

Tambahkan ke script grading-batch.sh sebuah ringkasan di bagian bawah yang menampilkan: jumlah mahasiswa per grade (A, B, C, D, E) menggunakan perulangan for kedua yang mengiterasi array MAHASISWA

Jawaban :


## Praktikum 9.4 Library Fungsi Validasi
1. Buat file library:
```
nano ~/praktikum-os/week09/scripts/lib-validasi.sh
```
Hasil :


2. Ketik isi berikut:
```
#!/bin/bash
# lib-validasi.sh - Library fungsi validasi

adalah_angka() {
    [[ "$1" =~ ^[0-9]+$ ]]
}

file_bisa_dibaca() {
    [ -f "$1" ] && [ -r "$1" ]
}

error_exit() {
    echo "ERROR: $1" >&2
    exit 1
}

info() { echo "[INFO] $1; }
sukses() { echo "[OK] $1; }
```
Hasil :


3. Buat script yang menggunkan library: 
```
nano ~/praktikum-os/week09/scripts/pakai-library.sh
```
Hasil :



4. Ketik isi berikut:
```
#!/bin/bash
# Muat library (seperti import di java)
source ~/praktikum-os/week09/scripts/lib-validasi.sh

ANGKA=$1
FILE=$2

[ -z "$ANGKA" ] || [ -z "$FILE" ] && \
    error_exit "Penggunaan: $0 <angka> <path-file>"

if adalah_angka "$ANGKA"; then
    sukses "Input '$ANGKA' adalah angka valid"
else
    error_exit "'$ANGKA' bukan angka"
fi

if file_bisa_dibaca "$FILE"; then
    sukses "File '$FILE' bisa dibaca"
    info "Jumlah baris: $(wc -l < "$FILE")"
else
    error_exit "File '$FILE' tidak ada atau tidak bisa dibaca"
fi
```
Hasil :


5. Beri izin dan uji semua skenario:
```
chmod +x ~/praktikum-os/week09/scripts/pakai-library.sh
./pakai-library.sh 42 /etc/hostname
./pakai-library.sh abc /etc/hostname
./pakai-library.sh 42 /tidak-ada.txt
./pakai-library.sh
```
Hasil :


### Latihan 9.4
Soal :

Tambahkan fungsi konfirmasi() ke lib-validasi.sh. Fungsi ini menampilkan pertanyaan, membaca input Y/N dari user, mengembalikan 0 jika Y dan 1 jika N. Buat script demo yang memanggil fungsi ini sebelum menghapus sebuah file.

Jawaban :



## Praktikum 9.5 Script Backup dengan Opsi
1. Buat script:
```
nano ~/praktikum-os/week09/scripts/backup-data.sh
```
Hasil :


2. Ketik isi berikut:
```
