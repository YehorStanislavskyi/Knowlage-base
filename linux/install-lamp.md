---
description: работает на  убунте 18.04, на 19.04 - и далее будут траблы с sql
---

# install lamp

## Install LAMP

### Install utils

```
Install Apache2.4 Web Server
```

```
$ sudo apt update
$ sudo apt install apache2
```

### Add current user to server group "www-data"

```
$ sudo chown -R $USER:www-data /var/www
```

### Install Mysql Server

```
$ sudo apt install mysql-server
$ sudo mysql_secure_installation
```

### Configure root mysql user

```
$ sudo mysql
```

```
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
mysql> FLUSH PRIVILEGES;
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
mysql> exit
```

### Load Time Zones

```
$ mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql -u root -p mysql
```

### Install PHP

```
$ sudo add-apt-repository ppa:ondrej/php
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install php7.3 libapache2-mod-php7.3 php7.3-mysql php7.3-common php7.3-cli php7.3-fpm php7.3-pdo php7.3-mysql php7.3-zip php7.3-gd php7.3-mbstring php7.3-curl php7.3-bcmath php7.3-json php7.3-xml php7.3-xmlrpc php7.3-gd php7.3-imagick php7.3-dev php7.3-imap php7.3-opcache php7.3-soap php7.3-zip php7.3-intl -y
```

### Configure Apache2

```
$ sudo nano /etc/apache2/mods-enabled/dir.conf
```

```
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

**restart Apache2**

```
$ sudo systemctl restart apache2
```

**Check Apache2 status**

```
$ sudo systemctl status apache2
```

### Configure PHP

```
$ sudo nano /etc/php/7.3/apache2/php.ini
```

```
upload_max_filesize = 32M 
post_max_size = 48M 
memory_limit = 256M 
max_execution_time = 600 
max_input_vars = 3000 
max_input_time = 1000
```

**restart Apache2**

```
$ sudo systemctl restart apache2
```

### Test PHP

```
$ nano /var/www/html/info.php
```

```
<?php
  phpinfo();
?>
```

> [http://localhost/info.php](http://localhost/info.php)

```
$ rm /var/www/html/info.php
```

### Install Composer

```
$ sudo apt update
$ cd ~
$ curl -sS https://getcomposer.org/installer -o composer-setup.php
```

**Go to link and**

> [https://composer.github.io/pubkeys.html](https://composer.github.io/pubkeys.html)

**set composer hash: HASH=\<composer hash>**

```
HASH=795f976fe0ebd8b75f26a6dd68f78fd3453ce79f32ecb33e7fd087d39bfeb978342fb73ac986cd4f54edd0dc902601dc
```

```
$ php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
$ sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

### Install NVM

```
$ curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
$ source ~/.profile 
$ source ~/.bashrc
$ nvm ls-remote
```

**Install NodeJS v12**

```
$ nvm install v12.18.4
```

### Install ZendServer (PHP 7.3)

```
$ sudo ./install_zs.sh 7.3
```

**Post install ZendServer (PHP 7.3)**

```
$ echo 'export PATH=$PATH:/usr/local/zend/bin' >> $HOME/.bashrc
$ echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/zend/lib' >> $HOME/.bashrc
```

### Uninstall zendServer

```
$ sudo /usr/local/zend/bin/uninstall.sh
```

### Manually Uninstall zendServer

```
$ sudo apt-get remove `dpkg -l | grep zend | grep ^ii | awk '{print $2}'`
$ sudo apt-get purge `dpkg -l | grep zend | awk '{print $2}'`
```

**Set ZendServer PHP to Alternatives**

```
$ sudo update-alternatives --install /usr/bin/php php /usr/local/zend/php/active/bin/php 1
$ php -i | grep "Loaded Configuration File"
```
