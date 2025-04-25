pipeline{
    agent any
    
    tools {
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages{
        stage("git clone"){
            steps{
                git branch: 'main', credentialsId: 'c32c6e7c-3757-42d7-89e2-1928c575d584', url: 'https://github.com/aakumar07/Career_001.git'
            }
        }

        stage("complie"){
            steps{
                sh "mvn compile"
            }
        }

        stage{
            steps{
                withSonarQubeEnv('SonarQube') {
                  sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=career \
                        -Dsonar.java.binaries=. \
                        -Dsonar.projectKey=career '''
            }
        }
    }

}
