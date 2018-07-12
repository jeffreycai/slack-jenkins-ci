#!/usr/bin/env groovy

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
