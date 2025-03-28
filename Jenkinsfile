pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                script {
                    sh 'javac Main.java' // Change 'Main.java' to your actual Java file
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    sh 'java Main' // Change 'Main' to your actual Java class
                }
            }
        }
    }
    
    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}

