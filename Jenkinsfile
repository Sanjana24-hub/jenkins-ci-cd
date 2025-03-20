pipeline {
    agent any
    environment {
        SMTP_CREDENTIALS = credentials('smtp-credentials-id') // Use Jenkins credentials
    }
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Tests') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
    post {
        always {
            script {
                emailext(
                    subject: "Jenkins Build - ${currentBuild.result}",
                    body: "Build ${env.JOB_NAME} - ${env.BUILD_NUMBER} has finished with status: ${currentBuild.result}\nCheck console output at ${env.BUILD_URL}",
                    to: 'sanjana4809.be23@chitkara.edu.in',
                    replyTo: 'no-reply@yourdomain.com',
                    attachLog: true
                )
            }
        }
    }
}


