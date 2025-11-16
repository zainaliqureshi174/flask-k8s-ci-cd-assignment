pipeline {
    agent any
    
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    sh 'docker build -t flask-app:latest .'
                    sh 'minikube image load flask-app:latest'
                }
            }
        }
        
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    echo 'Deploying to Kubernetes...'
                    sh 'kubectl apply -f kubernetes/'
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                script {
                    echo 'Verifying deployment...'
                    sh 'kubectl rollout status deployment/flask-app'
                    sh 'kubectl get pods'
                    sh 'kubectl get services'
                }
            }
        }
    }
}
