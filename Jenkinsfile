pipeline {
  agent any

  stages {
    stage('Build'){
      steps{
        sh './gradlew'
        sh 'echo "If this is the initial build, add gradle.properties"'
        sh 'set -e; if [ ! -f ~/.gradle/gradle.properties ]; then ./init.sh; fi'
      }
    }
    stage('Publish'){
      steps{
        sh 'set -e; ./gradlew publish'
      }
    }
  }
}
