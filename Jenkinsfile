pipeline {
    agent any
    
    parameters {
        string(name: 'SEARCH_STR', defaultValue: 'Jenkinsfile', description: 'Search string in commit msg')
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
                    def msgString=''
                    def changeLogSets=currentBuild.changeSets
                    for (i=0; i<changeLogSets.size(); i++) {
                        def entries=changeLogSets[i].items
                        
                        for(j=0; j<entries.size(); j++) {
                            def entry=entries[j]
                            echo "${entry.commitId} by ${entry.author}: ${entry.msg}"
                            msgString += entry.msg
                        }
                    }
                    writeFile(file: 'changeLog.txt', text: "${msgString}")
                    echo "${msgString}"
                }
            }
        }
        stage('Execute Steps') {
                steps {
                    script {
                        def readVar = readFile('changeLog.txt')
                        if (readVar.contains("${SEARCH_STR}")) {
                            echo "Search string  found in commit message"
                        }
                    }
                }
            }
        }
    }
