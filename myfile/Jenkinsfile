pipeline {
    agent any
    environment {
        AWS_CREDENTIALS = credentials('aws-credentials-id')
        KUBECONFIG = credentials('kubeconfig-id')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('my-app-image:latest')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        docker.image('my-app-image:latest').push()
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                withAWS(credentials: 'aws-credentials-id', region: 'us-east-1') {
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}

