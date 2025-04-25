pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    environment {
        SONARQUBE_ENV = 'SonarQube' // This must match the name in Jenkins > Configure System > SonarQube servers
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/aakumar07/Career_001.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'TOKEN')]) {
                        sh 'mvn verify sonar:sonar -Dsonar.login=$TOKEN'
                    }
                }
            }
        }
    }
}
