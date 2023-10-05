# Web Solutions With WordPress
- We will be Setting up storage infrastructure on a Red-Hart Linux server.


[WordPress](https://wordpress.com/) is indeed a free and open-source CMS written in **PHP**, and it works well with **MySQL** or **MariaDB** as the backend RDBMS. 
- Using WordPress for a basic web solution is a great choice.


This Project Consists of the 2 parts. 
  - 1. Configure storage subsystem for Web and Database servers based on Linux OS.
  - 2. Install WordPress and connect it to a remote MySQL database server.
   
### Step 1 — Prepare a Web Server
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

    

