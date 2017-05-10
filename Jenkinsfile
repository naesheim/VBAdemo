pipeline {
    agent any
        stages {
            stage ('Increment version'){
                steps {
                    sh './gradlew incrementVersion'
                }
            }

            stage('Publish'){
                steps{
                    sh 'set -e; ./gradlew publish'
                }
            }
    }
}
