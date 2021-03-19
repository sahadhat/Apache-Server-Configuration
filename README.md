# Apache-Server-Configuration
Install Apache
---------------------------------------------------------
sudo apt update && sudo apt install apache2

Configure Firewall

sudo ufw allow OpenSSH


sudo ufw allow in "Apache Full"


sudo ufw enable


sudo ufw status


Host Multiple Website on Droplets/Cloud Server/Any Ubuntu Linux
---------------------------------------------------------
:::Apache Configurations:::Ubuntu 20.04 LTS :::

Note : Change example.com with your own domain name.
------------------------------------------------------------------
mkdir -p /var/www/html/example.com/public_html

chown -R $USER:$USER /var/www/html/example.com/public_html

chmod -R 755 /var/www/html

sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sitesavailable/example.com.conf

nano /etc/apache2/sites-available/example.com.conf


<VirtualHost *:80>
ServerAdmin root@example.com
ServerName example.com
ServerAlias www.example.com
DocumentRoot /var/www/html/example.com/public_html
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

<Code>
	<VirtualHost *:80>
ServerAdmin root@example.com
ServerName example.com
ServerAlias www.example.com
DocumentRoot /var/www/html/example.com/public_html
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

</Code>

sudo a2ensite example.com.conf

systemctl restart apache2

a2dissite 000-default.conf

service apache2 restart

 

#Renew SSL Useful Commands
---------------------------------------------------------
sudo apt-get update


sudo apachectl stop

Without WWW

certbot renew --cert-name example.com 

With WWW

certbot renew --cert-name www.example.com 


sudo service apache2 start


service apache2 restart



#Create Subdomain
---------------------------------------------------------
sudo apt-get update

sudo mkdir -p /var/www/hi.example.com/public_html

sudo chown -R $USER:$USER /var/www/hi.example.com/public_html

sudo chmod -R 755 /var/www


sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/hi.example.com.conf


sudo nano /etc/apache2/sites-available/hi.example.com.conf


<VirtualHost *:80>
        ServerAdmin info@example.com
        ServerName hi.example.com
        DocumentRoot /var/www/hi.example.com/public_html
           <Directory /var/www/hi.example.com/public_html/>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>


```
<VirtualHost *:80>
        ServerAdmin info@example.com
        ServerName hi.example.com
        DocumentRoot /var/www/hi.example.com/public_html
           <Directory /var/www/hi.example.com/public_html/>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

```


sudo a2ensite hi.example.com.conf


sudo service apache2 restart



#Install ZIP/Unzip
---------------------------------------------------------
apt-get update


apt-get install zip unzip

#Enable .htaacess
---------------------------------------------------------
sudo apt-get update


sudo a2enmod rewrite


systemctl restart apache2


sudo nano /etc/apache2/sites-enabled/000-default.conf


<Directory "/var/www/html">
  AllowOverride All
</Directory>

#Configure Apache File
---------------------------------------------------------
sudo nano /etc/apache2/apache2.conf


<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
 </Directory>


 <Directory /var/www/html>
    Options -Indexes
 </Directory>


 ServerSignature Off
 ServerTokens Prod

#install SSL Certificate
---------------------------------------------------------
sudo apt update && sudo apt install certbot python3-certbot-apache


sudo certbot --apache


service apache2 restart

Permissions

sudo chown -R www-data:www-data /var/www

