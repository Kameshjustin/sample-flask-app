pipeline {
    agent {
        docker { image 'python:3.10-slim' }  // Use official Python image
    }
    environment {
        DOCKERHUB_CRED = credentials('dockerhub-credentials')
        IMAGE_NAME = 'kamesh/sample-flask-app'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Kameshjustin/sample-flask-app.git'
            }
        }

        stage('Install & Test') {
            steps {
                sh 'pip install --upgrade pip'
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }
}





















"""
pipeline {
    agent any
    environment {
        DOCKERHUB_CRED = credentials('dockerhub-credentials')
        IMAGE_NAME = 'kamesh/sample-flask-app'
    }
    stages {
        stage('Checkout') {
            steps { git branch: 'main', url: 'https://github.com/Kameshjustin/sample-flask-app.git'
 }
        }
        stage('Install & Test') {
            steps { sh 'pip install -r requirements.txt' }
        }
        stage('Docker Build') {
            steps { script { docker.build("{IMAGE_NAME}:latest") } }
        }
        stage('Docker Push') {
            steps { script { docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') { docker.image("${IMAGE_NAME}:latest").push() } } }
        }
    }
}

"""