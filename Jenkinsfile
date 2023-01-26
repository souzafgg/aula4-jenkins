pipeline {
  agent any

  stages {
    stage ('Build docker image') {
      steps {
        script {
          dockerapp = docker.build("szadhub/app-news:${env.BUILD_ID}", '-f ./kubeapp/Dockerfile ./kubeapp')
        }
      }
    }
    stage ('Push docker image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'docker-creds') {
            dockerapp.push('latest')
            dockerapp.push("${env.BUID_ID}")
          }
        }
      }
    }
    stage ('Deploy k8s') {
      steps {
        withKubeconfig([credentialsId: 'kube-creds']) {
          sh 'kubectl apply -f ./k8s/Secret.yaml'
          sh 'kubectl apply -f ./k8s/Service.yaml'
          sh 'kubectl apply -f ./k8s/Deployment.yaml'
        }
      }
    }
  }
}