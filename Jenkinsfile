pipeline {
    agent any
    
    environment {
        GIT_CREDENTIALS_ID = '86b95b27-66ee-45f4-81e0-0c1bcfc2065d'  
        GIT_REPO = 'https://github.com/Sanjana24-hub/jenkins-ci-cd.git'
        GIT_BRANCH = 'main'
        SMTP_CREDS = credentials('gmail-smtp') // Ensure this credential ID is correct
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
                    to: 'sanjanakumari5700@gmail.com', // Ensure this email is correct
                    from: 'jenkins@example.com', // Update with a valid sender email
                    replyTo: 'sanjanakumari5700@gmail.com',
                    mimeType: 'text/html'
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
