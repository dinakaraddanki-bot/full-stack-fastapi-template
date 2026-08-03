pipeline {

    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Verify Environment') {
            steps {
                bat '''
                git --version
                docker --version
                java -version
                '''
            }
        }

        stage('Docker Build') {
            steps {
                bat '''
                docker compose build
                '''
            }
        }

        stage('Start Application') {
            steps {
                bat '''
                docker compose up -d
                '''
            }
        }

        stage('Verify Containers') {
            steps {
                bat '''
                docker ps
                '''
            }
        }
    }

    post {
        always {
            bat '''
            docker compose down
            '''
        }
    }
}