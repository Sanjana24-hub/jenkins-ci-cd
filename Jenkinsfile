pipeline {
    agent any
    
    environment {
        GIT_CREDENTIALS_ID = '51dce4ea-fa48-4e6d-bd33-781e009f5571'
        GIT_REPO = 'https://github.com/Sanjana24-hub/jenkins-ci-cd.git'
        GIT_BRANCH = 'Main'  // ✅ FIX: Use "Main" to match Jenkins config
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/${GIT_BRANCH}"]],  // ✅ Use "Main"
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
                    to: 'sanjanakumari5700@gmail.com',
                    from: 'jenkins@example.com',
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
