pipeline {
    agent any
    
    stages {
        stage('Build Stage') {
            when {
                changelog 'Build'
            }
            steps {
                echo "Yes, changelog contains 'Build' string"
            }
        }
    }
}
