pipeline {
  agent any

  stages {
    stage('Build'){
      steps{
        sh './gradlew'
        sh 'echo "If this is the initial build, add gradle.properties"'
        sh 'set -e; if [ ! -f ~/.gradle/gradle.properties ]; then sh init.sh; fi'
      }
    }
    stage('Publish-release'){
      when {
        branch 'release'
      }
          steps{
            sh "echo ${BRANCH_NAME}"
            sh 'set -e; ./gradlew publish -P release=true'
          }
        }
    stage('Publish-snapshot'){
      when {
        branch 'master'
      }
      steps{
          sh "echo ${BRANCH_NAME}"
          sh 'set -e; ./gradlew publish'
      }
    }
  }
}
