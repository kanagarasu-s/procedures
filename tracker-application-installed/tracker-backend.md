## tracker_backend:
## tracker project location

```
 cd /var/www/html

```

## clone git repo

```
git clone https://github.com/SQ1Security/tracker-backend-v2.git

```
## create .env file tracker backend



## php install

```
Install PHP 8.3

```
## Install common extensions

```
sudo apt install php8.3-cli php8.3-common php8.3-fpm php8.3-mbstring php8.3-xml php8.3-mysql php8.3-curl php8.3-zip php8.3-gd php8.3-intl php8.3-opcache -y

```
## Check version

```
php -v

```
## Install GD for PHP 8.3

```
sudo apt update
sudo apt install php8.3-gd -y

```
## using Apache

```
sudo systemctl restart apache2

```
## Verify GD installation

```
php -m | grep gd

```

## Download Composer installer

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

```
## Verify installer (recommended)

```
php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('https://composer.github.io/installer.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

```

## Install Composer globally

```
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

```
## Remove installer file

```
php -r "unlink('composer-setup.php');"

```
## Check Composer Version

```
composer -V

```

## inside the project after load env file then ran "composer update" command

```
composer update

```

## env file database user name password

```
DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=tracker_v2
DB_USERNAME=root
DB_PASSWORD=Bellita@123

```

## clears all cached data used by Laravel.

```
php artisan optimize:clear

```

## generates the encryption keys that Laravel Passport

```
php artisan passport:keys

```

## all migrations from scratch

```
php artisan migrate:fresh --seed

```

## creates a personal access client

```

php artisan passport:client --personal

```


## backend configure file

```
nano tracker-backend.conf

```
```
<VirtualHost *:8085>
    ServerName example.com
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/tracker-backend-v2/public

    <Directory /var/www/html/tracker-backend-v2/public>
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/tracker-backend-error.log
    CustomLog ${APACHE_LOG_DIR}/tracker-backend-access.log combined
</VirtualHost>

```
## Enable the site

```
sudo a2ensite tracker-backend.conf

```
## apache service reload

```
sudo systemctl reload apache2

```
## Make Apache listen on port 8085

```
sudo nano /etc/apache2/ports.conf

```
## Add this line

```
Listen 8085

```
## this directory primission /tracker-backend-v2

```
sudo chmod -R 777 storage/

```
