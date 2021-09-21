# Ansible and Java

Ansible is a tool to help install and control what is on your instance.

### Install Ansible

Please refer to the following documents: 
+ https://www.redhat.com/en/blog/ansible-101-ansible-beginners
+ https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html
1. Install Ansible onto your machine
   + You can use a file provisioner
        + https://www.terraform.io/docs/language/resources/provisioners/file.html
    + You can also use a remote provisioner
        + https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
        + https://www.terraform.io/docs/language/resources/provisioners/remote-exec.html
2. SSH into your instance
3. To verify that this was installed, run the command: `ansible --version`

### Install Java

1. Using an Ansible playbook, write a script to install Java
   + note: you will not need a separate hosts file
2. For this you will need to use a File Provisioner 
For more reading: 
   + https://www.javatpoint.com/ansible-playbooks

