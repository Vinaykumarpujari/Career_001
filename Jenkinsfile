pipeline{
    agent any

    tools {
        maven 'maven3'
    }

    stages{
        stage("github cloing pahase"){
            steps{
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/aakumar07/Career_001.git'
            }
        }

        stage("maven complie"){
            steps{
                sh "mvn compile"
            }
        }
    }
}
