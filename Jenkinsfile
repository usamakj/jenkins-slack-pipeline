pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Build stage is running...'
            }
        }
    }

    post {
        success {
            slackSend (
                channel: '#general', 
                color: 'good', 
                message: "SUCCESSFUL: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check results: ${env.BUILD_URL}"
            )
        }
        failure {
            slackSend (
                channel: '#general', 
                color: 'danger', 
                message: "FAILED: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check console: ${env.BUILD_URL}"
            )
        }
    }
}
