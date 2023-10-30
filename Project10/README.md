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
Update the server as always first, Then Install Ansible

`sudo apt update`

`sudo apt install ansible`

Check your Ansible version by running `ansible --version`

Note: the config file path of ansible. 

