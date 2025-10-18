pipeline {
    agent any

    stages {
        stage('Build Jar') 
        {
            steps('Clean and Package') {
                bat "mvn clean package -DskipTests"
        }
        }
        stage('Build Docker Image') {
            steps {
                bat "docker build -t=adamburczykdev/selenium:latest ."
            }
        }
        stage('Push Docker Image') { 
            environment {
                DOCKER_HUB = credentials('dockerhub-creds')
            }
            steps {
                bat "echo ${DOCKER_HUB_PSW} | docker login --username ${DOCKER_HUB_USR} --password-stdin"
                bat "docker push adamburczykdev/selenium:latest"
                bat "docker tag adamburczykdev/selenium:latest adamburczykdev/selenium:${env.BUILD_NUMBER}"
                bat "docker push adamburczykdev/selenium:${env.BUILD_NUMBER}"
            }
        }
    }

    post {
        always {
            bat "docker logout"
        }
    }
}