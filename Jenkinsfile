pipeline {
    agent any

    environment {
        IMAGE_NAME = "blackdustin406exe/dockerwebapp"
        DOCKER_CREDENTIALS = credentials('dockerhub-cred')
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Pulling source code from GitHub...'
                git branch: 'main', credentialsId: 'github-cred', url: 'https://github.com/blackdustin406exe/dockerwebapp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    sh "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                echo 'Logging in to Docker Hub...'
                script {
                    sh "echo ${DOCKER_CREDENTIALS_PSW} | docker login -u ${DOCKER_CREDENTIALS_USR} --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing image to Docker Hub...'
                script {
                    sh "docker push ${IMAGE_NAME}:latest"
                }
            }
        }
    }

    post {
        success {
            echo 'Build & Push completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
