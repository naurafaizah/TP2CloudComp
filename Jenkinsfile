pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-creds'
        DOCKERHUB_USERNAME = 'naurafaizah'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'URL_REPO_GITHUB_KAMU'
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t $DOCKERHUB_USERNAME/backend-naura:latest ./backend'
            }
        }

        stage('Build Frontend') {
            steps {
                sh 'docker build -t $DOCKERHUB_USERNAME/frontend-naura:latest ./frontend'
            }
        }

        stage('Push Images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push $DOCKERHUB_USERNAME/backend-naura:latest
                    docker push $DOCKERHUB_USERNAME/frontend-naura:latest
                    '''
                }
            }
        }

        stage('Deploy to AKS') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}