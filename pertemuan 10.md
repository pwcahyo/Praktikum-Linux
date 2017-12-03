Samba Sharing
=============
Samba adalah paket sharing yang dapat digunakan untuk sharing printer maupun dokumen salah satunya pada sistem operasi Linux. Didalam samba itu sendiri support SMB dan CIFS protocol. SMB (Server Message Block) dan CIFS (Common Internet File System) adalah standard protocol untuk sharing file, printer, serial port dan komunikasi seperti name pipes dan mail antar komputer.

Installing samba
================
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
4. Lihat bagian `workgroup = WORKGROUP`. Untuk mengubah workgroup share dapat dilakukan edit pada `WORKGROUP` sesuaikan dengan nama jaringan workgroup yang ada. *apabila tidak ada, biarkan saja (tidak diedit)*
5. Sharing folder dengan tanpa batas *siapa saja boleh mengakses folder ***anonymous*** tanpa harus login*.Buka file `smb.conf` tersebut menggunakan editor `nano /etc/samba/smb.conf`. kemudian tambahkan baris berikut di bagian paling bawah.
```
[Anonymous]

path = /samba/anonymous
browsable = yes
writable = yes
read only = no
force user = nobody
```
6. Ciptakan folder `anonymous` didalam folder `samba`.
```
sudo mkdir -p /samba/anonymous
```
7. Sharing folder dengan user terbatas,* ***hanya user:shares dan pass:shares*** yang boleh melakukan akses folder ***shares*** *







