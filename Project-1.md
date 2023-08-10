
# First PBL Project -  WEBSTACK (LAMPSTACK) IN AWS!

LAMP (Linux, Apache, MySQL, PHP)

Updating lists of packages in package manager. 

`sudo apt update`

packages have been installed after the update.

<img width="891" alt="Screenshot 2023-08-10 at 11 51 01 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d73d14f6-6013-4671-960e-2081ac5e6c45">


Installing Apache!

`sudo apt install apache2`

Verify that apache2 is running as a Service

`sudo systemctl status apache2`

<img width="760" alt="Screenshot 2023-08-10 at 2 34 42 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/55103e90-9379-4878-a063-2e785419e86f">

apache2 service is running on the service = apache Web server has been launched in the clouds. 

Verification to access services locally in our shell using the `curl` command

`curl http://localhost:80 or curl http://127.0.0.1:80`

the above command gives the result that apache services is accesible in our local ubuntu shell

<img width="1029" alt="Screenshot 2023-08-10 at 2 39 19 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c60502b9-3b27-41fe-9f1c-948838968869">


Then we test how Apache HTTP server responds to requests from the internet by running my public IP address on a browser to default port 80

http://<Public-IP-Address>:80

The result confirms Apache web server is correctly installed and accessible through the web.

<img width="919" alt="Screenshot 2023-08-10 at 2 40 45 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/caed7aae-4bd8-4b14-87e8-169428956912">






INSTALLING MYSQL!

MYSQL - a  Database Management System (DBMS) to be able to store and manage data for your site.

 MySQL is a popular relational database management system used within PHP environments

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


Installing Programming Language (php)


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

Creating a virtual host for our website using apache!
