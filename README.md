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

```bash
cat > db-load-script.sql <<-EOF
USE ecomdb;
CREATE TABLE products (id mediumint(8) unsigned NOT NULL auto_increment,Name varchar(255) default NULL,ImageUrl varchar(255) default NULL,PRIMARY KEY (id)) AUTO_INCREMENT=1;

INSERT INTO products (Name,ImageUrl) VALUES ("Iphone8","iphone-8.jpg"),("Iphone10","iphone-10.jpg"),("Iphone11","iphone-11.jpg"),("Iphone12","iphone-12.jpg"),("Iphone13","iphone-13.jpg"),("Main","banner-image.png"),("Pink_Watch","cart-item2.jpg"),("HeavyWatch","insta-item2.jpg"),("Postedwatch","product-item8.jpg"),("Black_watch","product-item9.jpg"),("Black_watch","product-item10.jpg");

EOF
```
Run sql script

```bash
sudo mysql < db-load-script.sql
```

# Deploy and Configure Web
1. Install required packages

```bash
sudo yum install -y httpd php php-mysqlnd
sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
sudo firewall-cmd --reload
```

2. Configure httpd
   Change **DirectoryIndex index.html** to **DirectoryIndex index.php** to make the php page the default page
   
```bash
sudo sed -i 's/index.html/index.php/g' /etc/httpd/conf/httpd.conf
```

3. Start httpd

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

4. Download code

 ```bash
sudo yum install -y git
sudo git clone https://github.com/kodekloudhub/learning-app-ecommerce.git /var/www/html/
```

## License

[MIT](https://choosealicense.com/licenses/mit/)
