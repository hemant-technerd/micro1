pipeline {
    agent any
    
    triggers {
        pollSCM('* * * * *')
    }
    
    environment {
        GIT_REPO="https://github.com/hemant-technerd/micro1.git"
        GIT_BRANCH="*/main"
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: "$GIT_BRANCH"]],
                    userRemoteConfigs: [[url: "${GIT_REPO}", credentialsId: 'github-repo']]
                    
                    ])
            }
        }
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
