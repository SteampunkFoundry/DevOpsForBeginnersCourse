# Prerequisites
### Installing IntelliJ
1. Download the community version of Intellij Community version at the following link: https://www.jetbrains.com/idea/download/#section=windows
2. Run the installer
3. Run through the installer as needed. There shouldn’t be any settings to change, just hit “Next” until it installs.
4. Open IntelliJ

### Creating a GitHub
*GitHub is a website that allows for project sharing. A repository is created and files are added to the “main” or “develop” branch. Branches can be made off of other branches and each branch contains changes to the project that can be merged, called a pull request, into the parent branch by the owner(s) or the repository. Anyone who has the project can easily update if a pull request is completed.*
1. Open and follow the instructions on the site and use your STEAMPUNK email to sign up: https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home
2. For more information: https://guides.github.com/activities/hello-world/
3. Ask Alan Crouch for access to SteampunkFoundry: https://github.com/SteampunkFoundry
4. When access if given you should receive an email to login and gain access
5. For an explanation about Gitflow: https://github.com/SteampunkFoundry/GitOpsTutorial/tree/master/About_GitFlow

### Connecting Github to IntelliJ
1. Download GIT bash from https://git-scm.com/downloads  (follow the installer, defaults are ok) if its not already on your machine
    + To check if it’s already on your machine, go to the start button and type git, “Git Bash” should come up in the window.
2. Open a Git Bash window:
3. Follow step 1.A, and click to open a window
4. Use the command: `cd ~/.ssh`
5. Run the command: `ls`
6. Run the command: `ssh-keygen -o`
    + Enter “steampunk_rsa” as the file
7.