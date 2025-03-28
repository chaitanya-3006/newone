pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/chaitanya-3006/newone.git'
            }
        }

        stage('Build') {
            steps {
                bat 'echo Building the project...'
                // Replace with your actual build command
            }
        }

        stage('Test') {
            steps {
                bat 'echo Running tests...'
                // Replace with your test command
            }
        }
    }

    post {
        failure {
            echo "Build failed!"
        }
    }
}

