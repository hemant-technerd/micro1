//Add Description
pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'DEPLOY_ARTIFACT', defaultValue: false, description: 'Deploy Artifact')
        string(name: 'SEARCH_STRING', defaultValue: 'hello', description: 'Search string in Jenkinsfile')
    }
    triggers {
        pollSCM('* * * * *')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '2'))
    }
    
    stages {
        stage('Git Branch') {
            steps {
                echo "Git Branch: ${GIT_BRANCH}"
            }
        }
        stage('Deploy Artifact') {
            when {
                expression { readFile('Jenkinsfile').toLowerCase().contains(params.SEARCH_STRING) }
            }
            steps {
                echo "Deploy the artifact"
            }
        }
    }
}
