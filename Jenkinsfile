node {
    stage('build') {
            sh 'echo hello world'
    }
    stage('updatechecks') {
        withCredentials([usernamePassword(credentialsId: 'main_gh_app_org',
                                          usernameVariable: 'GITHUB_APP',
                                          passwordVariable: 'GITHUB_ACCESS_TOKEN')]) {
            sh("""
            STATUS=success
            DESCRIPTION=hiiiiiiiiii
            CONTEXT=sample_context
            GITHUB_API=https://api.github.com
            OWNER=testing-org-hritik10
            REPO=jenkins-test-repo
            COMMIT_SHA=\$(git rev-parse HEAD)
            curl "https://api.gitHub.com/repos/\${OWNER}/\${REPO}/statuses/\${COMMIT_SHA}" \
              -H "Authorization: Bearer \$GITHUB_ACCESS_TOKEN" \
              -H "Content-Type: application/json" \
              -X POST \
              -d '{\"state\":\"\$STATUS\",\"target_url\":\"\$BUILD_URL\",\"description\":\"\$DESCRIPTION\",\"context\":\"\$CONTEXT\"}'
              # -d "{\"state\": \"success\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"http://ec2-100-25-219-177.compute-1.amazonaws.com:8080/job/ghapp-test-job/\$BUILD_NUMBER/console\"}"
            """)
            // curl -i -H "Authorization: Bearer \$GITHUB_ACCESS_TOKEN" \
            //      -H "Content-Type: application/json" \
            //      -X POST \
            //      -d "{\"state\":\"\$STATUS\",\"target_url\":\"\$BUILD_URL\",\"description\":\"\$DESCRIPTION\",\"context\":\"\$CONTEXT\"}" \
            //      "\$GITHUB_API/repos/\$REPO_OWNER/\$REPO_NAME/statuses/\$COMMIT_SHA"
        }
    }
}
