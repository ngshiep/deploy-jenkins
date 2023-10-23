pipeline {
	agent none
  stages {
    stage('Docker Build') {
    	agent any
      steps {
        script {
          def containerExists = sh(script: "sudo docker ps -a --format '{{.Names}}' | grep -q 'cim_frontend_1'", returnStatus: true)

          if (containerExists == 0) {
              sh 'sudo docker container stop cim_frontend_1'
              sh 'sudo docker image rm frontend_web'
              echo "Stop container cim_frontend_1"
          }
        }
      	sh 'sudo docker container prune -f'
      	sh 'sudo docker-compose --build -f docker-compose.yml up -d'
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