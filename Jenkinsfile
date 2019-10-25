pipeline {
	
	agent any
	
	stages {
		
		stage('Build') {
			steps {
				bat label: '', script: 'mvn clean package'
			}
			post {
				success {
					echo 'Archiving the artifact....'
					archiveArtifacts '**/*.war'
				}
				failure {
					echo 'Failed to archive...'
				}
			}
		}
		
		stage('Deploy to staging') {
			steps {
				build 'deploy-to-staging'
			}
		}
		
		stage('Deploy to production') {
			steps {
				timeout(time: 3, unit: 'DAYS') {
					input 'Approve deployment to production?'
				}
				
				build 'deploy-to-production'
			}
			post {
				success {
					echo 'Application is deployed successfully....'
				}
				failure {
					echo 'Failed to deploy an application...'
				}
			}
		}
	}
}







