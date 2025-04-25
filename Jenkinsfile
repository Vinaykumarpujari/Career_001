pipeline{
    agent any

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
