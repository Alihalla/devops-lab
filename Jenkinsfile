pipeline {
    agent any

    stages {

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

        stage('Deploy Kubernetes') {
    	    steps {
        	bat 'set KUBECONFIG=C:\\Users\\lenovo\\.kube\\config && kubectl apply -f deployment.yaml'
        	bat 'set KUBECONFIG=C:\\Users\\lenovo\\.kube\\config && kubectl apply -f service.yaml'
    	    }
	}

    }
}