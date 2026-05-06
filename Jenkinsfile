pipeline {
    agent any

    environment {
        DOCKERHUB_USERNAME = 'naurafaizah'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/naurafaizah/TP2CloudComp.git'
            }
        }

        stage('Test Stage') {
            steps {
                echo 'Pipeline jalan sampai sini'
            }
        }

        stage('Build Backend') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker build -t $DOCKERHUB_USERNAME/backend-naura:latest ./backend'
                    } else {
                        bat 'docker build -t %DOCKERHUB_USERNAME%/backend-naura:latest ./backend'
                    }
                }
            }
        }
    }
}
