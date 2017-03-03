pipeline {
  agent any

  stages {
    stage('Build'){
      steps{
        sh "echo ${BRANCH_NAME}"
        sh './gradlew --no-daemon'
        sh 'echo "If this is the initial build, add gradle.properties"'
        sh 'set -e; if [ ! -f ~/.gradle/gradle.properties ]; then sh init.sh; fi'
      }
    }
    stage('Publish-release'){
      when { expression { return "${BRANCH_NAME}".contains('release')} }
          steps{
            sh 'set -e; ./gradlew publish -P release=true'
          }
        }
    stage('Publish-snapshot'){
      when { expresseion { return "${BRANCH_NAME}".contains('master')} }
      steps{
          sh 'set -e; ./gradlew publish'
      }
    }
  }
}
