Cron (System Daemon)
====================

Cron adalah sebuah sistem daemon yang digunakan untuk melakukan eksekusi pekerjaan (task) secara background process pada waktu tertentu.

Setiap user (termasuk root) memiliki crontab file. Cron daemon dapat melakukan pengecekan crontab user, tidak peduli apakah user yang menjalankan crontab `sedang login` kedalam sistem atau tidak.

melihat manual dari crontab dapat menggunakan `man crontab`

Perintah pada crontab
=====================
```
crontab [-u user] file
```
```
crontab [-u user] [i] {-l | -r | -e}
```
Keterangan:
```
-u user : Spesifik user cron
-l : melihat crontab list
-r : remove crontab yang sedang berjalan
-e : edit crontab dengan editor secara spesifik
-i : remove crontab dengan konfirmasi

```

Format Waktu Crontab
====================
Crontab memiliki format waktu eksekusi, format waktu tersebut adalah sebagai berikut:
```
.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
|  |  |  |  |
*  *  *  *  *  command to be executed
```
tanda bintang merupakan tidak ditentukan pada waktu tersebut.
contoh : `01 * * * * ./klik.sh` *file bash klik.sh akan dieksekusi setiap menit kesatu pada setiap jamnya*


Menggunakan Cron
================

1. Definisikan program yang akan dijalankan. berikut program untuk checking history log user active pada sebuah server linux ubuntu. `history_user.sh`
```
#!/bin/sh

DATE=`date`
WHO=`who`
printf "$DATE\n$WHO\n\n" >> history_user.log
```
`printf` merupakan perintah cetak output sederhana seperti echo akan tetapi lebih flexible dengan penambahan `\n` untuk menambahkan baris baru secara custom. Perintah `date` adalah perintah untuk melihat tanggal waktu sekarang. Perintah `who` digunakan untuk melihat user log. sedangkan tanda `$` diikuti nama variable adalah digunakan untuk mencetak isi variable yang telah didefinisikan sebelumnya.

2. Ubah file `history_user.sh` menjadi executable

3. Definisikan  periodecaly waktu eksekusi program, setiap jam 23 pada menit 59
```
crontab -e
```
```
01 01 * * * ./history_user.sh
```
secara otomatis crontab akan berjalan meskipun user logout dari system.

4. Check crontab pwcahyo yang sedang berjalan.
```
crontab -u pwcahyo -l
```
*Apabila ingin melihat crontab user lain, pastikan user yang melihat merupakan user root* 

5. Untuk menghentikan crontab dapat menggunakan 
```
crontab -r
``` 

Tugas Crontab
=============
Buat satu buah file bash dengan nama `home_detail.sh` untuk melihat list folder home secara detail pada setiap `bulan, tanggal 1, jam 10.30 Malam`. hasil listing tersebut disimpan secara append kedalam file `home_file.log`
