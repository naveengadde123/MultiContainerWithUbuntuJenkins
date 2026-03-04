pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "multiapp"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning repository..."
                checkout scm
            }
        }

        stage('Stop Old Containers') {
            steps {
                echo "Stopping old containers if running..."
                sh 'docker compose down || true'
            }
        }

        stage('Build Docker Images') {
            steps {
                echo "Building containers..."
                sh 'docker compose build'
            }
        }

        stage('Start Containers') {
            steps {
                echo "Starting containers..."
                sh 'docker compose up -d'
            }
        }

        stage('Verify Running Containers') {
            steps {
                echo "Checking running containers..."
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo "Deployment Successful!"
        }
        failure {
            echo "Deployment Failed!"
        }
    }
}