pipeline {
    agent any
    
    parameters {
        string(name: 'SEARCH_STR', defaultValue: 'Jenkinsfile', description: 'Search string in commit msg')
    }
    
    stages {
        stage('Change Log Set') {
            steps {
                script {
                    def msgString=''
                    def changeLogSets=currentBuild.changeSets
                    for (i=0; i<changeLogSets.size(); i++) {
                        def entries=changeLogSets[i].items
                        
                        for(j=0; j<entries.size(); j++) {
                            def entry=entries[j]
                            echo "${entry.commitId} by ${entry.author}: ${entry.msg}"
                            msgString = msgString + "${entry.msg}"
                        }
                    }
                }
            }
        }
        stage('Execute Steps') {
            stage {
                when {
                    expression {
                        msgString.contains(SEARCH_STR)
                    }
                }
                steps {
                    echo "Search string ${SEARCH_STR} found in commit message"
                }
            }
        }
    }
}
