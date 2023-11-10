# ANSIBLE-PROJECT 

## ANSIBLE REFACTORING AND STATIC ASSIGNMENTS (IMPORTS AND ROLES)

- Side Self Study: For better understanding or Ansible artifacts re-use – [read this article](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse.html).

### Code Refactoring

Refactoring is a general term in computer programming. It means making changes to the source code without changing expected behaviour of the software. The main idea of refactoring is to enhance code readability, increase maintainability and extensibility, reduce complexity, add proper comments without affecting the logic. In this case, you will move things around a little bit in the code, but the overal state of the infrastructure remains the same. Let us see how you can improve your Ansible code!

### Step 1 – Jenkins Job Enhancement

Before we begin, let us make some changes to our Jenkins job – now every new change in the codes creates a separate directory which is not very convenient when we want to run some commands from one place. Besides, it consumes space on Jenkins serves with each subsequent change. Let us enhance it by introducing a new Jenkins project/job – we will require Copy-Artifact plugin.

- Go to your Jenkins-Ansible server and create a new directory called `ansible-config-artifact` – we will store all artifacts after each build here.

`sudo mkdir /home/ubuntu/ansible-config-artifact`

- Change permissions to this directory, so Jenkins could save files there

`sudo chmod -R 0777 /home/ubuntu/ansible-config-artifact`

- Go to Jenkins web console -> Manage Jenkins -> Manage Plugins -> on Available tab search for Copy Artifact and install this plugin.

  
  <img width="1673" alt="copy-artifactplugin-inst" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/d5dba08b-4812-47a2-96f9-8f3fa8183e33">

  <img width="824" alt="copy-artifactplugin-inst1" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/e4738538-0be7-49b8-b657-e1cb82ce0d2c">


- Restart Jenkins if needed to make sure the plugin is functioning properly.

- Create a new Jenkins Freestyle project and name it `save_artifacts`.

This project will be triggered by completion of your existing ansible project. Configure it accordingly:

<img width="413" alt="save-arti-config" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/515e6490-982e-4c47-a0d8-953763cb7fdd">


Note: You can configure number of builds to keep in order to save space on the server, for example, you might want to keep only last 2 or 5 build results. You can also make this change to your ansible job.

