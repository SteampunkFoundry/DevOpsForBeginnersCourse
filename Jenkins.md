# Jenkins
You must be on the VPN to access Jenkins [add link to section]

## Accessing Jenkins
1. Go to: https://jenkins.dhsice.name/login
   + If you do not already, reach out to Prerna Hodge for the credentials

## Creating a Job
1. Click: `New Item`
2. The name should be `DevOpsForBeginners<First Name>`
   + It should be a `Multi-configuration project`

## Connect to Github 
1. Under configure>Advanced Project Options
2. Select: `Pipeline script from SCM`
   + Select SCM: `Git`
   + You want to link your repository and have it end with a .git
     + IE: https://github.com/SteampunkFoundry/FakeRepository.git
   + Credentials: `steampunk-bot`
3. Make sure the branch is your `develop` or `main` branch

## Creating the Jenkins Script
1. Using the following template create a script to run `Terraform Innit`, `Terraform Plan`, `Terraform Apply`
```
def label = "ImageBuildPod-${UUID.randomUUID().toString()}"

podTemplate(label: label,
containers: [
containerTemplate(name: 'git', image: 'alpine/git', ttyEnabled: true, command: 'cat')
],
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
   + On Jenkins: hit `Build Now`
   + Select the build and hit `Console Output`