# CLIENT-SERVER ARCHITECTURE WITH MYSQL
* Client-Server refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.
* In their communication, each machine has its own role: the machine sending requests is usually referred as _Client_ and the machine responding (serving) is called _Server_.

## Client - Server Architecture Using A Relational DB Sysytem.
### The Task of this project is to succesfully Implement a Client-Server Architecture using **MySQL Database Management System (DBMS)**.
* Create and configure two Linux-based virtual servers (EC2 instances in AWS).
  
      Server-A name - `mysql server`
      Server-B name - `mysql client`


Firstly, We have to update the apt packages with `sudo apt update`, then

  * Install  MySQL **SERVER** software on _mysql server_

    <img width="638" alt="Screenshot 2023-09-21 at 11 26 12 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ce2d76e0-8dac-4286-b718-792c99e684a8">

    

  * Then, Install MySQL **CLIENT** software on _mysql client_

    <img width="604" alt="Screenshot 2023-09-22 at 12 57 03 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c88be2e4-b43d-4df1-ae8d-11c939d91de9">

    

  * Both ec2 instance servers are located in the same local virtual network, so they can communicate to each other using local IP addresses.
  * Configure the inbound rules in the security group to allow _mysql server's_ local IP address to connect from _mysql client_.
  * MySQL server uses TCP port **3306** by default (MySQL/Aurora). Add this new rule then specify _mysql client's_ local IP Address (Private-Address) to allow access only to _mysql client_.



<img width="1364" alt="Screenshot 2023-09-21 at 11 20 58 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ded8b1e7-8a28-4dec-b8be-c78af3341a64">






### Setting up the MySQL server on _mysql server_

* Firstly, We are to secure our MySQL database properly by running this command `sudo mysql_secure_installation` to create and validate a password plugin.

  <img width="615" alt="Screenshot 2023-09-22 at 12 57 29 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c11c5c46-f7af-4814-ace1-ebd40467359b">


* Log back into the MySQL console after validating the password with `sudo mysql -p` prompting for the validated password.


  <img width="594" alt="Screenshot 2023-09-22 at 12 57 51 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c99d87df-42b1-4639-b433-7a5eaa3a17a8">

  

Create a user and a database - user = _henry_user_, database = _henry_db_

* `CREATE USER 'henry_user' Q'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';`
* `CREATE DATABASE henry_db;`
  
Grant the database privileges and access to the user with this command


* `GRANT ALL ON henry_db.* TO 'henry_user' @'%' WITH GRANT OPTION;`
  
Perform a flush-privileges operation To tell the server to reload the grant tables easily


* `FLUSH PRIVILEGES;`

  <img width="418" alt="Screenshot 2023-09-22 at 1 07 18 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/0d5ab8bc-aafe-41fd-9cd9-517bb70c86b5">
  

* We just created a new user, a new database, Granted the user privileges and flushed the operations above.
* Now, exit the MySQL console and restart the service with `sudo systemctl restart mysql`

<img width="535" alt="Screenshot 2023-09-22 at 1 15 27 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/28d66f5a-5c02-4f2d-b6e2-7e1a4af788b7">



### Configuring MySQL server on _mysql server_ to allow connections from remote hosts

* Using _nano_, get into this location and open this config file _mysqld.cnf_
* `sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`

* Search for 'bind address' in the file and replace **‘127.0.0.1’** to **‘0.0.0.0’**

  <img width="608" alt="Screenshot 2023-09-22 at 1 11 13 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e5f76e88-d322-42ca-bd0c-f746829c69e0">


* Close the editor and restart the MySQL Services again.


  ## Onto the _mysql client_

  
* From _mysql client_, Try to Connect remotely to the  _mysql server_ Database engine with this log in command.

* `sudo mysql -u henry_user -h 172.31.14.8 - p`

      -u flag for the user.
      -h to specify the hostname with IP address.
      -p flag to prompt for the log in password.


<img width="599" alt="Screenshot 2023-09-22 at 1 17 47 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/99180521-de08-4596-88f2-a747c5ba580d">

We have successfully remotely connected to the MySQL's _mysql server_ from _mysql_client_


Test the console by displaying the current databases. `SHOW DATABASES;`



<img width="326" alt="Screenshot 2023-09-22 at 1 18 11 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c99d91d4-8b74-4969-b987-17e783ea2916">


