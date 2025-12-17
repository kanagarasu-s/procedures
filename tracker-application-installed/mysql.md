## MySQL Database Installation & Adminer Configuration Guide
## Overview
```
This document describes the step-by-step procedure to install and configure **MySQL Server** and **Adminer** on an **Ubuntu Linux server** for application database management.
```

## Install MySQL Server

```
sudo apt install mysql-server -y

```
## Verify MySQL Installation
```
mysql --version
```

## Login to MySQL (Root User)

```
sudo mysql
```

## Configure MySQL Root Authentication

```
ALTER USER 'root'@'localhost'
IDENTIFIED WITH mysql_native_password
BY 'Bellita@123';

```
## Apply Changes & Exit
```
FLUSH PRIVILEGES;
EXIT;
```

## Verify MySQL Login Using Password
```
mysql -u root -p
```

## Enter password:
```
Bellita@123
```

## Install Adminer
```
sudo apt install adminer -y
```

## Enable Adminer Apache Configuration
```
sudo a2enconf adminer
```

## Restart Apache Service
```
sudo systemctl restart apache2
```

## Access Adminer Web Interface
```
http://your-server-ip/adminer
```
## Adminer User Verification
```
Login → Select database → Users → Select user
→ Edit → Change username to dev.u6@pro1hs.com → Save
```
