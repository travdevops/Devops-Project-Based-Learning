# The LEMP Webstack Implementation Project

 * Lemp Implementation Involves Installing Various Programs and Packages, Another technology stack which is a set of frameworks and tools used to develop a software product.

 * LEMP (Linux, Nginx, MySQL, PHP)

       - Linux - The Operating System Environment. 
       - Nginx - The Web Server.
       - MySQL - The Database Management System.
       - Php   - The Programming Language.
     

 * Project 2 covers similar concepts as Project 1 (LAMPstack) and helps to cement the skills needed for deploying Web solutions using webstacks.

* In this project we will implement a similar stack, but with an alternative Web Server – [NGINX](https://nginx.org/en/), which is also very popular and widely used by many websites in the Internet.

# Gathering the Prerequisities

 To successfully finish this project, we'll require an AWS account and a virtual server running Ubuntu Server OS. I already have ec2 Instance of t2.micro family with Ubuntu Server 20.04 LTS (HVM) image. 

 * After successfully launching the ec2 Instance on AWS and spinning up the server on the command line, (we'll be making use of [TERMIUS](termius.com) as the command line as opposed to the normal local machine terminal)

# Install the NGINX Web Server.

* We'll first of all update the apt package manager to have all the latest server package indexes.
* `sudo apt update`

<img width="937" alt="Screenshot 2023-08-25 at 7 37 58 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ce7af212-88c1-4540-b92e-1153fe1587dd">



* Then we install the web server NGINX
* `sudo apt install nginx`

<img width="1222" alt="Screenshot 2023-08-25 at 7 39 59 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/8fa0e466-eb80-4042-8c76-423f8c561bb4">

* Verify that NGINX was successfully installed and is running as a service
* ` sudo systemctl status nginx`

<img width="930" alt="Screenshot 2023-08-25 at 7 41 30 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/153cb84c-209d-4bc1-8856-c84d2eed245b">

* Before any traffic can on the web server we just installed, we need to open TCP Port 80 (default port) that web browsers use to access the webpages online.

*  On the security settings of the ec2 Instance on AWS, We will edit the inbound rules and add a new rule for the HTTP to listen to the default port 80 and to be accessible through the IP Address.

<img width="1316" alt="Screenshot 2023-08-25 at 7 43 03 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/24c99bac-cd17-4e2a-b9c8-80d434a3782f">

* Proceeding on saving the new inbound rule, run the command below to access it locally
* `$ curl http://localhost:80` or $ `curl http://127.0.0.1:80`
* We can either use our Public DNS Name or Public IP Address to access it locally.

<img width="591" alt="Screenshot 2023-08-25 at 7 49 29 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5f561c12-4875-4c90-bd6e-3546ee23681d">


* Now, we'll test to see how the NGINX server responds to internet requests on any browser.
* Run this http://(Public-IP-Address):80
* The webpage shows this result confirmed our NGINX server's Installation. 

<img width="836" alt="Screenshot 2023-08-25 at 7 51 34 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/1eecf5df-742c-4a87-93e2-f2c684202d4a">


# Installing MYSQL!

* MYSQL is the Database Management System of choice in this project, It is able to store and manage data for your site in a relational database
* We'll use this command below to install the software unto the server
* `sudo apt install mysql-server` and follow the prompts with '_Y_' to proceed with the installation.

  <img width="1227" alt="Screenshot 2023-08-30 at 7 11 31 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/99498781-38f5-4a58-be1e-055994f04044">

* After Installation Completion, Log into the MYSQL console:
* `sudo mysql`
  <img width="677" alt="Screenshot 2023-08-30 at 7 14 44 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/84a3e360-e4e1-47db-b2f6-96728bef5e81">

* To secure your MySQL database, run the pre-installed security script. Set the root user's password as "PassWord.1".
* `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`
  <img width="771" alt="Screenshot 2023-08-30 at 7 15 37 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/71e89295-3e6a-4559-ae82-122a803abeb6">

* Exit the MySQL shell with: mysql> `exit`
  <img width="325" alt="Screenshot 2023-08-30 at 7 16 02 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/3e59dee3-5e51-402c-9e14-3292c7bf291f">

* Log back into the MYSQL script by running `sudo mysql_secure_installation`
* The script will prompt us to configure the VALIDATE PASSWORD PLUGIN.
* Then we'll input our updated password 'PassWord.1'
* It's our decision whether to turn on password validation. If we'll choose to, MySQL will reject weak passwords.
* Answer _Y_ for _yes_, or anything else to continue without enabling.
* If we say "_yes_" to password validation, we can pick a level. Level 2 is the strongest, but it might give errors for weak passwords which doesn’t contain numbers, upper and lowercase letters, special characters.
* The server will next ask us to select and confirm a password for the MySQL root user, After enabling password validation, we'll see the password strength and be asked to confirm it. Enter "_Y_".
  <img width="893" alt="Screenshot 2023-08-30 at 7 20 25 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/32a42744-f0d4-48df-9793-d3b6b87d0f45">

* For the rest of the questions, press '_Y_' and hit the ENTER key at each prompt
<img width="706" alt="Screenshot 2023-08-30 at 7 21 08 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/eec57763-bec3-45d1-8785-7ec627fc5e32">

* Once finished, Test the MYSQL console by logging in with:
* `sudo mysql -p` Make sure to include the "_-p_" flag in the command to prompt for the new root user password.
  <img width="750" alt="Screenshot 2023-08-30 at 7 22 36 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e78f35f7-352d-4932-a741-475b556a320f">

* MySQL server is now installed and secured. 




# Installing PHP
* We have [Nginx](url) for serving content, MySQL for data management, and now we will install PHP for generating dynamic web content.
* Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server
* This helps To enhance performance in PHP-based websites, We will install _php-fpm_ (PHP fastCGI process manager) and configure Nginx to pass PHP requests to it.
* Additionally, installing _php-mysql_ allows PHP to communicate with MySQL databases. The core PHP packages will be installed automatically as dependencies.
* We will install both packages at once with this command `sudo apt install php-fpm php-mysql`
* Enter '_Y_' to proceed.
  
  <img width="980" alt="Screenshot 2023-08-30 at 7 23 34 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5c3cd585-fdfe-4469-990f-6607bea2031e">

* PHP compnents are installed!




# Configuring NGINX To Use PHP Processor

* When hosting multiple sites on Nginx, you can create separate server blocks within the configuration file for each site. This allows you to define different document root directories and manage each site individually. It's a great way to keep things organized and ensure smooth management of multiple websites.
* Create the root web directory for the domain
* `sudo mkdir /var/www/projectLEMP`
* Assign Ownership to $USER Environment
* `sudo chown -R $USER:$USER /var/www/projectLEMP`
* Then, open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor. Here, we’ll use _nano_:

*`sudo nano /etc/nginx/sites-available/projectLEMP`
* This will create a new blank file. Paste in the following bare-bones (As seen in the photo below)
* Close the nano editor.
* Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:
* `sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`
* This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:
* `sudo nginx -t`
* You shall see following message:
* _nginx: the configuration file /etc/nginx/nginx.conf syntax is ok. nginx: configuration file /etc/nginx/nginx.conf test is successful_
  
<img width="869" alt="Screenshot 2023-08-30 at 7 28 23 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/84198378-b673-4b5c-bc6e-a075044e1369">

  
* If any errors are reported, go back to your configuration file to review its contents before continuing.
* We also need to disable default Nginx host that is currently configured to listen on port 80, for this run:
* `sudo unlink /etc/nginx/sites-enabled/default`
* reload Nginx to apply the changes:
* `sudo systemctl reload nginx`

* Now, the website is active but the root directory is empty.
* Create an index.html file in that location so that we can test that your new server block works as expected:
* `sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html`
* On the browser, paste the public address to port 80 to test what we echoed into the web root directory.
* This is the result.
  <img width="979" alt="Screenshot 2023-08-30 at 7 30 57 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e6b732dc-0a87-4ee3-b9ea-4dc5deaa30cb">

# Testing PHP with NGINX.

* At this point, Our LEMP stack is completely installed and fully operational.
* Testing it to verify that NGINX responds to PHP files.
* You can do this by creating a test PHP file in your document root, Open a new file called _info.php_ within your document root in your text editor: Using nano.
* `sudo nano /var/www/projectLEMP/info.php`
* paste the following lines into the new file and close the nano editor
* access this page in your web browser by visiting the domain name or public IP address you’ve set up in your Nginx configuration file, followed by _/info.php_:
* web page containing detailed information about your server should come up as shown below:
* <img width="968" alt="Screenshot 2023-08-30 at 8 23 01 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/48b52e10-d600-452b-8495-84630d2a077e">



# Retrieving data from MySQL database with PHP

* In this step we will create a test database with simple “To do list” and configure access to it, so the Nginx website would be able to query data from the Database and display it.
* We’ll need to create a new user with the mysql_native_password authentication method in order to be able to connect to the MySQL database from PHP.
* We will create a database named _example_database_ and a user named _example_user_, but you can replace these names with different values.
* We will stick to the names pre-used.
* Log back into the MYSQL console
* `sudo mysql`
* create a new database from the MYSQL console
-     `CREATE DATABASE `example_database`;

  






