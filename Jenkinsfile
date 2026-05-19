pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t yigitsancar/swe304-pro4:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push yigitsancar/swe304-pro4:latest'
            }
        }

        stage('Kubernetes Deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
                sh 'kubectl rollout restart deployment swe304-pro4-deployment'
            }
        }

        stage('Kubernetes Status') {
            steps {
                sh 'kubectl get pods'
                sh 'kubectl get services'
            }
        }

    }
}
