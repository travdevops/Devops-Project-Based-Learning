
# PBL Project -  WEBSTACK (LAMPSTACK) IN AWS!

LAMP (Linux, Apache, MySQL, PHP)

Updating lists of packages in package manager. 

`sudo apt update`

Packages have been installed after the update.

<img width="891" alt="Screenshot 2023-08-10 at 11 51 01 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d73d14f6-6013-4671-960e-2081ac5e6c45">






# INSTALLING APACHE!

`sudo apt install apache2`

Verify that apache2 is running as a Service

`sudo systemctl status apache2`

<img width="760" alt="Screenshot 2023-08-10 at 2 34 42 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/55103e90-9379-4878-a063-2e785419e86f">

Apache2 service is running on the service = apache Web server has been launched in the cloud. 

Verification to access services locally in our shell using the `curl` command

`curl http://localhost:80 or curl http://127.0.0.1:80`

The above command gives the result that apache services is accesible in our local ubuntu shell

<img width="1029" alt="Screenshot 2023-08-10 at 2 39 19 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c60502b9-3b27-41fe-9f1c-948838968869">


Then we test how Apache HTTP server responds to requests from the internet by running my public IP address on a browser to default port 80

http://<Public-IP-Address>:80

The result confirms Apache web server is correctly installed and accessible through the web.

<img width="919" alt="Screenshot 2023-08-10 at 2 40 45 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/caed7aae-4bd8-4b14-87e8-169428956912">











# INSTALLING MYSQL!

`MYSQL` - a  Database Management System (DBMS) to be able to store and manage data for your site.

 
 `MySQL` - is a popular relational database management system used within PHP environments


run this command to install mysql

`sudo apt install mysql-server`

<img width="1078" alt="Screenshot 2023-08-10 at 2 43 43 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d860ca89-5f3d-4350-93a1-3bbee4e26612">

log into mysql server

`sudo mysql`

<img width="672" alt="Screenshot 2023-08-10 at 2 44 44 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/6156e06a-e023-45eb-8341-cd6f7068a717">

configure a database user on and set login password for Mysql

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`

exit mysql shell

`exit`

validate password plugin for mysql

<img width="831" alt="Screenshot 2023-08-10 at 2 49 32 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/70f5b356-643e-4b9d-98e3-7550e16df140">

then we have to login to mysql after password plugin validation with -p flag

`sudo mysql -p`

<img width="769" alt="Screenshot 2023-08-10 at 2 51 09 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/fc8c7c05-984e-415f-9967-6aa4770f2fed">


# INSTALLING PROGRAMMING LANGUAGE (php)


 PHP is the component of our setup that will process code to display dynamic content to the end user.

 In addition to the php package, we need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases.

 We’ll also need libapache2-mod-php to enable Apache to handle PHP files. 

 Core PHP packages will automatically be installed as dependencies.

 To install these 3 packages at once, run:

`sudo apt install php libapache2-mod-php php-mysql`

<img width="1122" alt="Screenshot 2023-08-10 at 2 52 21 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/b885d697-de19-4873-b934-153585132574">

Confirming our php installation and version

`php -v`

<img width="704" alt="Screenshot 2023-08-10 at 2 53 04 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5e4cee8c-8c8b-45ba-ab11-d2e2f02a8327">


At this point. LAMP Stack features are completely installed 

- [x] [Ubuntu - Linux Environment]
- [x] Apache HTTP - Web Server
- [x] MYSQL - Database Management System
- [x] php - Programming Language.

# CREATING A VIRTUAL HOST FOR OUR WEBSITE USING APACHE!

In this step - We'll set up a domain called projectlamp.

Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory.

We will create ours instead using `mkdir` command

`sudo mkdir /var/www/projectlamp`

then, we'll assign ownership of the directory with the our current system user

 `sudo chown -R $USER:$USER /var/www/projectlamp`

 Then, create and open a new configuration file in Apache’s sites-available directory using my preferred command-line editor. I will use nano and attach the configuration bare-bones in the newly created config file

`sudo nano /etc/apache2/sites-available/projectlamp.conf`


<img width="1239" alt="Screenshot 2023-08-10 at 2 56 48 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/2a02de2f-7830-43e4-ac84-fc0539bc1530">

save and close the file.

use `sudo ls /etc/apache2/sites-available` to view the directory containing our newly configured file

This virtualhost configuration was created to instruct apache to serve projectlamp using  /var/www/projectlampl as its web root directory.

run a2ensite command to enable new host:

`sudo a2ensite projectlamp`

then, use a2dissite to overwrite apache's default configuration to allow projectlamp become the new virtual host.

`sudo a2dissite 000-default`

make sure the configuration has no syntax errors

`sudo apache2ctl configtest`

<img width="522" alt="Screenshot 2023-08-10 at 3 03 46 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5c313869-47b9-4f5a-b3bd-f1598ca870d3">

as seen above, we reloaded apache's services for the changes to take effect with this command

`sudo systemctl reload apache2`

At this poitnt. The website is now active. 

we'll create an index.html file and echo some writings into the file in the web root to test the host.

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

Testing if our by checking the virtual host on the web browser with our Public IP address or Public DNS name

http://<Public-IP-Address>:80

the result shows as follows

<img width="629" alt="Screenshot 2023-08-10 at 3 07 46 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/f85d2c8a-8cf6-4149-9b69-9b6bf8238f8f">



## ENABLING PHP ON THE WEBSITE!

WE’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

Using my preferred command line editor `nano`

`sudo nano /etc/apache2/mods-enabled/dir.conf`

Adding configuration bare-bones to the dir.conf file

<img width="780" alt="Screenshot 2023-08-10 at 3 16 17 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/676f87c6-3460-4485-be2a-eed068b3c28c">

after saving and closing the file, run a systemctl command to reload the server's services

`sudo systemctl reload apache2`

Create a php script to test if php is correctly installed on the server

`nano /var/www/projectlamp/index.php`

add php script.


 <img width="654" alt="Screenshot 2023-08-10 at 3 18 33 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/069967b6-53c7-4a02-ba85-5d3f61c72f39">


save and close the file, then reload the web page and this result comes up.

<img width="1299" alt="Screenshot 2023-08-10 at 3 19 10 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e8a8b9aa-402f-4d2e-9b32-0b36ddd75ae7">


php is fully functional on the apache web server!






