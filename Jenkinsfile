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
                    echo 'Checking out code using Git...'
                    // Tool: Jenkins Git Plugin
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
                echo 'Building application using Maven/Gradle/npm'
                // Tool: Maven
                echo 'Tool: Maven - Executing: mvn clean package'
                
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit/pytest/Mocha/Jest/Selenium'
                // Tool: JUnit with Maven
                echo 'Tool: JUnit with Maven - Executing: mvn test'
                
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis using SonarQube'
                // Tool: SonarQube Scanner
                echo 'Tool: SonarQube Scanner - Executing: mvn sonar:sonar with SonarQube environment'
                
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Running security scan using OWASP Dependency Check/Snyk/Trivy...'
                // Tool: OWASP Dependency Check
                echo 'Tool: OWASP Dependency Check - Executing: dependency-check to scan project for vulnerabilities'
                
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging using Docker/Jenkins Deploy Plugin.'
                // Tool: Docker
                echo 'Tool: Docker - Executing: docker build, docker stop/rm, docker run to deploy to staging'
                
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging using Cypress/Postman...'
                // Tool: Cypress
                echo 'Tool: Cypress - Executing: npx cypress run for end-to-end testing'
                
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production using Kubernetes/Helm/Ansible/AWS CodeDeploy/Terraform...'
                // Tool: Kubernetes (kubectl)
                echo 'Tool: Kubernetes/kubectl - Executing: kubectl apply and rollout verification commands'
                
            }
        }
    }
    
    post {
        always {
            script {
                echo 'Sending email notification using Jenkins Email Extension Plugin (emailext)...'
                // Tool: Jenkins Email Extension Plugin
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
            // Tool: Jenkins Workspace Cleanup Plugin
            echo 'Tool: Jenkins Workspace Cleanup Plugin - Cleaning workspace after build completion'
        }
        success {
            echo 'Pipeline completed successfully!'
            // Tool: Jenkins Slack Notification Plugin
           
        }
        failure {
            echo 'Pipeline failed. Please check the logs for details.'
            // Tool: Jenkins Slack Notification Plugin
            
        }
    }
}
