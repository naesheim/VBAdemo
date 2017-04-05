Library('SharedLibrary@master') _

node {
    stage('Checkout'){
	       def repo='project'
	       repoCheckout repo
	       repoCheckout()
     }
     stage('Build'){
         steps{
             sh "echo ${BRANCH_NAME}"
             sh './gradlew'
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
      when { expression { return "${BRANCH_NAME}".contains('master')} }
      steps{
          sh 'set -e; ./gradlew publish'
      }
    }
}
