pipeline {
    agent any

    stages {
        stage('Test Stage') {
            steps {
                echo 'Testing Slack notification setup'
                // Debug: Verify credential exists
                script {
                    def creds = credentials('slack-webhook-url')
                    echo "Credential ID exists: ${creds}"
                }
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
                        message: """*${env.JOB_NAME}* - Build #${env.BUILD_NUMBER}
Result: ${currentBuild.currentResult}
Details: ${env.BUILD_URL}""",
                        tokenCredentialId: 'slack-webhook-url',
                        failOnError: true
                    )
                } catch (Exception e) {
                    error "Slack failed: ${e.getMessage()}"
                }
            }
        }
    }
}