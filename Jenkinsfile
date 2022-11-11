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
                    sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.8.0.2131:sonar" 
                }
            }
        }
    stage("Publish to Artifactory"){
            steps{
                rtMavenDeployer(
                    id: 'deployer',
                    serverId: '12345678@artifactory',
                    releaseRepo: 'varsha.rajput',
                    snapshotRepo: 'varsha.rajput'
                )
                rtMavenRun(
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: 'deployer'
                    )
                rtPublishBuildInfo(
                    serverId:'12345678@artifactory',
                )
            }        
        }
        stage("Invoke UI Test Pipeline"){
			steps{
				build job: 'Dev-Ops-Freestyle-Practice'
			}
		}
       
    }
    post{
        success{
            sh "echo success"
            }
        }
}
