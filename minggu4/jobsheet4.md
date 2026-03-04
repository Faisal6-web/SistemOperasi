# Laporan Praktikum Sistem Operasi Jobsheet 4

<h4>Nama : Faisal Rizky <h4>
<h4>NIM : 254107020224<h4>
<h4>Kelas : TI-1H<h4>

## Percobaan 1 : Direktory ##
1. Melihat direktori HOME
```
 pwd
 echo $HOME

 ```

2. Melihat direktori aktual dan parent direktori
```
 pwd
 cd .
 pwd
 cd ..
 pwd
 cd

```

3. Membuat satu direktori, lebih dari satu direktori atau sub direktori
```
 pwd
 mkdir A B C A/D A/E B/F A/D/A
 ls -l
 ls -l A
 ls -l A/D

 ```

4. Menghapus satu atau lebih direktori hanya dapat dilakukan pada       direktori kosong dan hanya dapat dihapus oleh pemiliknya kecuali bila diberikan ijin aksesnya
```
 rmdir B           (Terdapat pesan error, mengapa?)
 ls -l B
 rmdir B/F B
 ls -l B            (Terdapat pesan error, mengapa?)

 ```

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

2. Perintah mv untuk memindah file
```

mv contoh contoh2
ls -l
mv contoh1 contoh2 A/D
ls -l A/D
mv contoh contoh1 C
ls -l C

```

3. Perintah rm untuk menghapus file
```

rm contoh2
ls -l
rm -i contoh
rm -rf A C
ls -l

```


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

## Percobaan 4: Melihat Isi File ##

