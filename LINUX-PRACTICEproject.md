
# Introduction to Linux and Basic Commands

#### A command is a program that or utility that runs on the CLI and interacts with the system via texts and processes.


# _sudo_ command 

- superuser do, `sudo` is one of the most common Linux commands that lets you perform tasks that require administrative or root permissions.

For example 

`sudo apt update`

Updates apt packages in the server. 

<img width="961" alt="sudo" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/41a6c6d8-33b8-40db-8229-43e97b712cea">




# _pwd_ command

to find the path of your current working directory


<img width="469" alt="pwd" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/a089c7c1-6e65-4122-97d1-e2fe706ec60e">






# _cd_ command 

To navigate through the Linux files and directories,

`_cd .._`  moves one directory up.

`_cd -_`   moves to your previous directory.


<img width="538" alt="cd" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/3829140d-ffd1-4c82-be7b-0bbfee124fe8">



 
 
# _ls_ command


The `ls` command lists files and directories within a system.
Running it without a flag or parameter will show the current working directory’s content.


`ls -R` lists all the files in the subdirectories.
	•	`ls -a` shows hidden files in addition to the visible ones.
	•	`ls -lh` shows the file sizes in easily readable formats, such as MB, GB, and TB


<img width="507" alt="ls" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/a518df35-b68c-425a-99d6-a6d1a5ad8c35">






# _cat_ command 
(Concatenate)  this command lists, combines, and writes file content to the standard output

`cat > filename.txt` creates a new file called filename.txt

`cat filename1.txt filename2.txt filename3.txt` creates multiple files at once 
 
`cat filename1.txt filename2.txt > filename3.txt` merges filename1.txt and filename2.txt and stores the output in filename3.txt.

 
<img width="849" alt="cat" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/df24daf8-746e-48c8-ad8a-d5c166246070">



`tac` filename3.txt displays content in reverse order.



<img width="826" alt="tac" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/fe442c97-9e0c-45fe-9e50-8d43bb9d8cb8">


# _cp_ command

Use the `cp` command to copy files or directories and their content.

To copy one file from the current directory to another, enter `cp` followed by the file name and the destination directory.



<img width="472" alt="cp" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d1446979-ac4c-4312-af26-55dfe134df4a">



To copy files to a directory, enter the file names followed by the destination directory:



<img width="861" alt="cp multiple files" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/86956295-8db1-411b-a428-d47cb6229b1e">



to copy an entire directory, use `-R` flag followed by the destination directory


<img width="533" alt="cp -R" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/01c8dc29-6f9a-465b-b349-2bb8438d422f">





# _mv_ command


The primary use of the mv command is to move and files and directories.

Simply type `mv` followed by the filename and the destination directory. 


<img width="447" alt="mv move" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/31eda491-1adb-43d1-810a-9368bf3f3b3e">



You can also use the mv command to rename a file:

In the working directory, type `mv` followed by the filename and the new filename you want to rename to.


<img width="419" alt="mv rename" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/b42440ad-2475-4a1a-b807-9fee6fde8d7d">





# _mkdir_ command

Use the `mkdir` command to create one or multiple directories at once and set permissions for each of them.

Here’s the basic syntax:
`mkdir`  directory_name

For example, you want to create a directory called music:

`mkdir music`

To make a new directory called songs inside music, use this command:

`mkdir music/songs`

`-p` or `–parents` create a directory between two existing folders.

For example, `mkdir -p music/2023/songs` will make the new “2020” directory.


<img width="363" alt="mkdir" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ae0b65e0-3ef6-4ec8-846b-51b39585965d">






# _rmdir_ command

To permanently delete an empty directory, use the rmdir command. 

`rmdir` directory_name

For example, you want to remove an empty subdirectory named music/songs 



<img width="481" alt="rmdir" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/7cd0eac1-d91a-4afc-910c-22d3d5f24ba6">


 
 
 # _rm_ command

 this command is used to delete files within a directory.

`rm filename`


To remove multiple files, enter the following command:

`rm filename1 filename2 filename3`

<img width="655" alt="rm" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/80e144c0-a7d7-406b-acd6-01ce698b110f">



rm with flags

 `-i` prompts system confirmation before deleting a file.
 
<img width="538" alt="rm -i" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/8ee9b801-00d9-4b0d-bb72-80d7e42f4abd">

 

`-f` allows the system to remove without a confirmation.
 
<img width="445" alt="rm -f" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/79c215cb-16b1-4c62-bf02-75fab62d6166">



`-r` deletes files and directories recursively.
 


<img width="555" alt="rm -r" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/49e7e814-2b15-4ffc-b4b0-1dd11741c07b">



# _touch_ command


The `touch` command allows you to create an empty file or generate and modify a timestamp in the Linux command line.

