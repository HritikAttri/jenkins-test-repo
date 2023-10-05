node {
    stage('build') {
            sh 'echo hello world'
    }
    stage('updatechecks') {
        publishChecks detailsURL: '${BUILD_URL}', name: 'update-pr-status', summary: 'Updating PR status', text: 'Checking for status ...', title: 'Updating PR status - Title'
    }
}
