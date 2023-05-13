# Fast apache and MySQL setup
<details>
<summary> Debian/ubuntu based server </summary>
  
1. Update the system <br>
 1.1. ```# apt update && apt upgrade -y; apt-get update && apt-get upgrade -y; apt autoremove -y;``` <br>
2. Install ```apache2``` and ```mysql-server``` <br>
 2.1. ```# apt-get install apache2 mysql-server``` <br>
 2.2 ```# systemctl enable apache2; systemctl restart apache2``` <br>
 > By default you will serve the content in ```/var/www/html/``` <br>
 > **Apache security and configuration files** <br>
 > > 🔐 ```/etc/apache2/conf-enabled/security.conf```  <br>
 > >⚙️ ```/etc/apache2/sites-available/000-default.conf```  or ```/etc/apache2/sites-available/default.conf``` <br>
 > > ⚙️ ```/etc/apache2/apache2.conf``` <br>
 > > - You can use ```# apache2ctl configtest``` to check and test the config before ```systemctl restart apache2``` and apply changes.  <br>
 >> - At this point your able to see ```http:///localhost``` or ```http://192.168.*.* (check it in the server with "ip a | grep inet")```  or ```http://example.example```. **If you have issues... try ```# ufw allow http``` ** <br>

3. Enable and config **CGI** [OPTIONAL] <br>
	3.1. ```# a2enmod cgi``` <br>
	3.2. ```# nano /etc/apache2/sites-available/000-default.conf``` or  ```# nano/etc/apache2/sites-available/default.conf``` <br>
	> Put the following code inside ```<VirtualHost>{here}</VirtualHost>``` <br>
	``` 
	<Directory /var/www/html>
		Options +ExecCGI
		AddHanddler cgi-script.sh
		DirectoryIndex index.sh # you can put more filenames and extensions eg. index.html index.php
	</Directory>
	```
4. MySQL setup and usage<br> 
	4.1. Login as root ```# mysql -u root -p```<br>
	4.2. Create a new user ``` CREATE USER 'username'@'localhost' IDENTIFIED BY 'password'; ```<br>
	4.3. Re-log as that user with ```$/# mysql -u username -ppassword```<br>
	4.4. Create a DataBase and a Table ```CREATE DATABASE mydb;``` move into it ```USE mydb;``` create table ```CREATE TABLE mytable(name VARCHAR(100));```<br>
	4.5. Test it! ```INSERT INTO mytable(name) VALUES ('0utl4nder');``` then ``` SELECT * FROM mytable;```  Inspect it ```DESCRIBE mytable;```<br>
5. Start code!<br>
	5.1. ```# touch /var/www/html/index.sh && chmod +x /var/www/html/index.sh```<br>
	> If you will print html remember to add the content type or you will face an Internal Server Error (500), for example.<br>
	```
	#!/bin/bash
	function somethingCool {
	echo "Follow me at <a href="https://github.com/0utl4nder" target="_blank"> Github </a>"
	}
	
	echo "Content-type: text/html"
	echo ""
	somethingCool
	```
</details>
