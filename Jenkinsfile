pipeline {
  environment {
    registry = "qsecofr88/k2"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Build Image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Run Image') {
      steps {
        script {
          dockerContainer = dockerImage.run("-p 8080:8080")
        }
      }
    }
    stage('Remove local image') {
      steps{
        sh "docker rmi -f $registry:$BUILD_NUMBER"
        script {
           dockerContainer.stop()
        }
      }
    }
  }
}
