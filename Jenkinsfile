pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'DEPLOY_ARTIFACT', defaultValue: false, description: 'Deploy Artifact')
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
