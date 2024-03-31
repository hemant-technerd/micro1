pipeline {
    agent any
    
    environment {
        FILE_TO_SEARCH='Jenkinsfile'
    }
    
    stages {
        stage('ChangeSet File Type') {
            steps {
                script {
                    def affectedJenkinsFile=''
                    for (changeSet in currentBuild.changeSets) {
                        for (item in changeSet.items) {
                            for (affectedFile in item.affectedFiles) {
                                echo "Affected File: ${affectedFile.path}"
                                if (affectedFile.path.contains(env.FILE_TO_SEARCH)) {
                                    env.FILE_PRESENT='true'
                                }
                            }
                        }
                    }
                }
            }
        }
        stage('Perform Build') {
            when {
                expression { env.FILE_PRESENT='true' }
            }
            steps {
                echo "Building Project..."
            }
        }
    }
}
