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
                bat 'mvn test'
                junit 'target/surefire-reports/**/*.xml' 
                bat 'echo Running tests...'
                // Replace with your test command
            }
        }
        stage('Run JAR') {
            steps {
                script {
                    // Run the JAR file and capture the output
                    def output = bat(script: 'java -jar target/simple-java-project-1.0-SNAPSHOT.jar', returnStdout: true).trim()

                    // Print the output to Jenkins console
                    echo "Output from JAR: ${output}"
                }
            }
        }
    }

    post {
        failure {
            echo "Build failed!"
        }
    }
}

