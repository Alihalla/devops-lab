pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Alihalla/devops-lab.git'
            }
        }
	stage('Stop Old Container') {
    	    steps {
        	bat 'docker stop webapp || exit 0'
        	bat 'docker rm webapp || exit 0'
    	    }
	}
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t webapp:latest .'
            }
     	}

        stage('Run New Container') {
            steps {
                bat 'docker run -d -p 5000:5000 --name webapp webapp:latest'
            }
        }
    }
}
