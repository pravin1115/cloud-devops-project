pipeline {
    agent any

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main',
                url: 'https://github.com/pravin1115/cloud-devops-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t pravin1502/cloud-devops-app:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push pravin1502/cloud-devops-app:v1'
            }
        }
    }
}