## Install MySQL Client and Import Database into AWS RDS
## 1. Purpose
```
This document describes the procedure to install the MySQL client on a Linux server and import an existing MySQL database into an AWS RDS MySQL instance.
```
## 2. Prerequisites
```
Linux server with sudo access (Ubuntu/Debian)
Network connectivity to AWS RDS (Security Group allows port 3306)
RDS endpoint, username, and password
MySQL database backup file (.sql)
```

## Install MySQL Client
```
 sudo apt update
sudo apt install -y mysql-client
```

## Verify installation:
```
mysql --version
```

## Connect to AWS RDS MySQL Instance
```
mysql -h db-1-instance-1.cc9kkacauxks.us-east-1.rds.amazonaws.com \
      -u admin \
      -p
```

## Enter the RDS password when prompted.

## Verify Database in RDS
```
SHOW DATABASES;
```

## Create Application Database (If Not Exists)
```
CREATE DATABASE tracker_v2;
```

## verified database in mysql
```
show databases;
```

## Exit:
```
exit
```

## Transfer Database Backup File to EC2 Instance
```
/home/ubuntu/tracker_v2.sql
```

## Import the database:
```
mysql -h db-1-instance-1.cc9kkacauxks.us-east-1.rds.amazonaws.com \
     -u admin \
     -p \
     tracker_v2 < ./tracker_v2.sql
```

## Enter the RDS password when prompted.

## Verify Imported Database
```
mysql -h db-1-instance-1.cc9kkacauxks.us-east-1.rds.amazonaws.com \
      -u admin \
      -p
```

## Enter the RDS password when prompted.


## check and verficied database
```
show databases;
```

## Check database and tables:
```
USE tracker_v2;
SHOW TABLES;
```

## exit
```
exit
```
