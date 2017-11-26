Manajemen User dan Group
========================
Pada Linux ubuntu, informasi mengenai user account dan group disimpan dalam beberapa file teks, beberapa file teks tersebut berada dalam direktori `/etc/` . Melihat atau menambahkan daftar group dan daftar user misalnya. 

Melihat daftar user
===================
Untuk melihat daftar user yang dipisahkan perbaris, kita dapat mengakses isi file pada `/etc/passwd` dengan mengetik `cat /etc/passwd`. Didalamnya terdapat beberapa informasi mengenai `username`, `password`, `user id`, `group id`, `deskripsi`, `direktori home` dan `shell yang digunakan`.
Pemisahan informasi tersebut menggunakan tanda `:` pada informasi yang dimiliki oleh setiap user.
berikut ini contoh daftar user yang berada pada file `/etc/passwd`.
```
zero:x:1001:1001:,,,:/home/zero:/bin/bash
```
**Keterangan :**
- **zero** sebagai **_username_** : nama user yang diketik saat login sistem
- **x** sebagai **_password_** : berisi password user yang dienkripsi (atau x bila shadow password digunakan)
- **1001** sebagai **_user id (UID)_** : bilangan numerik secara unique sebagai id username
- **1001** sebagai **_group id (GID)_** : bilangan numerik secara unique sebagai id group
- **,,,** sebagai **_gecos_** : nama histori, kolom gecos bersifat optiona dan digunakan untuk menyimpan informasi tambahan (seperti nama lengkap user)
- **/home/zero** sebagai **_home directory_** : path absolute, lokasi direktori user
- **/bin/bash** sebagai **_shell_** : program otomatis dijalankan bila user login. berupa intepreter (shell)


Melihat daftar group
====================
Untuk melihat daftar group yang dipisahkan perbaris maka kita dapat mengakses file `/etc/group` dengan mengetik `cat /etc/group`  Didalamnya terdapat beberapa informasi mengenai `group name`, `group password`, `group id` dan `member list`.
Pemisahan informasi tersebut menggunakan tanda `:` pada informasi yang dimiliki oleh setiap group.
berikut ini contoh daftar user yang berada pada file `/etc/group`.
```
root:x:0:zero
```
**Keterangan :**
- **root** sebagai **_group name_**
- **x** sebagai **_group password_** : x apabila shadow password digunakan
- **0** sebagai **_group id (GID)_** : bilangan numerik secara unique sebagai id group
- **zero** sebagai **_anggota group_** : daftar user yang berada pada group tersebut

Aplikasi user account dan group
===============================
Terdapat dua tipe aplikasi dasar yang dapat digunakan untuk mengatur user account dan group pada sistem linux ubuntu:
- Aplikasi secara Graphical User Management.
- Perintah menggunakan terminal.

Beberapa perintah untuk memanajemen user account adalah sebagai berikut:

useradd
=======
Perintah untuk menambah user account. perintah dibawah adalah contoh penambahan user dengan nama `pwcahyo`
```
useradd pwcahyo
```
perintah untuk menciptakan user `pwcahyo` secara langsung memasukan user kedalam group yang sudah ada, yaitu group `pwcahyo_member`
```
useradd -g pwcahyo_member pwcahyo
```

userdel 
=======
Perintah untuk menghapus user account. perintah dibawah ini contoh perintah hapus user dengan nama `pwcahyo`
```
userdel -r pwcahyo
```
usermod
=======
Perintah untuk editing attribut user. secara umum penggunakan `usermod` adalah sebagai berikut
```
usermod [options] username
``` 
ada beberapa cara penggunakan `usermod` diantaranya adalah sebagai berikut:
- ### menambahkan informasi user
perintah berikut adalah menambahkan informasi `Ini adalah Puji Winar Cahyo` kedalam user `pwcahyo`
```
usermod -c "Ini adalah Puji Winar Cahyo" pwcahyo
```
melihat hasil penambahan informasi dapat menggunakan `grep -E --color 'pwcahyo' /etc/passwd`
- ### merubah direktori home user
Perintah berikut adalah mengubah direktori home pwcahyo yaitu `/home/pwcahyo` menjadi `/home/pwcahyo/home_new`

