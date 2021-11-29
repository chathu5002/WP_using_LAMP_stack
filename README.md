# Install WordPress on Ubuntu using LAMP stack

## Step 1: Install Apache Web Server on Ubuntu

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install apache2 apache2-utils 
```

#### Enable Apache2 web server to start at system boot time.

```
sudo systemctl enable apache2
sudo systemctl start apache2
sudo systemctl status apache2
```
#### Allow HTTP traffic on UFW firewall

```
sudo ufw allow in "Apache"
sudo ufw status
```


## Step 2: Install MySQL Database Server

`sudo apt-get install mysql-client mysql-server`

##### Optional: Install MariaDB

`sudo apt-get install mariadb-server mariadb-client`

##### Optional: (Recommended) Run a security script to remove insecure default settings and protect the database system.

`sudo mysql_secure_installation`
###### Firstly, you will be asked to install the ‘validate_password’ plugin, so type in Y/Yes and press Enter and also choose the default password strength level.


