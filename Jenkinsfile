pipeline {
	agent none
  environment {
    PATH = "$PATH:/usr/bin/docker-compose"
  }
  stages {
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker compose -f docker-compose.yml up -d'
      }
    }
  }
  post {
    success {
        echo 'Deployment to production completed successfully!'
    }
    unstable {
        echo 'Deployment was unstable. Please investigate.'
    }
    failure {
        echo 'Deployment to production failed.'
    }
  }
}