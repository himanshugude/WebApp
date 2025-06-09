pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                // Repo is already checked out automatically in multibranch or pipeline from SCM
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t my-http-app .'
            }
        }

        stage('Stop Previous Container') {
            steps {
                script {
                    def stopStatus = bat(script: 'docker stop my-http-container', returnStatus: true)
                    if (stopStatus != 0) {
                        echo "No existing container to stop"
                    }

                    def rmStatus = bat(script: 'docker rm my-http-container', returnStatus: true)
                    if (rmStatus != 0) {
                        echo "No existing container to remove"
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running new container...'
                bat 'docker run -d -p 8081:80 --name my-http-container my-http-app'
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    def stopStatus = bat(script: 'docker stop my-http-container', returnStatus: true)
                    if (stopStatus == 0) {
                        bat 'docker rm my-http-container'
                    }

                    def rmiStatus = bat(script: 'docker rmi my-http-app', returnStatus: true)
                    if (rmiStatus != 0) {
                        echo "Image already removed or doesn't exist"
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished. You can check Docker status if needed.'
        }
        failure {
            echo 'Pipeline failed. You may want to troubleshoot the logs above.'
        }
    }
}
