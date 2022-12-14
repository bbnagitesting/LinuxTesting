# LAMP setup and understanding:
My goal here is not to create a tutorial by which you copy and paste to get things done.
 I want to help you to understand exactly what you are doing and why.

## 0.0 set up a Linux machine or VM
In this example we will use the CentOS7 distribution of Linux and we will run it on a VM.
Open CentOS7 in VMware

## 1.0 install and set up Apache (HTTP server)
```
sudo yum install httpd
sudo systemctl start httpd.service 		//starts Apache server
sudo systemctl enable httpd.service 	//	configures Apache server to launch on startup
```
## 1.1 install and set up MySQL (your database)
```
sudo yum install -y mariadb-server
sudo systemctl start mariadb
sudo systemctl enable mariadb
```
# 1.2 configure MySQL
**NOTE: you should say yes to everything if you don't know exactly what you're doing. You will have to create a non-root account in your MySQL distribution if you want to access phpMyAdmin if you do this.**
```
sudo mysql_secure_installation
sudo mysql
mysql -u root -p
```
Then enter password to get into mariadb to make sure it works. exit

## 1.3 install and enable PHP
```
sudo yum install -y php php-mysql
sudo systemctl restart httpd.service
vi /var/www/html/info.php // add '<?php ?>' to make the file a php file
```
## 1.4 install and enable phpMyAdmin (web-based db administration system)

```
mysql -u [example_user] -p #enter password, make sure it works. exit
sudo yum install -y epel-release
sudo yum install -y phpmyadmin
vim /etc/httpd/conf.d/phpMyAdmin.conf
```
change the IP addresses from 127.0.0.1 to your computer's IP address (ipv4 from the `ipconfig` command in the CMD) to allow your computer to access

## 1.5 restart apache & MySQL
```sudo systemctl restart httpd
sudo systemctl restart mariadb.service
```

Now you should be able to log into `[your CentOS VM ip]/phpMyAdmin` with your `mariadb` credentials.


# Afterwords:
- Create an account in your database. This will be necessary if you disallow remote logins for the root user, which is a good idea for security purposes.
# After logging into your MariaDB root user `(mysql -u root -p)`
-`CREATE USER [username] IDENTIFIED BY [password];`
You should now be able to log in to phpMyAdmin using your [username] and [password]
