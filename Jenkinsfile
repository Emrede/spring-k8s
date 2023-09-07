pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from repository
                checkout scm
            }
        }
        
        stage('Build Spring Boot App') {
            steps {
                // Build Spring Boot application with Gradle
                sh './gradlew clean build'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                sh 'docker build -t helloworld-app .'
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push the Docker image to a registry
                sh 'docker tag helloworld-app:latest emrede/helloworld-app:latest'
                sh 'docker push emrede/helloworld-app:latest'
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                // Apply Kubernetes configurations
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
