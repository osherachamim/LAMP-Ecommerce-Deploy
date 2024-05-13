# LAMP-Ecommerce-Deploy
This repository serves as a comprehensive guide and toolkit for deploying e-commerce applications using the LAMP stack (Linux, Apache, MySQL, PHP). Whether you're a beginner exploring the fundamentals of e-commerce development or an experienced developer looking for deployment strategies, this repository has you covered.

This is a sample e-commerce application built for learning purposes.
Here's how to deploy it on CentOS systems:

# Deploy Pre-Requisites:
1. Install FirewallD

 ```bash
sudo yum install -y firewalld
sudo systemctl start firewalld
sudo systemctl enable firewalld
sudo systemctl status firewalld
```  

# Deploy and Configure Database
1. Install MariaDB

```bash
sudo yum install -y mariadb-server
sudo vi /etc/my.cnf
sudo systemctl start mariadb
sudo systemctl enable mariadb
``` 
2. Configure firewall for Database


```bash
sudo firewall-cmd --permanent --zone=public --add-port=3306/tcp
sudo firewall-cmd --reload
```
3. Configure Database

```bash
$ mysql
MariaDB > CREATE DATABASE ecomdb;
MariaDB > CREATE USER 'ecomuser'@'localhost' IDENTIFIED BY '4g4WJRvqduZ0XMkP168YhFbq';
MariaDB > GRANT ALL PRIVILEGES ON *.* TO 'ecomuser'@'localhost';
MariaDB > FLUSH PRIVILEGES;
```
4. Load Product Inventory Information to database

Create the db-loadcng-script.sql


## License

[MIT](https://choosealicense.com/licenses/mit/)
