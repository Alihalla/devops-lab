pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Alihalla/devops-lab.git'
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
	stage('Run Container') {
            steps {
                bat 'docker run -d -p 5000:5000 webapp:latest'
            }
        }
    }

    post {
        success {
            echo 'Pipeline exécuté avec succès'
        }
        failure {
            echo 'Pipeline échoué'
        }
    }
}
