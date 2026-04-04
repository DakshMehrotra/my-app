pipeline {
    agent any

    environment {
        IMAGE_NAME = "daksh24/myapp"
        DOCKER = "/usr/bin/docker"
    }

    stages {

        stage('Clone Source') {
            steps {
                git branch: 'main', url: 'https://github.com/DakshMehrotra/my-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '$DOCKER build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    sh 'echo $DOCKER_TOKEN | $DOCKER login -u daksh24 --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh '$DOCKER push $IMAGE_NAME:latest'
            }
        }
    }
}
