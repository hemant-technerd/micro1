pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'DEPLOY_ARTIFACT', defaultValue: false, description: 'Deploy Artifact')
    }
    triggers {
        pollSCM('* * * * *')
    }
    
    stages {
        stage('Deploy Artifact') {
            when {
                anyOf {
                    expression { params.DEPLOY_ARTIFACT }
                    branch 'main'
                }
            }
            steps {
                echo "Deploy the artifact"
            }
        }
    }
}
