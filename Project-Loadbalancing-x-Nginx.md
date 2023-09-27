# Intro to Load Balancing and NGINX
- Load balancing involves distributing tasks among multiple servers to improve efficiency and accelerate completion.

- Imagine you have a group of webservers serving your website. To evenly distribute the traffic and prevent any server from being overwhelmed, a **load balancer** is deployed. The load balancer acts as a gateway, receiving all incoming traffic and then distributing it across the webservers. This helps improve system performance by ensuring a balanced workload for each server.

- [NGINX](nginx.com) is a multifunctional and versatile software that serve as a a webserver, reverse proxy, and a load balancer etc, with the right configuration.


## Configuring and setting up a Basic Load Balancer
- Let's provision 2 Ubuntu 22.04 EC2 instances, install Apache webserver, open port 8000 on the security group, and update the default page to display the public IP address.

- Then, we will provision another EC2 instance running ubuntu 22.04, this time we will install Nginx and configure it to act as a load balancer distributing traffic across the webservers.

