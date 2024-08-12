## Install httpd server on both EC2 Instances (Web & App Server)

sudo yum install -y httpd

sudo systemctl start httpd

sudo systemctl enable httpd

sudo systemctl is-enabled httpd

sudo usermod -aG apache ec2-user

exit & re-login

groups -- To verify your membership in the apache group

sudo chown -R ec2-user:apache /var/www -- Change the group ownership of /var/www and its contents to the apache group.

sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \; -- To add group write permissions and to set the group ID on future subdirectories, change the directory permissions of /var/www and its subdirectories.

find /var/www -type f -exec sudo chmod 0664 {} \; -- To add group write permissions, recursively change the file permissions of /var/www and its subdirectories.

Add below proxy in /etc/httpd/conf/httpd.conf file
    
    <VirtualHost *:80>

        ProxyRequests Off
        ProxyPass /phpMyAdmin http://172.20.3.233/phpMyAdmin/
        ProxyPassReverse /phpMyAdmin http://172.20.3.233/phpMyAdmin/

        <Proxy *>
            Order deny,allow
            Allow from all
        </Proxy>
    </VirtualHost>

======= Install phpMyAdmin on App Server

sudo yum install php-mbstring php-xml php php-mysqlnd -y

sudo systemctl restart httpd

sudo systemctl restart php-fpm

cd /var/www/html

wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz

mkdir phpMyAdmin && tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin --strip-components 1

rm phpMyAdmin-latest-all-languages.tar.gz

modify the config.sample.inc.php to config.inc.php and update the RDS MySQL endpoint ($cfg['Servers'][$i]['host'] = 'sample-endpoint.rds.amazonaws.com'