![conf](https://github.com/travdevops/PBL-DevOps/assets/137777644/69f10f12-7171-4e8c-bfde-32597b5a11c5)


The main idea of `save_artifacts` project is to save artifacts into `/home/ubuntu/ansible-config-artifact` directory. To achieve this, 

- Create a Build step and choose Copy artifacts from other project, specify `ansible` as a source project and `/home/ubuntu/ansible-config-artifact` as a target directory.

  <img width="821" alt="save-arti-config2" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/4d0806b8-d6c7-49d7-a5e0-fe34dc786f45">

This setup makes the `ansible` Jenkins Job the Upstream Project and `save_artifact` the downstream project. 

- Test your set up by making some change in README.MD file inside your ansible-config-mgt repository (right inside main branch) or in another branch but merge the branch with main for the Jenkins build to be automatic.

<img width="640" alt="jenkinsbuild-upstream" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/d5c5e3df-ab0d-40e3-b8b1-af8ca9dca3d9">
<img width="749" alt="jenkinsbuild-dwnstream" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/12be0c54-2d98-4cb6-a9da-b7ed298db7d2">



If both Jenkins jobs have completed one after another – you shall see your files inside `/home/ubuntu/ansible-config-artifact` directory and it will be updated with every commit to your main branch. 

Now your Jenkins pipeline is more neat and clean.

### Step 2 – Refactor Ansible Code by Importing Other Playbooks into Site.yml
Before starting to refactor the codes, ensure that you have pulled down the latest code from (main) branch.

Let see code re-use in action by importing other playbooks.

Within playbooks folder, create a new file and name it `site.yml` – This file will now be considered as an entry point into the entire infrastructure configuration.

Other playbooks will be included here as a reference. In other words, (`site.yml` will become a parent to all other playbooks that will be developed) Including `common.yml` that you created previously.

- Create a new folder in root of the repository and name it `static-assignments`. The static-assignments folder is where all other children playbooks will be stored. 

This is merely for easy organization of your work. It is not an Ansible specific concept, therefore you can choose how you want to organize your work. 

- Move `common.yml` file into the newly created static-assignments folder.

- Inside `site.yml` file, import `common.yml` playbook.

      ---
      - hosts: all
      - import_playbook: /static-assignments/common. yml

The code above uses built in `import_playbook` Ansible module. 

- Your folder structure should look like this;

<img width="493" alt="tree ans-configmgt" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/ef12a82f-76bf-454e-849a-624c276bf73f">


- Run ansible-playbook command against the dev environment (dev.yml). 

<img width="1384" alt="playbook commonyml" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/aeb9dcd4-8207-4ef5-9e1f-b9432db084f8">


- Since you need to apply some tasks to your dev servers and wireshark is already installed – you can go ahead and create another playbook under static-assignments and name it common-del.yml. In this playbook, configure deletion of wireshark utility.


<img width="456" alt="common-delyml" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/233f6aa3-0ef6-45a7-986b-5a9fa46fe898">


- Update `site.yml` file with 

      - import_playbook: ../static-assignments/common-del.yml 
     
- Run it against dev environment:

      cd /home/ubuntu/ansible-config-artifact/
      ansible-playbook -i inventory/dev.yml playbooks/site.yml

<img width="1351" alt="playbook to remove wireshark" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/810ebd6b-b9e4-4a11-ac1f-b791f318ac45">


- Make sure that wireshark is deleted on all the servers by running wireshark --version

<img width="562" alt="wireshark removed" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/06377944-9f8f-45dc-a2a3-9dc70d77cae6">


Now you have learned how to use `import_playbooks` module and you have a ready solution to install/delete packages on multiple servers with just one command.

### Step 3 - Configure Uat Webservers With A Role Called Webserver
We have our nice and clean dev environment, so let us put it aside and configure 2 new Web Servers as uat . We could write tasks to configure Web Servers in the same playbook, but it would be too messy, instead, we will use a dedicated role to make our configuration reusable.

1. Launch 2 fresh EC2 instances using RHEL 9 image, we will use them as our uat servers (user-acceptance-testing). -Give them names accordingly - `Web1-UAT` and `Web2-UAT`.
2. To create a role, you must create a directory called `roles` in `ansible-config-mgt/` 

There are two ways how you can create this folder structure:

Opt 1. Use an Ansible utility called ansible-galaxy inside `ansible-config-mgt/roles` directory (you need to create roles directory upfront)

Opt 2. Create the directory/files structure manually.

### Tip: The first option is obviously the better option. 

    mkdir roles
    cd roles
    ansible-galaxy init webserver

<img width="749" alt="mkdir roles" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/eddfd8c8-71e8-49cb-b1b5-b91798343c80">


The entire folder structure should look like below

<img width="637" alt="tree webserver-before" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/2d27f2c8-4c21-469c-be2e-d53aa64fa18d">

We won't be needing some of the directories and files initialized by ansible-galaxy. Namely - tests, files and vars

The entire folder structure should look like below after deleting tests, files and vars

<img width="646" alt="tree webserver-after" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/6a2a44e9-19ac-4325-b1d2-2177be18e59d">

3. Update your inventory `ansible-config-mgt/inventory/uat.yml` file with IP addresses of your 2 UAT Web servers

<img width="493" alt="uatyml" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/c5422784-1539-4d3c-9924-e98fee3f62e4">


### NOTE: Ensure you apply the concept of ssh-agent to ssh into the Jenkins-Ansible instance and establish communication UAT Servers;

4. In `/etc/ansible/ansible.cfg` file, uncomment `roles_path` string and provide a full path to your roles directory `roles_path = /home/ubuntu/ansible-
config-mgt/roles`,so Ansible could know where to find configured roles.

In some other cases, the `ansible.cfg` might not create automatically following the installation on the server, If that's the case. 

- Create ansible.cfg manually with `touch ansible.cfg` on any preferred location and specificy the `roles_path` inside it

`roles_path = /home/ubuntu/ansible-config-mgt/roles`

<img width="543" alt="ansconfig-rolespath" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/b2ef0d86-5ac1-4d91-84c1-9cab0ab3327f">

5. It is time to start adding some logic to the webserver role.

- Go into tasks directory, and within the `main.yml` file, start writing configuration tasks to do the following:

      - Install and configure Apache ( httpd service)
      - Clone Tooling website from GitHub https://github.com/<your-name>/tooling-git
      - Ensure the tooling website code is deployed to /var/www/html on each of 2 UAT Web servers.
      - Make sure httpd service is started


Your `main.yml` may consist of following tasks:

<img width="499" alt="roles tasks mainyml" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/aa9e7adb-30b4-41fc-abba-b6acd98c91cb">

### Step 4 - Reference 'Webserver' role

Within the static-assignments folder, create a new assignment for uat-webservers `uat-webservers. yml`. This is where you will reference the role.

<img width="326" alt="uat-webserveryml" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/6dc48662-6d64-4773-a55a-a5a2d71d5e02">

- Remember that the entry point to our ansible configuration is the site.yml file. Therefore, you need to refer your `uat-webservers.yml` role inside `site.yml`.

- So, we should have this in `site. yml`

<img width="540" alt="siteyml" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/574efa4d-03b5-473f-88fa-fc274e3eba73">

### Step 5 - Commit & Test

- Commit your changes, create a Pull Request and merge them to main branch on github

<img width="955" alt="git merge-dev main" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/f813a6fe-16b7-486e-92fc-3e10e77d33a0">


- Make sure webhook triggered two consequent Jenkins jobs (ansible & save_artifact).
- Make sure they ran successfully and copied all the files to your Jenkins-Ansible server into `/home/ubuntu/ansible-config-artifact/` directory.

Now. FINALLY. Run your Ansible Playbook from the `/home/ubuntu/ansible-config-artifact/` directory. 

<img width="1498" alt="end of ans-refac" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/e8af4a0a-0ba8-45a5-a95f-811bff0bef3d">

- You should be able to see both of your UAT Web servers configured and you can try to reach them from your browser:

http://<Web1-UAT-Server-Public-IP>/index.php

http://<Web2-UAT-Server-Public-IP>/index.php

### Tip: Make sure you have TCP Port 80 open in the security group for both servers.

- The result: 

<img width="1429" alt="Screenshot 2023-11-10 at 1 08 19 AM" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/a4342b93-fc40-4bf4-9720-1709e8616717">


<img width="1464" alt="Screenshot 2023-11-10 at 1 10 14 AM" src="https://github.com/travdevops/PBL-DevOps/assets/137777644/ffca6b3c-f883-4d88-b801-3ea9fec0e868">
