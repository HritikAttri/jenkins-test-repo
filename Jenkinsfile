import groovy.json.JsonOutput
import groovy.json.JsonSlurperClassic
import java.text.SimpleDateFormat

node {
    def eventPayload = new groovy.json.JsonSlurperClassic().parseText(WEBHOOK_EVENT_DETAILS)
    try {
        sendGitHubCheck(eventPayload, 'BuildStarted', 'INPROGRESS', 'neutral', 'Pipeline execution has started...')
        stage('build') {
                sh 'exit 1'
                error("heyy")
        }
        stage('deploy') {
            sh 'echo deploy'
        }
    } catch (e) {
        println("failure case")
        sendGitHubCheck(eventPayload, 'BuildFailed', 'FAILURE', 'failure', 'Build failed!')
        currentBuild.result = 'FAILURE'
        error(e.message)
    }
    println("success case")
    sendGitHubCheck(eventPayload, 'BuildFailed', 'SUCCESS', 'success', 'Build succeeded!')
}

def sendGitHubCheck(def eventPayload, def status, def checkName, def conclusion, def description) {
        withCredentials([usernamePassword(credentialsId: 'main_gh_app_org',
                                          usernameVariable: 'GITHUB_APP',
                                          passwordVariable: 'GITHUB_ACCESS_TOKEN')]) {
            def date = new Date()
            def sdf = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss'Z'")
            Map dataJson = [ "output": [:] ]
            dataJson["name"] = checkName
            dataJson["head_sha"] = eventPayload.pull_request.head.sha
            dataJson["status"] = status
            dataJson["conclusion"] = conclusion
            dataJson["completed_at"] = sdf.format(date)
            dataJson["details_url"] = "http://ec2-100-25-219-177.compute-1.amazonaws.com:8080/job/${env.JOB_NAME}/${env.BUILD_NUMBER}/console"
            dataJson["output"]["title"] = description
            dataJson["output"]["summary"] = description
            writeFile file: 'data.json', text: JsonOutput.toJson(dataJson)
            sh("""
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