```
mkdir /home/pwcahyo/home_new
usermod -d /home/pwcahyo/home_new pwcahyo
```
melihat hasil penggantian direktori home menggunakan `grep -E --color '/home/pwcahyo/home_new' /etc/passwd`.
- ### Memasukan user account kedalam group dengan usermod
Perintah berikut memasukan user `pwcahyo` kedalam primer group `pwcahyo_member`
```
usermod -g pwcahyo_member pwcahyo
```
- ### modifikasi group pada user account 
Modifikasi group untuk dimasukan kedalam kelompok group primer atau sekunder. contoh berikut melakukan modifikasi user account `pwcahyo` dengan group sekunder `pwcahyo_secretary` dan `pwcahyo_servant`. kemudian memiliki group primer `pwcahyo_member`.
```
usermod -g pwcahyo_member -G pwcahyo_secretary,pwcahyo_servant pwcahyo
```
untuk melakukan checking group yang dimiliki `pwcahyo` dapat menggunakan perintah sebagai berikut.
```
id pwcahyo
```
- ### Mengganti password menggunakan `usermod`
Perintah berikut merupakan contoh perintah penggantian password pada user account `pwcahyo` dengan password baru `linux`
```
usermod -p linux pwcahyo
```

passwd
======
Perintah untuk setting password.
```
passwd pwcahyo
```
chpasswd
========
Perintah mengubah password secara bulk mode (update passwod secara banyak user).
```
chpasswd
```
kemudian masukan update password, contoh berikut username `pwcahyo` dirubah passwordnya menjadi `cahyo`. username `zero` menjadi `nol`.
```
pwcahyo:cahyo
zero:nol
```
selesai memasukan update password kemudian tekan `Ctrl+c`

chage
===== 
Perintah untuk melihat dan mengubah masa berlaku password (hampir sama dengan passwd). 
berikut ini contoh perintah untuk melihat masa berlaku password:
```
chage -l pwcahyo
```
Perintah berikut ini untuk melakukan setting habis masa berlaku password (expired). Setting user `pwcahyo` dengan aktif password selama 30 hari.
```
chage -M 30 pwcahyo
```
chfn
====
Perintah untuk mengubah informasi umum user account. berikut contoh perintah untuk mengubah informasi umum mengenai user `pwcahyo`
```
chfn pwcahyo
```
chsh
====
Perintah untuk mengubah shell default user.

Perintah manajemen group
========================
Beberapa perintah untuk memanajemen group adalah sebagai berikut:

groupadd
========
Perintah untuk menambahkan group, (akan tetapi tidak menentukan anggota user pada group tersebut). contoh berikut menambahkan group baru dengan nama `pwcahyos_member`, `pwcahyo_secretary` dan `pwcahyo_servant`.
```
groupadd pwcahyos_member
groupadd pwcahyo_secretary
groupadd pwcahyo_servant

```
untuk memasukan user yang sudah ada kedalam group dapat menggunakan `useradd` dan `usermod`. 

groupdel
========
Perintah untuk menghapus group. contoh berikut perintah untuk menghapus group `pwcahyo_secretary` dan `pwcahyo_servant`
```
groupdel pwcahyo_secretary
groupdel pwcahyo_servant
```
groupmod
========
Perintah untuk memodifikasi nama group atau group id (GID). akan tetapi tidak mengubah keanggotan group. contoh berikut merubah nama group `pwcahyo_servant` menjadi `pwcahyo_assistant`
```
groupmod -n pwcahyo_assistant pwcahyo_servant
```
gpasswd
=======
Perintah untuk mengubah keanggotaan group dan melakukan setting password untuk mengijinkan anggota selain group tersebut untuk bergabung. (digunakan juga untuk menentukan administrator group).
Contoh perintah memasukan single user `pwcahyo` kedalam group aktif `pwcahyo_servant`
```
gpasswd -a pwcahyo pwcahyo_servant
```
Contoh perintah memasukan multiple user `pwcahyo`, `mark`, `kate` kedalam group yang sudah aktif, yaitu group `pwcahyo_member`
```
gpasswd -M pwcahyo, mark, kate pwcahyo_member
```
grpc
====
perintah untuk memeriksa integritas file /etc/group dan /etc/gshadow

