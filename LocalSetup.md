# Local Setup

## Installing AWS CLI and WireGuard

### AWS CLI 

1.Go to: https://aws.amazon.com/cli/ and download the interface
2.Follow the instructions on the installer, defaults are okay

### WireGuard

1. Download and install WireGuard: https://www.wireguard.com/install/
   + WireGuard is the VPN service that we use at Steampunk

## Configuring AWS and VPN access

### AWS CLI 

1. Reach out to Victor Konn to get access to AWS CLI. He will generate
keys for you and provide you with an AWS_ACCESS_KEY_ID and 
AWS_SECRET_ACCESS_KEY. 
2. Once you receive these, open a terminal
3. Run the command `aws configure`
4. Enter the key information you were given in step 1
   + The default region is `us-east-1`
5. Run the code: `aws ec2 describe-instances --output text`
   + If configured successfully, the output should be a long list of 
   instances
6. Errors can look like the following:
   + *screenshot one*
   + *screenshot two*

### WireGuard 

1. Reach out to Victor Konn to get access to WireGuard 
2. To verify that the VPN works, go to
   + https://jenkins.dhsice.name/login
   + https://nexus.dhsice.name
   
## Creating a CLI Key 

To ssh onto the instance, we are going to create a key. This key should remain in your .ssh folder. _**DO NOT UPLOAD THIS INTO YOUR GIT REPOSITORY IF YOUR KEY IS IN YOUR DIRECTORY**_
1. To create a key: `aws ec2 create-key-pair --key-name rgooney-key --tag-specifications  "ResourceType=key-pair,Tags=[{Key=CreatorName,Value=rgooney}]" --output text > aws-key.pem `
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
