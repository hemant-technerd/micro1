pipeline {
    agent any
    
    parameters {
        string(name: 'SEARCH_STR', defaultValue: 'Jenkinsfile', description: 'Search string in commit msg')
    }
    environment {
        msgString=''
    }
    triggers {
        pollSCM('* * * * *')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '2'))
    }
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
                            env.msgString += entry.msg
                        }
                    }
                    echo "${env.msgString}"
                }
            }
        }
        stage('Execute Steps') {
                when {
                    expression {
                        env.msgString.contains(params.SEARCH_STR)
                    }
                }
                steps {
                    echo "Search string ${SEARCH_STR} found in commit message"
                }
            }
        }
    }
