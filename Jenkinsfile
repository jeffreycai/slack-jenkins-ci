#!/usr/bin/env groovy

slackSend(
  message: "Build Started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)",
  channel: '#general',
  tokenCredentialId: 'slack_jenkins_ci_integration_token',
  color: 'good'
)

properties(
  [buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '30', numToKeepStr: '50')), [$class: 'RebuildSettings', autoRebuild: false, rebuildDisabled: false], pipelineTriggers([])]
)

node {
 
  stage('Checkout') {
      checkout scm
      // Get branch and commit ID
      sh "git rev-parse --abbrev-ref HEAD > var_branch"
      // Get commit ID
      sh "git rev-parse HEAD | tail -c 8 > var_short_commit-id"
      // Stash branch name
      stash includes: "var_*", name: "var-stash"
  }

}

node {
//    JSONArray attachments = new JSONArray();
//    JSONObject attachment = new JSONObject();
//
//    attachment.put('text','I find your lack of faith disturbing!');
//    attachment.put('fallback','Hey, Vader seems to be mad at you.');
//    attachment.put('color','#ff0000');

//    attachments.add(attachment);
    slackSend(color: '#00FF00', channel: '#general', message: 'yeah')
}

post {
    def buildResult = currentBuild.currentResult
    def color, message

    switch (buildResult) {
        case "SUCCESS":
            color = "good"
            message = "Build completed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            break
        case "FAILURE":
            color = "danger"
            message = "Build failed - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            break
        case "UNSTABLE":
            color = "warning"
            message = "Build unstable - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            break
        default:
            color = "danger"
            message = "Build status unclear - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            break
    }

    slackSend(
      message: message,
      channel: '#general',
      tokenCredentialId: 'slack_jenkins_ci_integration_token',
      color: color
    )
}

