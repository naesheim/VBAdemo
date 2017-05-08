pipeline {
    agent any
        stages {
            stage ('Increment version'){
                steps {
                    script {
                        env.Version_Increment = input message: 'Bump patch, minor or major', ok : 'Bump!',
                        parameters: [choice(name: 'IncrementVersion', choices: 'Major\nMinor\nPatch\n', description: 'choose')]
                    }
                    echo "${env.Version_Increment}"
                    script {
                        def gradleCmd
                        switch(env.Version_Increment){
                            case "Major":
                                gradleCmd = 'bumpMajor'
                                break
                            case "Minor":
                                gradleCmd = 'bumpMinor'
                                break
                            case "Patch":
                                gradleCmd = 'bumpPatch'
                                break
                        }

                    }
                    sh "./gradlew ${gradleCmd}"
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
