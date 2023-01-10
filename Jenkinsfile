pipeline {
  agent { label 'localmac' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('jasonbitheads-dockerhub')
  }
  stages {
    stage('Open Docker') {
      steps {
        sh 'open -a Docker'
      }
    }
    stage('Build') {
      steps {
        sh 'docker build -t jasonbitheads/dp-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push jasonbitheads/dp-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}