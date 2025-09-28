pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/MaryannCU/ecommerce-devops-project',
                    credentialsId: 'github-token'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("your-dockerhub-username/ecommerce-app:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        docker.image("your-dockerhub-username/ecommerce-app:${BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
