## mysql client install and import database in aws rds service

## install mysql client
```
 sudo apt install -y mysql-client
```
## login mysql
```
mysql -u root -p
```
## enter mysql login password
```
mysql password
```
## create database application db
```
CREATE DATABASE tracker_v2;
```
## verified database in mysql
```
show databases;
```
```
exit
```
## check connect in AWS RDS 
```
mysql -h db-1-instance-1.cc9kkacauxks.us-east-1.rds.amazonaws.com -u admin -p
```
## enter password
```
password
```
## you already export mysql database backup to import this command
```
mysql -h db-1-instance-1.cc9kkacauxks.us-east-1.rds.amazonaws.com \
     -u admin \
     -p \
     tracker_v2 < ./tracker_v2.sql
```
## enter password
```
rds password
```
## check and verficied database
```
show databases;
```
## that database use
```
use tracker_v2
```
## verified database inside tables
```
show tables;
```
## exit
```
exit
```
