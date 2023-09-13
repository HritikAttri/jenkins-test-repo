pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "current build number: ${currentBuild.number}"
                sh 'echo hello world'
            }
        }
    }
}
