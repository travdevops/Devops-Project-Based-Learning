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

![sudo gdisk](https://github.com/travdevops/darey.io-pbl/assets/137777644/d4119847-35de-472e-a553-dcc9acecf0ae)

Confirm the partitions > `lsblk`

![lsblk2](https://github.com/travdevops/darey.io-pbl/assets/137777644/6af0bca7-d487-4d6c-8a41-ac9348a75b04)


Install _lvm2_ package using `sudo yum install lvm2`. 
Run `sudo lvmdiskscan` command to check for available partitions.

![lvmdiskscan](https://github.com/travdevops/darey.io-pbl/assets/137777644/7837d576-5447-4477-9427-685f849629a3)

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

