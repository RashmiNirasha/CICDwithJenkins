pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Example for Java project
                    sh 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Example for Java project
                    sh 'mvn test'
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis...'
                    // Example tool: SonarQube
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan...'
                    // Example tool: OWASP Dependency Check
                    sh 'mvn dependency-check:check'
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging...'
                    // Example deployment
                    sh 'scp target/my-app.jar user@staging-server:/path/to/deploy'
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Example test script
                    sh 'ssh user@staging-server "cd /path/to/deploy && ./run-tests.sh"'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production...'
                    // Example deployment
                    sh 'scp target/my-app.jar user@production-server:/path/to/deploy'
                }
            }
        }
    }

    post {
        always {
            script {
                // Archive the logs
                archiveArtifacts artifacts: 'target/*.log', allowEmptyArchive: true
            }
        }
        failure {
            emailext(
                to: 'nirashagunawardana9@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Failed",
                body: "Something went wrong with ${env.JOB_NAME} #${env.BUILD_NUMBER}. Please check the logs.",
                attachLog: true
            )
        }
        success {
            emailext(
                to: 'nirashagunawardana9@gmail.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Succeeded",
                body: "The build and deployment of ${env.JOB_NAME} #${env.BUILD_NUMBER} was successful.",
                attachLog: true
            )
        }
    }
}
