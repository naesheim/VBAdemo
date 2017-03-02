pipeline {
  agent any

  environment {
    branch = $env.BRANCH_NAME
  }
  stages {
    stage('Build'){
      steps{
        sh "echo ${branch}"
        sh './gradlew'
        sh 'echo "If this is the initial build, add gradle.properties"'
        sh 'set -e; if [ ! -f ~/.gradle/gradle.properties ]; then sh init.sh; fi'
      }
    }
    stage('Publish-release'){
      when { environment name: 'branch', value: 'origin/release/*' }
          steps{
            sh "echo ${env.BRANCH_NAME}"
            sh 'set -e; ./gradlew publish -P release=true'
          }
        }
    stage('Publish-snapshot'){
      when { environment name: 'branch', value: 'origin/master' }
      steps{
          sh "echo ${env.BRANCH_NAME}"
          sh 'set -e; ./gradlew publish'
      }
    }
  }
}
