pipeline {
	agent none
  stages {
    stage('Docker Build') {
    	agent any
      steps {
        script {
          // Kiểm tra xem container cim_frontend_1 có tồn tại không
          def containerExists = sh(script: "docker ps -a --format '{{.Names}}' | grep -q 'cim_frontend_1'", returnStatus: true)

          if (containerExists == 0) {
              echo "Container cim_frontend_1 tồn tại, đang dừng nó..."
              sh 'docker container stop cim_frontend_1'
              echo "Container cim_frontend_1 đã được dừng."
          } else {
              echo "Container cim_frontend_1 không tồn tại hoặc đã dừng trước đó."
          }
        }
        sh 'docker image prune -f'
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