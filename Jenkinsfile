pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = 'phone-shop'
        DOCKER_REGISTRY = 'freyda24'
        DOCKER_REGISTRY_CREDENTIALS = 'docker-hub-credentials'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/freyda-hash/phone-shop.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh "docker build -t ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}-frontend:latest ./client"
                sh "docker build -t ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}-backend:latest ./server"
                sh "docker build -t ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}-mysql:latest ./mysql-data"
            }
        }

        stage('Push Docker Images') {
            steps {
                withDockerRegistry([credentialsId: DOCKER_REGISTRY_CREDENTIALS, url: 'https://index.docker.io/v1/']) {
                    sh "docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}-frontend:latest"
                    sh "docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}-backend:latest"
                    sh "docker push ${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}-mysql:latest"
                }
            }
        }

        stage('Deploy') {
            steps {
                sh "docker compose -f docker-compose.yml up -d"
            }
        }

        stage('Cleanup') {
            steps {
                sh "docker system prune -f"
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Deployment failed.'
        }
