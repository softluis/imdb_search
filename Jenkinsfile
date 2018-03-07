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
                 		sh 'docker-compose up -d'
			
            	} 
            }
		stage('Test container') {
		steps {
					script{	
						ip = sh(returnStdout: true, script: "docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' imdbsearch_www_1").trim()
						sh "echo ${ip}"
						sh "echo ${link}"
						sh "echo ${porta}"
					result = sh(returnStdout: true, script: "echo $link$ip$porta").trim()
					
					sh "echo '${result}'"
					container = sh(returnStdout: true, script:"curl -o -I -L -s -w \"%{http_code}\n\" ${result}").trim()
					
					sh "echo '${container}'"

					if (container == '200' ){ 
						println('Container Saudavel')
						}
					else {
						println('Erro no Container')
						}
	
				}
		}		
			
        } 
        
    }
    post {
        always {
            deleteDir()
        }
    }     
}
