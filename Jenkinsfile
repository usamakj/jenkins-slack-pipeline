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
            // Jenkins ko batayen ke konsa credential istemal karna hai
            withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'SLACK_WEBHOOK_URL')]) {
                slackSend (
                    webhookUrl: env.SLACK_WEBHOOK_URL,
                    channel: '#general', 
                    color: 'good', 
                    message: "SUCCESSFUL: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check results: ${env.BUILD_URL}"
                )
            }
        }
        failure {
            withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'SLACK_WEBHOOK_URL')]) {
                slackSend (
                    webhookUrl: env.SLACK_WEBHOOK_URL,
                    channel: '#general', 
                    color: 'danger', 
                    message: "FAILED: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check console: ${env.BUILD_URL}"
                )
            }
        }
    }
}
