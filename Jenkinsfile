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
                script {
                    def tag = "v${BUILD_NUMBER}"
                    env.IMAGE_TAG = tag
                    bat "docker build -t webapp:${tag} ."
                }
            }
        }

        stage('Update Deployment File') {
            steps {
                script {
                    bat """
                    powershell -Command "(Get-Content deployment.yaml) -replace 'webapp:.*', 'webapp:${IMAGE_TAG}' | Set-Content deployment.yaml"
                    """
                }
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }

        stage('Verify') {
            steps {
                bat 'kubectl get pods'
            }
        }

    }
}