pipeline {
    agent any
    stages {
        stage('Build'){
            steps{
                sh "echo ${BRANCH_NAME}"
                sh './gradlew'
            }
        }

        stage('Publish'){
            steps{
                sh 'set -e; ./gradlew publish'
            }
        }
    }
}
