pipeline {
    agent any
    tools {
        maven 'maven'  // Make sure this tool is configured in Jenkins
        jdk 'jdk11'    // Add JDK tool configuration
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'  // Changed to bat for Windows
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
                junit 'target/surefire-reports/**/*.xml'
            }
        }

        stage('Run JAR') {
            steps {
                script {
                    def output = bat(script: 'java -jar target/simple-java-project-1.0-SNAPSHOT.jar', returnStdout: true).trim()
                    echo "Output from JAR: ${output}"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Only deploy if not on Windows
                    if (!isUnix()) {
                        echo "Skipping Docker deployment on Windows agent"
                    } else {
                        sh 'docker build -t myapp .'
                        sh 'docker run -d -p 8080:80 myapp'
                    }
                }
            }
        }
    }
}