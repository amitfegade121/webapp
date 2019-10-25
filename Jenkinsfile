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
	}
}