pipeline {
    agent any
    stages {
        stage ('Increment version'){
            steps {
                sh './gradlew bumpPatch'
            }
        }

        stage('Publish'){
            steps{
                sh 'set -e; ./gradlew publish'
            }
        }

        stage ('Update git') {
                steps {
                    sh 'git config user.email "hg.nesheim@gmail.com"'
                    sh 'git config user.name "naesheim"'
                    sh 'git add build.properties'
                    sh "git commit -m 'Jenkins automated build: ${BUILD_NUMBER}'"
                    sh 'git push'
                }
        }
    }
}
