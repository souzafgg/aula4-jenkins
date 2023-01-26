pipeline {
  agente any

  stages {
    stage ('Build docker image') {
      steps {
        script {
          dockerapp = docker.build("szadhub/app-news:${env.BUILD_ID}", '-f ./kubeapp/Dockerfile ./kubeapp')
        }
      }
    }
  }
}