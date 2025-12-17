## Tracker Backend (Laravel) – Installation & Configuration Guide
## Project Overview
```
This document describes the step-by-step procedure to install and configure the **Tracker Backend (Laravel)** application on **Ubuntu 22.04 / 24.04** using **Apache, PHP 8.3, MySQL, and Composer**.
```
## Project Directory Setup

## Create project directory
```
sudo mkdir -p /var/www/html
cd /var/www/html
```

## Clone Backend Repository
```
sudo git clone https://github.com/SQ1Security/tracker-backend-v2.git
```
## Apache Web Server Installation
## Install Apache
```
sudo apt install apache2 -y
```

## Start and check Apache status
```
sudo systemctl start apache2
sudo systemctl status apache2
```
## PHP 8.3 Installation (Ubuntu 22.04 / 24.04)
## Update system
```
sudo apt update -y
```

## Install required dependencies
```
sudo apt install software-properties-common ca-certificates lsb-release apt-transport-https -y
```

## Install PHP 8.3
```
sudo apt install php8.3 -y
```

## Install PHP extensions
```
sudo apt install php8.3-cli php8.3-common php8.3-fpm php8.3-mbstring php8.3-xml php8.3-mysql php8.3-curl php8.3-zip php8.3-gd php8.3-intl php8.3-opcache -y
```

## Verify PHP version
```
php -v
```

## Install and verify GD extension
```
sudo apt update
sudo apt install php8.3-gd -y
```

## Restart Apache
```
sudo systemctl restart apache2
```

## Verify GD installation
```
php -m | grep gd
```
## Composer Installation

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

## Remove installer
```
sudo php -r "unlink('composer-setup.php');"
```

## Verify Composer version
```
sudo composer -V
```
## MySQL Database Setup

## Install MySQL by following the below document:
```
https://github.com/kanagarasu-s/procedures/blob/main/tracker-application-installed/mysql.md
```
## Application Environment Configuration

## Navigate to project directory
```
sudo cd /var/www/html/tracker-backend-v2
```

## create .env file
```
sudo nano .env
```

## .env configuration tracker-backend
```
APP_NAME=tracker_v2
APP_ENV=local
APP_KEY=base64:slEBN4G6sBegipVOnjpecTfyLC/FM41DMjybWpGx9D4=
APP_DEBUG=true
APP_TIMEZONE=Asia/Kolkata
APP_URL=http://localhost

APP_LOCALE=en
APP_FALLBACK_LOCALE=en
APP_FAKER_LOCALE=en_US

APP_MAINTENANCE_DRIVER=file
# APP_MAINTENANCE_STORE=database

PHP_CLI_SERVER_WORKERS=4

BCRYPT_ROUNDS=12

LOG_CHANNEL=daily
LOG_STACK=single
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=localhost
DB_PORT=3306
DB_DATABASE=tracker_v2
DB_USERNAME=root
DB_PASSWORD=Bellita@123

DB_TIMEZONE=+05:30

SESSION_DRIVER=database
SESSION_LIFETIME=120
SESSION_ENCRYPT=false
SESSION_PATH=/
SESSION_DOMAIN=null

BROADCAST_CONNECTION=log
FILESYSTEM_DISK=local
QUEUE_CONNECTION=database

CACHE_STORE=file
CACHE_PREFIX=

MEMCACHED_HOST=127.0.0.1

REDIS_CLIENT=phpredis
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=smtp.zoho.in
MAIL_PORT=465
MAIL_ENCRYPTION=ssl
MAIL_USERNAME=dev.u6@pro1hs.com
MAIL_PASSWORD=PiXm0zCMAns7
MAIL_FROM_ADDRESS=dev.u6@pro1hs.com
MAIL_FROM_NAME=TrackerV2
TO_MAIL_ID=haripriya.s@sq1.security
CC_MAIL_ID=dev.u3@pro1hs.com

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

VITE_APP_NAME="${APP_NAME}"

AUTH_GUARD=api
AUTH_PASSWORD_BROKER=users
AUTH_MODEL=App\Models\User


ZOHO_CLIENT_ID=1000.5ZGNMB0OK2B4Z4BICSDZIWN5JAWVYM
ZOHO_CLIENT_SECRET=545820e53b42dd8c91115544a8302b1200928bfc7e
# ZOHO_REDIRECT_URI=http://localhost:8085/api/sso/login/zoho/callback
ZOHO_REDIRECT_URI=http://beta.bellita.co.in/sso/zoho

# ZOHO_REDIRECT_URI=http://192.168.6.8:8084/sso/zoho

# ZOHO_REDIRECT_URI_LOCAL=http://localhost:3000/sso/zoho
# ZOHO_REDIRECT_URI_REMOTE=http://192.168.6.8:8082/sso/zoho
# ZOHO_REDIRECT_URI_DEFAULT=http://localhost:3000/sso/zoho

AZURE_CLIENT_ID=719afa80-05eb-4131-a59e-d0544b37b751
AZURE_CLIENT_SECRET=EzS8Q~uqlyxWrsNQGg~U5k_E5LkPTmY0_pebsb_a
AZURE_REDIRECT_URI=http://localhost:8085/api/sso/login/azure/callback
AZURE_TENANT_ID=99305083-0700-45c6-8ab2-19cb66e5502c


PAGINATION_PER_PAGE=10
PAGINATION_MAX_PER_PAGE=25


# BROADCAST_DRIVER=pusher
# PUSHER_APP_ID=1918977
# PUSHER_APP_KEY=b335961e01c26e3d08ae
# PUSHER_APP_SECRET=1e2b7d49dec28889555d
# PUSHER_APP_CLUSTER=ap2

BROADCAST_DRIVER=pusher
PUSHER_APP_ID=1957164
PUSHER_APP_KEY=5fd42fbed1112ea74705
PUSHER_APP_SECRET=415ef96a6a0a2df2815a
PUSHER_APP_CLUSTER=ap2
PUSHER_HOST=null
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_ENCRYPTED=true

AWS_ACCESS_KEY_ID=AKIAXBNXN4DOSQGPWPPP
AWS_SECRET_ACCESS_KEY=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
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

SESSION_SECURE_COOKIE = false

CHART_STATISTICS_START_TIME= 07
PRODUCTION_START_TIME=07:00:00
PRODUCTION_END_TIME=06:00:00

OSCAR_PROJECT=0
LHP_PROJECT=0
AETNA_PROJECT=0
CLIENT_R_PROJECT=1
ANTHEM_ELEVANCE_PROJECT=11
ANTHEM_ELEVANCE_A2_PROJECT=12
HUMANA_PROJECT=13
HUMANA_WAVE2_PROJECT=16
PROMINENCE_PROJECT=17
LIBERTY_PROJECT=18

FRONTEND_URL=http://beta.bellita.co.in/

CACHE_DURATION=1
CACHE_STORE=file

```

