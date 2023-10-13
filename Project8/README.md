# Web Solutions With WordPress
- We will be Setting up storage infrastructure on a Red-Hart Linux server.


[WordPress](https://wordpress.com/) is indeed a free and open-source CMS written in **PHP**, and it works well with **MySQL** or **MariaDB** as the backend RDBMS. 
- Using WordPress for a basic web solution is a great choice.


This Project Consists of the different parts. 
  - Configure storage subsystem for Web and Database servers based on Linux OS.
  - Install WordPress and connect it to a remote MySQL database server.
   
### Step 1 — PREPARE A WEB SERVER
1. Launch an EC2 instance that will serve as “Web Server”
    - Create 3 volumes on the AWS Platform and attach them to the Web Server EC2, each of 10 GiB.
    - Attach the 10GB Volumes to the running Instance one after the other.
   
2. Begin Configuration on the terminal.
    - type this `lsblk` command to inspect what block devices are attached to the server.
    - Identify the 3 new volumes namely **_xvdf_**, _**xvdh**_ and **_xvdg_** with `ls /dev`
  
      <img width="1610" alt="verify the new-drives" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/14b71fb8-c176-49dd-9042-a32af676e06e">
 
    - Use `gdisk` utility to create a single partition on each of the 3 disks
    - All steps would be performed for the 3 disks
    - `sudo gdisk /dev/xvdf` for the first disk.
    - At the command prompt - enter `n` to add a new partition.
    - Click `enter` for the following questions prompts.
      
    <img width="672" alt="sudo gdisk command n" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/1c2ad6de-1dd4-4a53-b590-08d4db02e29b">
    
    - then write the disk at the next command prompt by clicking `w`
    - proceed to writing new GUID partition table to the xvdf disk.
    
    <img width="690" alt="sudo gdisk command w" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/86429956-1586-4796-893f-9c5eacce2d0a">
    
    - After having adding and writing partition tables for all 3 disks
    - use `lsblk` to view the newly configured partition on each of the 3 disks.
      
    - <img width="497" alt="lsblk-mounted-partitions" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c5e4a13f-e536-484f-ae4f-120e39bdd5c1">

    - Install [lvm2](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux)) package using `sudo yum install lvm2`.
    - Run `sudo lvmdiskscan` command to check for available partitions.

      <img width="519" alt="lvmdiskscan" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/6b557980-58a0-4d7f-afc2-987f1f2acb7b">


    - Use [pvcreate](https://linux.die.net/man/8/pvcreate) utility to mark each of 3 disks as physical volumesto (PVs)be used by LVM
    - `sudo pvcreate /dev/xvdf1 && sudo pvcreate /dev/xvdg1 && sudo pvcreate /dev/xvdh1`
    - another option is to use a script file to run these commands at once and make things easier
    - Verify that the Physical volume has been created successfully by running `sudo pvs`
  
      <img width="578" alt="pvs" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ed986c99-a5a4-47a8-8362-ea44e4aff235">

      

    - Use [vgcreate](https://linux.die.net/man/8/vgcreate) to add the Personal Volumes to a Volume Group (VG) - **webdata-vg**
    - `sudo vgcreate webdata-vg /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`
    - Verify that the VG has been created successfully by running `sudo vgs`
    - Use [lvcreate](https://linux.die.net/man/8/lvcreate) utility to create 2 logical volumes - apps-lv and logs-lv. Both Logical Volumes would share sizes of the Personal Volume.
    - apps-lv will be used to store data for the website while logs-lv will be used to store data for logs.
    - `sudo lvcreate -n apps-lv -L 14G webdata-vg && sudo lvcreate -n logs-lv -L 14G webdata-vg `
    - Verify that the Logical Volume has been created successfully by running `sudo lvs`

      <img width="838" alt="lvs" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/6fbbfc53-1f04-450a-859f-b762d1aa05ec">

      

    - Verify the whole setup - `sudo lsblk`

### Continuation of the Configuration 
- The next few steps of the command will be done with shell scripting to make things a bit easier. 
  - Create a file `lvmp.sh`
  - give the file ultimate permissions with `sudo chmod 777 lvmp.sh`
  - Type in all the steps and commands to run all in the script file using vi or nano or vscode editors to run them all at once


  <img width="1422" alt="Screenshot 2023-10-05 at 2 07 47 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/8583862a-7c5c-46f9-a119-6dd2f5f26290">


  - After the script is done running, we have the following output for our UUID parameters for apps-lv and logs-lv

    <img width="1320" alt="sudo blkid" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/924dabe6-84db-48fa-85df-18f987858835">

- Update /etc/fstab in this format using the UUID using nano file editor
   - nano isn’t automatically installed on Red-Hart Linux servers so we have to Install it with the command `sudo yum install nano`
   - `sudo nano /etc/fstab`
   - replace the UUID number with our apps-lv and logs-lv parameters
 
   - Test the configuration and reload the daemon
   - `sudo mount -a`
   - `sudo systemctl daemon-reload`
   - Verify your setup by running `df -h`, output must look like this:
 
     <img width="661" alt="df -h check" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/06ae1b79-9d65-4af3-adba-9e8dc61e47a7">


###  STEP 2 - PREPARE THE DATABASE SERVER

Repeat the same steps as for the Web Server, but instead of **apps-lv** and **logs-lv**, create **db-lv** and **logs-lv**, then mount it to _/db_ directory instead of _/var/www/html/_.


### STEP 3 - INSTALL WORDPRESS ON YOUR WEB SERVER

- Update the repository
   - `sudo yum -y update`

- Install wget, Apache and it’s dependencies
   - `sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json`

- Start Apache
    - `sudo systemctl start httpd`

- To install PHP and its depemdencies

      - sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
      - sudo yum module list php
      - sudo yum module reset php
      - sudo yum module enable php:remi-7.4
      - sudo yum install php php-opcache php-gd php-curl php-mysqlnd
      - sudo systemctl start php-fpm
      - sudo systemctl enable php-fpm
      - sudo setsebool -P httpd_execmem 1


- Restart Apache
   - `sudo systemctl restart httpd`

- Download wordpress and copy wordpress to var/www/html

      - cd   wordpress
      - sudo wget http://wordpress.org/latest.tar.gz
      - sudo tar xzvf latest.tar.gz
      - sudo rm -rf latest.tar.gz
      - sudo cp wordpress/wp-config-sample.php wordpress/wp-config.php
      - sudo cp -R wordpress /var/www/html/


- Configure SELinux Policies

      - sudo chown -R apache:apache /var/www/html/wordpress
      - sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R
      - sudo setsebool -P httpd_can_network_connect=1
      - sudo setsebool -P httpd_can_network_connect_db 1


### STEP 4 - INSTALL MYSQL ON YOUR DB SERVER

- `sudo yum install mysql-server`

- Verify that the service is up and running by using `sudo systemctl status mysqld`, if it is not running, restart the service and enable it so it will be running even after reboot:



- `sudo systemctl enable mysqld`

### STEP 5 - CONFIGURE DB TO WORK WITH WORDPRESS

    - CREATE DATABASE wordpress;
    - CREATE USER `myuser`@`<Web-Server-Private-IP-Address>` IDENTIFIED BY 'mypass';
    - GRANT ALL ON wordpress.* TO 'myuser'@'<Web-Server-Private-IP-Address>';
    - FLUSH PRIVILEGES;
    - SHOW DATABASES;
    - exit


<img width="710" alt="mysql-database" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/b3eaa3de-0b6a-4b52-aca5-8b36683da86e">


### STEP 6 - CONFIGURE WORDPRESS TO CONNECT TO THE REMOTE DATABASE


- Open MySQL port 3306 on DB Server EC2. For extra security, you shall allow access to the DB server ONLY from your Web Server’s IP address, so in the Inbound Rule configuration specify source as /32

- Install MySQL client and test that you can connect from your Web Server to your DB server by using mysql-client
- `sudo yum install mysql`

- Now edit mysql configuration file by typing `sudo nano /etc/my.cnf`. Add the following at the end of the file.

<img width="730" alt="Screenshot 2023-10-06 at 1 24 27 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/bf26233d-e406-4eb0-bf18-637a4a60e3c4">


- Restart mysqld service using
   - `sudo systemctl restart mysqld`

- Change permissions and configuration so Apache could use WordPress: Enable TCP port 80 in Inbound Rules configuration for your Web Server EC2 (enable from everywhere 0.0.0.0/0 or from your workstation’s IP)

- On the web server, edit wordpress configuration file.

- Get into the wordpress directory
  - `cd /var/www/html/wordpress`
  - `sudo nano wp-config.php`

- Disable the default page of apache so that you ca view the wordpress on the internet.

   - `sudo mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf_backup`

- Restart httpd.
   - `sudo systemctl restart httpd`

- Verify if you can successfully execute command and see a list of existing databases.

   
       - sudo mysql -u admin -p -h <DB-Server-Private-IP-address>

       - show databases; 

<img width="882" alt="mysql-serv-login" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/288b9102-b609-480e-837e-956da46eccbc">



<img width="283" alt="Screenshot 2023-10-06 at 12 52 53 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/4f377c7b-0866-4d16-8ddb-e281792d8956">





- Change permissions and configuration so Apache could use WordPress:

      - sudo chcon -t httpd_sys_content_t /var/www/html/wordpress -R
      - sudo setsebool -P httpd_can_network_connect=1
      - sudo setsebool -P httpd_can_network_connect_db 1

- Try to access from your browser the link to your WordPress http:///wordpress/




























