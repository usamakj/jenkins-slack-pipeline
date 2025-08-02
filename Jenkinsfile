pipeline{
  agent any 
  
   stages{
	stage('Built'){
		step{
		   echo 'Build stage is running...'
			}
		}
	}
  post{
    always {
	echo 'Pipeline line is finished.sending notification...'
	}
	success{
	  slackSend (
		channel:'#all-spsnet-internee',
		color: 'danger'
message: "Failed: Job ${env.JOB_NAME}'
)
}

failure {
            slackSend (
                channel: '#general', 
                color: 'danger', 
                message: "FAILED: Job '${env.JOB_NAME}' build #${env.BUILD_NUMBER}. Check console: ${env.BUILD_URL}"
            )
        }
    }
}
