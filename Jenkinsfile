pipeline {
    agent any

    stages {
        stage('Test Stage') {
            steps {
                echo 'This is a test to check Slack notification.'
            }
        }
    }

    post {
        always {
            script {
                try {
                    slackSend (
                        channel: '#all-spsnet-internee',
                        color: currentBuild.currentResult == 'SUCCESS' ? 'good' : 'danger',
                        message: """:jenkins: Job `${env.JOB_NAME}` 
Build #${env.BUILD_NUMBER} 
Status: ${currentBuild.currentResult}
URL: ${env.BUILD_URL}""",
                        tokenCredentialId: 'slack-webhook-url',
                        botUser: true,
                        failOnError: true
                    )
                } catch (Exception e) {
                    echo "Slack notification failed: ${e.getMessage()}"
                }
            }
        }
    }
}