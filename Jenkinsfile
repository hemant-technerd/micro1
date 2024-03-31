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
                    for (changeLogSet in changeLogSets) {
                        for (entry in changeLogSet.items) {
                            echo "${entry.commitId} by ${entry.author}: ${entry.msg}"
                            msgString += entry.msg
                        }
                    }
                    sh 'echo msgString > changeLog.txt'
                    echo "MsgString: ${msgString}"
                }
            }
        }
        stage('Execute Steps') {
                steps {
                    script {
                        def readVar = readFile('changeLog.txt').trim()
                        if (readVar.contains(params.SEARCH_STR)) {
                            echo "Search string  found in commit message"
                        }
                    }
                }
            }
        }
        
        post {
            cleanup {
                cleanWs()
            }
        }
    }
