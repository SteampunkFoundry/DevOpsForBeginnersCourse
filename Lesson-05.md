# Jenkins
You must be on the VPN to access Jenkins
+ More Jenkins Documentation: https://www.jenkins.io/doc/
+ VPN Access Information: https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/LocalSetup.md


## Accessing Jenkins


1. Go to: https://jenkins.dhsice.name/login
   + If you do not already, reach out to Prerna Hodge for the credentials

## Creating a Job

1. Click: `New Item`
2. The name should be `DevOpsForBeginners<First Name>`
   + It should be a `Pipeline`
    
## Connect to GitHub

1. Under Configure > Pipeline
2. Select: `Pipeline script from SCM`
   + Select SCM: `Git`
   + You want to link your repository and have it end with a .git
      + IE: https://github.com/SteampunkFoundry/FakeRepository.git
   + You need to give steampunk-bot read access to your repo. This is the user that allows Jenkins to view your 
     repository code. 
        - Go to your repository in GitHub
        - Navigate to **Settings** > **Manage Access**
        - Select **Add People** and add **steampunk-bot**

3. Make sure the branch is your `develop` or `main` branch, or which ever branch the Jenkins file you are testing is
   ![Configure](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/imgs/PipelineSetup_jenkins.PNG)

## Getting an IP Output
1. Open your ```main.tf```
2. Add this to the bottom of your file 
    ```terraform
    output "instance_private_ip" {
       description = "Public IP address of the EC2 instance"
       value       = aws_instance.app_server.private_ip
       }
    ```
## Creating the Jenkins Script

1. Using the following template create a script to run your Terraform commands, make sure its automated so there is no wait times.
   + For the `withCredentials` block use the Pipeline Syntax code generator in Jenkins by navigating to your project
     then selecting **Pipeline Syntax** 
    

```groovy
def label = "ImageBuildPod-${UUID.randomUUID().toString()}"

podTemplate(label: label,
containers: [
ccontainer('terraform'){
    withCredentials([]) <USE THE CODE GENERATOR TO CREATE THIS LINE OF CODE WITH KEY CREDITIALS>
    withCredentials([usernamePassword(<USE THE CODE GENERATOR TO CREATE AWS ACCESS WITH JEFFAWS>) {
            // some block
nodeSelector: 'role=workers')
{
node(label) {

        stage('Checkout Code') {
            cleanWs()
            checkout scm
        }

        stage('Initialize DB'){

            container('git'){

            }
        }

    }
}
```
2. To test:
   + Make sure your Jenkins file is in your repository and pushed to your main branch
   + When you are ready to test your code on Jenkins hit: `Build Now`
     ![Builds](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/imgs/Builds_jenkins.PNG)
   + Select the build and hit `Console Output`

     ![Output](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/imgs/ConsoleOutput_jenkins.PNG)
   
## Implement An Auto Destroy

We are going to include an auto approved destroy in your jenkinsfile
1. Go to your jenkisfile
2. In the ```node(label)``` section replace the entire code with:
```groovy
     try {
        sh 'cp $key $WORKSPACE/ssh-key.pem'
        sh 'chmod 600 ./ssh-key.pem'
        sh 'export TF_LOG=TRUE'
        sh <enter the 1st terraform command to start a build>
        sh <enter the 2nd terraform command to start a build>
        sh <enter the 3rd terraform command to start a build>
    } catch (e) {
        echo "terraform failed... destroying instance"
        throw(e)
    } finally {
        sh 'sleep <enter an amount of time in specify 'm' for minutes otherwise defaults to seconds'>'
        sh 'terraform destroy --auto-approve'
        sh 'rm -f ./ssh-key.pem'
    }
```
The above code will make sure that even if your build fails that it will still destroy the entire build

