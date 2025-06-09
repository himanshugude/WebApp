pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t my-http-app .'
            }
        }

       

        stage('Run Docker Container') {
            steps {
                echo 'Running new container...'
                bat 'docker run -d -p 8081:80 --name my-http-container my-http-app'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
