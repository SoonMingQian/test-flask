pipeline {
  agent any
  environment {
    IMAGE_NAME = 'qian2828/test-flask'
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/SoonMingQian/test-flask'
      }
    }
    stage('Build Docker image') {
      steps {
        sh "docker build -t %IMAGE_NAME%:latest ."
      }
    }
    stage('Push to Dockerhub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'Docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh """
          echo %DOCKER_PASS% |
          docker login -u %DOCKER_USER% --password-stdin |
          docker push %IMAGE_NAME%:latest
          docker logout
          """
        }
      }
    }
  }
}
