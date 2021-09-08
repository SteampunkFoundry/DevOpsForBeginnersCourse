# Prerequisites
## Installing IntelliJ
1. Download the community version of Intellij Community version at the following link: https://www.jetbrains.com/idea/download/#section=windows
2. Run the installer
3. Run through the installer as needed. There shouldn’t be any settings to change, just hit “Next” until it installs.
4. Open IntelliJ

## Creating a GitHub
*GitHub is a website that allows for project sharing. A repository is created and files are added to the “main” or “develop” branch. Branches can be made off of other branches and each branch contains changes to the project that can be merged, called a pull request, into the parent branch by the owner(s) or the repository. Anyone who has the project can easily update if a pull request is completed.*
1. Open and follow the instructions on the site and use your STEAMPUNK email to sign up: https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home
2. For more information: https://guides.github.com/activities/hello-world/
3. Ask Alan Crouch for access to SteampunkFoundry: https://github.com/SteampunkFoundry
4. When access if given you should receive an email to login and gain access
5. For an explanation about Gitflow: https://github.com/SteampunkFoundry/GitOpsTutorial/tree/master/About_GitFlow

## Connecting Github to IntelliJ
1. Download GIT bash from https://git-scm.com/downloads  (follow the installer, defaults are ok) if its not already on your machine
    + To check if it’s already on your machine, go to the start button and type git, “Git Bash” should come up in the window.
2. Open a Git Bash window:
3. Follow step 1.A, and click to open a window
4. Use the command: `cd ~/.ssh`
5. Run the command: `ls`
6. Run the command: `ssh-keygen -o`
```javascript
PS C:\Users\YourUser> ssh-keygen -o
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\YourUser/.ssh/steampunk_rsa):
Created directory 'C:\Users\YourUser/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\YourUser/.ssh/steampunk_rsa.
Your public key has been saved in C:\Users\YourUser/.ssh/steampunk_rsa.pub.
The key fingerprint is:
SHA256:8dvoBlfJDSSVqwAfVFQwzx7LOJWApbCWBMH9y/xwlPc azuread\youruser@USER-LT
The key's randomart image is:
+---[RSA 3072]----+
|       ++oOB+.   |
|      o... B+    |
|       o..+.+*  .|
|   o.o +oB o=.o.o|
|      + S.+o.o  o|
|        ..o+  = E|
|         oo .  + |
|         ..     .|
|         ..      |
+----[SHA256]-----+
```
7. Run the command: `ls`
8. Run the command:  `cat ~/.ssh/steampunk_rsa.pub`
   + Copy the entire output
9. If more help is needed: https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key
10. Open Github, login, and go to your settings
11. On the left side there is a tab titled: `SSH and GPG keys`
12. Click: `New SSH Key`
13. Copy the output from Step 7 and create a title
14. Upon completion, you will need to enter your password to confirm
15. On IntelliJ, you should see on the bottom left a tab that says “Git”, as well as the top header a tab that says “Git”, and on the middle left tabs that say “Commit” and “Pull Requests”

##Creating a Repository
1. Go to https://github.com/SteampunkFoundry and hit “New”
2. Call your repository:  `DevOpsforBeginners-[YOUR NAME]`
3. Make your repository public
4. Select the `Add a README.md file`
5. Hit “Create repository”

##Cloning a Repository
1. Go to https://github.com/SteampunkFoundry/DevOpsforBeginners-[YOURNAME]
2. On the Code drop down menu, hit SSH and copy the text.
3. On your IDE, open the terminal on the bottom. 
   + Run: `cd Users\[your id]`
   + Run the command: `git clone [copied text]`
```javascript
$ git clone https://github.com/SteampunkFoundry/GitOpsTutorial.git
Cloning into 'GitOpsTutorial'...
remote: Enumerating objects: 30, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (29/29), done.
remote: Total 30 (delta 7), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (30/30), 1.79 MiB | 2.54 MiB/s, done.
```
4. To Verify, Go to the directory in File Explorer and `DevOpsforBeginners-Rachel` should be a new folder


## Creating Changes and Creating a Pull Request:
1. Open the README file
2. Within this file change the name to reflect the name of your Repository
3. Change the Description section in the ReadMe file to say “This repository is to assit DevOps beginners start their projects and have a manual for any questions they may have.”
4. Open the terminal in IntelliJ
   + Run the code: git branch sampleBranch
      + This creates the branch
   + Run the code: git checkout sampleBranch
      + This allows you to make apply your changes to this new branch, to verify this worked check the highlighted portion of your IDE. If it doesn’t say sampleBranch something went wrong
5. On the left middle side there should be 3 tabs, hit the `Commit` Tab.
6. Select the README and hit `Commit and Push` and hit it a second time when the window pops up
7. Go to your repository make sure the branch was updated and then hit `Compare and Request`