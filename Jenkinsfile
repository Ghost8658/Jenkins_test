pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('DOCKER_CREDENTIALS')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t Ghost8658 .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push Ghost8658'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
