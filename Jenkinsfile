pipeline {
  agent any

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build App') {
      steps {
        sh 'npm install'
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t user-management-service:ci .'
      }
    }

  }

  post {
    success {
      echo "CI pipeline succeeded"
    }
    failure {
      echo "CI pipeline failed"
    }
  }
}
