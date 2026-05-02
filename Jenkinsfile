pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Alihalla/devops-lab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build --pull=false -t webapp:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker rm -f webapp || exit 0'
            }
        }

        stage('Run New Container') {
            steps {
                bat 'docker run -d -p 5000:5000 --name webapp webapp:latest'
            }
        }

    }

    post {
        success {
            echo 'Deployment successful! App is running on http://localhost:5000'
        }
        failure {
            echo 'Build failed, check logs'
        }
    }
}
