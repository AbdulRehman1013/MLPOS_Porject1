pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t flask-mlops-app .'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    // Stop and remove the old container if it exists
                    sh 'docker stop flask-container || true'
                    sh 'docker rm flask-container || true'
                    
                    // Run the newly built container and map port 8000
                    sh 'docker run -d -p 8000:8000 --name flask-container flask-mlops-app'
                }
            }
        }
    }
}