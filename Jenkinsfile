pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Alihalla/devops-lab.git'
            }
        }
        stage('Build Docker') {
            steps {
                bat 'docker build -t webapp:%BUILD_NUMBER% .'
            }
        }
        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl set image deployment/webapp webapp=webapp:%BUILD_NUMBER%'
            }
        }
    }
}