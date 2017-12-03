# Tugas Sharing Folder dan File
1. Buat group `[username]_group`
2. Buat user `[username]_user`, kemudian masukan kedalam group `[username]_group`
3. Setting password samba pada `[username]_user`
4. Buat direktori `[username]_sharing`
5. Ubah permission direktori `[username]_sharing` menjadi `0770`
6. Ubah kepemilikan folder dari `root` ke `[username]_group`
7. Setting konfigurasi `/etc/samba/smb.conf` agar hanya bisa diakses oleh user pada `[username]_group`
8. Letakan sebuah file pada folder `[username]_sharing` dengan nama `biodata.txt` dengan isi didalamnya sebagai berikut:
```
Nama 	: Nama Masing - Masing
NIM		: NIM Masing - Masing
PRODI	: Prodi Masing - Masing
ASAL	: Asal Daerah Masing - Masing
```
9. Restart samba service. 
10. Berikan *username dan password* ke salah satu teman sekelas, akses folder tersebut menggunakan *username dan password* yang sudah diberikan kedalam alamat ip masing2. Kemudian analisis apakah sharing dokumen tersebut berhasil.