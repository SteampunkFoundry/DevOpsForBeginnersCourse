![Logo](https://github.com/SteampunkFoundry/images/raw/master/steampunk_banner-white_pink_on_grey.jfif)

# DevSecOps for Beginners Course

This course is meant for those who are new to DevSecOps and would like to
learn some basic tools and principles that can be used to automate the
deployment of an application end-to-end. This course will start with local setup
and software requirements like Git and IntelliJ then will move into launching an
AWS instance using Terraform, then using Ansible to provision this instance, and
finally to automating this process with Jenkins.

# By the end of this Course
This course should teach you the basic tools that we mainly use for DevOps at Steampunk, but on top of that
you should be able to troubleshoot these tools and read their documentation if you don't know how to already.

## Table of Contents

+ [Lesson-01 Prerequisites](./Lesson-01.md)
    + Installing and Setting up IntelliJ
    + Useful Plugins
    + Installing Git Bash (Windows) and Generating an SSH key
    + Use Git Bash in IntelliJ
    + Creating a Git Repository
    + Cloning a Git Repository
    + Creating Changes and Creating a Pull Request


+ [Lesson-02 Local Setup](./Lesson-02.md)
    + Install AWS CLI & WireGuard
    + Configure AWS CLI access
    + WireGaurd SetUp

+ [Lesson-03 Terraform](./Lesson-03.md)
    + Install and configure Terraform on your machine
    + Create a Terraform project
    + Creating a CLI Key to Use to Connect to Instance
    + Connecting to Your Instance

+ [Lesson-04 Ansible](./Lesson-04.md)
    + Using Terraform to Install Ansible on an EC2 Instance
    + Using Ansible to Install Java
    

+ [Lesson-05 Jenkins](./Lesson-05.md)
  + Accessing Jenkins
  + Creating a Job
  + Connect to Github
  + Getting an IP Output
  + Creating the Jenkins Script
  + Implementing an Auto Destroy

  
+ [Lesson-06 Running Dockerfiles](./Lesson-06.md)
  + Final Lesson Overview
  + Creating a Dockerfile
  + Provision with Ansible
