pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')   // Jenkins credential ID
        IMAGE_NAME = "laxmir22095/java-cicd-app"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Laxmi7676/java-cicd-app.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh "${tool 'MAVEN_HOME'}/bin/mvn clean package -DskipTests"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                sh "docker push ${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "Build & Push Completed Successfully 🎉🚀"
        }
        failure {
            echo "Pipeline Failed ❌"
        }
    }
}
