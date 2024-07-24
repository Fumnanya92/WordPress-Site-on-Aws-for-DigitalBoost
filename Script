# Steps to Set Up a Web Server with EFS, Apache, PHP, MySQL, and WordPress

## 1. Create the HTML Directory and Mount the EFS to It
```bash
sudo su
yum update -y

sudo dnf install nfs-utils -y
mkdir -p /var/www/html
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-03c9b3354880b36a6.efs.us-east-1.amazonaws.com:/ /var/www/html
```

## 2. Install Apache
```bash
sudo yum install -y httpd httpd-tools mod_ssl
sudo systemctl enable httpd 
sudo systemctl start httpd
```

## 3. Install PHP 7.4
```bash
sudo amazon-linux-extras enable php7.4
sudo yum clean metadata
sudo yum install php php-common php-pear -y
sudo yum install php-{cgi,curl,mbstring,gd,mysqlnd,gettext,json,xml,fpm,intl,zip} -y
```

## 4. Install MySQL 5.7
```bash
sudo rpm -Uvh https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
sudo yum install mysql-community-server -y
sudo systemctl enable mysqld
sudo systemctl start mysqld
```

## 5. Set Permissions
```bash
sudo usermod -a -G apache ec2-user
sudo chown -R ec2-user:apache /var/www
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
sudo find /var/www -type f -exec sudo chmod 0664 {} \;
chown apache:apache -R /var/www/html 
```

## 6. Download WordPress Files
```bash
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
cp -r wordpress/* /var/www/html/
```

## 7. Create the `wp-config.php` File
```bash
cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
```

## 8. Edit the `wp-config.php` File
```bash
nano /var/www/html/wp-config.php
```

## 9. Restart the Web Server
```bash
service httpd restart
```
```
