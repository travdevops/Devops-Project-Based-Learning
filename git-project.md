# WELCOME TO MY GIT-PROJECT!

### - Git is basically the ultimate distributed version control system.

 ### - Git keeps track of the changes made to the source code. 
 
 ### - Git solves the basic issues with source code sharing. 

# INITIALZING A NEW REPOSITORY!

 We must have installed Git properly on the terminal.

     - open the terminal

    - create a new directory with the mkdir command

`mkdir Devops GIT` 

     - Move into the newly created directory with the cd command

   `cd Devops GIT` 

     - On the present working directory, run git init command to download git files to the workong directory. 


 <img width="987" alt="Screenshot 2023-08-20 at 9 01 05 AM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/d4345661-e7b2-4723-a88d-2a72a4e5c29b">


 # MAKING A COMMIT!

 Making a commit on git could also mean the same as saving current changes to the working files. Changes could vary in forms of adding, editing, modifying or even deleting files or texts. 

 Lets make some changes.

    - Inside the working _Devops GIT_ directory, create a file called index.txt with the touch command

 `touch index.txt`

    -  Add some text into the newly created (index.txt) file with the `echo` command

 `echo "Addition of a new line to my index file" > index.txt`

    - Add/move all the new changes to the staging phase

 `git add .`

    - Commit changes to git by running the command 

 `git commit -m "Initial Commit"   
 
The -m flag is used to provide a commit message or some context about what the current and latest commit is all about and making the work descriptive. 


<img width="991" alt="Screenshot 2023-08-20 at 9 01 05 AM copy" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/1ebdebb2-c061-408f-8780-597dcf4b55bb">


# BRANCHES IN GIT!

Branches in git helps to create different copies of the source code. Many changes can be made to the branches without affecting the main copy of the source code.

The Git branch feature is mostly used to develop a new feature which is untested not to affect the working source code on the main branch. 

Git branch is also essential for remote collaboration in the working team. For example, different developers working on a particular source code from different locations. They make different branches for their features and then converge their code to the main branch. 

# MAKE A GIT BRANCH!

     - Use this command to create and switch to a new branch, I will call the new branch [my-new-branch]

`git checkout -b my-new-branch`

<img width="850" alt="Screenshot 2023-08-21 at 6 43 34 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/c893b5c2-416b-4a4b-a74f-b2dd6e7743ee">


Lets list our branches with `git branch` command and see that we have been switched to the new branch (_my-new-branch_)


<img width="594" alt="Screenshot 2023-08-21 at 6 44 24 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/7f1590b8-d9f6-4168-afc4-8a0a6469df24">


We can use both `git switch` and `git checkout` to switch between different branches

`git switch` is used below. 


<img width="637" alt="Screenshot 2023-08-21 at 6 46 05 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/8f9cdbc6-8a1d-4d32-9c3c-d842961a528f">

While `git checkout` is used below


<img width="596" alt="Screenshot 2023-08-21 at 6 51 14 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/53dc0943-a412-415a-b780-12e8809c432c">


# MERGING A BRANCH INTO ANOTHER BRANCH!



<img width="1082" alt="Screenshot 2023-08-21 at 7 37 21 PM" src="https://github.com/travdevops/darey.io-pbl/assets/137777644/bbaef929-ebef-4c6a-b56b-07df41ad0d00">



# DELETING A GIT BRANCH!


Once done with all the new features added on different branches and all the work has been added to the main branch, we can terminate the other feature branches

Git branches can be deleted with this command

`git branch -d <branch-name>`




