pipeline {
  environment {
    imagename = "kevalnagda/flaskapp"
    registryCredential = 'kevalnagda'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/kevalnagda/movieapp.git', branch: 'main', credentialsId: 'kevalnagda'])
 
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