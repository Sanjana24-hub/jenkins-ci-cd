pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'  // Example using Maven
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'  // Example test command
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                sh 'sonar-scanner'  // Example using SonarQube
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                sh 'dependency-check.sh'  // Example using OWASP Dependency Check
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                sh './deploy-staging.sh'  // Assume you have a script for this
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running tests on staging...'
                sh './test-staging.sh'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                sh './deploy-prod.sh'  // Deploy script for production
            }
        }
    }

    post {
        always {
            mail to: 'sanjana4809.be23@chitkara.edu.in',
                 subject: "Jenkins Pipeline Execution - ${currentBuild.result}",
                 body: "Pipeline Execution Completed. Check Jenkins for details."
        }
    }
}
