pipeline {
    agent any

    tools {
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('gitcheckout') {
            steps {
                git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/aakumar07/Career_001.git'
            }
        }

        stage('Clean up broken files') {
            steps {
                sh '''
                    find . -type f | grep -P '[^\\x00-\\x7F]' | while read f; do
                      echo "Deleting problematic file: $f"
                      rm -f "$f"
                    done
                '''
            }
        }

        stage('Code-compile-maven') {
            steps {
                sh "mvn compile"
            }
        }

        stage('code-review-sonnarqube') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectName=career \
                        -Dsonar.java.binaries=. \
                        -Dsonar.projectKey=career \
                        -Dsonar.exclusions=**/Interview/**Core*Git*Concepts.txt'''
                }
            }
        }

        stage('nexus artifct'){
            steps{
                withMaven(globalMavenSettingsConfig: 'devops', jdk: '', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                  sh "mvn deploy"
              }
            }
        }
    }
}
