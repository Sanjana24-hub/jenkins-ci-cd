pipeline {
    agent any

    environment {
        GIT_CREDENTIALS_ID = 'github-credentials'  // Jenkins credentials ID for GitHub
        GIT_REPO = 'https://github.com/Sanjana24-hub/jenkins-ci-cd.git'
        GIT_BRANCH = 'main'
        SMTP_USER = credentials('gmail-smtp')  // Stored SMTP credentials for email notifications
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/${GIT_BRANCH}"]],
                        userRemoteConfigs: [[
                            url: GIT_REPO,
                            credentialsId: GIT_CREDENTIALS_ID
                        ]]
                    ])
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Skipping build step (No Maven)...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running tests on staging...'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
            }
        }
    }

    post {
        always {
            script {
                emailext(
                    subject: "Jenkins Pipeline Execution - ${currentBuild.result}",
                    body: """Pipeline Execution Completed. Check Jenkins for details.
                    <br>Check logs: <a href='${env.BUILD_URL}'>Build Logs</a>""",
                    to: 'sanjana4809.be23@chitkara.edu.in',
                    replyTo: env.SMTP_USER,
                    mimeType: 'text/html'
                )
            }
        }
    }
}
