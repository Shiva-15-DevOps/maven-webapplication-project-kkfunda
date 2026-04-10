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
}// stage ending
} //pipeline ending
	