`touch sqlitecommands.sh`


<img width="545" alt="touch" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/227cbf80-739b-4d17-9771-1b870bf7574a">



# _locate_ command

The `locate` command can find a file in the database system.

Moreover, adding the `-i` argument will turn off case sensitivity, so you can search for a file even if you don’t remember its exact name.



<img width="396" alt="locate" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ce844267-1938-439f-b2c3-b1f4f7fbd4db">




# _find_ command

Use the `find` command to search for files within a specific directory and perform subsequent operations. 

`find -name` filename to find files in the current directory.


<img width="818" alt="find" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/f71776c3-975a-48da-9750-da1293c54326">




# _grep_ command

Another basic Linux command on the list is grep or global regular expression print. It lets you find a word by searching through all the texts in a specific file.



<img width="640" alt="grep" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e19c422a-eaf8-4443-b3b6-5066965a79f3">



# _df_ command 

 used to view disk space shown in Kilobytes format

**syntax** - `df` [current working directory/ path to another directory]



<img width="498" alt="Screenshot 2023-08-16 at 5 45 35 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/8c4f8524-7e45-4dee-b0ac-b44cf8cb5ea3">







# _du_ command 

 to check how much space a file / directory takes up 




<img width="745" alt="du" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/8c242242-163c-4b52-b24f-6130790eae09">




# _head_ command


The `head` command allows you to view the first ten lines of a text. Adding an option lets you change the number of lines shown.


`head` filename


For instance, you want to view the first ten lines of note.txt, located in the current directory:


Below are some options you can add.

       `-n` or `–lines` prints the first customised number of lines. For example, enter head -n devops-file.txt to show the first five lines of filename.txt.
    
    `-q` or `–quiet` will not print headers specifying the file name.



<img width="730" alt="head" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/440ad8d3-6c0c-49c4-af30-e7faf35f76b7">



# _tail_ command

The `tail` command displays the last ten lines of a file. It allows users to check whether a file has new data or to read error messages.


`tail` filename

For example, you want to show the last 3 lines of the **devops-file.txt** file:

`tail -n 3` **devops-file.txt**



<img width="579" alt="tail" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/fd379216-6cde-4ecf-8188-1270e6eb2f7d">






# _diff_ command

Short for difference, the `diff` command compares two contents of a file line by line. After analyzing them, it will display the parts that do not match.

`diff`  file1 file2

For example, you want to compare two text files – **devops-file.txt** and **devops-file1.txt**

`diff **devops-file.txt** and **devops-file1.txt**`


<img width="672" alt="diff" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/f3910665-3ba9-4c3e-ac95-6b596b7debc8">




# _tar_ command

The `tar` command archives multiple files into a TAR file – a common Linux format similar to ZIP, with optional compression.


For instance, you want to create a new TAR archive named newarchive.tar in the /ubuntu/commandlinux directory:

`tar -cvf newarchive.tar /ubuntu/commandlinux`


<img width="753" alt="tar" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/901dfcb6-6a9f-4726-aefc-44a171060489">




# _chown_ command

The `chown` command lets you change the ownership of a file, directory, or symbolic link to a specified username.

synthax 

`chown` [group] [filename]



# _jobs_ command

A `job` is a process that the shell starts. The jobs command will display all the running processes along with their statuses.


# _kill_ command


Use the `kill` command to terminate an unresponsive program manually. It will signal misbehaving applications and instruct them to close their processes.


To `kill` a program, you must know its process identification number (PID). If you don't know the PID, run the following command:
Copy Below Code

`ps ux`


<img width="760" alt="Screenshot 2023-08-16 at 11 52 05 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/6c16996d-9272-4926-9f1c-5f059d547911">


After knowing what signal to use and the program's PID, enter the following syntax:

`kill` [signal_ option] pid




# _ping_ command

The `ping` command is one of the most used basic Linux commands for checking whether a network or a server is reachable.

syntax: 

`ping` [option] [hostname or IP address]

For example, you want to know whether you can connect to Google and measure its response time:

`ping google.com`


<img width="490" alt="Screenshot 2023-08-16 at 11 56 17 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c100d3d1-175c-4618-876c-d12979556ae0">




# _wget_ command

`wget` Linux command line lets you download files from the internet using the `wget` command.


The `wget` command retrieves files using HTTP, HTTPS, and FTP protocols. It can perform recursive downloads, which transfer website parts by following directory structures and links, creating local versions of the web pages.

`wget` [option] [url]



# _uname_ command

The `uname` or unix name command will print detailed information about your Linux system and hardware.

syntax:

`uname` 

`uname -a`


<img width="492" alt="Screenshot 2023-08-17 at 12 01 11 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/83d7076d-154a-44f5-83f6-2f042db9803e">


