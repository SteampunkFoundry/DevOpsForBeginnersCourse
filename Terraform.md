# Terraform

## Overview

Terraform is an Infrastructure as Code (IaC) tool used to define, provision, and create
cloud infrastructure. Terraform has nearly endless capabilities, including configuring
compute instances, storage, and networking in order to customize cloud infrastructure as 
needed. Terraform has many "providers", each with its own capabilities and specifications.


For this lesson we will be using the [AWS](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) 
provider in order to launch an Ubuntu Amazon Elastic Cloud Compute (EC2) instance in Steampunk's 
Virtual Private Cloud (VPC). Next, we will create an ssh key in AWS so that we can ssh to the 
live instance in order to troubleshoot. Later on we will provision this instance using various 
methods. You are encouraged to use Terraform's extensive [docs](https://www.terraform.io/docs/index.html) 
throughout this course! 

Begin by reviewing the following how-to guide on using Terraform with AWS: 
https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/aws-get-started

## Install and configure Terraform on your machine

### Windows Terraform Setup

1. Install Chocolately (https://chocolatey.org/install)
    + Open Powershell as an administrator
    + Run the following command: `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`
   [install1](!https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/rachel-updates/imgs/chocolatey1.png)
2. Run the command: `choco`
   [choco](!https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/rachel-updates/imgs/chocolatey2.png)
3. Run the command: `choco feature enable -n useFipsCompliantChecksums`
   [feature](!https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/rachel-updates/imgs/chocolatey3.png)
4. Run the command: `choco install terraform`
   [install2](!https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/rachel-updates/imgs/chocolatey4.png)
5. Type `Y` hit enter to finish the install
6. To verify that terraform is installed, run the command: `terraform -help`
   [verifying](!https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/rachel-updates/imgs/chocolatey5.png)

### MacOS and Linux Terraform Setup 

1.  run the command: 'brew tap hashicorp/tap'
   + this installs HashiCorp
2. run the command: 'brew install hashicorp/tap/terraform'
   + this installs terraform
3. run the command: 'brew update'
   + this updates Terraform
4. run the command: 'brew upgrade hashicorp/tap/terraform'
   + this upgrades Terraform
     5, To verify the installation, by running the code: 'terraform -help' 

## Create a Terraform project

1. Open your DevOps project in IntelliJ and create a new file named `main.tf`.
Change the highlighted portion of the below code to your name. This code will still run 
if you don’t do this, but it’s important to change the variables. 
```hcl
terraform { 
   required_providers { 
      aws = { 
         source  = "hashicorp/aws"
         version = "~> 3.27" 
      } 
   }
   required_version = ">= 0.14.9"
}

provider "aws" { 
   profile = "default"
   region  = "us-east-1"
}

resource "aws_instance" "app_server" { 
   ami           = "ami-099543e8a36a7890c"
   instance_type = "t2.micro"
   subnet_id = "subnet-0f83fd875df60928a"
   
   tags = { 
      Name = "<YOUR-NAME>-test-instance"
      CreatorName = <aws_username_given_with_your_key>
   } 
}
```

3. In the terminal window in IntelliJ: 
   + Run the code: `terraform init`
4. Run the code: `terraform plan`
   + This works to check your syntax and catches any blatant errors you may have. This will 
   not run the code, just verify there are no errors
5. If this is successful, commit and push the code to your repository
6. Run `terraform apply`
   + Type `yes`
   + Apply runs the code, this will create your instance. **Verify with your lead that your instance 
   has successfully been created in AWS.**
7. Run the code: `terraform destroy`
   + Type `yes`
   + This will tear down the instance. The goal is to keep the instance up for only as long as you 
   need it. **Make sure you destroy when you are done** and verify that your output is
[destroy](!https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/rachel-updates/imgs/destroy.png)

## Creating a CLI Key to Use to Connect to Instance

To ssh onto the instance, we are going to create a key. This key should remain in your .ssh folder
in the home directory. 
_**DO NOT UPLOAD THIS INTO YOUR GIT REPOSITORY IF YOUR KEY IS IN YOUR WORKING DIRECTORY**_
1. To create a key: `aws ec2 create-key-pair --key-name <YOUR-USERNAME>-key --tag-specifications  "ResourceType=key-pair,Tags=[{Key=CreatorName,Value=<YOUR-USERNAME>}]" --output text > aws-key.pem`
2. TODO: How to move key to ~/.ssh if it is not there already
3. For more information on how to create a key, see:
   + https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-keypairs.html
   + https://docs.aws.amazon.com/cli/latest/reference/ec2/create-key-pair.html
4. You want to add your key under the resource block as `key_name = <YOUR-KEY-NAME>`
5. Run the command: `chmod 600 ~/.ssh/aws-key.pem`
   + this changes the permissions on your aws key

## Connecting to Your Instance:

1. Now we need to modify our main.tf file to get an output of the IP of our instance so we can 
ssh to our instance.
2. At the very bottom of your main.tf file, you want to add in an output block
   + https://www.terraform.io/docs/language/values/outputs.html
   + Using the above link write the code to output the IP
3. When you get the output to work, run `terraform apply`, then ssh onto the instance 
   using the command:
   + `ssh -i ~/.ssh/aws-key.pem ubuntu@<IP-ADDRESS>`
4. Be sure to run `terraform destroy` when you have successfully logged into the instance.
