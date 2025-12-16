MySQL db install:
=================

## MySQL installed

```
sudo apt install mysql-server -y

```
## check and verification mysql
```
mysql --version
```

## login MySQL

```
sudo mysql
```

## Change authentication plugin in MySQL

```
ALTER USER 'root'@'localhost'
IDENTIFIED WITH mysql_native_password
BY 'Bellita@123';

```
## Apply changes
```
FLUSH PRIVILEGES;
EXIT;
```

## verify login 
```
mysql -u root -p
```

## mysql password
```
Bellita@123
```

## Install Adminer Using apt
```
sudo apt install adminer -y
```

## Enable the Adminer Apache configuration
```
sudo a2enconf adminer
```

## Restart Apache
```
sudo systemctl restart apache2
```

## Open Adminer in browser
```
http://your-server-ip/adminer
```
## login adminer and check user
```
user --> select data --> edit --> change username dev.u6@pro1hs.com and save
```
