pipeline{
    agent any
    	
    tools{
        maven 'Maven'
    }
    stages{
        stage("code checkout"){
            steps{
            sh "echo hello"
            }
        }   
        stage("code build"){
            steps{
            sh "mvn clean"
            }
        }
        stage("unit test"){
            steps{
            sh "mvn test"
            }
        }
        stage("Sonar Analysis"){
          steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    
       
    }
    post{
        success{
            sh "echo success"
            }
        }
}
