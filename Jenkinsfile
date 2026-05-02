pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\Users\\lenovo\\.kube\\config'
    }

    stages {

        stage('Clean') {
            steps {
                deleteDir()
            }
        }

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Alihalla/devops-lab.git'
            }
        }

        stage('Build Docker') {
            steps {
                bat 'docker build -t webapp:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker rm -f webapp-container || exit 0'
            }
        }

        stage('Run Container') {
            steps {
                bat 'docker run -d -p 5000:5000 --name webapp-container webapp:latest'
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
                bat 'kubectl rollout restart deployment webapp'
            }
        }
    }
}