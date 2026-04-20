pipeline{
    agent{
		lable 'Nodes'
	}
    tools{
	    maven "maven-3.9.6"
       }
 
      stages{
          stage('Git checkout'){
            steps{
	          git branch: 'uat', url: 'https://github.com/Shiva-15-DevOps/maven-webapplication-project-kkfunda.git'
	          }
  
            }
  
   
            stage('Code compile')
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
             
             stage('Sonar qube')
             {
              steps
              {
                sh "mvn sonar:sonar"
              }
             }
             
             stage('Nexus deploy')
             {
              steps
              {
               sh "mvn deploy"
              }
             }
             
             stage('Tomcat Deploy')
             {
              steps
              {
                 sh """
           
                      curl -u shiva:shiva@115G \
                 --upload-file /var/lib/jenkins/workspace/bsnl-dev/target/maven-web-application.war \
                 "http://13.200.253.67:8080/manager/text/deploy?path=/maven-web-application&update=true"
                 
                          """
              }
             }
            } //stages ending 
           
           } //Pipeline ending
