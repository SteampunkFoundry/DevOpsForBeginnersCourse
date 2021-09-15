# Local Setup

## Install AWS CLI
1. Reach out to Victor Konn about access to AWS CLI
2. Go to: https://aws.amazon.com/cli/ and download the interface
3. Follow the instructions on the installer, defaults are okay
   
## Configure CLI Access
1. Once installed, open a command prompt window
2. Enter the key information you were given in step 1
    + The region name is `us-east-1`
3. Run the code: `aws ec2 describe-instances --output text`
    + The output should be a long list of instances
4. Errors can look like the following:
   + *screenshot one*
   + *screenshot two*

## Install Wireguard and Configure Access
1. Download and install WireGuard: https://www.wireguard.com/install/
   + WireGuard is the VPN service that Steampunk uses.
2. Reach out to Victor Konn to get access to WireGuard
3. To verify that the VPN works, go to
   + https://jenkins.dhsice.name/login
   + https://nexus.dhsice.name

## Creating a CLI Key 
To ssh onto the instance, we are going to create a key. This key should remain in your .ssh folder. _**DO NOT UPLOAD THIS INTO YOUR GIT REPOSITORY IF YOUR KEY IS IN YOUR DIRECTORY**_
1. To create a key: `aws ec2 create-key-pair --key-name <YOURNAME>-key --tag-specifications  "ResourceType=key-pair,Tags=[{Key=CreatorName,Value= <YOURNAME> }]" --output text > aws-key.pem `
2. For more information on how to create a key
   + https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-keypairs.html
   + https://docs.aws.amazon.com/cli/latest/reference/ec2/create-key-pair.html
3. You want to add your key under the resource block as key_name = key name
4. Run the code: `chmod 600 ~/.ssh/aws-key.pem`
   + this changes the permissions on your aws-key

## Connecting to Your Instance:
1. Now we need to modify our main.tf file to get an output of the IP of our instance so we can ssh in to our instance.
2. At the very bottom of your main.tf file, you want to add in an output block
   + https://www.terraform.io/docs/language/values/outputs.html
   + Using the above link create the code to output the IP
3. When you finally get the output to work, run the below code to shh onto the instance
   + `ssh -i ~/.ssh/aws-key.pem ubuntu@IP ADDRESS`