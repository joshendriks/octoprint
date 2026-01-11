pipeline {
	agent none

    stages {
		stage('Deploy') {
			agent { label 'soyo' }
            steps {
                script {
					sh 'mkdir -p /home/sr/octoprint'
					sh 'cp docker-compose.yml /home/sr/octoprint/docker-compose.yml'
                    dir("/home/sr/octoprint") {
                        sh 'docker compose pull'
                        sh 'docker compose up -d'
                    }		
					withCredentials([string(credentialsId: 'ntfy-basic-auth', variable: 'authString')]) {
					    sh 'curl -H "Authorization: basic ${authString}" -d "octoprint deployed" https://notify.netwatwezoeken.nl/deploy'
					}
				}
            }			
        }
    }
}