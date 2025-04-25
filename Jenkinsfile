pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    environment {
        SCANNER_HOME = tool 'sonar_server'
    }

    stages {
        stage("GitHub Repo Clone") {
            steps {
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/aakumar07/Career_001.git'
            }
        }

        stage("Code Compile") {
            steps {
                sh "mvn compile"
            }
        }

        stage("Code Review") {
            steps {
                withSonarQubeEnv('sonar_server') {
                    sh "mvn clean sonar:sonar"
                }
            }
        }

        stage("Build Package") {
            steps {
                sh "mvn clean package"
            }
        }
    }
}
