pipeline {
    agent any
    tools {
        nodejs 'NodeJs'
    }
    environment {
        SONAR_PROJECT_KEY = 'devops'
        SONAR_SCANNER_HOME = 'sonarqubescanner'
        SONARQUBE_URL = 'http://localhost:9000' // Update with your SonarQube URL
    }
    stages {
        stage('GitHub') {
            steps {
                git branch: 'main', credentialsId: 'web-app-jenkins', url: 'https://github.com/youssefismail811/web-app-jenkins.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'npm test'
            }
        }       
        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'devops-token', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('sonarqube') {
                        sh """
                        ${SONAR_SCANNER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=${SONAR_PROJECT_KEY} \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=${SONARQUBE_URL} \
                        -Dsonar.login=${SONAR_TOKEN}
                        """
                    }
                }
            }
        }
    }
}
