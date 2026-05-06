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

        stage('Build & Push') {
            steps {
                sh '''
                docker build -t $DOCKERHUB_USERNAME/backend-naura:latest ./backend
                docker build -t $DOCKERHUB_USERNAME/frontend-naura:latest ./frontend

                docker push $DOCKERHUB_USERNAME/backend-naura:latest
                docker push $DOCKERHUB_USERNAME/frontend-naura:latest
                '''
            }
        }

        stage('Deploy') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'kubectl apply -f yaml/'
                    } else {
                        bat 'kubectl apply -f yaml/'
                    }
                }
            }
        }
    }
}
