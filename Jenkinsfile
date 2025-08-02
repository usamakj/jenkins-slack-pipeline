pipeline {

� � agent any
� � stages {

� � � � stage('Build') {

� � � � � � steps {

� � � � � � � � echo 'Build stage is running...'

� � � � � � }

� � � � }

� � }



� � post {

� � � � success {

� � � � � � slackSend (

� � � � � � � � channel: '#all-spsnet-internee',�

� � � � � � � � color: 'good',�

� � � � � � � � message: "SUCCESSFUL: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check results: ${env.BUILD_URL}",

� � � � � � � � tokenCredentialId: 'slack-webhook-url',

� � � � � � � � botUser: true

� � � � � � )

� � � � }

� � � � failure {

� � � � � � slackSend (

� � � � � � � � channel: '#all-spsnet-internee',�

� � � � � � � � color: 'danger',�

� � � � � � � � message: "FAILED: Job ${env.JOB_NAME} build #${env.BUILD_NUMBER}. Check console: ${env.BUILD_URL}",

� � � � � � � � tokenCredentialId: 'slack-webhook-url',

� � � � � � � � botUser: true

� � � � � � )

� � � � }

� � }

}
