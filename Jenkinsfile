pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = "sanjana4809.be23@chitkara.edu.in"
        SMTP_USER = "sanjana4809.be23@chitkara.edu.in"
        SMTP_PASS = "xklsxopfftsemvvq"  // Store securely in Jenkins credentials
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo "Step: Cloning the GitHub repository."
                checkout scm
            }
        }

        stage('Restore Dependencies') {
            steps {
                echo "Step: Restoring project dependencies."
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo "Step: Building the .NET application."
                sh 'dotnet build --configuration Release'
            }
        }

        stage('Run Unit & Integration Tests') {
            steps {
                echo "Step: Running unit and integration tests."
                sh 'dotnet test --logger trx'
            }
            post {
                always {
                    echo "Step: Collecting and publishing test results."
                    junit '**/*.trx'

                    echo "Step: Sending notification email."
                    emailext (
                        subject: "Jenkins Pipeline - Unit and Integration Tests Completed",
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
                        to: "$EMAIL_RECIPIENT",
                        mimeType: 'text/html',
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Step: Running static code analysis."
                sh 'dotnet build --configuration Release /p:EnableNETAnalyzers=true'
            }
        }
    }

    post {
        failure {
            echo "Step: Handling build failures."
            emailext (
                subject: "Jenkins Pipeline - Build Failed",
                body: "The build process has failed. Please check Jenkins for details.",
                to: "$EMAIL_RECIPIENT",
                attachLog: true
            )
        }
    }
}
