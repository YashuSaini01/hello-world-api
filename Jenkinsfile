pipeline {

    agent any

    tools {
        jdk 'JDK-21'
    }

    stages {

        stage('Build and Test') {
            steps {
                bat 'mvnw.cmd clean package'
            }
        }

        stage('Check Docker') {
            steps {
                bat 'docker --version'
                bat 'docker info'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t yashsaini1/hello-world-api:1.0 .'
            }
        }

        stage('Verify Docker Image') {
            steps {
                bat 'docker images'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_TOKEN'
                    )
                ]) {
                    bat '''
                        echo %DOCKER_TOKEN% | docker login -u %DOCKER_USERNAME% --password-stdin
                        docker push yashsaini1/hello-world-api:1.0
                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}