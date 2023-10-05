node {
    stage('build') {
            sh 'echo hello world'
    }
    stage('updatechecks') {
        println(env.BUILD_URL)
        publishChecks detailsURL: '${BUILD_URL}', name: 'update-pr-status', summary: 'Updating PR status', text: 'Checking for status ...', title: 'Updating PR status - Title',
            actions: [[label:'an-user-request-action', description:'actions allow users to request pre-defined behaviours', identifier:'an unique identifier']]
    }
}
