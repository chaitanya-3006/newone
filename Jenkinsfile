pipeline {
    agent any  // Runs on any available Jenkins agent
     tools{
    maven 'maven'  // Use the maven tool auto-installed by Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checks out code from your SCM (Git, etc.)
            }
        }

        // Stage 2: Build the project
        stage('Build') {
            steps {
                sh 'mvn clean package'  // For Java/Maven projects
                // Alternative for Node.js: sh 'npm install && npm run build'
            }
        }

        // Stage 3: Run tests
        stage('Test') {
            steps {
                sh 'mvn test'  // Runs unit tests
                // For test reports:
                junit 'target/surefire-reports/**/*.xml' 
            }
        }
        stage('Run JAR') {
            steps {
                script {
                    // Run the JAR file and capture the output
                    def output = sh(script: 'java -jar target/simple-java-project-1.0-SNAPSHOT.jar', returnStdout: true).trim()

                    // Print the output to Jenkins console
                    echo "Output from JAR: ${output}"
                }
            }
        }
        // Stage 4: Deploy (example for Docker)
        stage('Deploy') {
            steps {
                sh 'docker build -t myapp .'
                sh 'docker run -d -p 8080:80 myapp'
            }
        }
    }
    
}