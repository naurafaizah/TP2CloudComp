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
                script {
                    if (isUnix()) {
                        sh '''
                        echo "Build & Push (Linux)"

                        docker build -t $DOCKERHUB_USERNAME/backend-naura:latest ./backend
                        docker build -t $DOCKERHUB_USERNAME/frontend-naura:latest ./frontend
                        '''
                    } else {
                        bat '''
                        echo Build & Push (Windows)

                        docker build -t %DOCKERHUB_USERNAME%/backend-naura:latest ./backend
                        docker build -t %DOCKERHUB_USERNAME%/frontend-naura:latest ./frontend
                        '''
                    }
                }
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
