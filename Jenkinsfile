pipeline {
    agent any
    
    // Environment variables
    environment {
        SLACK_CHANNEL = '#all-spsnet-internee'
        GIT_REPO = 'https://github.com/usamakj/jenkins-slack-pipeline.git'
    }

    // Yeh trigger automatic build karega jab bhi GitHub pe change hoga
    triggers {
        pollSCM('* * * * *')  // Har minute check karega (tum change kar sakte ho)
    }

    stages {
        stage('Code Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                         branches: [[name: '*/main']],
                         userRemoteConfigs: [[url: env.GIT_REPO]]])
            }
        }
        
        stage('Build & Test') {
            steps {
                echo "Yahan tum apna build aur test commands daal sakte ho"
                // Example:
                // sh 'mvn clean package'
                // sh 'npm test'
            }
        }
    }
    
    post {
        always {
            script {
                withCredentials([string(credentialsId: 'slack-webhook-url', variable: 'WEBHOOK_URL')]) {
                    def emoji = currentBuild.currentResult == 'SUCCESS' ? ':green_heart:' : ':red_circle:'
                    def message = """
                        ${emoji} *${env.JOB_NAME}* 
                        Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}
                        Branch: ${env.GIT_BRANCH}
                        Duration: ${currentBuild.durationString}
                        URL: ${env.BUILD_URL}
                    """.stripIndent().trim()
                    
                    // Secure tarike se Slack message bhejna
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