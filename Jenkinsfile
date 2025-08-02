pipeline {
    // Jenkins ko batayen ke yeh job kahin bhi chal sakti hai
    agent any

    // Stages woh steps hain jo pipeline mein chalenge
    stages {
        stage('Build') {
            steps {
                echo 'Build stage is running...'
                // Yahan par aapki asal build commands ayengi, jaise:
                // sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'This is the test stage.'
                // Yahan par aapki test commands ayengi, jaise:
                // sh 'npm test'
            }
        }
    }

    // Post-build actions: Yeh hissa pipeline ke khatam hone ke baad chalta hai
    post {
        // Jab pipeline kamyaab ho
        success {
            slackSend (
                channel: '#all-spsnet-internee', // Apna Slack channel yahan likhen
                color: 'good', 
                message: "SUCCESSFUL: Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER}. Check results: ${env.BUILD_URL}",
                tokenCredentialId: 'slack-webhook-url', // Yeh Jenkins credential ID hai
                botUser: true
            )
        }
        // Jab pipeline fail ho
        failure {
            slackSend (
                channel: '#all-spsnet-internee', // Apna Slack channel yahan likhen
                color: 'danger', 
                message: "FAILED: Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER}. Check console: ${env.BUILD_URL}",
                tokenCredentialId: 'slack-webhook-url', // Yeh Jenkins credential ID hai
                botUser: true
            )
        }
    }
}