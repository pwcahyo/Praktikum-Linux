Praktikum Linux Pertemuan Ke-6
==============================

## Daftar Isi
- [History](#history) 
- [Bash Script](#bash-script)
- [Job Control](#job-control)
- [Alias](#alias)


Element dasar shell script
==========================

Shell script umumnya dibuat dengan editor teks (ASCII editor) dengan file ekstensi `.sh`. Shell script tersebut selalu diawali dengan komentar yang dimulai dengan tanda `#` kemudian diikuti dengan tanda `!` kemudian nama shell yang digunakan. seperti contoh berikut
```
#!/bin/sh
# Program Shell
#
```
History diadaptasi dari C-Shell, yaitu catatan dari semua instruksi yang sejauh ini telah dilakukan. Catatan ini dapat dilihat sebagai history, kemudian dapat dipilih kembali, diedit dan dieksekusi. History memudahkan pemakai untuk mengedit kembali instruksi kompleks dan panjang, terutama bila terjadi kesalahan pada penulisan instruksi maupun parameter.

Segala perintah yang telah dijalankan sebelumnya (history), dapat dilihat pada file `.bash_history` pada direktori `HOME` masing - masing.

Navigasi daftar history dapat dijalankan menggunakan karakter kontrol sebagai berikut :
```
^P (Ctrl-P)   melihat instruksi sebelumnya
^N (Ctrl-N)   melihat instruksi berikutnya
!!            eksekusi kembali instruksi sebelumnya
!–3           mengulangi instruksi ketiga (3) dari perintah yang dijalankan paling akhir
!88          ulangi instruksi no 88
```

### Percobaan History

1. Melihat batasan maksimum instruksi yang akan disimpan pada history
```
echo $HISTSIZE
```
2. Melihat daftar instruksi yang telah dilakukan dengan perintah `history`
```
history
```
3. Menggunakan fix command `fc` untuk melihat history
```
fc -l
```
4. Mengulangi perintah pada history number `40`
```
!40
```
5. Mengulangi perintah pada history ketiga (3) dari perintah history paling akhir
```
!-3
```
6. Selain menggunakan `history` dan `fc` untuk melakukan pencarian perintah yang pernah dijalankan bisa menggunakan `ctrl+r` di  keyboard yang nantinya akan muncul inputan `key word` pencarian. dengan contoh mencari perintah sebelumnya dengan `key word` : `cat .bash`
```
(reverse-i-search)`cat .bash': cat .bashrc 
```

[selebihnya](https://www.washington.edu/computing/unix/history.html)

Bash Script
===========

Bash-script adalah file yang berisi koleksi program yang dapat dieksekusi. Untuk eksekusi bash script gunakan . sebelum file bash-script yang berarti eksekusi shell dan tanda ./ berarti file bash-script berada pada direktori actual.
1. Membuat program bash script
```
nano bash1.sh
```
ketikan
```
#!/bin/bash
echo "program bash script praktikum linux"
```
`ctrl+x` kemudian tekan `y` tekan `enter` pada keyboard.

2. Jalankan file bash script dengan perintah:
```
bash bash1.sh
sh bash1.sh
. bash1.sh
```
kemudian jalankan menggunakan perintah
```
./bash1.sh
```
3. Mengubah file bash-script menjadi executable
```
ls -l bash1.sh
chmod +x bash1.sh
ls -l bash1.sh
```
4. Kemudian ulangi perintah menjalankan file bashscript menggunakan `./bash1.sh`
```
./bash1.sh
```
5. Buat file bash kedua dengan nama `bash2.sh`
```
nano bash2.sh
```
dengan isi program sebagai berikut:
```
#!/bin/bash
echo "program bash script yang kedua"
```
6. Kemudian jalankan kedua file bash-script tersebut menggunakan perintah
```
./bash1.sh ; ./bash2.sh
```
7. Menjalankan script sebagai proses background, sehingga terminal tidak menunggu program sampai selesai dijalankan. untuk menjalankan proses background bisa menggunakan tanda `&` di akhir perintah
```
./bash1.sh &
./bash2.sh &
```
8. Menjalankan 2 program atau lebih dalam satu block, kemudian dilakukan ekeskusi sebagai proses didalam background, menggunakan tanda `(...)` untuk mengelompokan dalam satu block
```
(./bash1.sh ; ./bash2.sh) > hasil_bash &
cat hasil_bash
```

# Job Control

1. Melihat proses foreground
```
ps x
ps x > proses_fg &
```
2. Melihat proses background yang berjalan
```
jobs
```
3. Membuat file program `loop.sh`
```
nano loop.sh
```
kemudian isikan file program sebagai berikut :
```
#!/bin/bash 
while [ true ] 
do
 sleep 3
 echo “Aku Lapar”
done
```
4. Buatlah file `loop.sh` menjadi executable. dengan menggunakan `chmod +x loop.sh` kemudian jalankan dengan menggunakan `./loop.sh` program akan berjalan selama 3 detik sekali. untuk menghentikannya bisa menggunakan perintah `ctrl+c` di keyboard
5. Jalankan file `loop.sh` sebagai background
```
./loop.sh &
```
6. Periksa kembali jobs yang aktif (setiap job akan mempunyai  PID), pindahi job background yang aktif menjadi foreground `fg %[PID background process]` :
```
fg %1
```
7. Untuk mengembalikan proses foreground ke background, tekan `ctrl+z` kemudian jalankan instrukis `bg`
```
bg
jobs
```

# Alias
Alias adalah mekanisme untuk memberi nama alias pada satu atau sekelompok instruksi. 
1. Untuk melihat alias yang sudah terdaftar pada system :
```
alias
```
2. Membuat beberapa alias
```
alias del_direktori="rm –r"
alias h="history"
```
3. Menghapus alias dapat menggunakan instruksi `unalias`
```
unalias del
```