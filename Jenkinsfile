pipeline {
    agent any
    stages {
        stage('GitHub'){
            steps {
                git branch: 'main', credentialsId: 'web-app-jenkins', url: 'https://github.com/youssefismail811/web-app-jenkins.git'
            }
        }
    }
}