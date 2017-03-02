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
    if ("${BRANCH_NAME}" == 'origin/release/'){
        stage('Publish-release'){
          steps{
            sh "echo ${BRANCH_NAME}"
            sh 'set -e; ./gradlew publish -P release=true'
          }
        }
    }
    else{
      stage('Publish-snapshot'){
        steps{
          sh "echo ${BRANCH_NAME}"
          sh 'set -e; ./gradlew publish'
        }
      }
    }
  }
}
