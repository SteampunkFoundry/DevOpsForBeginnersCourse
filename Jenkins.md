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



## Connect to Github
1. Under Configure>Pipeline
2. Select: `Pipeline script from SCM`
   + Select SCM: `Git`
   + You want to link your repository and have it end with a .git
      + IE: https://github.com/SteampunkFoundry/FakeRepository.git
   + You need to give 'steampunk-bot' read access to your repo
   + Credentials: `steampunk-bot`
3. Make sure the branch is your `develop` or `main` branch, or which ever branch the Jenkins file you are testing is
   ![Configure](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/imgs/PipelineSetup_jenkins.PNG)

## Creating the Jenkins Script
1. Using the following template create a script to run your Terraform commands, make sure its automated so there is no wait times.
   + For the withCredentials use the code generator on Jenkins
      + `<Project Name> > Pipeline Syntax`
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

##Installing TomCat onto the Instance
For more information: https://tomcat.apache.org/tomcat-9.0-doc/index.html
1. Using your Ansible Playbook, download `tomcat9-admin`

##Implement A Destroy
We are going to include an auto approved destroy in your jenkinsfile
1. Go to your jenkisfile
2. After the line: `sh 'terraform apply --auto-approve'`
3. Add in: `sh 'sleep 9m' //change as needed`
   1. You will have to change the time as needed, if you are just testing to make sure your code runs, use 1m or 2m
   2. Try to keep it minimal so your instance isn't running longer than you need it
4. Add in: `sh 'terraform destroy --auto-approve'`
5. Add in: `sh 'rm ./<keyname>.pem'`