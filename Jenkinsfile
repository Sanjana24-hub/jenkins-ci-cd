pipeline {
    agent any
    
    environment {
        // Git Credentials
        GIT_CREDENTIALS_ID = '51dce4ea-fa48-4e6d-bd33-781e009f5571'  
        GIT_REPO = 'https://github.com/Sanjana24-hub/jenkins-ci-cd.git'
        GIT_BRANCH = 'main'

        // SMTP Configuration
        SMTP_USER = 'sanjana4809.be23@chitkara.edu.in'
        SMTP_PASS = 'xklsxopfftsemvvq'
        SMTP_SERVER = 'smtp.gmail.com'
        SMTP_PORT = '587'
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
                echo 'Building the application...'
                // Add actual build commands here if needed
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                // Add your test commands here
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Add your code analysis commands here
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Add your security scan commands here
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                // Add your staging deployment commands here
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running tests on staging...'
                // Add your staging tests commands here
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                // Add your production deployment commands here
            }
        }
    }
    
    post {
        always {
            script {
                emailext(
                    subject: "Jenkins Pipeline: ${currentBuild.fullDisplayName} - ${currentBuild.result}",
                    body: """<html>
                        <body>
                            <h2>Build Summary</h2>
                            <p><b>Project:</b> ${env.JOB_NAME}</p>
                            <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                            <p><b>Status:</b> ${currentBuild.result}</p>
                            <p><b>Duration:</b> ${currentBuild.durationString}</p>
                            <p><b>Complete Build Log:</b> <a href='${env.BUILD_URL}console'>View Log</a></p>
                            <p><b>Changes:</b> <a href='${env.BUILD_URL}changes'>View Changes</a></p>
                        </body>
                    </html>""",
                    to: 'sanjana4809.be23@chitkara.edu.in',
                    from: SMTP_USER,
                    replyTo: SMTP_USER,
                    mimeType: 'text/html',
                    smtpHost: SMTP_SERVER,
                    smtpPort: SMTP_PORT,
                    username: SMTP_USER,
                    password: SMTP_PASS,
                    useSsl: false,
                    useTls: true
                )
            }
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs for details.'
        }
    }
}

