#Terraform
##Install and configure Terraform on your machine
Terraform is
Before completing this step please review the following documents: https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/aws-get-started
1. Install Chocolately (https://chocolatey.org/install)
    + Open Powershell as an administrator
    + Run the following command: `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`

2. Run the command: `choco`
3. Run the command: `choco feature enable -n useFipsCompliantChecksums`

4. Run the command: `choco install terraform`
5. Type `Y` hit enter to finish the install
6. To verify that terraform is installed, run the command: `terraform -help`

##Create a Terraform project
1. On IntelliJ in your DevOps project, right click the “README” file and hover over “New”, hit “File”. Name this file “main.tf’
2. Change the highlighted portion of the below code, to your name. This code will still run if you don’t do this, but it’s important to change the variables. THEN:Copy the following into your new “main.tf” file:
  ```terraform
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
ami           = " ami-099543e8a36a7890c”
instance_type = "t2.micro"
subnet_id = "subnet-0f83fd875df60928a"

tags = {
Name = "[your name]-test-instance"
CreatorName = [aws username *given with your key*]
}
}
````
3. On IntelliJ in the terminal: 
   + Run the code: `terraform init`
4. Run the code: `terraform plan`
   + This works to check your syntax and catches any blatant errors you may have. This will not run the code, just verify there are no small errors
5. If this is successful: push the code to your repository
6. Run the code terraform apply
   + Type: Yes
   + Apply runs the code, this will create your instance. Verify with your lead that your instance has been made on the AWS client.
7. Run the code: `terraform destroy`
   + Type: `yes`
   + This will deconstruct the instance. The goal is to keep the instance up for only as long as you need it. Make sure you destroy when you are done and verify that your output is
