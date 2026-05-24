pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/yigitsancar/swe304-pro4.git'
            }
        }

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
             sh 'cp -r /home/yigit/.kube /var/lib/jenkins/'
             sh 'cp -r /home/yigit/.minikube /var/lib/jenkins/'
             sh 'sed -i "s|/home/yigit/.minikube|/var/lib/jenkins/.minikube|g" /var/lib/jenkins/.kube/config'

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

