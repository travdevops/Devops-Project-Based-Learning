# PROJECT ON - DEVOPS TOOLING WEBSITE SOLUTION

## Side Self Study
Read about Network-attached storage (NAS), Storage Area Network (SAN) and related protocols like NFS, (s)FTP, SMB, and iSCSI. 
Explore what Block-level storage is and how it is used by Cloud Service providers, and know the difference from Object storage.
On the example of AWS services understand the difference between Block Storage, Object Storage and Network File System.

## Setup and technologies used
As a member of a DevOps team, you will implement a tooling website solution which makes access to DevOps tools within the corporate infrastructure easily accessible.

In this project you will implement a solution that consists of following components:
1.	Infrastructure: AWS
2.	Webserver Linux: One Red Hat Enterprise Linux 9
3.	Database Server: One Ubuntu 22.04 + MySQL
4.	Storage Server: One Red Hat Enterprise Linux 9 + NFS Server
5.	Programming Language: PHP
6.	Code Repository: GitHub

- To determine the suitable storage solution, we need to consider what data will be stored, its format, how it will be accessed, by whom, from where, and how frequently. This will help us choose the right storage system for our solution.

  
### STEP 1 – PREPARE NFS SERVER

Spin up a new EC2 instance with RHEL Linux 9 Operating System.
Based on your LVM experience from Project 6, Configure LVM on the Server.
But, We will repeat the configuration on this project for more clarification. 

# Configuring Logical Volumes. 
- On AWS, Create 3 volumes in the same Availability zones as your Web Server EC2, each of 10 GiB.
- Inspect your newly created volumes with viewing the files in /dev directory > `ls /dev`

