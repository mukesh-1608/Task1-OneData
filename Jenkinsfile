pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t task1-onedata-app .'
            }
        }
        stage('Run Docker Container') {
            steps {
                bat 'docker run -d --rm -p 3000:3000 --name task1-onedata-app task1-onedata-app'
            }
        }
    }
    post {
        always {
            bat 'docker rm -f task1-onedata-app || exit 0'
        }
    }
}
