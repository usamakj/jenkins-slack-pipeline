pipeline {
    agent any
    
    environment {
        SLACK_CHANNEL = '#all-spsnet-internee'
    }

    stages {
        stage('Build') {
            steps {
                echo "Yahan apna build commands aayega"
                // Example failure test (uncomment to simulate failure):
                // error "Forced failure for testing"
            }
        }
    }
    
    post {
        always {
            script {
                withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'WEBHOOK_URL')]) {
                    def baseMessage = """
                        :jenkins: Job `${env.JOB_NAME}` 
                        Build #${env.BUILD_NUMBER}
                        URL: ${env.BUILD_URL}
                    """.stripIndent().trim()

                    // Common message parts
                    def fullMessage = "${baseMessage}\nStatus: ${currentBuild.currentResult}"
                    
                    sh '''
                        curl -s -X POST \
                        -H 'Content-type: application/json' \
                        --data '{"text":"$MESSAGE", "channel":"$CHANNEL"}' \
                        "$WEBHOOK_URL"
                    '''.replace('$MESSAGE', fullMessage)
                       .replace('$CHANNEL', env.SLACK_CHANNEL)
                }
            }
        }
        
        failure {
            script {
                withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'WEBHOOK_URL')]) {
                    def failMessage = """
                        :rotating_light: *BUILD FAILED* :rotating_light:
                        Project: ${env.JOB_NAME}
                        Build #${env.BUILD_NUMBER}
                        Failed Stage: ${env.STAGE_NAME}
                        Please check immediately!
                        ${env.BUILD_URL}console
                    """.stripIndent().trim()

                    sh '''
                        curl -s -X POST \
                        -H 'Content-type: application/json' \
                        --data '{"text":"$MESSAGE", "channel":"$CHANNEL", "link_names": 1}' \
                        "$WEBHOOK_URL"
                    '''.replace('$MESSAGE', failMessage)
                       .replace('$CHANNEL', env.SLACK_CHANNEL)
                    
                    // Optional: Tag specific people
                    sh '''
                        curl -s -X POST \
                        -H 'Content-type: application/json' \
                        --data '{"text":"<!subteam^S01ABCDEF|dev-team> Build failed!", "channel":"$CHANNEL"}' \
                        "$WEBHOOK_URL"
                    '''.replace('$CHANNEL', env.SLACK_CHANNEL)
                }
            }
        }
        
        success {
            script {
                withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'WEBHOOK_URL')]) {
                    def successMessage = """
                        :white_check_mark: *BUILD SUCCESS* 
                        Project: ${env.JOB_NAME}
                        Build #${env.BUILD_NUMBER}
                        Duration: ${currentBuild.durationString}
                        ${env.BUILD_URL}
                    """.stripIndent().trim()

                    sh '''
                        curl -s -X POST \
                        -H 'Content-type: application/json' \
                        --data '{"text":"$MESSAGE", "channel":"$CHANNEL"}' \
                        "$WEBHOOK_URL"
                    '''.replace('$MESSAGE', successMessage)
                       .replace('$CHANNEL', env.SLACK_CHANNEL)
                }
            }
        }
    }
}