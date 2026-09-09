pipeline {

    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                bat 'mvnw.cmd clean package'
            }
        }
    }

    post {
        success {
            echo 'Build and tests completed successfully.'
        }

        failure {
            echo 'Build failed.'
        }
    }
}