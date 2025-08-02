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
        // Yeh block hamesha chalega, chahe build success ho ya fail
        always {
            slackSend (
                channel: '#all-spsnet-internee', 
                color: 'good', 
                message: "TEST: Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER}. Status: ${currentBuild.currentResult}",
                tokenCredentialId: 'slack-webhook-url',
                botUser: true
            )
        }
    }
}