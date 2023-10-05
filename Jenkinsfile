pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                println("Branch name: ${env.WEBHOOK_EVENT_DETAILS['pull_request']}")
                // sh 'echo ${WEBHOOK_EVENT_DETAILS} > tmp.json'
                // BRANCH_NAME=sh('cat tmp.json | jq -r .pull_request.head.ref', returnStdout: true).trim()
                // sh 'echo ${BRANCH_NAME}'
            }
        }
    }
}
