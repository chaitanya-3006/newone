pipeline {
    agent any
    tools{
    maven 'maven'  // Use the maven tool auto-installed by Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checks out code from your SCM (Git, etc.)
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
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

