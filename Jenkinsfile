pipeline {
    agent any
    
    stages {
        stage('Test Webhook') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'WEBHOOK_URL')]) {
                        // Verify first/last chars (no full print for security)
                        echo "Webhook exists (truncated): ${WEBHOOK_URL.take(5)}...${WEBHOOK_URL.drop(WEBHOOK_URL.length()-5)}"
                        
                        // Test connection
                        def response = sh(returnStdout: true, script: """
                            curl -s -X POST -H 'Content-type: application/json' \
                            --data '{"text":"Test from Jenkins at \$(date)"}' \
                            ${WEBHOOK_URL}
                        """)
                        echo "Slack response: ${response}"
                    }
                }
            }
        }
    }
}