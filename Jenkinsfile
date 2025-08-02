pipeline {
    agent any
    
    environment {
        SLACK_CHANNEL = '#all-spsnet-internee'
    }

    stages {
        stage('Test Webhook') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'WEBHOOK_URL')]) {
                        // Safe way to handle secrets
                        def safeDate = sh(returnStdout: true, script: 'date').trim()
                        def payload = '{"text":"Test from Jenkins at ' + safeDate + '"}'
                        
                        // Secure curl command
                        sh '''
                            curl -s -X POST \
                            -H 'Content-type: application/json' \
                            --data "$PAYLOAD" \
                            "$WEBHOOK_URL"
                        '''.replace('$PAYLOAD', payload)
                    }
                }
            }
        }
        
        stage('Real Pipeline') {
            steps {
                echo "Your actual build steps go here"
            }
        }
    }
    
    post {
        always {
            script {
                withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'WEBHOOK_URL')]) {
                    def message = """
                        :jenkins: Job `${env.JOB_NAME}` 
                        Build #${env.BUILD_NUMBER}
                        Status: ${currentBuild.currentResult}
                        URL: ${env.BUILD_URL}
                    """.stripIndent().trim()
                    
                    sh '''
                        curl -s -X POST \
                        -H 'Content-type: application/json' \
                        --data '{"text":"$MESSAGE", "channel":"$CHANNEL"}' \
                        "$WEBHOOK_URL"
                    '''.replace('$MESSAGE', message)
                           .replace('$CHANNEL', env.SLACK_CHANNEL)
                }
            }
        }
    }
}