## Dependency Installation

## Install PHP dependencies
```
sudo composer update
```

## Laravel Application Setup

## Clear cache
```
sudo php artisan optimize:clear
```

## Generate Passport keys
```
sudo php artisan passport:keys
```

## Run migrations
```
sudo php artisan migrate
```

## Fresh migration with seed
```
sudo php artisan migrate:fresh --seed
```

## Create Passport personal access client
```
sudo php artisan passport:client --personal
```

## enter 
```
authTOKEN
```
## Apache Virtual Host Configuration

## Create virtual host file
```
sudo vi /etc/apache2/sites-available/tracker-backend.conf
```

```
<VirtualHost *:8082>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost

        DocumentRoot /var/www/html/tracker-backend-v2/public

        <Directory "/var/www/html/tracker-backend-v2/public">

        AllowOverride All
        Order allow,deny
        allow from all
        </Directory>

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>


```
## go to project directory
```
cd /var/www/html/tracker-backend-v2
```

## Enable Site & Configure Port
```
sudo a2ensite tracker-backend.conf
sudo systemctl reload apache2
```

## Configure Apache to listen on port 8082
```
sudo nano /etc/apache2/ports.conf
```
## Add:
```
Listen 8082
```
## Reload Apache:
```
sudo systemctl reload apache2
```
## CORS Configuration
## Create CORS config file
```
cd /var/www/html/tracker-backend-v2/config
sudo nano cors.php
```
```
<?php
 
return [
 
    /*
    |--------------------------------------------------------------------------
    | Cross-Origin Resource Sharing (CORS) Configuration
    |--------------------------------------------------------------------------
    |
    | Here you may configure your settings for cross-origin resource sharing
    | or "CORS". This determines what cross-origin operations may execute
    | in web browsers. You are free to adjust these settings as needed.
    |
    | To learn more: https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
    |
    */
 
    'paths' => ['api/*', 'sanctum/csrf-cookie'],
 
    'allowed_methods' => ['*'],
 
    'allowed_origins' => ['*'],
 
    'allowed_origins_patterns' => [],
 
    'allowed_headers' => ['*'],
 
    'exposed_headers' => [],
 
    'max_age' => 0,
 
    'supports_credentials' => true,
 
];
```

## File Permissions
```
sudo chmod -R 777 .
```
## Apache Troubleshooting Commands

## Disable site
```
sudo a2dissite tracker-backend.conf
```

## Reload Apache
```
sudo systemctl reload apache2
```

## Enable site
```
sudo a2ensite tracker-backend.conf
```

## Reload Apache
```
sudo systemctl reload apache2
```
