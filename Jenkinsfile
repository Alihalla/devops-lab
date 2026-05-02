pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\Users\\lenovo\\.kube\\config'
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Alihalla/devops-lab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t webapp:latest .'
            }
        }

        stage('Remove Old Container (if exists)') {
            steps {
                bat 'docker rm -f webapp-container || exit 0'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }

        stage('Force Update (VERY IMPORTANT)') {
            steps {
                bat 'kubectl rollout restart deployment webapp'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }

    }
}