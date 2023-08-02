pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        registry = "gevireddyofficial/smarthotelapp"
        registryCredential = 'DockerHub'        
    }
    
    stages{
// This stage will be inlcude in pipeline script as there we dont clone from git
//       stage('Git Clone'){
//           steps{
//               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/GevireddyOffcial/SmartHotelApp.git']])
//           }
//       }
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
        stage('Trigger ManifestUpdate') {
          steps{
            script {
              echo "triggering updatemanifestjob"
              build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: "$BUILD_NUMBER")]
            }
          }     
        }

   }
}
