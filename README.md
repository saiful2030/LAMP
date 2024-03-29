# LAMP
## Linux + Apache + MySQL + PHP.

## Features

- [Ubuntu server](https://ubuntu.com/download/server)
- [Apache](https://httpd.apache.org/)
- [Mysql](https://www.mysql.com/)
- [Php](https://www.php.net/)

## Installation

Langkah 1 : Install [Apache](https://httpd.apache.org/)

```sh
sudo su
```
```sh
sudo apt update
```
```sh
sudo apt upgrade -y
```
```sh
sudo apt install apache2 
```
```sh
sudo ufw app list
```
kita juga harus mendaftarkan Apache de firewall
```sh
sudo ufw app info "Apache Full" 
```
Output :
```sh
Profile: Apache Full
Title: Web Server (HTTP,HTTPS)
Description: Apache v2 is the next generation of the omnipresent Apache web
server.

Ports:
80,443/tcp
```
Untuk mengizinkan lalu lintas HTTP dan HTTPS
```sh
sudo ufw allow "Apache Full"
```
Langkah 2 : Install [Mysql](https://www.mysql.com/)

```sh
sudo apt install mysql-server -y
```
```sh
sudo mysql
```
jalankan Query berikut ini
```sh
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'password_kamu_disini';
```
silakan ganti `password_kamu_disini` dengan password yang diinginkan
setelah itu, tekan `ENTER`
```sh
mysql> exit;
```
```sh
sudo mysql_secure_installation
```
```sh
Please set the password for root here.

New password:

Re-enter new password:
```
```sh
Remove anonymous users? (Press y|Y for Yes, any other key for No)
```
silakan ketik `Y` dan `ENTER`
```sh
Disallow root login remotely? (Press y|Y for Yes, any other key for No)
```
silakan ketik `N` dan `ENTER`
```sh
Remove test database and access to it? (Press y|Y for Yes, any other key for No)
```
silakan ketik `Y` dan `ENTER`
```sh
Reload privilege tables now? (Press y|Y for Yes, any other key for No) :
```
silakan ketik `Y` dan `ENTER`
```sh
mysql -u root -p
```
```sh
mysql> exit;
```
Langkah 3 : Install [Php](https://www.php.net/)
```sh
sudo apt update
```
```sh
sudo apt install software-properties-common
```
```sh
sudo add-apt-repository ppa:ondrej/php
```
```sh
sudo apt update
```
```sh
sudo apt install php8.1-fpm -y
```
```sh
php -v
```
Output:
```sh
PHP 8.1.9 (fpm-fcgi) (built: Aug 15 2022 09:40:11)
Copyright (c) The PHP Group
Zend Engine v4.1.9, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.9, Copyright (c), by Zend Technologies
```
intall extensi di PHP
```sh
sudo apt install php8.1-common php8.1-mysql php8.1-xml php8.1-xmlrpc php8.1-curl php8.1-gd php8.1-imagick php8.1-cli php8.1-dev php8.1-imap php8.1-mbstring php8.1-opcache php8.1-soap php8.1-zip php8.1-redis php8.1-intl -y
```
Testing PHP
```sh
sudo nano /etc/nginx/sites-available/default
```
sialkan skrol ke bawah dan cari kode berikut ini
```sh
index index.html index.htm index.nginx-debian.html;
```
kemudian tambahkan `index.php` didalam list tersebut seperti berikut ini
```sh
index index.php index.html index.htm index.nginx-debian.html;
```
hapus tanda `#` dan beberapa kode berikut ini
```sh
#location ~ \.php$ {
#       include snippets/fastcgi-php.conf;
#
#       # With php-fpm (or other unix sockets):
#       fastcgi_pass unix:/run/php/php7.4-fpm.sock;
#       # With php-cgi (or other tcp sockets):
#       fastcgi_pass 127.0.0.1:9000;
#}
```
dan hasilnya seperti berikut ini.
```sh
location ~ \.php$ {
       include snippets/fastcgi-php.conf;
       fastcgi_pass unix:/run/php/php7.4-fpm.sock;
}
```
ubah `fastcgi_pass unix:/run/php/php7.4-fpm.sock;` menjadi seperti berikut
```sh
fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
```
silakan simpan dengan `CTRL`+ `X` kemudian `Y` dan `ENTER`
Restart Nginx
```sh
sudo systemctl restart nginx
```
tambahkan code berikut ini
```sh
<?php

phpinfo();
```
silakan simpan dengan `CTRL`+ `X` kemudian `Y` dan `ENTER`


























