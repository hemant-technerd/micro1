pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'DEPLOY_ARTIFACT', defaultValue: false, description: 'Deploy Artifact')
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
                anyOf {
                    expression { params.DEPLOY_ARTIFACT }
                    expression { env.GIT_BRANCH.contains('main') }
                }
            }
            steps {
                echo "Deploy the artifact"
            }
        }
    }
}
