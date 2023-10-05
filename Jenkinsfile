node {
    stage('build') {
            sh 'echo hello world'
    }
    stage('updatechecks') {
        withCredentials([usernamePassword(credentialsId: 'hritik10-ghapp-test',
                                          usernameVariable: 'GITHUB_APP',
                                          passwordVariable: 'GITHUB_ACCESS_TOKEN')]) {
            sh("""
            STATUS=success
            DESCRIPTION=hiiiiiiiiii
            CONTEXT=sample_context
            GITHUB_API=https://api.github.com
            REPO_OWNER=testing-org-hritik10
            REPO_NAME=jenkins-test-repo
            COMMIT_SHA=\$(git rev-parse HEAD)
            curl -i -H "Authorization: Bearer \$GITHUB_ACCESS_TOKEN" \
                 -H "Content-Type: application/json" \
                 -X POST \
                 -d "{\"state\":\"\$STATUS\",\"target_url\":\"\$BUILD_URL\",\"description\":\"\$DESCRIPTION\",\"context\":\"\$CONTEXT\"}" \
                 "\$GITHUB_API/repos/\$REPO_OWNER/\$REPO_NAME/statuses/\$COMMIT_SHA"
            """)
        }
    }
}
