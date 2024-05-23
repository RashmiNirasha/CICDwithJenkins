pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Example for Java project on Windows
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Example for Java project on Windows
                }
            }
            post {
                success {
                    emailext(
                        to: 'nirasha999@gmail.com',
                        subject: "Unit and Integration Tests Successful - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The unit and integration tests stage was successful.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'nirasha999@gmail.com',
                        subject: "Unit and Integration Tests Failed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The unit and integration tests stage failed. Please check the logs.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Running code analysis...'
                    // Add your code analysis steps here
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Running security scan...'
                    // Add your security scan steps here
                }
            }
            post {
                success {
                    emailext(
                        to: 'nirasha999@gmail.com',
                        subject: "Security Scan Successful - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The security scan stage was successful.",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        to: 'nirasha999@gmail.com',
                        subject: "Security Scan Failed - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                        body: "The security scan stage failed. Please check the logs.",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging...'
                    // Add your deployment steps here
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Add your integration test steps here
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production...'
                    // Add your deployment steps here
                }
            }
        }
    }

    post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    
        failure {
            emailext(
                to: 'nirasha999@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Failed",
                body: "Something went wrong with ${env.JOB_NAME} #${env.BUILD_NUMBER}. Please check the logs.",
                attachLog: true
            )
        }
        success {
            emailext(
                to: 'nirasha999@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Succeeded",
                body: "The build and deployment of ${env.JOB_NAME} #${env.BUILD_NUMBER} was successful.",
                attachLog: true
            )
        }
    }
}
