pipeline {
    agent any
    stages {
        stage('Clean Up') {
            steps {
                sh 'docker compose down || true'
                sh 'docker rm -f my-app-container || true'
            }
        }
        stage('Build and Run with Docker Compose') {
            steps {
                sh 'docker compose up -d --build --force-recreate'
                sh 'sleep 5'
                sh 'docker ps -a'
                sh 'docker logs my-app-container || true'
            }
        }
        stage('Test App') {
            steps {
                sh 'sleep 15'
                sh '''
                    echo "Checking container status..."
                    docker ps -a | grep my-app-container || {
                        echo "Container not running!"
                        docker logs my-app-container || true
                        exit 1
                    }
                    echo "Testing app with curl..."
                    curl -s --retry 5 --retry-delay 2 http://my-app-container:3000 | grep -q "Hello,.*World" || {
                        echo "Test failed, response was:"
                        curl -s http://my-app-container:3000
                        exit 1
                    }
                    echo "Test passed!"
                '''
            }
        }
    }
    post {
        always {
            sh 'docker compose down || true'
        }
    }
}
