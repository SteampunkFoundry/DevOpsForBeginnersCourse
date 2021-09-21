# Ansible and Java

Ansible is a software provisioning, configuration management, application deployment, 
and orchestration tool that is used to automate installation and configuration of software
in cloud or on-prem infrastructure or local VMs. Ansible files are called "playbooks" and
are written in YAML format. In addition to the playbook, an Ansible hosts file is often 
used to specify which host to provision -- this will not be used in this lesson, but is a 
critical component of Ansible, as it is often used to configure multiple hosts at once. 

In this lesson you will use Terraform to install Ansible on your instance, then write 
a simple Ansible playbook that will install Java on a linux machine, and finally you will 
use Ansible in conjunction with Terraform to run this playbook and as a result provision 
your instance. Feel free to use Ansible's [docs](https://docs.ansible.com/ansible/latest/index.html)
for reference as needed! 

For some background on Ansible, refer to the following documents:
+ https://www.redhat.com/en/blog/ansible-101-ansible-beginners
+ https://docs.ansible.com/ansible/latest/user_guide/intro_getting_started.html

## Using Terraform to Install Ansible on an EC2 Instance

1. Using the following reference docs and sample code, install Ansible on your 
instance one of two ways:
   + Using a `remote-exec` provisioner:
      + https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
      + https://www.terraform.io/docs/language/resources/provisioners/remote-exec.html
     
      ```hcl
      provisioner "remote-exec" { 
         inline = [
            "< shell script to install ansible >"
         ]
      }
      ```

   + Using a `file` provisioner and a `remote-exec` to run a shell script:
     + https://www.terraform.io/docs/language/resources/provisioners/file.html
     
     ```hcl
      provisioner "file" { 
       source      = "./<your-install-script>.sh"
       destination = "~/<your-install-script>.sh"
      }
       
      provisioner "remote-exec" { 
       inline = [
          "~/<your-install-script>.sh"
        ]
      }
     ```
   + **NOTE**: you will need a `connection` block in your `main.tf` file
   so that terraform has a way to connect to the instance to run the provisioners.
   Add the following code to your file:
   TODO: 
      ```hcl

      ```
   
3. SSH into your instance to confirm the installation was successful
4. To verify that it is installed, run the command: `ansible --version`
5. Remember to run `terraform destroy` when you are done!

## Using Ansible to Install Java

1. Write an Ansible playbook that will install Java on your EC2 instance
   + note: you will not need to create a hosts file
2. For this you will need to use a `file` provisioner in `main.tf` and a `remote-exec`,
similar to the steps followed above, but the file should be an Ansible playbook file.
   + For more reading: https://www.javatpoint.com/ansible-playbooks
