pipeline {
    agent any
    stages {
        stage('Clean Up') {
            steps {
                sh 'docker-compose down || true'
            }
        }
        stage('Build and Run with Docker Compose') {
            steps {
                sh 'docker-compose up -d --build'
            }
        }
        stage('Test App') {
            steps {
                sh 'sleep 5'
                sh 'curl -s http://my-app-container:3000 | grep "Hello, World!"'
            }
        }
    }
    post {
        failure {
            sh 'docker-compose down || true'
        }
    }
}
