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


# Install MYSQL!

* MYSQL is the Database Management System of choice in this project, It is able to store and manage data for your site in a relational database
* We'll use the command below to install the software unto the server
* `sudo apt install mysql-server` and follow the prompts with '_Y_' to proceed with the installation.

  <img width="1227" alt="Screenshot 2023-08-30 at 7 11 31 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/99498781-38f5-4a58-be1e-055994f04044">

* After Installation COmpletion, Log into the MYSQL console:
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






