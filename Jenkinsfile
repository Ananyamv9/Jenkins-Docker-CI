
pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "abh-app"
        DOCKER = "C:/Users/STUDENT/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe"
        PYTHON = "C:/Users/STUDENT/AppData/Local/Programs/Python/Python313/python.exe"
    }

    stages {

        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                echo "Running Python Application..."

                bat "\"${PYTHON}\" app.py"
            }
        }

        stage('3. Build & Tag Docker Image') {
            steps {
                echo "Building Docker Image..."

                bat "\"${DOCKER}\" build -t ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} -t ${REGISTRY}/${IMAGE_NAME}:latest ."
            }
        }

        stage('4. Push Image to Registry') {
            steps {
                echo "Pushing Docker Image to Local Registry..."

                bat "\"${DOCKER}\" push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}"

                bat "\"${DOCKER}\" push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded!"
            echo "Image ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} pushed successfully."
            echo "Image ${REGISTRY}/${IMAGE_NAME}:latest pushed successfully."
        }

        failure {
            echo "Pipeline failed! Check Jenkins Console Output."
        }

        always {
            echo "Jenkins Pipeline Execution Completed."
        }
    }
}
