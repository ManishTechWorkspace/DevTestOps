pipeline {
    agent any
   tools{
        maven 'Maven'
    }
    stages {
       stage('Checkout') {
            steps {
                checkout scm
            }
       }
          stage('Build') {
            steps {
                sh "mvn install"
            }
          }
             stage('Unit Testing') {
            steps {
                sh "mvn test"
            }
            }
        stage('SonarQube analysis ') {
            steps {
                withSonarQubeEnv("Test Sonar")
              {
                 {
		                   sh "echo Sonar Run half"
                       sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.8.0.2131:sonar"        
                }
              }
               
            }
        }
    }
  post
  {
    success
    {
      sh "echo success"
    }
  }
}
}
