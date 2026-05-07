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
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'USER',
                        passwordVariable: 'PASS'
                    )
                ]) {

                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin

                    docker build -t naurafaizah/backend-naura:latest ./backend
                    docker build -t naurafaizah/frontend-naura:latest ./frontend

                    docker push naurafaizah/backend-naura:latest
                    docker push naurafaizah/frontend-naura:latest
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                kubectl apply -f yaml/
                '''
            }
        }
    }
}
