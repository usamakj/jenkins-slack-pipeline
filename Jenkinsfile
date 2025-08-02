pipeline {

Â Â agent any
Â Â stages {

Â Â Â Â stage('Build') {

Â Â Â Â Â Â steps {

Â Â Â Â Â Â Â Â echo 'Build stage is running...'

Â Â Â Â Â Â }

Â Â Â Â }

Â Â }



Â Â post {

Â Â Â Â success {

Â Â Â Â Â Â slackSend (

Â Â Â Â Â Â Â Â channel: '#all-spsnet-internee',Â

Â Â Â Â Â Â Â Â color: 'good',Â

Â Â Â Â Â Â Â Â message: "SUCCESSFUL: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check results: ${env.BUILD_URL}",

Â Â Â Â Â Â Â Â tokenCredentialId: 'slack-webhook-url',

Â Â Â Â Â Â Â Â botUser: true

Â Â Â Â Â Â )

Â Â Â Â }

Â Â Â Â failure {

Â Â Â Â Â Â slackSend (

Â Â Â Â Â Â Â Â channel: '#all-spsnet-internee',Â

Â Â Â Â Â Â Â Â color: 'danger',Â

Â Â Â Â Â Â Â Â message: "FAILED: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check console: ${env.BUILD_URL}",

Â Â Â Â Â Â Â Â tokenCredentialId: 'slack-webhook-url',

Â Â Â Â Â Â Â Â botUser: true

Â Â Â Â Â Â )

Â Â Â Â }

Â Â }

}
