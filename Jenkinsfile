pipeline {

    agent any

    stages {
        stage('Build Jar') 
        {
            steps {
                bat "mvn clean package -DskipTests"
        }
        stage('Build Docker Image') {
            steps {
                bat "docker build -t=adamburczykdev/selenium ."
            }
        }
        stage('Push Docker Image') {
            steps {
                bat "docker push adamburczykdev/selenium"
            }
        }
    }
    }

    post {
        always {
            echo 'This will always run after the stages.'
        }
        success {
            echo 'This will run only if the pipeline succeeds.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
    }
}