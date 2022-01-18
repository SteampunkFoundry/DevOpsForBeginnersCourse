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
1. Under configure>Pipeline
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
                containerTemplate(name: 'terraform', image: 'hashicorp/terraform', ttyEnabled: true, command: 'cat')
        ],
        nodeSelector: 'role=workers')
        {
            node(label) {
                stage('Checkout Code') {
                    cleanWs()
                    checkout scm
                }


                stage('Terraform Run') {


                   containers: [
                           containerTemplate(name: 'terraform', image: 'hashicorp/terraform', ttyEnabled: true, command: 'cat')
                   ],
                   nodeSelector: 'role=workers')
                   {
                      node(label) {
                         stage('Terraform Run') {
                            ansiColor('xterm') {
                               container('terraform') {
                                  withCredentials([sshUserPrivateKey(credentialsId: <key name>, keyFileVariable: 'key', passphraseVariable: '', usernameVariable: <variable name>)]) {
                                     withCredentials([usernamePassword(credentialsId: <key name>, passwordVariable: <password variable name>, usernameVariable: <ID name>)]) {
                                        //  create ssh key in workspace 
                                        //  add correct permissions on key
                                        //  terraform code 
                                        //  delete key 
                                     }
                                  }
                               }
                }

            }

        }
```
### withCredentials

+ withCredentials allows critical login information (such as keys or passwords) to be fed into the build to be used by Jenkins and Terraform to gain access without user interferance.
+ In order to use credentials on your build, you have to enter the credentials into the Jenkins globabl credentials which can be found under `Manage Jenkins` > `Manage Credentials`
   + For More information: https://www.jenkins.io/doc/book/using/using-credentials/
+ This allows for the build to login and to verify users, allowing for the pipeline to be created securely and automatically.

+ withCredentials Documentation: https://www.jenkins.io/doc/pipeline/steps/credentials-binding/

2. To test:
    + Make sure your Jenkins file is in your repository and pushed to your main branch
    + When you are ready to test your code on Jenkins hit: `Build Now`
      ![Builds](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/imgs/Builds_jenkins.PNG)
    + Select the build and hit `Console Output`
      ![Output](https://github.com/SteampunkFoundry/DevOpsForBeginnersCourse/blob/main/imgs/ConsoleOutput_jenkins.PNG)

