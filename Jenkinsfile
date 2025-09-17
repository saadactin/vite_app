pipeline {
    agent any

    environment {
        IMAGE_NAME = "react_vite_app"
        CONTAINER_NAME = "react_vite_container"
        PORT = "5173"
        GIT_REPO = "https://github.com/saadactin/vite_app.git"
    }

    stages {
        stage('Checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/saadactin/react_app.git'

            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME} ."
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Remove old container if it exists
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    
                    // Run new container
                    sh "docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        success {
            echo "React Vite app is running on port ${PORT}"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
