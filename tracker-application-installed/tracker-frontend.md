## Tracker Frontend (Vite / React) – Installation & Deployment Guide:
## Project Overview
```
This document provides step-by-step instructions to install, build, and deploy the **Tracker Frontend** application on **Ubuntu Linux** using **Node.js, PNPM, and Apache**.
```
## Project Directory Setup
```
 cd /var/www/html
```

## Clone Frontend Repository
```
sudo git clone https://github.com/SQ1Security/tracker-frontend.git
```

## Install Build Essentials
```
sudo apt update
sudo apt install -y build-essential
```
## Install NVM (Node Version Manager)

## Install NVM (Official Script)
```
sudo curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

## Load NVM into the current shell
```
source ~/.bashrc
```

## Verify NVM installation
```
nvm -v
```
## Install Node.js Using NVM

## Install latest LTS version
```
nvm install --lts
```

## List installed Node versions
```
nvm ls
```

## Use required Node.js version
```
nvm use 24.12.0
```

## Verify Node.js version
```
node -v
```

## Set Ownership & Permissions
```
sudo chown -R ubuntu:ubuntu /var/www/html/tracker-frontend
```

## Apply safe permissions
```
sudo find /var/www/html/tracker-frontend -type d -exec chmod 755 {} \;
sudo find /var/www/html/tracker-frontend -type f -exec chmod 644 {} \;
```
## Install PNPM & Dependencies

## Navigate to project directory
```
cd /var/www/html/tracker-frontend
```

## Install PNPM globally (without sudo)
```
npm install -g pnpm
```

## Verify PNPM version
```
pnpm -v
```

## Install project dependencies
```
 pnpm install
```
## Environment Configuration

## create .env file

```
VITE_APP_BACKEND_BASE_URL=http://beta.bellita.co.in:8082/api/
VITE_APP_BACKEND_FILES_URL=http://beta.bellita.co.in:8082/evidences/
VITE_APP_TAB_TITLE=Pro 1
VITE_APP_SECRET_KEY=541f8551773b2f6a7cd5434d9fb51ad9bbb1cca3be49df30bea6bd08a0d54729
GENERATE_SOURCEMAP=false
VITE_APP_CLIENTR=1
# VITE_APP_ANTHEM_ELEVANCE_A1=11
# VITE_APP_ANTHEM_ELEVANCE_A2=12
VITE_APP_ANTHEM_ELEVANCE=14
VITE_APP_HUMANA=13
VITE_APP_LIBERTY=18
VITE_APP_PROMINENCE=17
VITE_APP_HUMANA_WAVE_2=16

```
## Build Frontend Application
```
pnpm run build
```

## Apache Virtual Host Configuration

## Create / edit Apache site configuration
```
sudo vi /etc/apache2/sites-available/
```

```
<VirtualHost *:80>

        # The ServerName directive sets the request scheme, hostname and port that

        # the server uses to identify itself. This is used when creating

        # redirection URLs. In the context of virtual hosts, the ServerName

        # specifies what hostname must appear in the request's Host: header to

        # match this virtual host. For the default virtual host (this file) this

        # value is not decisive as it is used as a last resort host regardless.

        # However, you must set it for any further virtual host explicitly.

        ServerName 35.154.125.140

        DocumentRoot /var/www/html/tracker-frontend/dist

        <Directory "/var/www/html/tracker-frontend/dist">

        AllowOverride All
        Require all granted

        # React routing fix
        RewriteEngine On
        RewriteBase /
        RewriteRule ^index\.html$ - [L]
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteCond %{REQUEST_FILENAME} !-d
        RewriteRule . /index.html [L]

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

## Enable Apache Modules & Site

## Enable rewrite module
```
sudo a2enmod rewrite
```
## Restart Apache
```
sudo systemctl restart apache2
sudo systemctl reload  apache2
```

## Enable site
```
sudo a2ensite 000-default.conf
```

## Restart Apache
```
sudo systemctl reload apache2
```

## if you want disable configure
```
sudo a2dissite 000-default.conf
```

## restart services
```
sudo systemctl restart apache2
sudo systemctl reload  apache2
```

## Copy .htaccess to Build Directory
```
sudo cp .htaccess dist
```


