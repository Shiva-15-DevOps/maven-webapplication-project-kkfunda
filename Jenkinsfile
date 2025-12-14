pipeline
{
	agent any
	tools
	{
	  maven "Maven-3.9.6"
	}
	stages
	{
      stage('Git checkout')
      {
         steps
         {
          notifyBuild('STARTED')
          git branch: 'Dev', url: 'https://github.com/Shiva-15-DevOps/maven-webapplication-project-kkfunda.git'
         }
      }
      stage('Code Compile')
      {
        steps
        {
          sh "mvn compile"
        }
      }
      stage('Build')
      {
        steps
        {
         sh "mvn clean package"
        }
      }
      stage('SQ Report')
       {
         steps
         {
          sh "mvn sonar:sonar"
         }
       }
       stage('Deploy to Nexus')
        {
          steps	
           {
            sh "mvn deploy"
           }
        }
        stage('Deploy to Tomcat')
        {
          steps
          {
            sh """

           curl -u shiva:Shiva@115G \
      --upload-file /var/lib/jenkins/workspace/Jio-Declarative-PL-dev/target/maven-web-application.war \
      "http://13.201.193.191:8080/manager/text/deploy?path=/maven-web-application&update=true"
      
               """
          }
        }      
	} //stages ending

  post{
       success {

       script 
       {
         notifyBuild(currentBuild.result)
       }

       }

       failure {

       script
       {
         notfiyBuild(currentBuild.result)
       }

       }

  }

} //Pipeline ending


// Notification method
def notifyBuild(String buildStatus = 'STARTED') {
    buildStatus = buildStatus ?: 'SUCCESS'

    def colorCode
    def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
    def summary = "${subject} (${env.BUILD_URL})"

    switch (buildStatus) {
        case 'STARTED':
            colorCode = '#FFFF00' // Yellow
            break
        case 'SUCCESS':
            colorCode = '#00FF00' // Green
            break
        default:
            colorCode = '#FF0000' // Red
    }

    slackSend(color: colorCode, message: summary, channel: '#jio-declaratie-job')
}
