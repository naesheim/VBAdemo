@Library('SharedLibrary@master') _

node {
    stage ('gitcheckout') {
        checkout scm
    }

    stage('EchoOut') {
        def output = 'Mundoss!'
	    hello output
    }

   stage('env') {
        echo sh(returnStdout: true, script: 'env')
    }

    stage ('gitCommit') {
        gitCommit
    }


    stage('changeStage') {
        def changeLogSets = currentBuild.changeSets
        for (int i = 0; i < changeLogSets.size(); i++) {
            def entries = changeLogSets[i].items
            for (int j = 0; j < entries.length; j++) {
                def entry = entries[j]
                echo "${entry.commitId} by ${entry.author} on ${new Date(entry.timestamp)}: ${entry.msg}"
            }
        }
    }
}
