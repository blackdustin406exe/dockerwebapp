pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-cred')
        IMAGE_NAME = "duynguyen406/dockerwebapp"
    }

        stage('Checkout Code') {
            steps {
                echo '📥 Pulling source code from GitHub...'
                git branch: 'main', credentialsId: 'github-cred', url: 'https://github.com/duynguyen406/DockerWebApp.git'
            }
        }


        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${IMAGE_NAME}:latest"
                }
            }
        }
    }

    post {
        success {
            echo "Build and Push completed successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
