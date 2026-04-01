pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "altinelg/demo-app"
        VERSION = "altinelg/demo-app:${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:$VERSION .'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push $DOCKER_IMAGE:$VERSION'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/demo-app demo-app=$DOCKER_IMAGE:$VERSION'
            }
        }
    }
}
