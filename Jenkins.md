# Jenkins
You must be on the VPN to access Jenkins [add link to section]

## Accessing Jenkins


1. Go to: https://jenkins.dhsice.name/login
   + If you do not already, reach out to Prerna Hodge for the credentials

## Creating a Job
1. Click: 'New Item'
2. The name should be 'DevOpsForBeginners<First Name>'
   + It should be a 'Multi-configuration project'

## Connect to Github 
elaborate

## Creating the Jenkins Script
1. Using the following template create a script to run 'Terraform Innit', 'Terraform Plan', 'Terraform Apply'
   + 
'def label = "ImageBuildPod-${UUID.randomUUID().toString()}"

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
}'
