pipeline {
	environment {
		registry = "mrvenky123/github-docker-jenkins"
		registryCredential = 'mrvenky123'
		dockerImage = ''
		dockerRunCommand = 'docker run -d -p 8080:8080 -name myapp mrvenky123/github-docker-jenkins '
	}
	agent any
	stages {
		stage("Building docker image") { 
			steps {
				script {
					dockerImage = docker.build registry + ":$BUILD_NUMBER"
				}
			}
		}
		stage("Pushing image to DockerHub") { 
			steps {
				script {
					docker.withRegistry( '', registryCredential ) {
						dockerImage.push()
						dockerImage.push( 'latest' )
					}
				}
			}
		}
	}
}
