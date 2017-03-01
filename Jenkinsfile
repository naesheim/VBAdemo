pipeline {
  agent any

  stages {
    stage('Build'){
      steps{
        sh './gradlew'
      }
    }
    stage('Publish'){
      steps{
        sh './gradlew publish'
      }
    }
  }
}

