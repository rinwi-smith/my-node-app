pipeline {
    agent any
    stages {
        stage('Build and Run with Docker Compose') {
            steps {
                sh 'docker compose down || true'
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
