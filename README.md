# Install WordPress on Ubuntu using LAMP stack

## Step 1: Install Apache Web Server on Ubuntu

`sudo apt-get update`  
`sudo apt-get upgrade`  
`sudo apt-get install apache2 apache2-utils` 


#### Enable Apache2 web server to start at system boot time.

`sudo systemctl enable apache2`  
`sudo systemctl start apache2`  
`sudo systemctl status apache2`  

#### Allow HTTP traffic on UFW firewall

`sudo ufw allow in "Apache"`  
`sudo ufw status`


## Step 2: Install MySQL Database Server

`sudo apt-get install mysql-client mysql-server`

##### Optional: Install MariaDB

`sudo apt-get install mariadb-server mariadb-client`

##### Optional: (Recommended) Run a security script to remove insecure default settings and protect the database system.

`sudo mysql_secure_installation`

###### Firstly, you will be asked to install the ‘validate_password’ plugin, so type in Y/Yes and press Enter and also choose the default password strength level.

![alt text](https://github.com/chathu5002/WP_using_LAMP_stack/blob/main/Set-MySQL-Root-Password.png?raw=true)

###### For the remaining questions, press Y and hit the ENTER key at each prompt.

## Step 3: Install PHP and modules in Ubuntu

`sudo apt-get install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip`

#### Restart Apache.

`sudo systemctl restart apache2`

#### Create a info.php file inside /var/www/html to test if php is working in collaboration with the webserver.

`sudo vi /var/www/html/info.php`

#### And paste the code below into the file.

```
<?php 
phpinfo();
?>
```

#### Open web browser and type in the following URL in the address bar.

> http://server_address/info.php


## Step 4: Install WordPress in Ubuntu

#### Download and extract the latest version of the WordPress package.

`wget -c http://wordpress.org/latest.tar.gz`  
`tar -xzvf latest.tar.gz`

#### Move the WordPress files from the extracted folder to the Apache default root directory, /var/www/html/:

`sudo mv wordpress/* /var/www/html/`

#### Set the correct permissions on the website directory, that is give ownership of the WordPress files to the webserver:

`sudo chown -R www-data:www-data /var/www/html/`  
`sudo chmod -R 755 /var/www/html/`

## Step 5: Create WordPress Database

#### Execute the command below and provide the root user password, then hit Enter to move to the mysql shell:

`sudo mysql -u root -p`

```
mysql> CREATE DATABASE wp_myblog;
mysql> CREATE USER 'username'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
mysql> GRANT ALL ON wp_myblog.* TO 'username'@'%';
mysql> FLUSH PRIVILEGES;
mysql> EXIT;
```
#### Rename wp-config-sample.php to wp-config.php inside /var/www/html/ directory. Remove the default Apache index page.

`cd /var/www/html/`  
`sudo mv wp-config-sample.php wp-config.php`  
`sudo rm -rf index.html`


#### Update database information under the MySQL settings section 
![alt text](https://github.com/chathu5002/WP_using_LAMP_stack/blob/main/WordPress-MySQL-Settings.png?raw=true)


## Step 6: Restart the web server and mysql service:

`sudo systemctl restart apache2.service`   
`sudo systemctl restart mysql.service`
