pipeline{
    agent any

    tools {
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-server'
    }

    stages{
        stage("GitHub repo Clone"){
            steps{
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/aakumar07/Career_001.git'
            }
        }

        stage("Code complile"){
            steps{
                sh "mvn compile"
            }
        }
    }
}
