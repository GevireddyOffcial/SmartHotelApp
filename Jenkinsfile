pipeline {
  environment {
    imagename = "mydotnetapp"
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/GevireddyOffcial/SmartHotelApp.git', branch: 'main', credentialsId: 'GevireddyOfficial'])
 
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
  }
}