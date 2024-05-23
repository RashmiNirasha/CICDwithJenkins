pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Example for Java project on Windows
                    bat 'mvn clean package'
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Example for Java project on Windows
                    bat 'mvn test'
                }
            }
        }
        stage('Run Application') {
            steps {
                script {
                    echo 'Running the application...'
                    // Run the compiled Java application
                    bat 'java -cp target/hello-jenkins-1.0-SNAPSHOT.jar HelloJenkins'
                }
            }
        }
        // Additional stages...
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
                to: 'developer@example.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Failed",
                body: "Something went wrong with ${env.JOB_NAME} #${env.BUILD_NUMBER}. Please check the logs.",
                attachLog: true
            )
        }
        success {
            emailext(
                to: 'developer@example.com',
                subject: "Jenkins Job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) Succeeded",
                body: "The build and deployment of ${env.JOB_NAME} #${env.BUILD_NUMBER} was successful.",
                attachLog: true
            )
        }
    }
}
