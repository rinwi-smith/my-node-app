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
    }
    post {
        always {
            sh 'docker compose down || true'
        }
    }
}
