# ANSIBLE-AUTOMATE-PROJECT!

This Project will make you appreciate DevOps tools even more by making most of the routine tasks automated with Ansible Configuration Management, at the same time you will become confident at writing code using declarative language such as **YAML**.

We will also be using Jenkins added for automation

Task
- Install and configure Ansible client to act as a [Jump Server](https://en.wikipedia.org/wiki/Jump_server)/[Bastion Host](https://en.wikipedia.org/wiki/Bastion_host)
- Create a simple Ansible playbook to automate servers configuration

## INSTALL AND CONFIGURE JENKINS & ANSIBLE ON AN EC2 INSTANCE
- Spin up an ec2 instance with ubuntu OS and name it Jenkins-Ansible. We will use this server to run playbooks and setup up Jenkins for Continous Integration. 

- In your GitHub account create a new repository and name it ansible-config-mgt.

### Install ANSIBLE.
- Update the server as always first, Then Install Ansible

- `sudo apt update`

- `sudo apt install ansible`

- Check your Ansible version by running `ansible --version`

Note: the config file path of ansible. 

<img width="802" alt="ans--version" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/23e384d6-45a9-4c68-beb9-95d316374467">


### Lets Talk Jenkins

DevOps is about Agility, and speedy release of software and web solutions. One of the ways to guarantee fast and repeatable deployments is Automation of routine tasks.

In this project we are going to start automating part of our routine tasks with a free and open source automation server – Jenkins. It is one of the most popular CI/CD tools, it was created by a former Sun Microsystems developer Kohsuke Kawaguchi and the project originally had a named “Hudson”.

Jenkins is a free-open source tool for Continuous integration (CI), (CI) is a software development strategy that increases the speed of development while ensuring the quality of the code that teams deploy. Developers continually commit code in small increments (at least daily, or even several times a day), which is then automatically built and tested before it is merged with the shared repository.

In our project we are going to utilize Jenkins CI capabilities to make sure that every change made to the source code in GitHub https://github.com/<yourname>/tooling will be automatically be updated.

Configure Jenkins build job to save your repository content every time you change it – this will solidify your Jenkins configuration skills.

### Step 1 – Install Jenkins server
Jenkins can be installed on any server but we will Install Jenkins on iur same Ansible server for the sake of this project.
Jenkins for Ubuntu/Debian

      - sudo apt update
      - sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
          https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
      - echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
          https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
          /etc/apt/sources.list.d/jenkins.list > /dev/null
      - sudo apt-get update
      - sudo apt-get install fontconfig openjdk-11-jre
      - sudo apt-get update
      - sudo apt-get install jenkins

- Make sure Jenkins is up and running

`sudo systemctl status jenkins`

Sometimes, the password for the Jenkins UI could also be found when checking the status of Jenkins.

<img width="1339" alt="jenkins--1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/51892779-2952-4a83-aa0c-21565f7b4390">


- By default Jenkins server uses TCP port 8080 – open it by creating a new Inbound Rule in your EC2 Security Group.

- Perform initial Jenkins setup.
- From your browser access http://<Jenkins-Server-Public-IP-Address-or-Public-DNS-Name>:8080
- You will be prompted to provide a default admin password.

- Retrieve it from your server:

`sudo cat /var/lib/jenkins/secrets/initialAdminPassword` 

<img width="989" alt="Screenshot 2023-10-30 at 6 20 17 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/634ed1a8-e6db-4f3a-92cb-6ab08330ab19">

- Incase there's an error accessing the folder, Change the Permissons for the folder with `sudo chmod 777` command.

- Then you will be asked which plugins to install – choose suggested plugins.

<img width="756" alt="Screenshot 2023-10-30 at 6 20 41 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/7bf3b4fc-a67f-4021-8f08-5e6ce004487b">

- Once plugins installation is done – create an admin user and you will get your Jenkins server address.

The installation is completed!

![image](https://github.com/travdevops/darey.io-pbl/assets/137777644/8109b731-c205-4257-bb0d-46103e0a4edd)


### Step 2 – Configure Jenkins to retrieve source codes from GitHub using Webhooks
In this part, you will learn how to configure a simple Jenkins job/project (these two terms can be used interchangeably). This job will be triggered by GitHub webhooks and will execute a ‘build’ task to retrieve codes from GitHub and store it locally on Jenkins-Ansible server.

- Enable webhooks in your GitHub repository settings for builds to occur automatically on Jenkins

<img width="675" alt="webhook" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/480c4bb6-f4ac-41af-8991-6d9035098e4d">

<img width="835" alt="webhook2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/729ef9cb-072e-40b1-990e-1108df1f7f1c">


- Create a new Freestyle project `ansible` in Jenkins and point it to your ‘ansible-config-mgt’ repository.

<img width="1393" alt="jen-git setup" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/f3099b9f-64e1-4436-9b74-2880534f958f">

**Note:** Trigger Jenkins project execution only for /main branch. Other branches can be added depending on the project requirements

<img width="976" alt="jen-git setup2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d70f8e9a-a575-4404-acbb-5bb51daf47d5">

<img width="848" alt="jen-gitsetup" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/fe14c47a-effa-4448-8a33-08560b0e12f2">

- Configure a Post-build job to save all (**) files

<img width="774" alt="Screenshot 2023-10-30 at 6 38 40 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/4e26f12b-9cdf-40a5-a435-ce291a622781">

<img width="326" alt="Screenshot 2023-10-30 at 6 39 45 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/62f7b58a-73b9-46b3-ae37-40cef493f8c0">


- Test your setup by making some change in README.MD file in main branch and make sure that builds starts automatically and Jenkins saves the files (build artifacts) in following folder.

<img width="452" alt="Screenshot 2023-10-30 at 6 40 50 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/4b66cc17-fc41-4925-870e-40d3a496bd2f">


`ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/`


### Step 3 – Prepare your development environment using Visual Studio Code
Development ‘DevOps’ means you will require to write some codes and you shall have proper tools that will make your coding and debugging comfortable. you need an Integrated development environment (IDE) or Source-code Editor. There is a plethora of different IDEs and Source-code Editors for different languages with their own advantages and drawbacks, you can choose whichever you are comfortable with. **Visual Studio Code** is what you will use in this project.  

After you have successfully installed VSC, configure it to connect to your newly created GitHub repository.

<img width="523" alt="conn-githb-vsc" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/0799dae2-e717-469b-b012-0cb3f1a2fbc9">

<img width="688" alt="conn-githb-vsc2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/afca21d9-2c12-4984-b39f-5c8e6ab3b990">


- Clone down your ansible-config-mgt repo to your Jenkins-Ansible instance `git clone <ansible-config-mgt repo link>`

<img width="825" alt="git clone down to server" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5b088bf7-31b9-47c3-94b0-0e718768c3bf">


### BEGIN ANSIBLE DEVELOPMENT
In your ansible-config-mgt GitHub repository, create a new branch that will be used for development of a new feature. This task can either be done on the Github or cloned down to the Jenkins-Ansible server. We will clone it down. 

- Checkout the newly created development branch to your local machine and start building your code and directory structure
    - Create a directory and name it 'playbooks' – it will be used to store all your playbook files.
    - Create a directory and name it 'inventory' – it will be used to keep your hosts organised.
    - Within the playbooks folder, create your first playbook, and name it 'common.yml'
    - Within the inventory folder, create an inventory file (.yml) for each environment (Development, Staging Testing and Production) dev, staging, uat, and prod respectively.

<img width="720" alt="create yml files and directories" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/3e017a76-9ef1-4a4c-ae9c-163e46f7b0b5">

Also create an Ansible configuration file to help with configs `touch ansible.cfg`

<img width="773" alt="ansible" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d1e35944-080f-4312-8245-082cdce4a512">

### Step 4 – Set up an Ansible Inventory
An Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. Since our intention is to execute Linux commands on remote hosts, and ensure that it is the intended configuration on a particular server that occurs. It is important to have a way to organize our hosts in such an Inventory.

Save below inventory structure in the _inventory/dev_ file to start configuring your development servers. Ensure to replace the IP addresses according to your own setup.

Note: Ansible uses TCP port 22 by default, which means it needs to ssh into target servers from Jenkins-Ansible host – for this you can implement the concept of **ssh-agent**.

- Now you need to import your key into **ssh-agent**:

   - Exit the Jenkins-Ansible, On the directory where the keypair used to create the Jenkins-Ansible lies, Setup ssh-agent.

     `eval `ssh-agent -s`
      ssh-add <path-to-private-key OR private-key>

- Confirm the key has been added with the command below, you should see the name of your key

      ssh-add -l

- Now, ssh into your Jenkins-Ansible server using ssh-agent

      ssh -A ubuntu@public-ip

<img width="836" alt="ssh eval" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/3dc704fb-80b0-45ff-af37-5ee663947b50">


Note: Ubuntu-based servers user is **ubuntu** and user for RHEL-based servers is **ec2-user**.

- From the Jenkins-Ansible, ssh into all the remote servers with the same command `ssh user@public-ip`

<img width="845" alt="ssh 2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ae131853-fa3e-4530-ab87-ae643cdf8427">


We currently have a few servers we want Ansible and ssh to communicate with to be able to run our playbooks.

    1 Nfs server - RHEL-based
    2 Webservers - RHEL-based
    1 Database Server - Ubuntu-based

- Update your inventory/dev.yml file with this snippet of code:

      [nfs]
      172.31.0.164 ansible_ssh_user='ec2-user'

      [webservers]
      172.31.15.42 ansible_ssh_user='ec2-user'
      172.31.7.5 ansible_ssh_user='ec2-user'

      [db]
      172.31.1.93 ansible_ssh_user='ubuntu'

<img width="428" alt="devyml contents" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/70a7932c-b6f7-4292-a288-cdf9c13aeaa5">


### Step 5 – Create a Common Playbook
It is time to start giving Ansible the instructions on what you needs to be performed on all servers listed in inventory/dev.

In common.yml playbook you will write configuration for repeatable, re-usable, and multi-machine tasks that is common to systems within the infrastructure.

- Update your playbooks/common.yml file with following code:

      ---
      - name: update web, nfs and db servers
        hosts: webservers, nfs
        remote_user: ec2-user
        become: yes
        become_user: root
        tasks:
          - name: ensure wireshark is installed and at its latest version
            yum:
              name: wireshark
              state: latest

      - name: update DB server
        hosts: db
        remote_user: ubuntu
        become: yes
        become_user: root
        tasks:
          - name: Update apt repo
            apt: 
              update_cache: yes

          - name: ensure wireshark is installed and at its latest version
            apt:
              name: wireshark
              state: latest


<img width="549" alt="commomyaml" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/be8009fe-b525-4980-b835-7ddb336f0bee">

Examine the code above and try to make sense out of it. This playbook is divided into two parts, each of them is intended to perform the same task: **install wireshark utility** (or make sure it is updated to the latest version) on your RHEL and Ubuntu servers. It uses root user to perform this task and respective package manager: yum for RHEL and apt for Ubuntu.

### Step 6 – Update GIT with the latest code
- Now all of your directories and files live on your machine
- From the local development branch, Merge them to the local main branch and push the changes made locally to the remote GitHub.

Working with an organization, It is always advicable to make a pull request first to update changes made remotely down to the local branch before pushing the changes made on the local branch. 

- Commit your code into GitHub:

- use git commands to add, commit and push your branch to GitHub.

      `git status`

      `git add <selected files>`

      `git commit -m "commit message"`


- Create a Pull request (PR)

- Act as a reviewer. If the reviewer is happy with your new feature development, merge the code to the main/master branch.

- Head back on your terminal, checkout from the feature branch into the main/master, and pull down the latest changes.

- Once your code changes appear in main/master branch – Jenkins will do its job and save all the files (build artifacts) to /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/ directory on Jenkins-Ansible server.

### Step 7 – Run first Ansible test
- Now, it is time to execute ansible-playbook command and verify if your playbook actually works:

- On the Jenkins-Ansible server.

- `cd ansible-config-mgt` 

- Firstly, we will try to ping all the servers just to check if our ansible connection is setup properly with the ansible ping module

- `ansible all -i inventory/dev.yml -m ping`

  <img width="1498" alt="playbook ping" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/77a1d83f-fe76-4021-9b18-cb693df597b9">

- Now, We will run our playbook.

- `ansible-playbook -i inventory/dev.yml playbooks/common.yml`

<img width="1258" alt="playbook1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5306fa86-1acc-483d-af7f-36f8bb52ee72">

- You can go to each of the servers and check if wireshark has been installed by running `which wireshark` or `wireshark --version`

Example -

<img width="432" alt="test-server-wireshark" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/10a54af3-1b44-4d24-b5b7-bf126b486d59">

- Optional step – Repeat once again - Another Task.

- Update your ansible playbook with some new Ansible tasks

- Here, we will ask ansible to install Nginx 

<img width="1261" alt="playbook2-nginx" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/62b791e8-6da9-4863-bd16-30cc0b92a1d4">


- Go through the full checkout -> change codes -> commit -> PR -> merge -> build -> ansible-playbook cycle again to run it.

 
SEE HOW EASILY YOU CAN MANAGE A SERVERS FLEET OF ANY SIZE WITH JUST ONE COMMAND!


![image](https://github.com/travdevops/darey.io-pbl/assets/137777644/fbb6fc80-0e37-4043-a145-14ad57afbe7e)


