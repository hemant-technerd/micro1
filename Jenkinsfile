pipeline {
    agent any
    
    stages {
        stage('Change Log Set') {
            steps {
                script {
                    def changeLogSets=currentBuild.changeSets
                    for (i=0; i<changeLogSets.size(); i++) {
                        def entries=changeLogSets[i].items
                        
                        for(j=0; j<entries.size(); j++) {
                            def entry=entries[j]
                            echo "${entry.commitId} by ${entry.author}: ${entry.msg}"
                        }
                    }
                }
            }
        }
    }
}
