pipeline {
  environment {
    imagename = "radhouenassakra/angular-demo"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  node {
    stage('Cloning Git') {
      deleteDir()
      checkout scm
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"

      }
    }
  }
}