# _top_ command


The `top` command in Linux Terminal will display all the running processes and a dynamic real-time view of the current system.

The `top` command can also help you identify and terminate a process that may use too many system resources.

`top`


<img width="962" alt="Screenshot 2023-08-17 at 12 03 52 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/bbcf78db-db1a-4f86-a68c-d19f21293e29">



# _history_ command:

With history, the system will list up to 500 previously executed commands, allowing you to reuse them without re-entering.

Only users with sudo privileges can run this command.

`sudo history`



# _man_ command


The `man` command provides a user manual of any commands or utilities you can run in Terminal, including the name, description, and options.


For example, you want to access the manual for the ls command:

`man ls`




# _echo_ command

The `echo` command is a built-in utility that displays a line of text or string using the standard output.

syntax:

`echo` string


# _zip_, _unzip_ commands

Use the `zip` command to compress your files into a ZIP file, a universal format commonly used on Linux.

The `zip` command is also useful for archiving files and directories and reducing disk usage.

For example, you have a file named scotty.txt that you want to compress into archive.zip in the current directory:


`zip archive.zip scotty.txt`

<img width="366" alt="Screenshot 2023-08-17 at 12 22 45 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/28c82373-9c7f-45eb-9c18-a45d086f747d">


So, to `unzip` the file called archive.zip in the current directory, enter:

`unzip archive.zip scotty.txt`


<img width="547" alt="Screenshot 2023-08-17 at 12 25 00 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/e18a1b35-cc54-448a-9f8e-a319d892c487">





# _hostname_ command

Run the `hostname` command to know the system's hostname. You can execute it with or without an option.

`hostname`

`hostname -i` - displays the machine's IP address.

`hostname -a` - -a or -alias displays the hostname's alias.



# _useradd_ command

`useradd` is used to create a new account, while the **passwd** command allows you to add a password. Only those with root privileges or sudo can run the useradd command.

When you use the `useradd` command, it performs some major changes:

- Edits the /etc/passwd, /etc/shadow, /etc/group, and /etc/gshadow files for the newly created accounts.

- Creates and populates a home directory for the user.

- Sets file permissions and ownerships to the home directory.

-   Here's the basic syntax:

`useradd` [option] username

set password

`passwd` [password combination] 




# _userdel_ command

To delete a user account, use the `userdel` command:

`userdel` username





# _apt-get_ command


`apt-get` is a command line tool for handling  ***Advanced Package Tool*** (APT) libraries in Linux. 

It lets you retrieve information and bundles from authenticated sources to manage, update, remove, and install software and its dependencies.


Running the ***apt-get*** command requires you to use sudo or root privileges.

for example


`sudo apt get`

`apt get install mlocate` - to install the locate command package files



# _nano_, _vi_, _jed_ commands

these are text editors used to edit and manage files, `nano` and `vi` come with the operating system, while `jed` has to be installed.


The `nano` command denotes keywords and can work with most languages.

`nano` filename


`vi` uses two operating modes to work - insert and command. 

insert is used to edit and create a text file.

On the other hand, the command performs operations, such as saving, opening, copying, and pasting a file.

`vi` or `vim` filename 


`jed` has a drop-down menu interface that allows users to perform actions without entering keyboard combinations or commands.




# _alias_, _unalias_ commands



`alias` allows you to create a shortcut with the same functionality as a command, file name, or text. When executed, 

it instructs the shell to replace one string with another.


`alias` Name=string

for example - `alias where=pwd`


<img width="326" alt="Screenshot 2023-08-17 at 1 06 20 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/0f8b16f5-e218-4cc8-803c-6654e56e8a55">


On the other hand, the `unalias` command deletes an existing alias.

`unalias where`


<img width="380" alt="Screenshot 2023-08-17 at 1 07 01 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/bc556c47-914e-465e-8cc3-c1d0aa1c1cc2">


# _su_ command
    
The switch user or `su` command allows you to run a program as a different user. 

It changes the administrative account in the current log-in
session.

When executed without any option or argument, the su command runs through root privileges. It will prompt you to authenticate and use the
sudo privileges temporarily.

`-p` or -preserve-environment keeps the same shell environment, consisting HOME, SHELL, USER, and LOGNAME. 

`-s` or -shell lets you specify a different shell environment to run.

`-|` or -login runs a login script to switch to a different username. Executing it requires you to enter the user's password.




# _htop_ command

The `htop` command is an interactive program that monitors system resources and server processes in real time.

`htop` [options]




# _ps_ command

The process status or `ps` command produces a snapshot of all running processes in your system.


`-T` displays all processes associated with the current shell session.

`-u` username lists processes associated with a specific user. 

`-A` or `-e` shows all the running processes
