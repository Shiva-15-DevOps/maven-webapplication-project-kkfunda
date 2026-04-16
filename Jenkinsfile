@Library('Sharedlibslack') _

pipeline{
    agent any
    tools{
        maven "maven-3.9.6"
    }

     stages{   // stage starting
         stage('Git Checkout'){
             steps{
                 git branch: 'f2',
                    url: 'https://github.com/Shiva-15-DevOps/maven-webapplication-project-kkfunda.git'
             }
         }

         stage('Compile'){
             steps{
                 sh "mvn compile"
             }
         }

         stage('BuildToNexus'){
             steps{
                 buildToNexus()
             }
         }
     } //stages ending

    post{
        success{
            script{
                sendSlackNotifications(currentBuild.result)
            }
        }
        failure{
            script{
                sendSlackNotifications(currentBuild.result)
            }
        }
    }
}
