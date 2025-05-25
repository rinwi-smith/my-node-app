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
                sh 'docker compose up -d --build --force-recreate'
            }
        }
        stage('Test App') {
            steps {
                sh 'sleep 15'
                sh 'curl -s --retry 3 --retry-delay 2 http://localhost:3000 | grep -q "Hello,.*World"'
            }
        }
    }
    post {
        always {
            sh 'docker compose down || true'
        }
    }
}
