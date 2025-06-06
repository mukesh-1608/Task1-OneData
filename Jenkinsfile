pipeline {
    agent any
    environment {
        IMAGE_NAME = 'task1-onedata-app'
        IMAGE_TAG = 'latest'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mukesh-1608/Task1-OneData.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                sh "docker run -d --rm -p 3000:3000 --name ${IMAGE_NAME} ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }
    post {
        always {
            sh "docker rm -f ${IMAGE_NAME} || true"
        }
    }
}
