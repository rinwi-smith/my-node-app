pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-node-app .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker rm -f my-app-container || true'
                sh 'docker run -d -p 3000:3000 --name my-app-container my-node-app'
            }
        }
    }
}
