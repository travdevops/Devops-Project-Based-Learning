# PROJECT ANSIBLE
### ANSIBLE-REFACTORING
### ANSIBLE-ASSIGNMENTS
### ANSIBLE-IMPORTS 

## ANSIBLE REFACTORING AND STATIC ASSIGNMENTS (IMPORTS AND ROLES)

Side Self Study: For better understanding or Ansible artifacts re-use – [read this article](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse.html).

Code Refactoring

Refactoring is a general term in computer programming. It means making changes to the source code without changing expected behaviour of the software. The main idea of refactoring is to enhance code readability, increase maintainability and extensibility, reduce complexity, add proper comments without affecting the logic. In this case, you will move things around a little bit in the code, but the overal state of the infrastructure remains the same. Let us see how you can improve your Ansible code!

### Step 1 – Jenkins Job Enhancement

Before we begin, let us make some changes to our Jenkins job – now every new change in the codes creates a separate directory which is not very convenient when we want to run some commands from one place. Besides, it consumes space on Jenkins serves with each subsequent change. Let us enhance it by introducing a new Jenkins project/job – we will require Copy Artifact plugin.

Go to your Jenkins-Ansible server and create a new directory called ansible-config-artifact – we will store there all artifacts after each build.

`sudo mkdir /home/ubuntu/ansible-config-artifact`

Change permissions to this directory, so Jenkins could save files there
`sudo chmod -R 0777 /home/ubuntu/ansible-config-artifact`

Go to Jenkins web console -> Manage Jenkins -> Manage Plugins -> on Available tab search for Copy Artifact and install this plugin.

Restart Jenkins if needed to make sure the plugin is functioning properly.

Create a new Freestyle project and name it `save_artifacts`.

This project will be triggered by completion of your existing ansible project. Configure it accordingly:

Note: You can configure number of builds to keep in order to save space on the server, for example, you might want to keep only last 2 or 5 build results. You can also make this change to your ansible job.

The main idea of save_artifacts project is to save artifacts into `/home/ubuntu/ansible-config-artifact` directory. To achieve this, create a Build step and choose Copy artifacts from other project, specify ansible as a source project and `/home/ubuntu/ansible-config-artifact` as a target directory.

Test your set up by making some change in README.MD file inside your ansible-config-mgt repository (right inside main branch) or in another branch but merge the branch with main for the Jenkins build to be automatic.

If both Jenkins jobs have completed one after another – you shall see your files inside `/home/ubuntu/ansible-config-artifact` directory and it will be updated with every commit to your main branch. Now your Jenkins pipeline is more neat and clean.

### REFACTOR ANSIBLE CODE BY IMPORTING OTHER PLAYBOOKS INTO SITE.YML

Step 2 – Refactor Ansible code by importing other playbooks into **site.yml**

Before starting to refactor the codes, ensure that you have pulled down the latest code from (main) branch.

Let see code re-use in action by importing other playbooks.

Within playbooks folder, create a new file and name it site.yml – This file will now be considered as an entry point into the entire infrastructure configuration.

Other playbooks will be included here as a reference. In other words, (site.yml will become a parent to all other playbooks that will be developed)

Including common.yml that you created previously.

Create a new folder in root of the repository and name it static-assignments. The static-assignments folder is where all other children playbooks will be stored. 

This is merely for easy organization of your work. It is not an Ansible specific concept, therefore you can choose how you want to organize your work. You will see why the folder name has a prefix of static very soon.

Move common.yml file into the newly created static-assignments folder.

Inside site.yml file, import common.yml playbook.

The code above uses built in import_playbook Ansible module. 

Your folder structure should look like this;

Run ansible-playbook command against the dev environment (dev.yml). 

Since you need to apply some tasks to your dev servers and wireshark is already installed – you can go ahead and create another playbook under static-assignments and name it common-del.yml. In this playbook, configure deletion of wireshark utility.

Update site.yml file with 

     - import_playbook: ../static-assignments/common-del.yml 
     
instead of common.yml and run it against dev servers:

cd /home/ubuntu/ansible-config-artifact/

ansible-playbook -i inventory/dev.yml playbooks/site.yml

Make sure that wireshark is deleted on all the servers by running wireshark --version

Now you have learned how to use import_playbooks module and you have a ready solution to install/delete packages on multiple servers with just one command.

### CONFIGURE UAT WEBSERVERS WITH A ROLE called WEBSERVER