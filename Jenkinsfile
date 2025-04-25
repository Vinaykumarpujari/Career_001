pipeline {
    agent any

    tools {
        maven 'maven3' // Define this under Jenkins → Global Tool Configuration
        sonarQubeScanner 'SonarScanner' // Also define this under tools
    }

    environment {
        SONARQUBE_ENV = 'SonarQube'         // Name of SonarQube server in Jenkins config
        SONAR_TOKEN = credentials('SONAR_TOKEN') // Sonar token stored securely in Jenkins
    }

    stages {
        stage("Git Checkout") {
            steps {
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/aakumar07/Career_001.git'
            }
        }

        stage("Compile") {
            steps {
                sh "mvn clean compile"
            }
        }

        stage("SonarQube Analysis") {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh "mvn verify sonar:sonar -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }
    }
}
