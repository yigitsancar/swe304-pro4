pipeline {
    agent any

    stages {

        stage('Clone Check') {
            steps {
                sh 'pwd'
                sh 'ls'
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
                sh 'docker build -t swe304-pro4:latest .'
            }
        }

        stage('Docker Images') {
            steps {
                sh 'docker images'
            }
        }

    }
}
