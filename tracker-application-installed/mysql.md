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

## create user and privilages in MySQL

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Bellita@123';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
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
