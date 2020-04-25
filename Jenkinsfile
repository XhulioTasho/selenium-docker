pipeline {
  environment {
    registry = "xhuliot/selenium-docker"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent {
           docker {
                   image 'maven:3-alpine'
                    args '-v $HOME/.m2:/root/.m2'
                  }
          }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/XhulioTasho/selenium-docker.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}