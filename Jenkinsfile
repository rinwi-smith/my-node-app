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
                sh 'sleep 10'
                sh 'curl -s http://host.docker.internal:3000 | grep -q "Hello, World"'
            }
        }
    }
    post {
        always {
            sh 'docker compose down || false'
        }
    }
}
