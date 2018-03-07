def link = 'http://'
def porta = ':80'
pipeline {
    agent any  
    stages{
        stage('Download Repository') {
            steps {
                checkout scm
            }
		}
		stage('Build Docker-Compose'){
			 steps {
                 		sh 'docker-compose build'
			
            	} 
            }
        stage('Create Container'){
			 steps {
                 		sh 'docker-compose up'
			
            	} 
            }
		
        
    }
    post {
        always {
            deleteDir()
        }
    }     
}
