Praktikum Linux Pertemuan Ke-6
==============================

## Daftar Isi
- [Element dasar shell script](#element-dasar-shell-script) 
- [Variable shell script](#variable-shell-script)
- [Membaca input dari keyboard](#membaca-input-dari-keyboard)
- [Parameter](#parameter)

## Latihan
- [Latihan 1 penggunaan variable](#latihan-1-penggunaan-variable)
- [Latihan 2 menggunakan input dari keyboard](#latihan-2-menggunakan-input-dari-keyboard)
- [Latihan 3 argumen terminal kedalam variable](#latihan-3-argumen-terminal-kedalam-variable)
- [Latihan 4 bash script dengan argument terminal](#latihan-4-bash-script-dengan-argument-terminal)
- [Latihan 5 bash script parameter](#latihan-5-bash-script-parameter)


Element dasar shell script
==========================

Shell script umumnya dibuat dengan editor teks (ASCII editor) dengan file ekstensi `.sh`. Shell script tersebut selalu diawali dengan komentar yang dimulai dengan tanda `#` kemudian diikuti dengan tanda `!` kemudian nama shell yang digunakan. seperti contoh berikut
```
#!/bin/sh
# Program Shell
#
```

Variable shell script
=====================
Variable shell  digunakan untuk menampung berbagai macam data yang nantinya dapat digunakan untuk operasi selanjutnya, penulisan variable shell adalah sebagai berikut : 
```
nama_var = nilai_var
```
nama variable harus dimulai dengan alphabet kemudian disusul dengan alfanumerik maupun karakter lain. variable dapat ditulis menggunakan huruf kecil atau huruf besar atau campuran keduanya *(case sensitive)*:
```
NAMA=cahyo
j=5
```
Penggunaan nama variable tidak boleh dipisahkan menggunakan spasi ataupun tanda baca yang lain. Dikarenakan shell akan mengenali pemisahan tersebut sebagai parameter, seperti contoh berikut
```
NAMA =cahyo		#salah
NAMA= cahyo		#salah
```
sedangkan untuk mencetak isi dari variable dapat menggunakan tanda `$` didepan nama variable tersebut kemudian memanfaatkan fungsi echo untuk dapat menampilkan isi variable tersebut. sebagai contoh:
```
NAMA=cahyo
echo $NAMA

UMUR=12
echo $UMUR
echo $NAMA $UMUR
```
penggunaan string lebih dari satu kata harus diantara tanda kutip, sebagai contoh:
`$NAMA="Puji Winar Cahyo"`

Membaca input dari keyboard
===========================
Nilai variable dapat berupa masukan melalui ketikan dari keyboard, dengan menggunakan instruksi *read*

Parameter
=========
Program bash shell dapat mempunyai parameter sebanyak 9 parameter dan direpresentasikan melalui variable khusus yaitu `$1,$2,$3,$4,$5,$6,$7,$8,$9` bila tidak memberikan parameter maka nilai dari `$#` adalah `0`.
```
Shell variable `$*` menyatakan seluruh string menjadi parameter atau argumen sebuah script.
Shell variable `$$` menyatakan nomor proses id (PID) dari script yang dijalankan. 
proses PID ini akan terus berubah apabila dilakukan eksekusi (umumnya perubahan secara increment)
```

Latihan 1 penggunaan variable
=============================
1. Buat file biodata.sh dengan isi code bash shell sebagai berikut
```
#!/bin/sh
# Biodata
#
nama=cahyo
hobi=coding
pekerjaan=mahasiswa
```

2. Menggabungkan beberapa string kedalam satu cetak, *edit file* `biodata.sh` kemudian tambahkan :
```
echo "Biodata Saya"
echo nama:${nama}
echo hobi:${hobi}
echo pekerjaan:${pekerjaan}
```

3. Eksekusi file bash `./biodata.sh` dengan terlebih dahulu merubah permission file menjadi executable

Latihan 2 menggunakan input dari keyboard
=========================================
1. Buat file `biodata2.sh` kemudian isikan code bash shell sebagai berikut:

```
#!/bin/sh
# Biodata 2
#
echo "Nama saya : "
read nama
echo "Hobi : "
read hobi
echo "Pekerjaan : "
read pekerjaan
```

2. Tambahkan kode berikut untuk menampilkan hasil input:
```
echo
echo "Biodata saya : $nama, $hobi, $pekerjaan"
```

3. Perintah echo akan memunculkan baris baru pada command line, untuk menghindari hala tersebut dapat menggunakan argument `-n` untuk menghilangkan baris baru. edit file `biodata2.sh` kemudian tambahkan `-n` setelah echo.
```
echo -n "Nama saya : "
read nama
echo -n "Hobi : "
read hobi
echo -n "Pekerjaan : "
read pekerjaan
```
4. Eksekusi file `biodata2.sh`


Latihan 3 argumen terminal kedalam variable
===========================================
Hasil eksekusi argument pada terminal dapat dimasukan kedalam variable dengan memasukan perintah tersebut diantara tanda petik terbalik 
```
nama_variable=`argument`
```
sebagai contoh sebagai argumen diterminal sebagai berikut:
```
ME=`whoami`
echo $ME
```

Latihan 4 bash script dengan argument terminal
==============================================
Buat file `direktori_password.sh` dengan isi code bash sebagai berikut:
```
#!/bin/sh
# password direktori
#
echo -n "Masukan password : "
read PASSWORD
if [ $PASSWORD = "cahyo" ]
then
	HOME=`pwd`
	echo "direktori saya : $HOME"
fi
```

Latihan 5 bash script parameter
===============================
1. Buat file `biodata3.sh` kemudian isi dengan code bash sebagai berikut:
```
#!/bin/sh
# bash parameter
#
echo "Jumlah parameter yang dimasukan : $#"
echo "Nama program : $0"
echo "Parameter 1 : $1"
echo "Parameter 2 : $2"
echo "Parameter 3 : $3"
echo "Total parameter : $*"
echo "PID program ini : $$"
```

2. Eksekusi program `biodata3.sh` tersebut

*`pwcahyo@gmail.com`*

