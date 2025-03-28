pipeline {
    agent {
        docker {
            image 'maven:3.8.6-jdk-11'  // Pre-configured Java/Maven environment
            args '-v /root/.m2:/root/.m2'  // Persistent Maven cache
        }
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
                    extensions: [[
                        $class: 'CleanBeforeCheckout'
                    ]],
                    userRemoteConfigs: [[
                        url: 'https://github.com/chaitanya-3006/newone.git',
                        credentialsId: 'github-credentials'  // Create this in Jenkins
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
                junit 'target/surefire-reports/**/*.xml'  // Test reports
            }
        }

        stage('Build Docker Image') {
            when {
                branch 'main'  // Only run for main branch
            }
            steps {
                script {
                    docker.build("${APP_NAME}:${VERSION}-${env.BUILD_NUMBER}")
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed - cleaning workspace'
            cleanWs()  // Clean up workspace
        }
        success {
            slackSend(
                channel: '#builds',
                message: "✅ Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
            )
        }
        failure {
            slackSend(
                channel: '#build-errors',
                message: "❌ Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
            )
        }
    }
}