![ls-dev](https://github.com/travdevops/darey.io-pbl/assets/137777644/17c4efa3-17dc-41cc-91f7-d63409e5eaa3)

- Use lsblk command to inspect what block devices are attached to the server.

![lsblk](https://github.com/travdevops/darey.io-pbl/assets/137777644/9324e037-dec9-4136-9b05-59f7051bafc0)

Use gdisk utility to create a single new partition on each of the 3 disks and write the partitions.

`sudo gdisk /dev/xvdf` for the first partition

![sudo gdisk](https://github.com/travdevops/darey.io-pbl/assets/137777644/0f653e4f-7684-4ba5-a863-c881891edf7f)


Confirm the partitions > `lsblk`

![lsblk2](https://github.com/travdevops/darey.io-pbl/assets/137777644/982981ba-f0b6-4c95-9fae-3c044cf3163b)



Install _lvm2_ package using `sudo yum install lvm2`. 
Run `sudo lvmdiskscan` command to check for available partitions.

![lvmdiskscan](https://github.com/travdevops/darey.io-pbl/assets/137777644/884d70d0-d3c0-48ba-9186-540e158346c9)


Use _pvcreate_ utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM

    sudo pvcreate /dev/xvdf1
    sudo pvcreate /dev/xvdg1
    sudo pvcreate /dev/xvdh1

![pvcreate](https://github.com/travdevops/darey.io-pbl/assets/137777644/070b5380-116d-4acb-b7e6-96c83244de33)

Verify that your Physical volume has been created successfully by running `sudo pvs`

![pvs](https://github.com/travdevops/darey.io-pbl/assets/137777644/e5842bae-fbae-4c87-8355-0c3c614a44bb)


Use _vgcreate_ utility to add all 3 Physical Volumess to a Volume Group (VG). Name the VG **webdata-vg**

`sudo vgcreate webdata-vg /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`

Verify that your VG has been created successfully by running `sudo vgs`

![vgcreate](https://github.com/travdevops/darey.io-pbl/assets/137777644/ab468ce0-d8fc-43e2-8736-35036478572d)

Use _lvcreate_ utility to create 3 logical volumes. Namely **lv-opt**, **lv-apps** and **lv-logs**

Instead of formating the disks as _ext4_ as we did in the previous project, you will use _xfs_

    sudo lvcreate -n lv-opt -L 9G webdata-vg
    sudo lvcreate -n lv-apps -L 9G webdata-vg
    sudo lvcreate -n lv-logs -L 9G webdata-vg

![lvcreate](https://github.com/travdevops/darey.io-pbl/assets/137777644/56b7c2cc-8855-4fdb-bf03-96e2e3b4ca27)

Verify that your Logical Volumes has been created successfully by running `sudo lvs`


![lvs](https://github.com/travdevops/darey.io-pbl/assets/137777644/62b40395-4135-44c4-b27b-1a259adb7009)

Verify the LVs Setups 

![lsblk3](https://github.com/travdevops/darey.io-pbl/assets/137777644/d340aa88-b5e1-444b-a744-c9ad8ce6efdc)


- Use mkfs.xfs to format the logical volumes with xfs filesystem

    sudo mkfs -t xfs /dev/webdata-vg/lv-opt /mnt/opt
    sudo mkfs -t xfs /dev/webdata-vg/lv-apps /mnt/apps
    sudo mkfs -t xfs /dev/webdata-vg/lv-logs /mnt/logs

- Create mount points on /mnt directory for the logical volumes as follows:
   - lv-opt - /mnt/opt
   - lv-apps - /mnt/apps
   - lv-logs - /mnt/logs

- Make the mount directories > `sudo mkdir /mnt/opt /mnt/apps /mnt/logs`

![mkdir mnt etc](https://github.com/travdevops/darey.io-pbl/assets/137777644/12e2b886-db10-46c1-ab57-e94394bf1a75)


- Mount the LVs on the directories
    - sudo mount /dev/webdata-vg/lv-opt /mnt/opt
    - sudo mount /dev/webdata-vg/lv-apps /mnt/apps
    - sudo mount /dev/webdata-vg/lv-logs /mnt/logs


Verify the Mountpoints with `lsblk`

![mountpoints](https://github.com/travdevops/darey.io-pbl/assets/137777644/980bcef6-b2d0-40b6-8dfc-de0356d27e0b)

Update **/etc/fstab** file so that the mount configuration will persist after restart of the server. The UUID of the mounted Logical volumes device will be used to update the /etc/fstab file. Use `sudo blkid` command to get the UUID information for the device

![blkid](https://github.com/travdevops/darey.io-pbl/assets/137777644/b16dffdc-0a38-472f-90d6-44adde29aeaf)

Update /etc/fstab in this format using your own UUID.

`sudo nano /etc/fstab`

![nano fstab](https://github.com/travdevops/darey.io-pbl/assets/137777644/6d44c7c7-2a4a-4e72-a50f-46b065150bdb)

- Test the configuration and reload the daemon

      sudo mount -a
      sudo systemctl daemon-reload
  
- Verify your setup by running df -h, output must look like this

![mount-daemon](https://github.com/travdevops/darey.io-pbl/assets/137777644/40974386-587a-4ecf-ae88-e0ff4e1a1b45)


# Install NFS server
- Configure it to start on reboot and make sure it is up and running

      sudo yum -y update
      sudo yum install nfs-utils -y
      sudo systemctl start nfs-server.service
      sudo systemctl enable nfs-server.service
      sudo systemctl status nfs-server.service


![nfs service](https://github.com/travdevops/darey.io-pbl/assets/137777644/caeb6a0e-f625-4aed-9ff9-60b7f51c18ba)


Export the mounts for webservers **subnet cidr** to connect as clients. 
(For simplicity, you will install your all three Web Servers inside the same subnet, but in production set up you would probably want to separate each tier inside its own subnet for higher level of security.)
To check your subnet cidr – open your EC2 details in AWS web console and locate ‘Networking’ tab and open a Subnet link

<img width="1198" alt="Screenshot 2023-10-19 at 3 56 00 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/9d3d869b-9b6e-4a8b-8c55-788722ea9b7d">      <img width="1151" alt="Screenshot 2023-10-19 at 3 55 27 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/eece81c4-ba26-41bb-bb62-f07c48947f13">


Make sure we set up permission that will allow our Web servers to read, write and execute files on NFS:

    sudo chown -R nobody: /mnt/apps
    sudo chown -R nobody: /mnt/logs
    sudo chown -R nobody: /mnt/opt

    sudo chmod -R 777 /mnt/apps
    sudo chmod -R 777 /mnt/logs
    sudo chmod -R 777 /mnt/opt

    sudo systemctl restart nfs-server.service
  
  
Configure access to NFS for clients within the same subnet (example of Subnet CIDR – 172.31.0.0/20 )

`sudo vi /etc/exports`

Put in the Subnet CIDR.

![subnet-export](https://github.com/travdevops/darey.io-pbl/assets/137777644/20fac347-f025-4c14-9d3e-73f1ee534285)

Save the file.
`sudo exportfs -arv`


Check the ports which port is used by NFS > `rpcinfo -p | grep nfs`

![rpcinfo](https://github.com/travdevops/darey.io-pbl/assets/137777644/b23e33e6-f472-4c80-a684-0bf20548d3c1)

Important note: In order for NFS server to be accessible from your client servers (DB server and Other servers), you must also open following ports: TCP 111, UDP 111, UDP 2049 and set them all to be accessible from the Subnet CIDR – 172.31.0.0/20

<img width="1322" alt="securitygroup-subnet" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/7a16e9f4-0068-40d3-9aa8-6f49880b66a9">


### STEP 2 – PREPARE & CONFIGURE DATABASE SERVER

- Install MySQL server > `sudo yum install mysql-server -y`
- Log into Mysql console > `sudo mysql`
- Create a database and name it tooling > `create database tooling;`
- Create a DB User named webaccess create user > `create user 'webaccess'@'172.31.0.0/20 identified by 'mypass';`
- Grant permission to webaccess user on tooling database to do anything only from the webservers subnet cidr > `grant all on tooling.* to
'webaccess'0'172.31.0.0/20';`

![mysql-tooling](https://github.com/travdevops/darey.io-pbl/assets/137777644/01fb2e2f-046a-4a43-bb72-840060ad1e30)

![mysql](https://github.com/travdevops/darey.io-pbl/assets/137777644/e3fe96bb-8bbc-415f-b566-19b3131f9ca4)







