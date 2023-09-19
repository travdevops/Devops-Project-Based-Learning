# Intro to SHELL-SCRIPTING & USER-INPUT
* Shell scripting is a super handy way to automate tasks using commands in a Unix/Linux shell. 

* Shell scripting basically deals with writing a series of commands in a text file that can be executed in a shell.

* Shell scripting allows automation of repetitive tasks, perform system administration tasks, and create complex workflows. 

* Shell scripting Uses variables, loops, conditionals, and functions to make your scripts more powerful and flexible. 
* It's a great skill to have as a DevOps Engineer, as it can help you streamline processes and save time.

## SS (Shell Scripting) Syntax.

* Working with **Variables**: Variables can store data of various types such as numbers, strings, and arrays. You can assign values to variables using the = operator, and access their values using the variable name
preceded by a $ sign.

   - Assigning value to a variable: name="John" 
   - Retrieving value from a variable: echo $name

 * Working with **Control Flow**: These statements allow you to make decisions, iterate over lists, and execute different
commands based on conditions. Statements like *if-else* for loops, and and case statements to control the flow of execution in your scripts.

* Using if-else to execute scripts on different conditions. 
* This code asks you to enter a number and then displays whether it's positive or negative.
  <img width="612" alt="if-else" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/77332030-f7f1-4bff-b292-f725a6f0d856">

* The result on the local machine is as follows.

<img width="387" alt="if-else2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/f4abde1e-cbc6-4324-ba99-c9eb52126866">



* Using as a loop to create a list
  <img width="643" alt="scripts-loop1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/55e0be32-0571-40ab-8312-86196eda9c3e">

* The result on the local machine is as follows.
<img width="360" alt="script-loop2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/2555bdc5-d560-4abe-93c1-772373a6cc52">


## USER INPUT
* **Input and Output**: Bash provides various ways to handle input and output. 
* You can use the read command to accept user input, and output text to the console using the echo command.
* Additionally, you can redirect input and output using
some operators.
* Example - Accept User Input:
  - `echo "Enter your name:"`
  - `read name`
* Example - Output text to terminal:
  - `echo "Hello World"`
* Example - Out the result into a file
  - `echo "hello world" > index.txt`
* Example - Pass the file content as input to a command
  - `grep "pattern" < input.txt`
* Example - Pass the result of a command as input to another command
    - `echo "hello world" | grep "pattern"`


* Working with **Functions**: Functions provide a way to
modularize your code and make it more reusable.
* You can define functions using the function keyword or simply by declaring the function name followed by parentheses.

  
<img width="608" alt="Screenshot 2023-09-18 at 8 36 34 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/207a1eb8-f455-41af-8230-83fa0afebe52">


* The Result is as Follows:



  <img width="363" alt="Screenshot 2023-09-18 at 8 36 06 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/26b67de6-ab4e-49a2-bc0e-3baf97044dbd">

# First SS.
* Create a file on the terminal called _shell-scripting_ with the `mkdir` command. This file will contain our script codes.
* create a file in the directory (folder) with the `touch` command called _user-input.sh_
* Edit the file with scripts codes with any command line editor of your choice. I'll use **Vscode** over here. 

<img width="421" alt="user-input1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/0a028055-140e-42ef-8c84-1018919cf6ac">
* Save the file.

* Grant the file executive privileges with the `chmod +x user-input.sh` command

* * Run the script file with `./user-input.sh`   

* The result is as follows:

<img width="439" alt="user-input2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/6150df6d-b5d1-4b48-8bfb-ad82b0a3a019">

# Directory Manipulation & Navigation Script.

    - This script will display the current directory 
    - create a new directory called _"my_directory."_ 
    - change to that directory 
    - create two files inside it 
    - list the files 
    - move back one level up 
    - remove the _"my_directory"_ and its contents 
    - and finally list the files in the current directory again.

* Just as we did in the first script. Create a script file named _navigating-linux-filesys.sh_ and give it executable privileges
* Write the script in the file with your editor.
* Run the command on the terminal with `./ <filename>`

<img width="499" alt="nav1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/7190a899-1b8c-43c5-9644-ea736b02d0d4">

* The result is as follows:

<img width="611" alt="nav2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/f0536a37-b83a-4be2-b9cf-7916f3f83163">

* All the tasks are done with just one click. Thats the beauty of scripts writing.

# Personal Navigation Script.

* I will add one more personal task and navigating script and make it a little bit more interesting. 

* Using the same file as the _navigating-linux-filesys.sh_. 

      - The Script will create a reminder_list directory
      - Move into the reminder_list directory
      - Display path to current working directory
      - Create a todo_list file
      - Put some tasks in the todo_list file
      - View/List all tasks in the todo_list file
      - Move back to the previous working directory
      - And finally, display current working directory.
    
* I added the `sleep` command in between the script codes to make the task creation a little bit more interesting.

<img width="650" alt="nav-travie1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/90d1e0d3-5051-4154-bab0-3afdb08be7d5">

<img width="603" alt="nav-travie2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/06cc9d25-6656-4078-8c91-5aa1606d5bbd">


* The Script result is as follows in the recording below:


[nav -travie rec3.zip](https://github.com/travdevops/darey.io-pbl/files/12658168/nav.-travie.rec3.zip)

# File Operations and Sorting
* We will be writing a simple shell script that focuses on File Operations and Sorting.
* Script file name <_sorting.sh_>
  
      - This script creates three files (file 1.txt, file2.txt, and file3.txt)
      - displays the files in their current order,
      - sorts them alphabetically,
      -  saves the sorted files in sorted files.txt,
      -  displays the sorted files,
      -  removes the original files,
      -  renames the sorted file to sorted files_sorted_alphabetically.txt,
      -  and finally displays the contents of the final sorted file.

* Using the same steps as previous scripts.

<img width="514" alt="sorting 1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/a9735e0c-4d4d-4779-b799-e2a74c86f532">

<img width="426" alt="sorting 2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/57d6fa7e-c8a2-4520-81c5-b843c322e856">

* The Result:

<img width="656" alt="sorting3" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/b48f94dd-1b51-4826-84cc-bc91f7e1b1cb">




# Numbers and Calculations. 

* Script file name - <_calculations.sh_>

    - This script defines two variables num 1 and num2 with numeric values 
    - performs basic arithmetic operations (addition, subtraction, multiplication, division, and modulus) and displays the results. 
    - It also performs more complex calculations such as raising num1 to the power of 2 
    - and also calculating the square root of num2, 
    - and displays those results as well.


<img width="712" alt="calc1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5eb6ff6c-8a72-4313-8611-6126240999cf">


# File Backup and Timestamping

* As a DevOps Engineer backing up databases and other storage devices is one of the most common task you get to carryout.
* This shell scripting example is focused on file backup and timestamp.
* Script file name <_backup.sh_>

      - This script defines the source directory and backup directory paths. 
      - It then creates a timestamp using the current date and time, 
      - creates a backup directory with the timestamp appended to its name. 
      - The script then copies all files from the source directory to the backup directory using the cp command with the -r option for recursive copying. 
      - Finally, it displays a message indicating the completion of the backup process and shows the path of the backup directory with the timestamp.

<img width="637" alt="backup2" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/5885cfc4-3ddd-4253-b501-df292dac5bb5">

The result: 

<img width="603" alt="backup 1" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/6a2ac3b0-0124-4299-af41-b8550e4fbbf7">


