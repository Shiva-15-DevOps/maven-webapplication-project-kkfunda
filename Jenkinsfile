pipeline{

    agent any
    tools{
    maven "maven-3.9.6"
    }
    
    stages{ 
     
     stage('Git checkout'){
	 
	 steps{
	 
        git branch: 'f2', url: 'https://github.com/Shiva-15-DevOps/maven-webapplication-project-kkfunda.git'

	 }
	  
	 }
	  
     stage('compile'){
       
     steps{
	 
	 sh "mvn compile"
	 
	 }
	 
   }
    
    stage('Maven and SQ'){
	
	steps{
	
	parallel(
	
	"Build":{
	sh "mvn clean package"
	},
	
	"Sonar":{
	sh "mvn sonar:sonar"
	}
	
	)
	
	}
	
	}

     stage('nexus and Tomcat'){
	 
	 steps{
	  parallel(
	  "Nexus"{
	  
	  sh "mvn deploy"
	  
	  },
	  
	  "Tomcat"{
	  
	  sh """

           curl -u shiva:shiva@115G \
      --upload-file /var/lib/jenkins/workspace/bsnl-dev/target/maven-web-application.war \
      "http://13.200.253.67:8080/manager/text/deploy?path=/maven-web-application&update=true"
      
               """
	  
	}  
   )	 
  } 
 }
}// stage ending
} //pipeline ending
	
