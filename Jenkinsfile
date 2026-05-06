pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-creds'
        DOCKERHUB_USERNAME = 'naurafaizah'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/naurafaizah/TP2CloudComp.git'
            }
        }

        stage('Build & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin

                    docker build -t $DOCKERHUB_USERNAME/backend-naura:latest ./backend
                    docker build -t $DOCKERHUB_USERNAME/frontend-naura:latest ./frontend

                    docker push $DOCKERHUB_USERNAME/backend-naura:latest
                    docker push $DOCKERHUB_USERNAME/frontend-naura:latest
                    '''
                }
            }
        }

        stage('Deploy ke Azure AKS') {
            steps {
                sh 'kubectl apply -f yaml/'
            }
        }
    }
}
