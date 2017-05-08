pipeline {
    agent any
        stages {
            stage ('Increment version'){
                steps {
                    script {
                        env.Version_Increment = input message: 'Bump patch, minor or major', ok : 'Bump!',
                        parameters: [choice(name: 'IncrementVersion', choices: 'patch,minor,major', description: 'choose'), choice(name: 'yolo', choices: 'yo/lo', description: 'yolo')]
                    }
                    echo "${env.Version_Increment}"
                    sh './gradlew bumpMinor'
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
                    sh 'git push origin HEAD:master'
                }
            }
    }
}
