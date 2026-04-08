# Laporan Praktikum Sistem Operasi Jobsheet 7

<h4>Nama : Faisal Rizky <h4>
<h4>NIM : 254107020224 <h4>
<h4>Kelas : TI-1H <h4>

## Praktikum 7.1 — Mengenali Bash dan Menyiapkan Workspace
1. Lihat shell login dan shell aktif saat ini:
```
echo "Shell login : $SHELL"
echo "Shell aktif : $0"
bash --version | head -n 1
```
Hasil :


2. Lihat proses shell yang sedang berjalan: 
```
echo $$
ps -p $$ -o pid,ppid,args
```
Hasil :


3. Buat workspace praktikum:
```
mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}
cd ~/praktikum-os/week07-bash
pwd
```
Hasil :


4. Buat beberapa file contoh yang akan dipakai pada praktikum berikutnya:
```
touch sample-app.conf
touch logs/app-01.log logs/app-02.log logs/app-03.log
touch sampel/catatan-a.txt sampel/catatan-b.txt
touch sampel/backup-01.tar sampel/backup02.tar
touch sampel/laporan-harian.log sampel/laporan-mingguan.log sampel/laporan-bulanan.log
touch "ruang-nama/laporan server april.txt"
touch "ruang-nama/backup [mingguan] server.conf"
ls -R
```
Hasil :


## Praktikum 7.2 — Membuat Ringkasan Sesi Terminal
1. Masuk ke workspace praktikum:
```
cd ~/praktikum-os/week07-bash
```
Hasil :


2. Simpan informasi sesi terminal ke file laporan:
```
{
    echo "=== RINGKASAN SESI BASH ==="
    date
    echo "User          : $(whoami)"
    echo "Hostname      : $(hostname)"
    echo "Shell login   : $SHELL"
    echo "Shell aktif   : $0"
    echo "PID shell     : $$"
    echo "Direktori     : $(pwd)"
} | tee session-info.txt
```
Hasil :


3. Verifikasi isi file laporan:
```
cat session-info.txt
```
Hasil :


## Praktikum 7.3 — Menambahkan Konfigurasi Aman pada .bashrc
1. Lihat file konfigurasi Bash pada home directory:
```
ls -la ~ | grep -E 'bashrc|bash_profile|profile'
```
Hasil :


2. Buat backup .bashrc:
```
cp ~/.bashrc ~/.bashrc.bak-praktikum
```
Hasil :


3. Tambahkan blok konfigurasi praktikum:
```
cat <<'EOF' >> ~.bashrc

# --- Praktikum Bash Shell --- 
export PRAKTIKUM_BASH_DIR="$HOME/praktikum-os/wekk07-bash"
export EDITOR=nano
# --- End Praktikum Bash Shell ---

EOF
```
Hasil :


4. Terapkan konfigurasi tanpa logout:
```
source ~/.bashrc
echo "$PRAKTIKUM_BASH_DIR"
echo "$EDITOR"
```


## Praktikum 7.4 — Menyiapkan .bash_profile untuk Shell Login
1.  Backup .bash_profile jika sudah ada:
```
[ -f ~/.bash_profile ] && cp ~/.bash_profile ~/.bash_profile.bak-praktikum
```
Hasil :


2. Tambahkan konfigurasi login shell:
```
cat <<'EOF' >> ~/.bash_profile

# --- Praktikum Bash Login Shell ---
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi

echo "Login Bash pada $(date '+%F %T')" >> "$HOME/praktikum-os/week07-bash/login-audit.log"
# --- End Praktikum Bash Login Shell ---

EOF
```
Hasil :


3. Uji dengan membuka login shell baru:
```
bash -l
tail -n 3 ~/praktikum-os/week07-bash/login-audit.log
exit
```
Hasil :


## Praktikum 7.5 — Membedakan Variabel Shell dan Environment Variable
1. Buat variabel lokal:
```
