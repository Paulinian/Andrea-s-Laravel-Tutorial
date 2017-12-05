# Andrea-s-Laravel-Tutorial

--- INSTALLING LARAVEL ---
Step 1:Update your system first
yum -y update

yum -y install epel-release
yum -y update
yum clean all

Step 2: Install mariadb
yum -y install httpd mariadb-server mariadb
(Laravel does not supports PHP versions lower than 5.6.4)
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
yum -y update
yum clean all
(Now you can install either PHP 5.6 or PHP 7.0 in your system)
yum -y install php56w php56w-mysql php56w-mcrypt php56w-dom php56w-mbstring

yum -y install php70w php70w-mysql php70w-mcrypt php70w-dom php70w-mbstring (Php 7)
(Now check the version of your php by typing this command)
php -v
(Now start your httpd and mariadb) 
systemctl start httpd
systemctl start mariadb
(Now enable your httpd and mariadb)
systemctl enable httpd
systemctl enable httpd
(Now secure your mariadb installation)
mysql_secure_installation

[root@ip-172-31-28-226 ~]# mysql_secure_installationNOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
          SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!In order to log into MariaDB to secure it, we'll need the current
    password for the root user.  If you've just installed MariaDB, and
    you haven't set the root password yet, the password will be blank,
    so you should just press enter here.Enter current password for root (enter for none):
    OK, successfully used password, moving on...Setting the root password ensures that nobody can log into the MariaDB
    root user without the proper authorisation.Set root password? [Y/n] y
    New password:
    Re-enter new password:
    Password updated successfully!
    Reloading privilege tables..
     ... Success!By default, a MariaDB installation has an anonymous user, allowing anyone
    to log into MariaDB without having to have a user account created for
    them.  This is intended only for testing, and to make the installation
    go a bit smoother.  You should remove them before moving into a
    production environment.Remove anonymous users? [Y/n] y
     ... Success!Normally, root should only be allowed to connect from 'localhost'.  This
    ensures that someone cannot guess at the root password from the network.Disallow root login remotely? [Y/n] y
     ... Success!By default, MariaDB comes with a database named 'test' that anyone can
    access.  This is also intended only for testing, and should be removed
    before moving into a production environment.Remove test database and access to it? [Y/n] y
     - Dropping test database...
     ... Success!
     - Removing privileges on test database...
     ... Success!Reloading the privilege tables will ensure that all changes made so far
    will take effect immediately.Reload privilege tables now? [Y/n] y
     ... Success!Cleaning up...All done!  If you've completed all of the above steps, your MariaDB
    installation should now be secure.
Thanks for using MariaDB!

Step 3: Installing composer
curl -sS https://getcomposer.org/installer | php

Step 4: To make composer available globally 
mv composer.phar /usr/bin/composer
chmod +x /usr/bin/composer
(Now check your composer)
composer -V

Step 5: Now we have everything configured, we can install Laravel
yum -y install git
cd /var/www/
git clone https://github.com/laravel/laravel.git

Step 6: Now navigate to Laravel files directory and use composer to install the dependencies and software
cd /var/www/laravel
composer install

Step 7: Composer will take some time to install the dependencies. After composer finishes the installation, you will have to set the appropriate permissions for Laravel directory, so that it can be owned and managed by Apache.
chown -R apache:apache /var/www/laravel
chmod -R 755 /var/www/laravel

Step 8: Rename .env.example 
cd /var/www/laravel
mv .env.example .env

Step 9:Once you have .env file ready, you can generate the new application key using the following command
php artisan key:generate

Step 10:The above command will generate the random application key as well as it will write the key into environment file .env. You can verify if the key has been set using the following command
nano .env

Step 11:
[root@ip-172-31-28-226 laravel]# cat /var/www/laravel/.env
    APP_ENV=local
    APP_KEY=base64:PllGKlCqZSwTJKGyGacEN8FEJeEt0Jlyx1n8xMea3Iw=
    APP_DEBUG=true
    APP_LOG_LEVEL=debug
    APP_URL=http://localhostDB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE='name of your database'
    DB_USERNAME=root
    DB_PASSWORD=
    
 Step 12:Now create a new Apache virtual host file so that our application can be accessed through the web browser. Edit the /etc/httpd/conf/httpd.conf file using your favorite editor. In this tutorial we will be using nano editor, if you do not have nano installed, you can run yum -y install nano to install nano editor.
 nano /etc/httpd/conf/httpd.conf
 
 Step 13: In order for you to view the Laravel type this commands at the end of the httpd.conf
 <VirtualHost *:80>
       ServerName 'Your ip add"
       DocumentRoot /var/www/laravel/public
       
       <Directory /var/www/laravel>
            AllowOverride All
            Require all granted
      </Directory>
  </VirtualHost>
  
  Step 14: Now restart your httpd
  systemctl restart httpd
  
  Step 15:
  Type your ip add on the browser inorder for you to test it
  
  --- THANK YOU ---
  


