pipeline {
    agent any

    tools {
        maven "maven-3.9.6"
    }

    stages {

        stage('Git checkout') {
            steps {
                git branch: 'f2',
                    url: 'https://github.com/Shiva-15-DevOps/maven-webapplication-project-kkfunda.git'
            }
        }

        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }

        stage('Build and Sonar') {
            steps {
                script {
                    parallel(
                        Build: {
                            sh "mvn clean package"
                        },
                        Sonar: {
                            sh "mvn sonar:sonar"
                        }
                    )
                }
            }
        }

        stage('Nexus and Tomcat Deploy') {
            steps {
                script {
                    parallel(
                        Nexus: {
                            sh "mvn deploy"
                        },
                        Tomcat: {
                            sh """
                                curl -u shiva:shiva@115G \
                                --upload-file /var/lib/jenkins/workspace/Parallel-job-Pl/target/maven-web-application.war \
                                "http://13.200.253.67:8080/manager/text/deploy?path=/maven-web-application&update=true"
                            """
                        }
                    )
                }
            }
        }
    }
}
