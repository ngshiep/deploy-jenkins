pipeline {
	agent none
  stages {
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker-compose build --no-cache && docker-compose up --build -d'
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