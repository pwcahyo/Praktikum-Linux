Installasi XAMPP (LAMPP)
========================

LAMPP adalah web server sederhana yang didalamya sudah tersedia Apache, MariaDB dan PERL. Penggunakan LAMPP tersebut sangatlah sederhana, tidak membutuhkan banyak konfigurasi untuk bisa menjalankannya. Untuk dapat menggunakan LAMPP tersebut maka,

1. Download LAMPP di halaman website berikut :
```
wget https://www.apachefriends.org/xampp-files/7.1.11/xampp-linux-x64-7.1.11-0-installer.run
```
2. Ubah permission xampp menjadi `executable`:
```
chmod +x xampp-linux-x64-7.1.11-0-installer.run
```
3. Install LAMPP menggunakan perintah:
```
sudo ./xampp-linux-x64-7.1.11-0-installer.run
```
Kemudian akan keluar konfigurasi sebagai berikut:
```
Welcome to the XAMPP Setup Wizard.

----------------------------------------------------------------------------
Select the components you want to install; clear the components you do not want 
to install. Click Next when you are ready to continue.

XAMPP Core Files : Y (Cannot be edited)

XAMPP Developer Files [Y/n] :Y

Is the selection above correct? [Y/n]: Y

----------------------------------------------------------------------------
Installation Directory

XAMPP will be installed to /opt/lampp
Press [Enter] to continue:

----------------------------------------------------------------------------
Setup is now ready to begin installing XAMPP on your computer.

Do you want to continue? [Y/n]: Y

----------------------------------------------------------------------------
Please wait while Setup installs XAMPP on your computer.

 Installing
 0% ______________ 50% ______________ 100%
 #########################################

----------------------------------------------------------------------------
Setup has finished installing XAMPP on your computer.
```
4. Ubah kepemilikan folder htdocs menjadi `775`.
```
sudo chmod -R /opt/lampp/htdocs/
```
5. Aktifkan LAMPP dengan menggunakan perintah:
```
sudo /opt/lampp/lampp start
```
6. Untuk menonaktifkan LAMPP, dapat dilakukan dengan menggunakan perintah:
```
sudo /opt/lampp/lampp stop
```
untuk restart
```
sudo /opt/lampp/lampp restart
```
7. Untuk melihat berhasil atau tidaknya bisa dicoba dengan mengakses localhost. ketikan `localhost` di url browser. Kemudian ketikan `localhost/phpmyadmin`
8. Apabila mengalami error, maka edit konfigurasi LAMPP pada `httpd-xampp.conf`
```
sudo nano /opt/lampp/etc/extra/httpd-xampp.conf
```
menjadi berikut.
```
<Directory "/opt/lampp/phpmyadmin">
    AllowOverride AuthConfig Limit
    Require all granted
    ErrorDocument 403 /error/XAMPP_FORBIDDEN.html.var
</Directory>
```
9. Akses kembali `localhost/phpmyadmin`

Installasi Wordpress
====================

1. Download wordpress pada url berikut `http://wordpress.org/latest.tar.gz` dengan menggunakan `wget` :
`wget -O wordpress.tar.gz http://wordpress.org/latest.tar.gz`
2. Extract file `wordpress.tar.gz`:
```
tar xzvf wordpress.tar.gz
```
3. Rename folder hasil ekstrak dengan username masing - masing `pwcahyo`
4. Pindah folder `pwcahyo` kedalam `/opt/lampp/htdocs`:
```
mv pwcahyo /opt/lampp/htdocs
```
5. Cek wordpress dengan mengetikan `localhost/pwcahyo` pada address bar web browser. apabila diminta untuk melakukan setting `Database` maka lanjutkan pada proses ke 6.
6. Masuk kedalam mysql konsole dengan mengetikan perintah berikut.
```
/opt/lampp/bin/./mysql -u root -p
```
Diminta memasukan password ***Dikosongi saja***
7. Buat Database Wordpress dengan nama username masing - masing, contoh `pwcahyo`.
```
CREATE DATABASE wordpress_pwcahyo
```
8. Kemudian akses `localhost/pwcahyo` isikan :
- Database : `wordpress_pwcahyo`
- Username for database : `root`
- Password for database : ``
- Host : `localhost`
- Table setting : `wp_`
Atau
Copy `wp-config-sample.php` menjadi `wp-config.php` kemudian edit file tersebut `nano /opt/lampp/htdocs/cahyo/wp-config.php` menjadi
```
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress_cahyo');

/** MySQL database username */
define('DB_USER', 'root');

/** MySQL database password */
define('DB_PASSWORD', '');

/** MySQL hostname */
define('DB_HOST', 'localhost');
```
9. Kemudian akses kembali `localhost/pwcahyo`.
- Masukan Username wordpress
- Masukan Password
- Konfirmasi Password
- Masukan Nama Website

10. Untuk masuk kedalam administrator `wordpress` ketik `localhost/pwcahyo/wp-admin` kemudian masukan `Username` dan `Password`
11. Untuk Melihat hasil `Website` ketikan `localhost/pwcahyo` pada address bar web browser.
