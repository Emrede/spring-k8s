pipeline {
    agent any 

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from repository
                checkout scm
            }
        }
        
        // Uncomment this stage to install dependencies if needed
        // stage('Install Dependencies') {
        //     steps {
        //         // Install Java
        //         sh '''
        //           apt-get update
        //           apt-get install -y openjdk-17-jdk
        //         '''
        //     }
        // }
        
        stage('Build Spring Boot App') {
            steps {
                // Build Spring Boot application with Gradle
                sh '''
                    cd HelloWorld
                    ./gradlew clean build
                    '''
            }
        }

        // Dockerize the Java app
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                sh '''
                    cd HelloWorld
                    docker build -t spring-hello-world .
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push the Docker image to a registry
                sh '''
                    docker tag spring-hello-world:latest emrede/spring-hello-world:latest
                    docker push emrede/spring-hello-world:latest
                '''
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
