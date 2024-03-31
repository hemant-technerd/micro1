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
                    writeFile(file: 'changeLog.txt', text: msgString)
                    echo "${msgString}"
                }
            }
        }
        stage('Execute Steps') {
                steps {
                    script {
                        def readVar = readFile('changeLog.txt')
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
