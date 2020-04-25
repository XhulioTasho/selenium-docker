pipeline {
  environment {
    registry = "xhuliot/selenium-docker"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/XhulioTasho/selenium-docker.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          app = docker.build("xhuliot/selenium-docker")
        }
      }
    }
    stage('Push Image') {
                steps {
                    script {
    			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
    			        	app.push("${BUILD_NUMBER}")
    			            app.push("latest")
    			        }
                    }
                }
            }
     }
  }
}