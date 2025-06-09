pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-http-app .'
            }
        }

        stage('Stop Previous Container') {
            steps {
                bat 'docker stop my-http-container || echo "No container to stop"'
                bat 'docker rm my-http-container || echo "No container to remove"'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat 'docker run -d -p 8080:80 --name my-http-container my-http-app'
            }
       
        }  
        stage('Cleanup') {
            steps {
                bat 'docker stop my-http-container && docker rm my-http-container'
                bat 'docker rmi my-http-app'
    }
}
    }
}
