node {
    stage('build') {
            sh 'echo hello world'
    }
    stage('updatechecks') {
        withCredentials([usernamePassword(credentialsId: 'hritik10-ghapp-test',
                                          usernameVariable: 'GITHUB_APP',
                                          passwordVariable: 'GITHUB_ACCESS_TOKEN')]) {
            sh("""
            COMMIT_SHA=\$(git rev-parse HEAD)
            curl -H "Authorization: Bearer \$GITHUB_ACCESS_TOKEN" \
                 -H "Content-Type: application/json" \
                 -X POST \
                 -d "{\"state\":\"success\",\"target_url\":\"\$BUILD_URL\",\"description\":\"hiiiiiiii\",\"context\":\"sample-context\"}" \
                 "https://api.github.com/repos/testing-org-hritik10/jenkins-test-repo/statuses/\$COMMIT_SHA"
            """)
        }
    }
}
