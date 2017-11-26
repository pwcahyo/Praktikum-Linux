Manajemen User dan Group
========================
Pada Linux ubuntu, informasi mengenai user account dan groups disimpan dalam beberapa file teks, beberapa file teks tersebut berada dalam direktori `/etc/` . Melihat atau menambahkan daftar group dan daftar user misalnya. 

1. File `/etc/passwd`.
======================
Untuk melihat daftar user yang dipisahkan perbaris, kita dapat mengakses isi file pada `/etc/passwd`. Didalamnya terdapat beberapa informasi mengenai `username`, `password`, `user id`, `group id`, `deskripsi`, `direktori home` dan `shell yang digunakan`.
Pemisahan informasi tersebut menggunakan tanda `:` pada informasi yang dimiliki oleh setiap user.
berikut ini contoh daftar user yang berada pada file `/etc/passwd`.
```
zero:x:1001:1001:,,,:/home/zero:/bin/bash
```
Keterangan :
```
zero sebagai *username* : nama user yang diketik saat login sistem
x sebagai *password* : berisi password user yang dienkripsi (atau x bila shadow password digunakan)
1001 sebagai *user id (UID)* : bilangan numerik secara unique sebagai id username
1001 sebagai *group id (GID)* : bilangan numerik secara unique sebagai id group
,,, sebagai *gecos* : nama histori, kolom gecos bersifat optiona dan digunakan untuk menyimpan informasi tambahan (seperti nama lengkap user)
/home/zero sebagai *home directory* : path absolute, lokasi direktori user
/bin/bash sebagai *shell* : program otomatis dijalankan bila user login. berupa intepreter (shell)
```

2. File `/etc/group`
====================
Untuk melihat daftar group yang dipisahkan perbaris maka kita dapat mengakses file `/etc/group` Didalamnya terdapat beberapa informasi mengenai `group name`, `group password`, `group id` dan `member list`.
Pemisahan informasi tersebut menggunakan tanda `:` pada informasi yang dimiliki oleh setiap group.
berikut ini contoh daftar user yang berada pada file `/etc/group`.
```
root:x:0:zero
```
Keterangan :
```
root sebagai *group name*
x sebagai *group password*  : x apabila shadow password digunakan
0 sebagai *group id (GID)* : bilangan numerik secara unique sebagai id group
zero sebagai *anggota group* : daftar user yang berada pada group tersebut
```


