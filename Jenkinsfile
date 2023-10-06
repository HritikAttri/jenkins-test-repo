import groovy.json.JsonOutput
import groovy.json.JsonSlurperClassic

node {
    stage('build') {
            sh 'echo hello worldab'
    }
    stage('updatechecks') {
        withCredentials([usernamePassword(credentialsId: 'main_gh_app_org',
                                          usernameVariable: 'GITHUB_APP',
                                          passwordVariable: 'GITHUB_ACCESS_TOKEN')]) {
            Map dataJson = [:]
            def eventPayload = new groovy.json.JsonSlurperClassic().parseText(WEBHOOK_EVENT_DETAILS)
            def apiUrl = 'https://api.github.com'
            // dataJson["state"] = "success"
            // dataJson["target_url"] = "http://ec2-100-25-219-177.compute-1.amazonaws.com:8080/job/ghapp-test-job/${env.BUILD_NUMBER}/console"
            // dataJson["description"] = "Jenkins"
            // dataJson["context"] = "continuous-integration/jenkins"
            dataJson["name"] = "Jenkins Build"
            dataJson["head_sha"] = eventPayload.pull_request.head.sha
            dataJson["state"] = "completed"
            dataJson["conclusion"] = "success"
            dataJson["details_url"] = "http://ec2-100-25-219-177.compute-1.amazonaws.com:8080/job/${env.JOB_NAME}/${env.BUILD_NUMBER}/console"
            writeFile file: 'data.json', text: JsonOutput.toJson(dataJson)
            // pull_request.head.sha
            sh("""
            STATUS=success
            DESCRIPTION=hiiiiiiiiii
            CONTEXT=sample_context
            GITHUB_API=https://api.github.com
            OWNER=testing-org-hritik10
            REPO=jenkins-test-repo
            # COMMIT_SHA=\$(git rev-parse HEAD)
            curl -X POST "https://api.gitHub.com/repos/\${OWNER}/\${REPO}/check-runs" \
              -H "Authorization: Bearer \$GITHUB_ACCESS_TOKEN" \
              -H "Accept: application/vnd.github+json" \
              -H "X-GitHub-Api-Version: 2022-11-28" \
              --data-binary "@data.json"
              # -d '{\"state\":\"\\\$STATUS\",\"target_url\":\"\\\$BUILD_URL\",\"description\":\"\$DESCRIPTION\",\"context\":\"\$CONTEXT\"}'
              # -d "{\"state\": \"success\",\"context\": \"continuous-integration/jenkins\", \"description\": \"Jenkins\", \"target_url\": \"https://ec2-100-25-219-177.compute-1.amazonaws.com:8080/job/ghapp-test-job/\$BUILD_NUMBER/console\"}"
            """)
            // curl -i -H "Authorization: Bearer \$GITHUB_ACCESS_TOKEN" \aa
            //      -H "Content-Type: application/json" \
            //      -X POST \
            //      -d "{\"state\":\"\$STATUS\",\"target_url\":\"\$BUILD_URL\",\"description\":\"\$DESCRIPTION\",\"context\":\"\$CONTEXT\"}" \
            //      "\$GITHUB_API/repos/\$REPO_OWNER/\$REPO_NAME/statuses/\$COMMIT_SHA"
        }
    }
}
