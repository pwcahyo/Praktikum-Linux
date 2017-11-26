Manajemen User dan Group
========================
Pada Linux ubuntu, informasi mengenai user account dan group disimpan dalam beberapa file teks, beberapa file teks tersebut berada dalam direktori `/etc/` . Melihat atau menambahkan daftar group dan daftar user misalnya. 

Melihat daftar user
======================
Untuk melihat daftar user yang dipisahkan perbaris, kita dapat mengakses isi file pada `/etc/passwd`. Didalamnya terdapat beberapa informasi mengenai `username`, `password`, `user id`, `group id`, `deskripsi`, `direktori home` dan `shell yang digunakan`.
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
Untuk melihat daftar group yang dipisahkan perbaris maka kita dapat mengakses file `/etc/group` Didalamnya terdapat beberapa informasi mengenai `group name`, `group password`, `group id` dan `member list`.
Pemisahan informasi tersebut menggunakan tanda `:` pada informasi yang dimiliki oleh setiap group.
berikut ini contoh daftar user yang berada pada file `/etc/group`.
```
root:x:0:zero
```
**Keterangan :**
- **root** sebagai **_group name*
- **x** sebagai **_group password_** : x apabila shadow password digunakan
- **0** sebagai **_group id (GID)_** : bilangan numerik secara unique sebagai id group
- **zero** sebagai **_anggota group_** : daftar user yang berada pada group tersebut


