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
            steps{
            withSonarQubeEnv("Test_SonarQube")
                {
		    sh "echo Sonar Run half"
                        sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.8.0.2131:sonar"        
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
