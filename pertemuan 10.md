Samba Sharing
=============
Samba adalah paket sharing yang dapat digunakan untuk sharing printer maupun dokumen salah satunya pada sistem operasi Linux. Didalam samba itu sendiri support SMB dan CIFS protocol. SMB (Server Message Block) dan CIFS (Common Internet File System) adalah standard protocol untuk sharing file, printer, serial port dan komunikasi seperti name pipes dan mail antar komputer.


## Installing samba
1. Buka terminal linux kemudian install samba dengan beberapa dependency yang dibutuhkan.
```
sudo apt-get install -y samba samba-common python-glade2 system-config-samba
```
atau download dari repository ubuntu:
```
http://security.ubuntu.com/ubuntu/pool/main/s/samba/samba_4.3.11+dfsg-0ubuntu0.16.04.12_amd64.deb
```
2. Apabila samba berhasil diinstall, maka letak konfigurasi utama ada pada file:
```
/etc/samba/smb.conf
```
3. Backup file `smb.conf` tersebut kedalam file `smb.conf.bak` dengan menggunakan.
```
sudo cp -pf /etc/samba/smb.conf /etc/samba/smb.conf.bak
```
4. Lihat bagian `workgroup = WORKGROUP`. Untuk mengubah workgroup share dapat dilakukan edit pada `WORKGROUP` sesuaikan dengan nama jaringan workgroup yang ada. *apabila tidak ada, biarkan saja (tidak diedit)

# Share folder dan file tanpa batas
Sharing folder dengan tanpa batas yaitu siapa saja boleh mengakses folder ***anonymous*** tanpa harus *login*. Buka file `smb.conf` menggunakan editor `nano /etc/samba/smb.conf`. kemudian tambahkan konfigurasi berikut pada baris paling bawah.
```
[Anonymous]

path = /samba/anonymous
browsable = yes
writable = yes
read only = no
force user = nobody
```
Ciptakan folder `anonymous` didalam folder `samba`.
```
sudo mkdir -p /samba/anonymous
```
Kemudian restart samba service untuk mengatur ulang konfigurasi.
```
sudo service smbd restart
```


# Share folder dan file hanya untuk user tertentu
Sharing folder dengan user terbatas, pada kasus ini hanya user pada ***smbgrp*** yang boleh melakukan akses kedalam folder ***secure*** salah satunya adalah user dengan ***user:shares dan pass:shares*** yang nanti akan kita buat. Berikut langkah - langkah yang harus dijalankan:
- Tambahkan group baru yaitu ***smbgrp***
```
sudo addgroup smbgrp
```
- Tambahkan user ***shares*** kedalam group ***smbgrp***
```
sudo useradd shares -G smbgrp
```
- Berikan ***password*** pada user ***shares***.
```
smbpasswd -a shares
```
- Buat folder ***secure*** didalam folder ***samba***
```
sudo mkdir -p /samba/secure
```
- Ubah permission direktori tersebut.
```
sudo chmod -R 0770 /samba/secure
```
- Ubah kepemilikan folder.
```
sudo chown root:smbgrp /samba/secure
```
- Buka kembali file `smb.conf` pada `/etc/samba/smb.conf` dengan editor nano.
```
nano /etc/samba/smb.conf
```
tambahkan konfigurasi berikut pada baris paling bawah.
```
[SECURED]

path = /samba/secure
valid users = @smbgrp
browsable = yes
writable = yes
read only = no
```
- Kemudian restart samba service untuk mengatur ulang konfigurasi.
```
sudo service smbd restart
```

## Check hasil
Masukan beberapa file pada folder anonymous dan folder secure. 
kemudian lihat hasil sharing masing - masing dengan komputer lain.
***Windows*** : buka windows-explorer kemudian ketikan `\\alamat ip` pada url bar
***Linux*** : buka `Files` kemudian pilih `Connect to Server` masukan `smb://alamat ip`








