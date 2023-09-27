# Intro to Load Balancing and NGINX
- Load balancing involves distributing tasks among multiple servers to improve efficiency and accelerate completion.

- Imagine you have a group of webservers serving your website. To evenly distribute the traffic and prevent any server from being overwhelmed, a **load balancer** is deployed. The load balancer acts as a gateway, receiving all incoming traffic and then distributing it across the webservers. This helps improve system performance by ensuring a balanced workload for each server.

- [NGINX](nginx.com) is a multifunctional and versatile software that serve as a a webserver, reverse proxy, and a load balancer etc, with the right configuration.


## Configuring and setting up a Basic Load Balancer
- Let's provision 2 Ubuntu 22.04 EC2 instances, install Apache webserver, open port 8000 on the security group, and update the default page to display the public IP address.

- Then, we will provision another EC2 instance running ubuntu 22.04, this time we will install Nginx and configure it to act as a load balancer distributing traffic across the webservers.

  - After carrying out the tasks above. Using **[Termius](url)** custom terminal to log into our Linux Environment.
  - Splitting the two web servers side by side to make it understanding. 
  - Firstly Update the package manager with `sudo apt update && sudo apt-get update`
 
    <img width="1220" alt="Screenshot 2023-09-26 at 11 00 59 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d58b8e4d-56cd-4de9-a55a-bfe11ae7464c">



  - then install apache webserver on both servers using `sudo apt install apache2`
  - confirm that apache is correctly install and running smoothly
  - 

<img width="1232" alt="Screenshot 2023-09-26 at 11 03 35 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/95028304-72b2-4324-9748-55560a197382">

### Configuring Apache to serve content on Port:8000

- Using nano to configure this file
- `sudo nano /etc/apache2/ports.conf`
- Add a new Listen directive for Port 8000.

<img width="600" alt="Screenshot 2023-09-26 at 11 05 53 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/04377f0b-5ae1-4d78-84e0-a123edf3d881">

* Next step is to edit virtualhost port from 80 to 8000 of this _000-default.conf_ file
   - `sudo nano /etc/apache2/sites-available/000-default.conf`


<img width="593" alt="Screenshot 2023-09-26 at 11 08 08 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e7a76add-6298-4ee4-963f-b5ee37a4561a">


* Run `sudo systemctl restart apache2` to load the new configurations.
- Create a new index.html file and paste some html code to serve the webpage.

- `sudo nano index.html`

<img width="603" alt="Screenshot 2023-09-26 at 11 13 36 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/a6a0503a-7d2c-4c78-8dfe-dea9a4cd4357">


- Change the file ownership (index.html)
- `sudo chown www-data:www-data ./index.html`
- Use this file to Override the default html file of the apache server.
- i.e Copying the newly created index.html file on the path of the default html file of the apache webserver (/var/www/html)
- reload the new configurations with `sudo systemctl restart apache2`
- Then run the Public address on a web URL
- It should serve this our configuration below!
  

<img width="542" alt="Screenshot 2023-09-26 at 11 19 32 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/411aa0bf-96f7-4eaf-8ff4-10e1412af057">

## REPEAT ALL TASKS ABOVE FOR THE 2ND APACHE SERVER!



## Configuring NGINX as a Perfect Load Balancer

- Start up another New AWS Instance.
- Update the Apt Package manager and Install Nginx server.
- `sudo apt update -y && sudo apt install nginx -y
- Verify nginx is functioning Properly
- `sudo systemctl status nginx`

  <img width="1124" alt="Screenshot 2023-09-26 at 11 30 34 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/03f17ae4-a2a0-454a-be14-7d1da530e0bf">



* Create and configure a Loadbalancer configuration file in the nginx configuration directory.
* `sudo nano /etc/nginx/conf.d/loadbalancer.conf`

* Add these configurations to and edit to the current Public IP addressses & Ports for both servers.


<img width="931" alt="Screenshot 2023-09-26 at 11 40 38 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/66ed9500-a918-429b-a473-03ca6c24bbe5">


* Crosscheking the Public IP addresses for the 3 servers



* <img width="1224" alt="Screenshot 2023-09-26 at 11 53 44 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/cc357c47-1362-4ca6-ad10-cc86767c3caf">


* Verify the Nginx configurations for errors
* `sudo nginx -t`


<img width="694" alt="Screenshot 2023-09-26 at 11 54 57 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/de183284-c424-421b-8652-7901585c3aa7">



* Load the new configurations made
* `sudo systemctl restart nginx`



* Serve the Public IP address of the Nginx Server playing the role of a load balancer to the web browser.
* We should see the same webpages served by the Other apache webservers.

* We have two different contents on each server and the load balancer will serve both after multiple browser refreshing.

* As Shown below


<img width="612" alt="Screenshot 2023-09-26 at 11 55 46 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/1b4f7a60-61a6-4c06-b2cb-92cf5baebae0">            <img width="631" alt="Screenshot 2023-09-26 at 11 56 23 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/0cb8aa75-2eea-434f-a4f3-e2e73560e5d6">







  
    


    
