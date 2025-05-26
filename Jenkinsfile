pipeline {
    agent any
    stages {
        stage('Clean Up') {
            steps {
                sh 'docker compose down || true'
            }
        }
        stage('Build and Run with Docker Compose') {
            steps {
                sh 'docker compose up -d --build'
            }
        }
        stage('Test App') {
            steps {
                sh 'sleep 15'
                sh 'curl -s http://localhost:3000 | grep "Hello, World!"'
            }
        }
    }
    post {
        always {
            sh 'docker compose down || true'
        }
    }
}
