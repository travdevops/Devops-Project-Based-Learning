
# Introduction to Linux and Basic Commands

#### A command is a program that or utility that runs on the CLI and interacts with the system via texts and processes.


**sudo** command > superuser do, sudo is one of the most common Linux commands that lets you perform tasks that require administrative or root permissions.

For example 

`sudo apt update`

Updates apt packages in the server. 

<img width="961" alt="sudo" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/41a6c6d8-33b8-40db-8229-43e97b712cea">




pwd command to find the path of your current working directory


<img width="469" alt="pwd" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/a089c7c1-6e65-4122-97d1-e2fe706ec60e">



cd command = To navigate through the Linux files and directories,
	•	cd .. moves one directory up.
	•	cd- moves to your previous directory.


<img width="538" alt="cd" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/3829140d-ffd1-4c82-be7b-0bbfee124fe8">



 ls command
The ls command lists files and directories within a system.
Running it without a flag or parameter will show the current working directory’s content.


ls -R lists all the files in the subdirectories.
	•	ls -a shows hidden files in addition to the visible ones.
	•	ls -lh shows the file sizes in easily readable formats, such as MB, GB, and TB


<img width="507" alt="ls" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/a518df35-b68c-425a-99d6-a6d1a5ad8c35">


cat command - (Concatenate) 
Cat command lists, combines, and writes file content to the standard output

	•	cat > filename.txt creates a new file.
 
	•	cat filename1.txt filename2.txt > filename3.txt merges filename1.txt and filename2.txt and stores the output in filename3.txt.

 
<img width="849" alt="cat" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/df24daf8-746e-48c8-ad8a-d5c166246070">


tac filename3.txt displays content in reverse order.

<img width="826" alt="tac" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/fe442c97-9e0c-45fe-9e50-8d43bb9d8cb8">


cp command
Use the cp command to copy files or directories and their content.
To copy one file from the current directory to another, enter cp followed by the file name and the destination directory.


<img width="472" alt="cp" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d1446979-ac4c-4312-af26-55dfe134df4a">

To copy files to a directory, enter the file names followed by the destination directory:

<img width="861" alt="cp multiple files" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/86956295-8db1-411b-a428-d47cb6229b1e">



to copy an entire directory, use -R flag followed by the destination directory


<img width="533" alt="cp -R" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/01c8dc29-6f9a-465b-b349-2bb8438d422f">


mv command
The primary use of the mv command is to move and files and directories.

Simply type mv followed by the filename and the destination directory. 

<img width="447" alt="mv move" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/31eda491-1adb-43d1-810a-9368bf3f3b3e">



You can also use the mv command to rename a file:

In the working directory, type mv followed by the filename and the new filename you want to rename to.


<img width="419" alt="mv rename" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/b42440ad-2475-4a1a-b807-9fee6fde8d7d">




mkdir command
Use the mkdir command to create one or multiple directories at once and set permissions for each of them.

Here’s the basic syntax:
mkdir [option] directory_name
For example, you want to create a directory called music:
mkdir Music
To make a new directory called songs inside music, use this command:
mkdir music/songs

-p or –parents create a directory between two existing folders.

For example, mkdir -p music/2023/songs will make the new “2020” directory.


<img width="363" alt="mkdir" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/ae0b65e0-3ef6-4ec8-846b-51b39585965d">


rmdir command
To permanently delete an empty directory, use the rmdir command. 

rmdir [option] directory_name

For example, you want to remove an empty subdirectory named music/songs 














