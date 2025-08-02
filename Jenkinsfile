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
                channel: '#all-spsnet-internee', 
                color: 'good', 
                message: "SUCCESSFUL: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check results: ${env.BUILD_URL}",
                webhookUrl: "curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, this is a direct test from the terminal!"}' 'https://hooks.slack.com/services/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'",
                botUser: true
            )
        }
        failure {
            slackSend (
                channel: '#all-spsnet-internee', 
                color: 'danger', 
                message: "FAILED: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check console: ${env.BUILD_URL}",
                webhookUrl: "curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, this is a direct test from the terminal!"}' 'https://hooks.slack.com/services/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'",
                botUser: true
            )
        }
    }
}