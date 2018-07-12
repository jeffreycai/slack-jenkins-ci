#!/usr/bin/env groovy

//import net.sf.json.JSONArray;
//import net.sf.json.JSONObject;

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
    slackSend(color: '#00FF00', channel: '#general', text: 'yeah')
}


