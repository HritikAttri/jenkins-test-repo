import groovy.json.JsonOutput
import groovy.json.JsonSlurperClassic
import java.text.SimpleDateFormat

node {
    try {
        stage('build') {
                sh 'echo hello worldab
        }
        stage('deploy') {
            def eventPayload = new groovy.json.JsonSlurperClassic().parseText(WEBHOOK_EVENT_DETAILS)
        }
    } catch (e) {
        sendGitHubCheck('failure', 'Build failed')
    }
    sendGitHubCheck('success', 'Build success')
}

def sendGitHubCheck(def eventPayload, def status, def description) {
        withCredentials([usernamePassword(credentialsId: 'main_gh_app_org',
                                          usernameVariable: 'GITHUB_APP',
                                          passwordVariable: 'GITHUB_ACCESS_TOKEN')]) {
            def date = new Date()
            def sdf = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss")
            Map dataJson = [ "output": [:] ]
            def checkName = "Jenkins Build"
            dataJson["name"] = checkName
            dataJson["head_sha"] = eventPayload.pull_request.head.sha
            dataJson["state"] = "completed"
            dataJson["conclusion"] = status
            dataJson["completed_at"] = sdf.format(date)
            dataJson["details_url"] = "http://ec2-100-25-219-177.compute-1.amazonaws.com:8080/job/${env.JOB_NAME}/${env.BUILD_NUMBER}/console"
            dataJson["output"]["title"] = "${checkName} Results"
            dataJson["output"]["summary"] = description
            writeFile file: 'data.json', text: JsonOutput.toJson(dataJson)
            sh("""
            STATUS=success
            DESCRIPTION=hiiiiiiiiii
            CONTEXT=sample_context
            GITHUB_API=https://api.github.com
            OWNER=testing-org-hritik10
            REPO=jenkins-test-repo
            curl -X POST "https://api.gitHub.com/repos/\${OWNER}/\${REPO}/check-runs" \
              -H "Authorization: Bearer \$GITHUB_ACCESS_TOKEN" \
              -H "Accept: application/vnd.github+json" \
              -H "X-GitHub-Api-Version: 2022-11-28" \
              --data-binary "@data.json"
            """)   
        }
}
