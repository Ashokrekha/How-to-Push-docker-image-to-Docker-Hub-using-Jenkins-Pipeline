pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git branch: 'main', url: 'https://github.com/Ashokrekha/live01.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t ashok223/project-1a .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push ashok223/project-1a'
			}
		}
		stage('deploy') {

			steps {
				sh 'docker run -d -p 8081:8080 --name project-1a ashok223/project-1a'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
