# AUTOMATING LOADBALANCER CONFIGURATION WITH SHELL-SCRIPTING!


* With shell scripting and CI/CD on [Jenkins](https://www.jenkins.io/)

   * You can automate load balancer configuration, making it more efficient and reducing manual effort. 

### Automate the Deployment of Webservers
- From the previous project [Implementing Loadbalancing with NGINX](https://github.com/travdevops/darey.io-pbl/blob/main/LOADBAL-x-NGINX-Project.md).
- We deployed two backend servers, with a load balancer distributing traffic across the webservers. We did that by typing commands right on our terminal.
- In this project we will be automating the entire process.
- In the load balancer automation project, we'll write a shell script to automate the deployment process.
- Automation is essential for DevOps Engineers to speed up deployments and minimize errors.
- This course will provide a fantastic introduction to automation.

### Getting Things Ready!

- In the Previous Project, We commissioned 2 AWS Instances and Applied the rule on the security groups to Listen to Port 8000. We will do the same again here.
- Write the script on the file locally and cross check for errors and make sure everything is intact.
- We will carry out the configurations on both servers.
- Create a file with `sudo nano apache1-config.sh` for webserver1 and `sudo nano apache2-config.sh` for webserver2
- This is the script in the file.

apache1-config.sh

<img width="994" alt="nano content apa1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/9422defb-04fd-46c3-ad65-28ea6302adc1">



apache2-config.sh
<img width="1136" alt="nano content apa2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/421cc85a-74b2-42aa-a592-f6623fea327c">




- Change the file permissions of the file to make them executable.
- `sudo chmod +x apache1-config.sh` and `sudo chmod +x apache2-config.sh`
- Run the scripts on the seperate servers `bash apache1-config.sh` and `bash apache2-config.sh`

 The images below shows the results after running the script on both servers.
 <img width="895" alt="completion of apa1 script" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e5035545-5d18-454e-8bab-c31628eba5ba">


<img width="1123" alt="completion of apa2 script" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d64086a1-d79c-485c-b128-ef5bfb2a6573">

- Testing the configurations on the web browser
apache server 1


<img width="545" alt="screenshot of apa1 url" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d987e788-e19a-4fb9-80fc-22c2ea61a454">


apache server2

<img width="562" alt="Screenshot of apa2 url" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/f05e8409-4242-4999-ae6a-a7274fdf0219">



### Deploying & Configuring NGINX as the Load Balanacer



Just as in the previous project. We will also create a 3rd server for the Load Balancing server.

- After creating the 3rd AWS Instance. 
- Write the script into the file _nginx.sh_ with the command `sudo nano nginx.sh`


<img width="1109" alt="nano content nginx" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/a79e28a4-3961-4a2e-9bf6-961dc6ddcc84">

- exit the nano file.
- set the permissions of the file to be executable.
- `sudo chmod +x nginx.sh`

- Now. Run the script while calling 3 arguments, (Public_IP of the Nginx server) (Public_IP of the 1st apache server) (Public_IP of the 2nd apache server).

- `bash nginx.sh <Public_IP of the nginx server> <Public_IP of the apache server1> <Public_IP of the apache server2>`


<img width="984" alt="running-script nginx" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/b085ce93-01ea-4539-a0e4-f2272e441eeb">

Reload the NGINX service to load the new configurations with `sudo nginx -t`


After running the script. 
Verify the load balancing by placing the Public IP of the load balancer on the web browser. 
Refresh the Browser multiple times and the servers would change. 
As ahown below. 


<img width="620" alt="nginx end 1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/0b70a201-63e4-44ec-96cc-ceeca99a7110">     

<img width="582" alt="nginx end 2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/6ecb310a-cf8e-4a6e-8303-9078a956deb7">



