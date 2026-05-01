pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Alihalla/devops-lab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t webapp:latest .'
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
}
