pipeline {
	agent none
  stages {
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker container stop cim_frontend_1'
      	sh 'docker container prune -f'
      	sh 'docker-compose -f docker-compose.yml up -d'
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