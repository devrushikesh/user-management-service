pipeline {
  agent any

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh "docker build -t user-management-service:${env.BRANCH_NAME} ."
      }
    }

    stage('Branch Info') {
      steps {
        echo "Building branch: ${env.BRANCH_NAME}"
      }
    }

    stage('Integration Checks') {
      when {
        branch 'develop'
      }
      steps {
        echo "Running integration checks for develop"
      }
    }

    stage('Feature Validation') {
      when {
        expression { env.BRANCH_NAME.startsWith('feature/') }
      }
      steps {
        echo "Validating feature branch"
      }
    }

  }

  post {
    success {
      echo "CI passed for ${env.BRANCH_NAME}"
    }
    failure {
      echo "CI failed for ${env.BRANCH_NAME}"
    }
  }
}
