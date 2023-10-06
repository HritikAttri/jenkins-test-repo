node {
    stage("build") {
        if (WEBHOOK_EVENT_DETAILS_JSON) {
            def WEBHOOK_EVENT_DETAILS_JSON = new groovy.json.JsonSlurper().parseText(env.WEBHOOK_EVENT_DETAILS)
            println(WEBHOOK_EVENT_DETAILS_JSON.pull_request.head.ref)
        }
    }
}
