# Local Setup

## Installing AWS CLI and WireGuard
These are particular to Steampunk, you will have to reach out to Punks to finish this portion of the course.
This is going to be where we may have to figure out billing codes if you haven't already. 

### AWS CLI 

1. Go to: https://aws.amazon.com/cli/ and download the interface
2. Follow the instructions on the installer, defaults are okay

### WireGuard Install

1. Download and install WireGuard: https://www.wireguard.com/install/
   + WireGuard is the VPN service that we use at Steampunk

## Configuring AWS and VPN access

### AWS CLI 
 
1. Reach out to Victor Konn to get access to AWS CLI. He will generate
keys for you and provide you with an AWS_ACCESS_KEY_ID and 
AWS_SECRET_ACCESS_KEY. Store these in a safe place and do not share them 
with anyone, as they give the user access to our private cloud in AWS. 
2. Once you receive these, open a terminal
3. Run the command `aws configure`
4. Enter the key information you were given in step 1
   + The default region is `us-east-1`
5. Run the code: `aws ec2 describe-instances --output text`
   + If configured successfully, the output should be a long list of 
   instances
6. Errors can look like the following:
   + ![error 1](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/rachel-updates/imgs/awsKeyError1.jpg)
   + ![error 2](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/master/imgs/awsKeyError2.png)

### WireGuard Set Up

1. Reach out to Victor Konn to get access to WireGuard 
2. To verify that the VPN works, go to
   + https://jenkins.dhsice.name/login
   + https://nexus.dhsice.name
   
Previous Lesson: [Lesson-01 Prerequisites](./Lesson-01.md) | Next Lesson: [Lesson-03 Terraform](./Lesson-03.md)
