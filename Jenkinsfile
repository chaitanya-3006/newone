pipeline {
    agent any
    
    tools {
        maven 'maven'  // Must match exact name in Jenkins Global Tool Config
        jdk 'JDK11'    // Must match exact name in Jenkins Global Tool Config
    }
    
    environment {
        APP_NAME = 'newone'
        VERSION = '1.0.0'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/chaitanya-3006/newone.git',
                        credentialsId: 'github-credentials'
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
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
                bat 'java -jar target/simple-java-project-1.0-SNAPSHOT.jar'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed'
            // Simple cleanup - remove 'cleanWs()' if plugin not installed
            deleteDir()  
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
