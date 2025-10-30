pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling source code from Git...'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t molugarisaideepthi07/flask-demo:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                echo 'Logging in to Docker Hub...'
                bat "docker login -u %DOCKERHUB_CREDENTIALS_USR% -p %DOCKERHUB_CREDENTIALS_PSW%"
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing image to Docker Hub...'
                bat 'docker push molugarisaideepthi07/flask-demo:latest'
            }
        }
    }

    post {
        success {
            echo '✅ Docker image pushed successfully!'
        }
        failure {
            echo '❌ Build failed. Check Jenkins logs.'
        }
    }
}
